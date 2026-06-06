# Codex Category — Locations

Shared location workflow for the codex skill. Read this when creating any location entry, **then read the subtype doc** — it holds the creation-mode questions, frontmatter, infobox, body templates, and gold standard for that subtype, while this base holds everything the subtypes share.

| Subtype | What it is | Subtype reference | Status |
|---|---|---|---|
| **World** | The world itself — the planet or setting that contains continents and provides the cosmological and historical overview for all other entries | `references/locations/world.md` | **Supported** |
| **Continent** | A landmass within the world (e.g. Valtorra) that contains Regions | `references/locations/continent.md` | **Supported** |
| **Plane** | A self-contained realm of existence parallel to or beyond the world (e.g. Faewild, Shadowfell) — same structure as a Continent but without a parent World anchor | `references/locations/continent.md` | **Supported** |
| **Region** | A broad geographic area — a forest, gulf, mountain range within a continent | `references/locations/region.md` | **Supported** |
| **City** | A settlement — town, city, or port; the hub for the landmarks, establishments, and people within it | `references/locations/city.md` | **Supported** |
| **Point of Interest** | A single notable place — a ruin, landmark, natural feature, structure, or site within a larger region | `references/locations/poi.md` | **Supported** |

**Telling the subtypes apart (from largest scale to smallest):**
- **World** — the whole world (Elandis). One page per world. No parent anchor — it IS the top.
- **Continent** — a landmass on the world (Valtorra). Parent: `World: "[[Elandis]]"`. Contains Regions.
- **Plane** — a parallel/extra-planar realm (Faewild, Shadowfell). No parent World (runs parallel to the world, not nested in it). Contains Regions. Uses `continent.md` reference with Plane-specific additions.
- **Region** — a broad geographic area within a continent (a forest, gulf, mountain range). Parent: `Continent: "[[Valtorra]]"` or `Plane: "[[Faewild]]"`.
- **City** — a settlement (town, city, port). Hub for its internal landmarks, establishments, and people.
- **Point of Interest** — a single ruin, landmark, or site within a Region or City.

Hubs at each level: World → Continents + Planes; Continent/Plane → Regions; Region → Cities + POIs; City → establishments, Tier A POIs, and factions inside it.

## Vault locations

Each subtype writes to its own folder; everything else (stubs, assets) is shared.

| Subtype | Public folder | Restricted folder |
|---|---|---|
| World | `Codex/Locations/Worlds/<Name>.md` | `Codex - Restricted/Locations/Worlds/<Name> - Restricted.md` |
| Continent | `Codex/Locations/Continents/<Name>.md` | `Codex - Restricted/Locations/Continents/<Name> - Restricted.md` |
| Plane | `Codex/Locations/Planes/<Name>.md` | `Codex - Restricted/Locations/Planes/<Name> - Restricted.md` |
| Region | `Codex/Locations/Regions/<Name>.md` | `Codex - Restricted/Locations/Regions/<Name> - Restricted.md` |
| City | `Codex/Locations/Cities/<Name>.md` | `Codex - Restricted/Locations/Cities/<Name> - Restricted.md` |
| Point of Interest | `Codex/Locations/Points of Interest/<Name>.md` | `Codex - Restricted/Locations/Points of Interest/<Name> - Restricted.md` |

- **Root-level stubs:** `<Name>.md` at vault root (migration case)
- **Image assets:** published under a subtype subfolder with **underscores, no spaces** — `Codex/Assets/Locations/Worlds/` for Worlds, `Codex/Assets/Locations/Continents/` for Continents, `Codex/Assets/Locations/Planes/` for Planes, `Codex/Assets/Locations/Regions/` for Regions, `Codex/Assets/Locations/Cities/` for Cities, `Codex/Assets/Locations/Points_of_Interest/` for POIs (working copies under `x_Assets/Locations/`). The infobox path must include this subfolder.

---

## Step 1 — Parse input

Extract from the user's message whatever they've already provided:
- Location **name**
- **Subtype:** World, Continent, Plane, Region, City, or Point of Interest. Use the scale table above — the whole world is a World; a continental landmass is a Continent; a parallel plane of existence (Faewild, Shadowfell) is a Plane; a broad geographic area within a continent is a Region; a settlement is a City; a single ruin or landmark is a Point of Interest. Confirm if ambiguous.
- **Importance:** Major or Minor
- Whether a **restricted companion document** is also needed

If anything is missing, ask for it all in one message — don't ask one field at a time. Name, subtype, and importance are required before proceeding.

**Once the subtype is settled, read its reference doc now** (`references/locations/world.md`, `references/locations/continent.md`, `references/locations/region.md`, `references/locations/city.md`, or `references/locations/poi.md`) and keep this base doc for the shared steps below. Continent and Plane both use `continent.md`.

---

## Step 2 — Check for existing files and research the location

Before asking for details, check the vault:

1. Does the entry already exist in its subtype folder (e.g. `Codex/Locations/Worlds/<Name>.md`, `Codex/Locations/Continents/<Name>.md`, `Codex/Locations/Planes/<Name>.md`, `Codex/Locations/Regions/<Name>.md`, `Codex/Locations/Cities/<Name>.md`, or `Codex/Locations/Points of Interest/<Name>.md`)? If so, warn the user and ask whether they want to update/migrate rather than overwrite.
2. Does `<Name>.md` exist at the vault root? If so, read it — its content informs the entry and whether a restricted companion is needed (see Stub File Format below). Root location stubs are often already well-researched DM notes; treat their geography and lore as canon unless the synopses contradict them.
3. Grep all synopsis files under `Campaigns/The Bloody Nails/Sessions/` for the location's name (and any short-form aliases or the names of structures within it). Collect every matching snippet with its session number. Ignore hits inside `Transcript.md` files — never read those.
4. **Reconcile session attributions.** A root stub may cite session numbers from memory; the synopses are the source of truth. If the stub says an event happened in Session N but the synopses place it elsewhere, trust the synopses, correct it in the entry, and flag the discrepancy to the user.
5. Glob for image files matching the location name in `x_Assets/Locations/` and the appropriate subtype subfolder under `Codex/Assets/Locations/` (`Worlds/`, `Continents/`, `Planes/`, `Regions/`, `Cities/`, or `Points_of_Interest/`) — patterns: `Name*.webp`, `Name_with_underscores*.webp` — also check `*.png`. If found, use the real filename **and its subtype subfolder** in the infobox path.

**Region** adds a hub-discovery research step (finding the child Cities/POIs to link) — see `references/locations/region.md`. A **City** is also a hub, but its landmarks, establishments, and people come from its root stub and the synopses rather than a vault-wide grep — see `references/locations/city.md`.

### Stub file format

A root-level stub may be freeform notes. If it contains a `## Restricted` section, treat everything before it as public information and everything under it as DM-only secrets. In this case, automatically create both files without asking — the DM structured it that way intentionally.

---

## Step 3 — Present research and gather details

**If a root stub was found OR synopsis mentions were found (migration mode):**

Present your findings in one message before asking anything:

```
**Research for [Name]**

Root stub: [summary of content, or "empty"]

Synopsis appearances:
- Session N: [brief quote or summary of the relevant snippet]
- Session N: [...]

[Any corrected session attributions — "the stub says X happened in Session N, but the synopses place it in Session M."]

Based on this, I'd suggest: [Major/Minor] — [one sentence reasoning].

What would you like to add before I generate the entry? Drop in any bullet notes —
geography, atmosphere, history, current state, secrets, anything not in the synopses.
```

Wait for the user's notes, then proceed. Don't ask a structured question list in migration mode — the user's notes are freeform and that's fine.

If the stub contained a `## Restricted` section, note that you'll create both files and confirm this is still what they want.

**If this is a fresh location with no existing files (creation mode):**

Ask for everything in one message, using the **creation-mode question list in the subtype doc** (`poi.md` or `region.md`). Only ask for what isn't already provided.

---

## Step 4 — Generate the public document

Assemble the **frontmatter, infobox, and body** from the templates in the subtype doc, observing these shared rules.

### Universal infobox rules

- Escape pipes inside wikilinks within blockquotes using `\|` — Obsidian rendering requirement.
- Omit rows for unknown values — but **always keep the parent row** (`Location` for a POI, `Continent`/`Plane` for a Region); it's the reader's map reference.
- Image path: underscores, no spaces, in **both the filename and the subtype subfolder** — `Codex/Assets/Locations/Points_of_Interest/Location_Name_small.webp` / `Codex/Assets/Locations/Points_of_Interest/Location_Name.webp` for a POI, and `Codex/Assets/Locations/Regions/...` for a Region. Never point the link at the bare `Codex/Assets/Locations/` folder.
- If a real image was found in Step 2, use its actual filename; otherwise use the placeholder (the user generates art from the prompt later).

### Rules that apply to all locations

- The **opening paragraph is world-focused** — describe the place as it exists in Elandis. The party doesn't appear in the opening paragraph; their deeds belong in the Campaign section.
- **Always anchor the place geographically, in a required first body section.** Every location leads its body with a mandatory geography section that places it on the map, then describes its physical setting — and it always comes first, even when the rest of the sectioning flexes:
  - **POI:** `## Location & Geography` — where the *point* sits relative to a known, mappable location (e.g. "north-east of [[Farhaven]]", "in the far south of [[Valtorra]], roughly 50 miles west of [[Darmouth]]"). Mirrors the infobox `Location` field.
  - **Region:** `## Geography & Landscape` — which continent or plane the *area* occupies, what it borders, and its rough extent, then the whole-area terrain and climate. Mirrors the infobox `Continent`/`Plane` field.
  - **City:** `## Geography & Layout` — which region/continent and coast or river the *settlement* sits on, then the map in prose (walls, gates, roads/causeways, waterways, docks, and the districts they form). Mirrors the infobox `Region` field.

  The opening paragraph should gesture at the location too, but this section is where the map reference is guaranteed.
- **Definite-article naming (wiki convention).** Omit a leading "The" from page titles and display text unless "The" is an inseparable part of the proper name. Evocative tavern/inn/shop names keep it (*The Gilded Crow*, *The Rusty Anchor*); fortresses, institutions, civic structures, and natural features take "the" only as an ordinary sentence article, never in the name — *the Red Bastion*, *the High Sept*, *the Underrun*, not *The Red Bastion*. **Never render a doubled article:** when an existing page title genuinely begins with "The", don't write `the [[The High Sept]]` — drop the preceding article, or use a display alias so prose reads correctly: `the [[The High Sept|High Sept]]` → "the High Sept". (Renaming a heavily-linked existing page is out of scope; alias instead.)
- **Session link format:** `#### [[Session N - <Title>]]` — direct basename link, no path, no alias. Each session file's basename is unique vault-wide, so Obsidian resolves it directly. Verify the exact basename (early sessions are zero-padded, e.g. `Session 08 - The High Road`).
- If no campaign appearances were provided, omit the Campaign section entirely.
- Trivia is Major-only.
- The public document contains only what the players currently know. If a restricted companion is also being created, secrets are omitted here and woven into the restricted version instead.

---

## Step 5 — Generate the restricted companion document (if needed)

Create this when: the stub had a `## Restricted` section, the user asked for a restricted doc, or the user flagged restricted content during Step 3.

Write to the subtype's restricted folder:
- POI: `Codex - Restricted/Locations/Points of Interest/<Name> - Restricted.md`
- Region: `Codex - Restricted/Locations/Regions/<Name> - Restricted.md`
- City: `Codex - Restricted/Locations/Cities/<Name> - Restricted.md`

### What the restricted document is

The restricted document holds **only the DM-reserve delta** — the hidden features, secret history, concealed powers, undiscovered locations, and plot hooks deliberately kept *out* of the public entry. It is **not** a copy of the public article. The public entry stays the single source of truth for what the players have found; the restricted doc carries just the reserve, in a lightweight notes format that's quick to jot and edit and detailed enough to fold into the public entry later, when the place is explored or the secret revealed.

**Do not duplicate the public doc.** No copied frontmatter, infobox, geography prose, session logs, or image prompt. If a fact already appears in the public entry, it does not belong here. The public doc owns what's discovered; the restricted doc owns the reserve.

> **Exception — standalone full entry.** Sometimes the DM writes a *complete* entry in restricted first, before the party has reached the place, intending to move it to the public Codex as-is later. Only when the user explicitly says this is a not-yet-public full entry, build the full public-style article here (full frontmatter, infobox, body using the subtype's heading set, image prompt — Steps 4 & 6) instead of the slim delta. The slim delta below is the default.

### Restricted document structure (slim delta — the default)

```markdown
---
Type: Location
tags:
  - dm-notes
---

> [!abstract] Public Entry: *[[<Location Name>]]*

## <Theme heading>
- Concise reserve notes — hidden features, secret history, plot hooks.

## <Another theme>
- ...
```

Guidance:
- Group the reserve material under a few clear `##` headings that fit the content — e.g. `Hidden Features`, `Secret History`, `Undiscovered Locations`, `Concealed Powers`, `Plot Hooks`, `Open Threads`. Don't force a fixed heading set; use what the secrets call for. (For a partly-explored **city**, this is where not-yet-found establishments wait, grouped by district, for the DM to promote into the public hub as the party finds them.)
- Prefer concise bullets. Where the DM has authored substantial reserve prose (a full secret history), keep it as prose under a heading — never discard authored detail.
- Keep `[[wikilinks]]` on proper nouns. Frontmatter is just `Type` + the `dm-notes` tag. No infobox, no image prompt, no duplicated session log.

---

## Step 6 — Generate the image prompt

Place this at the **very top of the public file**, before the frontmatter, in a fenced code block. Always generate it — even if an image already exists. The slim restricted doc gets no image prompt; only a standalone full restricted entry carries one.

Locations use the **same painterly art style as characters** — so the whole wiki shares one look. Only the framing differs: a 16:9 landscape instead of a 3:4 portrait. The `[STYLE]` line must be identical to the character prompt's (just "portrait" → "landscape"); do **not** substitute a matte-painting, semi-realistic, or photoreal style.

```
[STYLE]: Fantasy RPG landscape. Bold painterly strokes, visible brushwork, digital painting aesthetic. Rich dramatic colour palette. NOT photorealistic — stylized like official D&D 5e module artwork.
[SUBJECT]: <the place — key visual features, scale, materials, any notable structures>
[MOOD]: <emotional tone — e.g. "vast, awe-inspiring, ancient", "desolate and haunted">
[LIGHTING]: <dramatic, high-contrast lighting — e.g. "low golden sun and long cool shadows", "shafts of pale light through deep gloom">
[FORMAT]: 16:9 cinematic landscape
```

Keep the `[STYLE]` line identical across every location entry; only `[SUBJECT]`, `[MOOD]`, and `[LIGHTING]` change per place. Derive those three from the place's geography, history, and current state, and make them specific — a good prompt conjures an exact vista, not a generic fantasy backdrop. Favour the warm-against-cool, high-contrast lighting of the character art. The subtype doc has a one-line note on **framing** (foreground a feature for a POI; a characteristic vista for a Region).

**Large settlements (cities, sprawling ports, anything meant to read as vast) are the exception to "make it specific."** Do **not** enumerate the city's individual buildings, streets, causeways, or named landmarks in `[SUBJECT]`. The generator treats every named structure as a must-include and crams them all into frame at equal size — the result looks cluttered, evenly-packed, and obviously AI, and nothing reads as big because everything competes for the same space. Instead:
- **Describe the whole, not the parts.** Lead with the overall form — "an immense walled port city straddling a river mouth," "an endless sprawl of terracotta rooftops climbing into hazy hills." Keep only the broad identity-defining anchors (river, bridge, harbour, wall, dominant roof colour/material).
- **Demote landmarks to background texture.** If notable buildings must appear, frame them as "a few monumental structures rising above the rooftops, distant and small against the scale of the whole — not the focus." Never list them by name or give each its own clause.
- **Sell scale through distance and haze.** Vastness reads from atmospheric depth, not detail. Use "high, distant aerial vista," "atmospheric haze deepening into the distance," "stretching beyond what the eye can hold." This is the single biggest cue that says *huge*.

---

## Step 7 — Write the files

Assemble the **public document** in this order:
1. Image prompt fenced code block
2. Frontmatter (YAML between `---` delimiters)
3. Infobox callout
4. Opening paragraph
5. Remaining body sections

Assemble the **slim restricted doc** (if any) in its own order: minimal frontmatter (`Type` + `dm-notes` tag) → a `> [!abstract] Public Entry: *[[<Name>]]*` callout → themed reserve sections. No H1 title (Obsidian shows the note title already), no image prompt, no infobox. (A standalone full restricted entry instead follows the public order above.)

Write each file to its correct path. Report all paths written when done.

If a root-level stub was detected in Step 2, ask the user to confirm deletion of the stub file — don't delete it automatically. (Because the new Codex file shares the stub's basename, Obsidian will resolve existing `[[Name]]` links to it once the duplicate root file is gone. If the stub had a different name than the Codex page, add the old name to `aliases` so links still resolve.)
