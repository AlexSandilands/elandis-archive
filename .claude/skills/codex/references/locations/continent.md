# Codex Location Subtype — Continent / Plane

Continent/Plane-specific content for the codex skill. Read this **together with `references/location.md`** (the shared location workflow) when creating a Continent or Plane entry. This file holds only what's unique to these subtypes: an extra research step, the creation-mode questions, frontmatter, infobox, body templates, and the gold standard. Everything else — migration-mode research, restricted-companion machinery, image prompt, write order, and the shared location rules — lives in `location.md`.

**Continent vs Plane — the distinction:**
- A **Continent** is a landmass within the world (e.g. Valtorra). Its parent is the World (`World: "[[Elandis]]"`). It contains Regions, which contain Cities and POIs.
- A **Plane** is a self-contained realm of existence running parallel to or beyond the material world (e.g. Faewild, Shadowfell). It has no parent World anchor — it is its own domain. It contains Regions (and Cities/POIs within those).

Both use this same reference because their structure, scale, and hub function are identical. The Plane body template adds two sections absent from continents: **Nature of the Plane** (planar properties) and **Entry & Egress** (how to get there and back). The Plane-specific additions are clearly marked below.

- **Continent public:** `Codex/Locations/Continents/<Name>.md`
- **Plane public:** `Codex/Locations/Planes/<Name>.md`
- **Restricted:** `Codex - Restricted/Locations/Continents/<Name> - Restricted.md` (Continents) or `Codex - Restricted/Locations/Planes/<Name> - Restricted.md` (Planes)

---

## Extra research step — discover child places (hub-building)

In addition to the shared research steps in `location.md`, a Continent/Plane doc links to the Regions it contains, so find them. Grep `Codex/` for pages whose frontmatter anchors to this entry:

- Regions on a Continent: `grep -rl 'Continent: "\[\[<Name>' Codex/ --include="*.md"`
- Regions within a Plane: `grep -rl 'Plane: "\[\[<Name>' Codex/ --include="*.md"`
- Also a loose content grep for the name across `Codex/` to catch places that reference it in prose but anchor elsewhere.

Collect the matches as candidate entries for the **Regions & Territories** section. Verify each exact page basename before linking. (Re-run this grep whenever the continent/plane doc is later updated, so the hub stays current as child pages are added.)

---

## Creation-mode questions

Ask only in creation mode (a fresh entry with no existing files). In migration mode, use the freeform presentation in `location.md`. Ask for everything in **one message**, and only for what isn't already provided.

**Major Continent** — ask for:
- Parent World (required for continents — which world it sits on)
- Defining feature (the one-line "what is this continent")
- Geography (position on the world, bordering seas, rough extent, major terrain zones and climate bands — the continental overview)
- History (the great ages, founding civilisations, empires built and fallen, the events that shaped the continent)
- Peoples & Powers (dominant cultures, ruling empires or factions, the major forces operating at continental scale)
- Regions & Territories (the named regions the DM wants documented — these supplement the ones auto-discovered above)
- Dangers (continent-scale threats — ancient evils, ongoing wars, environmental hazards spanning multiple regions)
- Capital and Ruling Power (if the continent has a single seat of power or dominant empire — optional)
- Connections (other continents or planes with strong links — trade routes, historical ties, ongoing conflicts)
- Status
- Aliases (alternate names)
- Campaign appearances (session numbers + what happened at continental scale)
- If creating a restricted companion: hidden history, secret powers, continent-scale plot hooks

**Minor Continent** — ask for:
- Parent World
- Defining feature
- A brief description (1–3 sentences) — geography, character, role
- Notable regions within it (if any)
- Status
- Campaign appearances (session numbers + brief notes)

**Major Plane** — ask for:
- Defining feature (the one-line "what is this plane")
- Nature of the plane (fundamental rules of reality — how time, magic, and physics work differently here; what a traveller would feel the moment they arrive)
- Geography (the physical character of the plane — its terrain, sky, whether it has geography at all, and its scale or boundlessness)
- History (how the plane came to exist or was shaped, the great events in its past)
- Peoples & Powers (the native denizens, ruling courts or factions — the Unseelie Court, the lords of a plane, etc.)
- Regions within the plane (named areas, sub-realms, notable territories — supplements auto-discovered ones)
- Dangers (plane-specific hazards — time distortion, predatory spirits, the physical toll of the plane's nature)
- Entry & Egress (how travellers enter and leave — portals, rituals, known crossing points, the risks of staying too long)
- Capital and Ruling Court (if the plane has a seat of power — optional)
- Connections (other planes or the material world this one brushes against)
- Status
- Aliases
- Campaign appearances

**Minor Plane** — ask for:
- Defining feature
- A brief description — nature, character, danger level
- Known regions or named sub-realms
- Entry method (brief — how does one get here?)
- Status

---

## Frontmatter

### Continent

```yaml
---
Type: Continent
World: "[[Elandis]]"            # Required — the world this continent sits on
Defining Feature: <short phrase>
Capital: "[[Capital City]]"     # optional — the continent's seat of power, if it has one
Ruling Power: <faction or empire> # optional
Connections:                    # optional — other continents or planes with significant links
  - "[[Other Continent]]"
Importance: Major | Minor
Status: Active | Contested | Ruined | Lost | Unknown
NoteIcon: region
cssclasses:
  - hide-header-underline-3
tags:
  - location
  - location/continent
aliases: [AltName]
---
```

### Plane

```yaml
---
Type: Plane
Defining Feature: <short phrase>
Capital: "[[Seat of Power]]"    # optional — e.g. the Unseelie Court's stronghold
Ruling Power: <court or faction> # optional — rename to Ruling Court when apt
Connections:                    # optional — planes or worlds this one touches
  - "[[Elandis]]"
Importance: Major | Minor
Status: Active | Contested | Unknown
NoteIcon: region
cssclasses:
  - hide-header-underline-3
tags:
  - location
  - location/plane
aliases: [AltName]
---
```

Rules:
- **Continent requires `World:`** — this is the doc's parent anchor and map reference. Never omit it.
- **Plane has no parent field** — it is a self-contained realm. Use `Connections:` instead to name what it borders or touches.
- `Capital`, `Ruling Power`/`Ruling Court`, and `Connections` are optional in both cases — include only those that actually apply.
- `Connections` is a YAML list.
- Omit unknown fields; aliases as an inline list (or omit).

---

## Infobox

### Continent

```markdown
> [!infobox|wikipedia]
> # Continent Name
> [![[Codex/Assets/Locations/Continents/Continent_Name_small.webp|cover hsmall]]](Codex/Assets/Locations/Continents/Continent_Name.webp)
> ###### Location Information
> Attribute |  Details |
> ---|---|
> Type | Continent |
> World | [[Elandis\|Elandis]] |
> Defining Feature | <short phrase> |
> Capital | [[Capital City]] |
> Ruling Power | <empire or faction> |
> Connections | [[Other Continent]] (relation)<br>[[Plane\|Plane]] (relation) |
> ###### Status
> Attribute |  Details |
> ---|---|
> Status | <status> |
```

### Plane

```markdown
> [!infobox|wikipedia]
> # Plane Name
> [![[Codex/Assets/Locations/Planes/Plane_Name_small.webp|cover hsmall]]](Codex/Assets/Locations/Planes/Plane_Name.webp)
> ###### Location Information
> Attribute |  Details |
> ---|---|
> Type | Plane |
> Defining Feature | <short phrase> |
> Ruling Court | <ruling power> |
> Connections | [[Elandis\|Material World]] (border plane)<br>[[Other Plane\|Other]] (relation) |
> ###### Status
> Attribute |  Details |
> ---|---|
> Status | <status> |
```

- **Continent:** The `World` row is the reader's map reference — always keep it.
- **Plane:** No parent row. `Connections` carries the spatial relationship instead.
- Multi-value `Connections` rows use `<br>` with a short parenthetical, as in the Region infobox.
- See `location.md` for the universal infobox rules (pipe escaping, omitting unknown rows, image filename).
- Image paths: `Codex/Assets/Locations/Continents/...` for continents, `Codex/Assets/Locations/Planes/...` for planes.

---

## Body — Major Continent

```markdown
**Continent Name** is a [defining feature] [in/on — its position on the world or relative to known seas]. [Second sentence: its scale, character, or the defining tension of the current era.] [Optional third: the dominant power, its relation to the Empire, or a historical shadow.]

## Geography & Landscape

[**Required first section.** Open by anchoring the continent: which world it sits on, which seas it faces, its rough position (north, south, east, west) and extent. Then describe the continental-scale terrain — major mountain ranges, great rivers, climate zones, dominant flora. This is the overview; individual Region pages carry the detail. Wikilink Regions, seas, and major geographic features as they appear.]

## History

[The continent's grand history — founding civilisations, great ages, the rise and fall of empires, cataclysms that reshaped it. Full paragraphs. Structure into named eras if the continent has a strong historical identity. Wikilink historical factions, places, and events where Codex pages exist.]

## Peoples & Powers

[Who shapes this continent at the widest scale — dominant cultures, ruling empires, the major factions that operate across more than one region. Wikilink the ruling power and notable factions. Subsection freely when a dominant empire warrants its own treatment (e.g. "The Valtorran Empire" as a sub-heading with its own strata). Continent-specific peoples belong here; world-wide peoples belong in the World doc.]

## Regions & Territories

[Hub section — the continent's map in a list. Every Region wikilinked with a one-line gloss on what it is and where on the continent it lies. Include all auto-discovered matches from the hub-building step plus any the DM named. Verify every basename before linking. Keep this list current as new Region pages are added.]

- **[[Region Name]]** — <what it is, and where on the continent it lies>

## Dangers

[Continental-scale threats — ancient evils that span multiple regions, ongoing wars or conflicts, environmental hazards operating at the widest scale. Bullets or prose, whichever fits.]

## Significance

[Optional, Major. Why this continent matters — geopolitically, to the campaign's central conflict, or cosmologically. Add further bespoke sections (relations with a neighbouring continent, a dominant religion, a named great war) as the continent warrants.]

## [[The Bloody Nails|Campaign: The Bloody Nails]]

#### [[Session N - <Title>]]

[Narrative paragraph: what happened at continental scale this session, and the party's role in it.]

## Trivia

- [A worldbuilding aside, a naming note, or a behind-the-scenes detail]
```

---

## Body — Major Plane

The Plane body is the same as a Major Continent body, with these differences:
- Replace `## Geography & Landscape` with a two-section opening: `## Nature of the Plane` (required, goes first, before Geography) + `## Geography & Landscape` (required, goes second). The geography section anchors the physical space; the nature section anchors the plane's fundamental rules.
- Add `## Entry & Egress` after `## Peoples & Powers` and before `## Regions & Territories`.
- `## Regions & Territories` may be renamed `## Realms & Territories` if the plane uses "realms" as its vocabulary.

### Nature of the Plane (Planes only — required, goes first)

```markdown
## Nature of the Plane

[The fundamental rules of this plane — what a traveller experiences the moment they step through. Does time pass differently here? Is magic enhanced, altered, or suppressed? Do normal physical laws hold? What does the air, light, and sound feel like? This section is what makes the plane feel *alien*, and it grounds every other detail.]
```

### Entry & Egress (Planes only)

```markdown
## Entry & Egress

[How one gets to this plane and back. Known portals, their locations, and who controls them. Rituals or conditions required for entry. The risks of lingering — do you age, forget your old life, become fey-touched? Are there ways to be stranded? This section should feel like practical adventuring knowledge laced with threat.]
```

---

## Body — Minor Continent

```markdown
**Continent Name** is a [defining feature] [on/in — world context]. [Second sentence: its terrain, character, or role.]

## Geography & Landscape

[**Required.** One to two paragraphs. Open by placing the continent on the world (which world, where roughly, what seas it faces), then describe its terrain, climate, and character. Wikilink known regions inline.]

## [[The Bloody Nails|Campaign: The Bloody Nails]]

#### [[Session N - <Title>]]

Brief summary of what happened here this session — one sentence or a short bullet.
```

---

## Body — Minor Plane

```markdown
**Plane Name** is a [defining feature] — [one-sentence character of the plane, its feel or fundamental rule].

## Nature of the Plane

[**Required.** One to two paragraphs. The fundamental rules, what a traveller feels on arrival, and what makes this plane dangerous or strange.]

## Geography & Landscape

[**Required.** One to two paragraphs. The physical character of the plane — terrain, sky, scale, named sub-realms if any. Wikilink known regions inline.]

## [[The Bloody Nails|Campaign: The Bloody Nails]]

#### [[Session N - <Title>]]

Brief summary of what happened here this session — one sentence or a short bullet.
```

The required first body section for a Continent is `## Geography & Landscape`. For a Plane it is `## Nature of the Plane`, followed immediately by `## Geography & Landscape`. The shared rules (world-focused opening, geography-first, session link format, Trivia is Major-only, public-only content) are in `location.md`.

---

## Restricted body heading set (standalone full entry only)

The default restricted companion is a **slim DM-reserve delta** — themed notes only, no body article (machinery in `location.md`). This heading set applies **only** to the standalone-full-entry exception.

**Continent:** `## Geography & Landscape`, `## History`, `## Peoples & Powers`, `## Regions & Territories`, `## Dangers`, `## Significance`

**Plane:** `## Nature of the Plane`, `## Geography & Landscape`, `## History`, `## Peoples & Powers`, `## Entry & Egress`, `## Regions & Territories`, `## Dangers`

---

## Image prompt framing

The shared painterly landscape style is in `location.md`. For a Continent, choose the single most characteristic vista that captures the whole — the view a traveller arriving by sea would see, or a dramatic overhead angle showing the great terrain features (a continent-spanning mountain range, a vast inland sea). Convey scale and breadth rather than one settlement or ruin.

For a Plane, lean into the alien quality: the lighting, sky, and atmosphere should feel *wrong* in a beautiful or terrifying way. The image should say "you are not in the material world" — an eternal twilight sky, trees made of crystal, a forest where the horizon is above your head. The style stays painterly (same `[STYLE]` line as always); only `[SUBJECT]`, `[MOOD]`, and `[LIGHTING]` convey the planar strangeness.

---

## Gold standard

There is currently no finished Continent or Plane entry in the Codex — Valtorra and Faewild are the first candidates. Mirror the quality bar of the best Region entries (`Vale of Eternal Night.md` at root) but at a grander scale. For a Continent, aim for the sweep of an encyclopaedia entry on a real continent — geography, history, peoples, and power. For a Plane, aim for the tone of a sourcebook entry on the Feywild: poetic but with practical adventuring weight.
