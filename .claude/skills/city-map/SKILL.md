---
name: city-map
description: Use this skill when the user asks to "/city-map", "generate a city map prompt", "make a nanobanana prompt for X", "turn my city sketch into a map", "create a map for the city of X", "generate the artwork prompt for [city]", or wants a NanaBanana / Gemini image prompt that turns a hand-drawn city sketch into a finished top-down D&D-style city map. Reads the city's Codex page and its Excalidraw sketch note, then emits a paste-ready prompt built from a fixed art-style block (for consistency across every city) plus a per-city content block drawn from the notes. The user pastes the prompt + sketch PNG into Gemini/NanaBanana; the result is published via /process-wiki-image.
---

# City Map Prompt Generator

Generate a paste-ready **NanaBanana (Gemini) image prompt** that turns a hand-drawn city sketch into a finished, top-down D&D-module-style city map.

This skill **only produces the prompt text**. The user then pastes that prompt — together with the exported sketch PNG — into Gemini/NanaBanana, gets the image back, and publishes it with `/process-wiki-image`. (Same pattern as `whisperx-prompt` and `session-context`: the skill's job is a perfect prompt, not the artefact.)

## The core idea: consistency comes from a fixed STYLE BLOCK

Every prompt is two parts:

1. **STYLE BLOCK** — *identical, verbatim, every single time.* This is what makes all the city maps look like they belong in the same atlas: same medium, camera angle, palette, label typography, and border treatment. Copy it exactly. **Never paraphrase or "improve" it per-city** — drift here is exactly what we're preventing.
2. **CONTENT BLOCK** — *rebuilt per city* from the Codex page and the sketch: this city's footprint, walls, gates, river, avenues, landmarks, districts, docks, and lore-driven surroundings, plus the exact label list.

Architecture may change city to city (different buildings, different layout) — that's expected and fine. The **art style must not.** The sketch defines *what is where*; the STYLE BLOCK defines *how it looks*.

## Vault locations

- **Codex city page:** `Codex/Locations/Cities/<Name>.md`
- **Sketch note (Excalidraw):** `x_Assets/Locations/<Name> Sketch.md`
- **Published map asset:** `Codex/Assets/Locations/Cities/<Name>.webp` (+ `_small.webp`) — created later by `/process-wiki-image`

Asset filenames use underscores and strip apostrophes/accents (e.g. `Val_Miriel.webp`); the page keeps its real name.

## Steps

### 1. Identify the city and locate its files

From the user's message, get the city name. Then:
- Read the Codex city page (`Codex/Locations/Cities/<Name>.md`). This is the primary source for geography and surroundings.
- Read the sketch note (`x_Assets/Locations/<Name> Sketch.md`) — **only the `## Text Elements` section near the top.** Excalidraw notes store every label as plain text there, which gives you the exact label list and a rough sense of layout. **Do not** decompress or read the `compressed-json` drawing payload — it's huge and useless as text.

If either file is missing, tell the user and ask for the path (or proceed from whichever source exists — the Codex page alone is enough for the content block; the sketch PNG is what the user feeds Gemini).

### 2. Extract the content from the Codex page

Pull out, in the city's own terms:
- **Footprint / overall shape** — walled? roughly what shape (from the sketch)?
- **Walls & gates** — how many gatehouses, roughly where.
- **Internal structure** — rivers/canals and their path; the main road(s); the named avenues/quarters and what monumental building sits at the head of each.
- **Landmarks** — the few big buildings that should render large and detailed, and where they sit.
- **Districts & character** — which quarters are rough/poor vs wealthy/grand (reflect this in building density and quality), markets, parks.
- **Waterfront & docks** — quays, harbour, which side is rough vs clean.
- **Surroundings (lore-driven hinterland)** — what lies *outside* each side of the wall: sea/gulf, the river entering and leaving, plains/forest/hills, approach roads. Use only terrain the Codex actually names for this city. This is the "show the outside too" requirement — the walls must sit in a real landscape, not float on blank parchment.

### 3. Build the label list

Take the place labels from the sketch's Text Elements, cross-checked against the Codex page (the Codex spelling wins). Then:
- **Keep:** districts, the avenues/Ways, landmarks, gates, bridges, markets, docks, named shops/sites — every *permanent place*.
- **Drop campaign-transient labels:** one-off session markers like "Barricade", and travel-time annotations like the "30mins" arrows. Those belong on a play-map, not the canonical atlas map.

If the user explicitly asks to keep transients or travel-time arrows, honour that instead.

### 4. Assemble the prompt

Concatenate, in this order:

1. A one-line **instruction** ("Here is a hand-drawn sketch of my city's layout. Turn it into a finished top-down fantasy city map, faithfully following the sketch's positions and labels.").
2. The **STYLE BLOCK**, verbatim (below).
3. The **CONTENT BLOCK**, filled in for this city (template below).
4. The **SURROUNDINGS** line (lore-driven hinterland from step 2).
5. The **LABELS** line — the cleaned list from step 3, with a note to letter them exactly and place each at its sketched location.
6. The **MAP FURNITURE** line — title cartouche bearing the city's name, a compass rose in a corner, and a scale bar.

Output the whole thing inside one fenced code block so the user can copy it in a single action.

### 5. Closing reminder

After the prompt, in one or two lines, remind the user:
- Paste the prompt **and attach the exported sketch PNG** into Gemini/NanaBanana.
- When happy, run `/process-wiki-image` to make the published WebP pair. The infobox already expects `Codex/Assets/Locations/Cities/<Name>_small.webp`.
- Suggested archive root for city maps: `/mnt/storage/Misc/DnD/The Bloody Nails/Art/Locations/Cities/` (process-wiki-image will confirm).

---

## STYLE BLOCK (fixed — copy verbatim, every city)

> Render as a premium tabletop-RPG city map in the tradition of a D&D module / Mike Schley & Fantastic Maps cartography: hand-painted watercolour with fine ink linework, not a photo and not a flat cartoon.
>
> **View & light:** a high-oblique bird's-eye view, looking down at roughly 65°, with every building drawn in slight 3/4 isometric relief so both red rooftops and stone facades are visible. Use this exact camera height and angle. Light falls consistently from the upper-left, casting soft, uniform shadows.
>
> **Palette:** warm and muted — terracotta and russet roof tiles, weathered grey stone for walls and towers, translucent blue-green water, sage and olive greens for parks and gardens, sandy ochre roads, all over an underlying parchment tan. Painterly and slightly desaturated; never neon or glossy.
>
> **City fabric:** a very large city read as massed neighbourhoods, not individual households — dense clusters of small red-tiled buildings, tighter and rougher in poor quarters, grander and more spaced in wealthy ones. A crenellated grey curtain wall with regularly spaced round towers and distinct gatehouses. Ochre avenues thread through the blocks; green spaces mark parks and grounds. The few named landmarks (cathedrals, keeps, fortresses, theatres) are drawn larger, taller, and in finer detail so they clearly stand out.
>
> **Water & docks:** rivers and harbour in translucent layered blue-green watercolour with faint ripples; timber quays, jetties, and a scatter of small boats at the waterfront; small colourful market tents where trade gathers along the banks.
>
> **Labels:** place names in small, clean black serif lettering, the more important ones on faint parchment caption plaques; avenue and road names hand-lettered in a lighter italic that follows the line of the road. Legible and sparse — labels never crowd or obscure the art.
>
> **Surface & frame:** the whole map sits on aged cream-to-tan parchment with subtle mottling, faint stains, and softly torn, lightly scorched edges, enclosed by a fine decorative double-rule border. Antique heraldic corner flourishes (small inked beasts or wax seals) are welcome but kept subtle.

## CONTENT BLOCK (template — fill per city)

> **The city — <Name>:** <one-line identity from the Codex, e.g. "a vast walled river-port, the religious heart of the realm">. Follow the attached sketch for the position of every feature.
>
> **Footprint:** <overall shape / walled outline from the sketch>.
> **Walls & gates:** <number and rough position of gatehouses>.
> **Water & main roads:** <river path through the city; the principal causeway/road; the named avenues and the monumental building at the head of each>.
> **Landmarks (render large and detailed):** <landmark — where it sits>; <landmark — where>; … .
> **Districts:** <quarter — character, rough vs grand>; <quarter — character>; … reflect wealth in building density and quality.
> **Waterfront:** <docks/harbour, which side is rough vs clean, notable dockside sites>.

## SURROUNDINGS (lore-driven — fill per city)

> **Beyond the walls:** <what meets each side of the wall, from the Codex — e.g. "open sea and the gulf past the southern docks; the river flowing in from the north-west and out to the sea; rolling grassland and approach roads beyond the landward walls">. Paint this hinterland so the city sits in a real landscape, not on blank parchment.

## MAP FURNITURE (fixed elements, per city)

> Include an ornate title cartouche (a painted banner or scroll) bearing the city's name "**<Name>**"; a small decorative compass rose in one corner with north marked; and a short scale bar.

---

## Worked example — Val Miriel

For Val Miriel the content block fills out roughly like this (drawn from `Codex/Locations/Cities/Val Miriel.md`):

> **The city — Val Miriel:** the continent's greatest walled river-port and the religious heart of the realm, built where the Luminor River meets the sea. Follow the attached sketch for the position of every feature.
>
> **Footprint:** a huge oval walled city straddling a river, joined across it by a single great bridge.
> **Walls & gates:** old grey curtain walls with three gatehouses — Valena's Portal in the north-west, a south-west gate, and an eastern gate.
> **Water & main roads:** the Luminor River cuts north-west to south-east through the heart of the city, dividing a western and eastern bank crossed only at Valena's Bridge; one broad causeway runs west-to-east from Valena's Portal across the bridge to the eastern gate; four great avenues — the Ways — run north to south, each falling from a monument toward the docks: Military Way from the Red Bastion, Royal Way from the Governor's Keep, Divine Way from the High Sept, Artisan Way from the Theater of Dreams.
> **Landmarks (render large and detailed):** the Red Bastion (a red-walled fortress, west); the Governor's Keep (overlooking the gulf, west); the High Sept (a vast circular cathedral, east); the Theater of Dreams (ornate, east); Valena's Bridge over the river; the River Market's tented stalls on both banks by the bridge.
> **Districts:** Military Way — soldiers, barracks, hardest edge toward the water; Royal Way — old money and nobility; Divine Way — clergy and scholars; Artisan Way — fine craft and wealth; the riverbanks crowded with the River Market.
> **Waterfront:** the docks where the river meets the gulf — the rough Grey Docks to the west, the cleaner Green Docks (with Mawbreakers Hold) to the east.

> **Beyond the walls:** the Gulf of Miriel and open sea past the southern docks where the river empties out; the Luminor flowing in from the north-west; rolling grassland and approach roads beyond the landward walls.

Labels to keep (from the sketch, transients dropped): Valena's Portal, Valena's Bridge, Miriel's Keep, Miriel's Rest, The Red Bastion, The High Sept, Theater of Dreams, Librarium Valoris, The Silver Forge, The Gilded Crow, The Bridge of Stars, Military Way, Royal Way, Divine Way, Artisan Way, The Alchemists Retreat, Green Griffon, The Coal, Fur and Fang, The Rusty Anchor, The River Market (W), The River Market (E), River's Watch, Potion Seller, Mawbreakers Hold, Grey Docks, Green Docks. **Dropped:** "Barricade", the "30mins" travel-time arrows.
