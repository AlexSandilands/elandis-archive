# Codex Location Subtype — Point of Interest

Point-of-Interest-specific content for the codex skill. Read this **together with `references/location.md`** (the shared location workflow) when creating a Point of Interest. This file holds only what's unique to POIs: the creation-mode questions, frontmatter, infobox, body templates, and the gold standard. Everything else — research, migration-mode presentation, restricted-companion machinery, image prompt, write order, and the shared location rules — lives in `location.md`.

A Point of Interest is a single notable place — a ruin, landmark, natural feature, structure, or site within a larger region or city.

- **Public:** `Codex/Locations/Points of Interest/<Name>.md`
- **Restricted:** `Codex - Restricted/Locations/Points of Interest/<Name> - Restricted.md`

---

## Creation-mode questions

Ask only in creation mode (a fresh place with no existing files). In migration mode, use the freeform presentation in `location.md`. Ask for everything in **one message**, and only for what isn't already provided.

**Major Point of Interest** — ask for:
- Parent location (the region/city/continent it sits within)
- Defining feature (the one-line "what is this place")
- Geography / appearance (scale, terrain, materials, atmosphere — the richer the better)
- History (how it came to be, notable events)
- Current state / significance (what it is now, why it matters — strategically, culturally, or to the campaign)
- Status (Active / Ruined / Destroyed / Abandoned / Lost / Unknown)
- Aliases (alternate names)
- Campaign appearances (session numbers + what happened there)
- If creating a restricted companion: any secrets, hidden history, plot hooks tied to the place

**Minor Point of Interest** — ask for:
- Parent location
- Defining feature
- A brief description (1–3 sentences) — appearance, role, atmosphere
- Status
- Campaign appearances (session numbers + brief notes)
- If creating a restricted companion: the secrets to document

---

## Frontmatter

```yaml
---
Type: Point of Interest
Location: "[[Parent Location]]"
Defining Feature: <short phrase>
Importance: Major | Minor
Status: Active | Ruined | Destroyed | Abandoned | Lost | Unknown
NoteIcon: poi
cssclasses:
  - hide-header-underline-3
tags:
  - location
  - location/poi
aliases: [AltName]
---
```

Rules:
- Omit any field where the value is unknown — never write `???` or leave blanks — **except `Location`, which is required** (see below).
- `Location` is the place this sits within and the doc's map anchor — **always set it**. Use the nearest mappable place a reader could find on a map: a settlement, region, or continent. Inline string `"[[Name]]"` for one; YAML list when there are several parent/connected places.
- Aliases: YAML inline list `[Name1, Name2]`; omit the field entirely if there are none.

---

## Infobox

```markdown
> [!infobox|wikipedia]
> # Location Name
> [![[Codex/Assets/Locations/Points_of_Interest/Location_Name_small.webp|cover hsmall]]](Codex/Assets/Locations/Points_of_Interest/Location_Name.webp)
> ###### Location Information
> Attribute |  Details |
> ---|---|
> Type | Point of Interest |
> Location | [[Parent Location\|Display Name]] |
> Defining Feature | <short phrase> |
> ###### Status
> Attribute |  Details |
> ---|---|
> Status | <status> |
```

- The `Location` row is the reader's map reference — **always keep it**, even when other rows are omitted.
- See `location.md` for the universal infobox rules (pipe escaping, omitting unknown rows, image filename).

---

## Body — Major Point of Interest

```markdown
**Location Name** is a [defining feature] in/on/near [parent location — where it sits in the world]. [Second sentence: a key detail, its scale or atmosphere, or what makes it matter.]

## Location & Geography

[**Required first section — every location doc leads with this.** Open by placing the location on the map: where it sits relative to known, mappable places (settlement, region, continent), with directions and distances where known. Then describe its physical geography and setting — scale, terrain, materials, approach, atmosphere — what a traveller would see and feel. Paint a picture, not a bullet list.]

## History

[How the place came to be, and the notable events that shaped it. Full paragraphs.]

## [Significance / Strategic Significance / Current State]

[A place-appropriate section: why it matters, what it's used for now, who frequents or contests it. Rename the heading to fit the place — "Strategic Significance" for a military chokepoint, "Current State" for a ruin, "Significance" for a cultural site. Add further bespoke sections as the place warrants — match the depth and free-form sectioning of the Vale of Eternal Night gold standard.]

### [[The Bloody Nails|Campaign: The Bloody Nails]]

#### [[Session N - <Title>]]

[Narrative paragraph: what happened at or to this place during the session, and the party's role in it.]

## Trivia

- [A worldbuilding aside, a naming note, or a behind-the-scenes detail]
```

---

## Body — Minor Point of Interest

```markdown
**Location Name** is a [defining feature] in/on/near [parent location]. [Second sentence: its role in the world or a defining trait.] [Optional third sentence: a brief atmospheric or historical note.]

## Location & Geography

[**Required.** Concise prose — one to two paragraphs. Open by placing the location on the map (relative to a known, mappable place), then cover what the place is, its appearance, and how it has intersected with the campaign. Focused on what is known.]

### [[The Bloody Nails|Campaign: The Bloody Nails]]

#### [[Session N - <Title>]]

Brief summary of what happened here this session — one sentence or a short bullet.
```

The required first body section for a POI is **`## Location & Geography`**. The shared rules (world-focused opening, geography-first, session link format, Trivia is Major-only, public-only content) are in `location.md`.

---

## Restricted body heading set

When a restricted companion is created (machinery in `location.md`), use this subtype's heading set, geography section first, with the full truth woven in:

`## Location & Geography`, `## History`, `## [Significance / Current State]`

---

## Image prompt framing

The shared painterly landscape style is in `location.md`. For a POI, foreground a defining structure or feature if the place has one (a ruin, a bridge, a chasm).

---

## Gold standard

`Codex/Locations/Points of Interest/Aeolian Chasm.md` — required `## Location & Geography` first, a renamed "Strategic Significance" section, and a multi-session Campaign section. Read it to see the exact quality bar to match.
