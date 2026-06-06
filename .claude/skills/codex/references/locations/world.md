# Codex Location Subtype — World

World-specific content for the codex skill. Read this **together with `references/location.md`** (the shared location workflow) when creating a World entry. This file holds only what's unique to Worlds: an extra research step, the creation-mode questions, frontmatter, infobox, body templates, and the gold standard. Everything else — migration-mode research, restricted-companion machinery, image prompt, write order, and the shared location rules — lives in `location.md`.

A World is the highest-level geographic entry in the Codex. It has **no parent anchor** — it is the world itself (Elandis, the material-plane setting). A World page is the grand hub: it links out to every Continent, lists known Planes, and provides the cosmological and historical overview that gives all other location entries their context.

- **Public:** `Codex/Locations/Worlds/<Name>.md`
- **Restricted:** `Codex - Restricted/Locations/Worlds/<Name> - Restricted.md`

---

## Extra research step — discover child places (hub-building)

In addition to the shared research steps in `location.md`, a World doc links to the Continents it contains and the Planes associated with it. Find them:

- Continents: `grep -rl 'World: "\[\[<Name>' Codex/ --include="*.md"`
- Also a loose content grep for the world name across `Codex/` to catch entries that reference it in prose but don't carry a `World:` frontmatter field.
- Planes: `grep -rl 'Type: Plane' Codex/ --include="*.md"` — collect any Plane docs to list in the Planes section (they're parallel to the world, not nested within it, so they won't have a `World:` field).

Collect the matches as candidate entries for the **Continents** and **Planes** sections. Verify each exact page basename before linking.

---

## Creation-mode questions

Ask only in creation mode (a fresh World entry with no existing files). In migration mode, use the freeform presentation in `location.md`. Ask for everything in **one message**, and only for what isn't already provided.

**Major World** — ask for:
- Defining feature (the one-line "what is this world")
- Scale and overall character (size, age, current era)
- Geography overview (how many continents, major oceans, climate character)
- History of the world (great ages or eras, cataclysms, the events that shaped it — as much depth as the DM has)
- Peoples & Species (the major races, cultures, or peoples spread across the world — not one continent, the whole world)
- Known continents (names and brief descriptions — these become the hub links)
- Known planes associated with the world (Faewild, Shadowfell, etc.) — if any
- Magic & Power (the fundamental arcane or divine forces that shape this world — how magic works, the divine order, major metaphysical forces). Omit if covered in individual Lore entries
- Status
- Aliases (alternate names)
- Campaign appearances (if the world itself, not just a specific place in it, has been a subject of play — e.g. a vision of the world's history, a threat to the world as a whole)
- If creating a restricted companion: hidden history, unknown continents, cosmological secrets, plot hooks

**Minor World** — ask for:
- Defining feature
- A brief description (1–3 sentences) — scale, character, current era
- Known continents or regions (names and one-liners)
- Status

---

## Frontmatter

```yaml
---
Type: World
Defining Feature: <short phrase>
Status: Active | Ancient | Sundered | Unknown
NoteIcon: region
cssclasses:
  - hide-header-underline-3
tags:
  - location
  - location/world
aliases: [AltName]
---
```

Rules:
- A World entry has **no parent field** — it is the top of the geographic hierarchy.
- `Status` options: `Active` (inhabited, ongoing history), `Ancient` (a deep-past or mythic world-state), `Sundered` (broken or fundamentally changed), `Unknown` (the full world hasn't been mapped or its fate is unclear).
- `NoteIcon: region` is the closest available icon — use it until a dedicated world icon exists.
- Omit unknown fields; aliases as an inline list (or omit).

---

## Infobox

```markdown
> [!infobox|wikipedia]
> # World Name
> [![[Codex/Assets/Locations/Worlds/World_Name_small.webp|cover hsmall]]](Codex/Assets/Locations/Worlds/World_Name.webp)
> ###### Location Information
> Attribute |  Details |
> ---|---|
> Type | World |
> Defining Feature | <short phrase> |
> ###### Status
> Attribute |  Details |
> ---|---|
> Status | <status> |
```

- No `Continent` or parent row — the world has no parent.
- If the world has a known cosmological context (e.g. it sits in the Material Plane of a wider cosmology), a `Cosmology` row may be added — but this is uncommon and optional.
- See `location.md` for the universal infobox rules (pipe escaping, omitting unknown rows, image filename).

---

## Body — Major World

```markdown
**World Name** is [defining description — what kind of world this is]. [Second sentence: its age, scale, or the defining character of the current era.] [Optional third: the central tension, the dominant force shaping history, or the cosmological position.]

## Geography

[**Required first section.** Place the world at the largest scale: how many continents, the major oceans and seas, rough climate character, and the overall layout. This isn't a continent-by-continent breakdown (those pages carry the detail) — it's the one paragraph that gives the reader a globe in their head. Wikilink the continents and notable geographic features as they appear.]

## History

[The world's grand history — great ages or eras from earliest memory through the present. Major cataclysms, empire-building and collapse, cosmic shifts that changed the nature of the world. Structure into named eras if the world has a strong historical identity (e.g. "The Age of Circles", "The Sundering", "The Age of Empires"). Full paragraphs.]

## Peoples & Species

[The major peoples and species of the world at the widest scale — not one continent's inhabitants, but the full breadth of who lives here. Dominant races, ancient peoples, widespread cultures. Link individual Codex pages where they exist. This section covers what's world-wide or cross-continental; continent-specific peoples belong in their own Continent pages.]

## Continents

[Hub section — the world's map rolled into a list. One entry per continent, each wikilinked with a one-line gloss on its defining character and rough position on the world. Verify every basename before linking. This list should be kept current as new Continent pages are added.]

- **[[Continent Name]]** — <one-line defining character and position on the world>

## Planes

[Optional. List the known planes tied to or accessible from this world — the Faewild, Shadowfell, and any setting-specific planes. One wikilink and a one-line gloss per plane. Omit this section entirely if planes aren't a significant part of the setting or none have Codex pages yet.]

- **[[Plane Name]]** — <one-line nature and its relation to this world>

## Magic & Power

[Optional, Major only. The world's arcane and divine architecture at the widest scale — how magic works fundamentally, the divine order, the major metaphysical forces that shape history. Omit if this is better covered in individual Lore (Cosmology) entries; include here when it's indispensable context for reading any other location in the Codex.]

## [[The Bloody Nails|Campaign: The Bloody Nails]]

#### [[Session N - <Title>]]

[Campaign appearances for a World entry are rare — include only when the party engaged with the world itself as a subject (a vision of deep history, a threat to the world as a whole, a cosmological revelation). Otherwise omit this section entirely.]

## Trivia

- [A worldbuilding aside, a naming note, or a behind-the-scenes detail]
```

---

## Body — Minor World

```markdown
**World Name** is [defining description]. [Second sentence: its character, age, or current state.]

## Geography

[**Required.** One to two paragraphs. Place the world at the largest scale — how many continents, the major oceans, the broad climate. Wikilink known continents inline.]

## [[The Bloody Nails|Campaign: The Bloody Nails]]

#### [[Session N - <Title>]]

Brief summary if applicable — one sentence or a short bullet.
```

The required first body section for a World is **`## Geography`**. The shared rules (world-focused opening, geography-first, session link format, Trivia is Major-only, public-only content) are in `location.md`.

---

## Restricted body heading set (standalone full entry only)

The default restricted companion is a **slim DM-reserve delta** — themed notes only, no body article (machinery in `location.md`). This heading set applies **only** to the standalone-full-entry exception. In that case, use these headings, geography section first:

`## Geography`, `## History`, `## Peoples & Species`, `## Continents`, `## Planes`, `## Magic & Power`

---

## Image prompt framing

The shared painterly landscape style is in `location.md`. For a World entry, choose a framing that conveys **planetary or cosmological scale** — either an orbital or high-altitude vista showing the curve of the world, a landmark that embodies the whole world's identity (an ancient world-tree, a world-spanning sea, a sky full of moons), or the most iconic landscape that reads as "this world". Avoid showing a specific town or ruin — the image should feel like the world itself.

---

## Gold standard

There is currently no finished World entry in the Codex — Elandis is the first. Mirror the quality bar of the best Region entries (`Vale of Eternal Night.md`) but at a grander scale: literary world-focused prose, geography-first, with grand-historical sweep in the History section. Aim for the tone of an encyclopaedia entry on Earth written for someone who has never heard of it.
