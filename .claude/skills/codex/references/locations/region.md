# Codex Location Subtype — Region

Region-specific content for the codex skill. Read this **together with `references/location.md`** (the shared location workflow) when creating a Region. This file holds only what's unique to Regions: an extra research step, the creation-mode questions, frontmatter, infobox, body templates, and the gold standard. Everything else — migration-mode research, restricted-companion machinery, image prompt, write order, and the shared location rules — lives in `location.md`.

A Region is a broad geographic area (a forest, gulf, mountain range, or plane) that **contains and links to** the Cities and Points of Interest inside it — it is both a lore article and the map-hub that ties its child places together.

- **Public:** `Codex/Locations/Regions/<Name>.md`
- **Restricted:** `Codex - Restricted/Locations/Regions/<Name> - Restricted.md`

---

## Extra research step — discover the child places (hub-building)

In addition to the shared research steps in `location.md`, a Region doc links to the Cities and POIs that sit within it, so find them. Grep `Codex/` for pages whose frontmatter anchors to this region:

- Cities: `grep -rl 'Region: "\[\[<Name>' Codex/ --include="*.md"`
- POIs: `grep -rl 'Location: "\[\[<Name>' Codex/ --include="*.md"`
- Also a loose content grep for the region name across `Codex/` to catch places that reference it in prose but anchor elsewhere.

Collect the matches as candidate entries for the **Settlements & Sites** section. Combine these with any places the DM names in their notes; verify each exact page basename before linking. (Re-run this grep whenever the region doc is later updated, so the hub stays current as child pages are added.)

---

## Creation-mode questions

Ask only in creation mode (a fresh region with no existing files). In migration mode, use the freeform presentation in `location.md`. Ask for everything in **one message**, and only for what isn't already provided.

**Major Region** — ask for:
- Continent (or Plane, for fae/other-planar regions) it occupies, and what it borders
- Defining feature (the one-line "what is this region")
- Geography & landscape (extent, terrain, climate, flora, the things a traveller would see — the richer the better)
- History (how it came to be, the events and peoples that shaped it)
- Peoples & powers (who/what lives there, the ruling faction or court, notable inhabitants)
- Settlements & sites (any the DM wants featured — these supplement the ones auto-discovered above)
- Dangers (region-scale threats and hazards)
- Capital, Ruling power, and neighbouring/connected regions (if any — optional infobox fields)
- Significance (why it matters — strategically, culturally, or to the campaign)
- Status (Active / Contested / Ruined / Lost / Unknown)
- Aliases (alternate names)
- Campaign appearances (session numbers + what happened there)
- If creating a restricted companion: hidden history, secret powers, plot hooks tied to the region

**Minor Region** — ask for:
- Continent (or Plane) and what it borders
- Defining feature
- A brief description (1–3 sentences) — terrain, character, role
- Notable settlements or sites within it (if any)
- Status
- Campaign appearances (session numbers + brief notes)
- If creating a restricted companion: the secrets to document

---

## Frontmatter

```yaml
---
Type: Region
Continent: "[[Continent]]"        # parent/map anchor — REQUIRED. Use Plane: "[[Faewild]]" instead for fae/other-planar regions
Defining Feature: <short phrase>
Capital: "[[Capital City]]"       # optional — the region's seat, if it has one
Ruling Power: <faction or court>  # optional — rename to Ruling Court when apt (e.g. The Unseelie Court)
Connections:                      # optional — neighbouring or linked regions; omit if none
  - "[[Neighbour Region]]"
Importance: Major | Minor
Status: Active | Contested | Ruined | Lost | Unknown
NoteIcon: region
cssclasses:
  - hide-header-underline-3
tags:
  - location
  - location/region
aliases: [AltName]
---
```

Rules:
- The **parent field is required** and is the doc's map anchor. Use `Continent` by default; use `Plane` instead (not in addition) when the region sits in the Faewild or another plane — mirror whichever the place actually belongs to.
- `Capital`, `Ruling Power`/`Ruling Court`, and `Connections` are **optional** — include only those the region actually has, and omit the rest entirely. `Connections` is a YAML list.
- Omit unknown fields; aliases as an inline list (or omit). See `location.md` for the universal location rules.

---

## Infobox

```markdown
> [!infobox|wikipedia]
> # Region Name
> [![[Codex/Assets/Locations/Regions/Region_Name_small.webp|cover hsmall]]](Codex/Assets/Locations/Regions/Region_Name.webp)
> ###### Location Information
> Attribute |  Details |
> ---|---|
> Type | Region |
> Continent | [[Continent\|Display Name]] |
> Defining Feature | <short phrase> |
> Capital | [[Capital City]] |
> Ruling Power | <court or faction> |
> Connections | [[Neighbour]] (relation)<br>[[Other Region\|Other]] (relation) |
> ###### Status
> Attribute |  Details |
> ---|---|
> Status | <status> |
```

- Swap the `Continent` row for a `Plane` row when the region is planar.
- Multi-value `Connections` are separated with `<br>`, each with a short parenthetical on the relationship — match the [[Vale of Eternal Night]] infobox.
- The parent row (`Continent`/`Plane`) is the reader's map reference — **always keep it**, even when other rows are omitted.
- See `location.md` for the universal infobox rules (pipe escaping, omitting unknown rows, image filename).

---

## Body — Major Region

```markdown
**Region Name** is a [defining feature] [in/on — its place within the continent or plane]. [Second sentence: its scale, character, or what makes it matter in Elandis.] [Optional third: the dominant power or peoples, or a defining tension.]

## Geography & Landscape

[**Required first section — every region doc leads with this.** Open by placing the region in the world: which continent or plane it occupies, what it borders, its rough extent and the directions it spans. Then paint the whole-area picture — terrain, climate, flora, the things a traveller crossing it would see and feel. Prose, not a bullet list. This section mirrors the infobox parent field and is the reader's guaranteed map reference.]

## History

[How the region came to be what it is, and the events and peoples that shaped it. Full paragraphs. Rename to "History & Lore" when myth and belief are as load-bearing as recorded fact — see the Vale.]

## Peoples & Powers

[Who and what lives here — peoples, rulers, the dominant faction or court. Wikilink the ruling power and notable inhabitants. Subsection freely when a single power dominates the region (mirror the Vale's "The Unseelie Court" treatment, with sub-headings for its strata).]

## Settlements & Sites

[The region's map-hub. Wikilink the Cities and Points of Interest that sit within it — the ones discovered in research plus any the DM named — each with a one-line gloss on what it is and where in the region it lies. Verify every basename before linking. Omit this section only if the region genuinely contains no documented places.]

- **[[City Name]]** — <what it is, and where in the region it sits>
- **[[Point of Interest]]** — <one line>

## Dangers

[Region-scale threats and hazards — hostile creatures, environmental perils, lawless or cursed stretches. Bullets or prose, whichever fits. Rename to "Hazards" if that reads better for the place.]

## Significance

[Why the region matters — strategically, culturally, or to the campaign. Add further bespoke sections (Relations with a neighbour, a notable Capital, Past Conflicts) as the region warrants — match the depth and free-form sectioning of the [[Vale of Eternal Night]] gold standard.]

## [[The Bloody Nails|Campaign: The Bloody Nails]]

#### [[Session N - <Title>]]

[Narrative paragraph: what happened in this region during the session, and the party's role in it.]

## Trivia

- [A worldbuilding aside, a naming note, or a behind-the-scenes detail]
```

---

## Body — Minor Region

```markdown
**Region Name** is a [defining feature] [in/on — continent or plane]. [Second sentence: its terrain, character, or role in the world.] [Optional third: an atmospheric or historical note.]

## Geography & Landscape

[**Required.** One to two paragraphs. Open by placing the region in the world (continent or plane, what it borders, rough extent), then describe its terrain, climate, and character. Wikilink any known settlements or sites within it inline.]

## [[The Bloody Nails|Campaign: The Bloody Nails]]

#### [[Session N - <Title>]]

Brief summary of what happened here this session — one sentence or a short bullet.
```

The required first body section for a Region is **`## Geography & Landscape`**. The shared rules (world-focused opening, geography-first, session link format, Trivia is Major-only, public-only content) are in `location.md`.

---

## Restricted body heading set (standalone full entry only)

The default restricted companion is a **slim DM-reserve delta** — themed notes only, no body article (machinery in `location.md`). This heading set applies **only** to the standalone-full-entry exception (a complete not-yet-public entry drafted in restricted to move to the public Codex as-is later). In that case, use this subtype's heading set, geography section first:

`## Geography & Landscape`, `## History`, `## Peoples & Powers`, `## Settlements & Sites`, `## Dangers`, `## Significance`

---

## Image prompt framing

The shared painterly landscape style is in `location.md`. For a Region, choose a single *characteristic vista* that captures the whole area — the view that says "this is the region" (e.g. for the [[Vale of Eternal Night]], a sunless blackthorn forest under a bruised-iron sky). Convey scale and breadth rather than one object.

---

## Gold standard

`Vale of Eternal Night.md` (root) — the gold standard for Regions. Literary world-focused prose, geography-first sectioning, a dominant ruling power broken into strata, optional `Plane`/`Capital`/`Ruling Court`/`Connections` frontmatter, YAML list Connections, and `\|` pipe escaping in the infobox. Read it to see the exact quality bar; the body templates above are richer than the bare `x_Templates/Codex/Region.md`, so match the template's *frontmatter/infobox* and the Vale's *prose and sectioning*.
