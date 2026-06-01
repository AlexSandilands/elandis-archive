# Codex Location Subtype — City

City-specific content for the codex skill. Read this **together with `references/location.md`** (the shared location workflow) when creating a City. This file holds only what's unique to Cities: the hub model, the creation-mode questions, frontmatter, infobox, body templates, the staging-area restricted mechanic, and the gold standard. Everything else — migration-mode research, the base restricted-companion machinery, image prompt, write order, and the shared location rules — lives in `location.md`.

A City is a settlement — a town, city, or port. Like a Region, it is **both a lore article and a map-hub**: it contains districts, establishments, landmarks, factions, and NPCs, and it links out to the ones rich enough to hold their own page. Unlike a Region (which contains whole settlements and wild sites), a City's hub operates at finer grain — streets, shops, and the great buildings within its walls.

- **Public:** `Codex/Locations/Cities/<Name>.md`
- **Restricted:** `Codex - Restricted/Locations/Cities/<Name> - Restricted.md`

---

## The City model — tiered hub-and-spoke

A city has far more inside it than one page can hold at full depth, so it works as a **hub** with everything tiered by how load-bearing it is. The city doc is the **canonical at-a-glance entry for everything in the city**; richer things spoke out to their own pages.

**Three tiers for places inside the city:**

| Tier | What it is | Where it lives |
|---|---|---|
| **A — Landmark** | A great structure with its own interior, cast, and plot weight — players go *inside* it | **Its own Point of Interest page**, teased + linked from the city's **Landmarks** section |
| **B — Establishment** | A shop, tavern, or guildhall with flavour and a proprietor, but no interior map | **Inline** under its district, at full detail |
| **C — Mention** | A name with a line of colour | **Named only** in the district text |

**The threshold test:** *would a player ever follow a link straight to this, or look it up on its own?* Yes → Tier A. It only matters as texture of the city → B or C.

**Graduation by link-out, not by moving content.** When a Tier B establishment or an inline NPC earns a fuller page (the party spent many scenes there; a character recurs), it **stays inline at the same level of detail** — the heading or name simply becomes a `[[wikilink]]` to the deeper page. **Split-out pages are supplementary depth, never replacements.** Nothing shrinks or moves out of the hub; it just gains a link. This applies equally to:
- **Establishments** — the district sub-heading becomes a link to a POI page (e.g. a tavern the party haunts).
- **NPCs** — described inline in their establishment's section, with the name linking out to a character page where one exists. Most named, recurring city NPCs will already have their own character page; link to it, don't restate the bio.

**Districts stay as sections,** not their own pages — they're the city doc's internal structure. Only graduate a district to its own page in the rare case it becomes too rich to sit inline; default is a subsection under `## Districts`.

**City docs are evergreen.** Write a timeless portrait of the place, not a snapshot shaped by recent events. Campaign events ride in the `### Campaign` section by default; only a *genuinely transformative* event (one that permanently changed the city) graduates to its own short in-body section — a judgment call per event, confirmed with the DM.

---

## Extra research step — gather the hub (existing pages that belong to this city)

In addition to the shared research steps in `location.md`, a city links to the characters, factions, and landmark POIs already documented within it. Find them so the hub links out correctly instead of restating content:

- Characters based here: `grep -rln "<City Name>" Codex/Characters/ --include="*.md"`
- Factions/chapters here: `grep -rln "<City Name>" Codex/Factions/ --include="*.md"`
- Landmark POIs already written: check `Codex/Locations/Points of Interest/` for the city's great buildings.

For every NPC and faction that already has a page, **link to it and keep only the inline gloss** — never paste the full bio into the city doc. Verify each exact basename before linking.

---

## Creation-mode questions

Ask only in creation mode (a fresh settlement with no existing files). In migration mode, use the freeform presentation in `location.md`. Ask for everything in **one message**, and only for what isn't already provided.

**Major City** — ask for:
- Parent **Region** (the region or continent it sits in — the map anchor; this is what lets the region hub find it)
- Defining feature (the one-line "what is this city")
- Population / scale (rough size; how long to cross; how cosmopolitan)
- Government (who rules and how)
- Imperial Presence (how heavy the [[Valtorran Empire]]'s hand is here — garrison, governor, light touch, or free)
- Geography & layout (walls, gates, major roads/causeways, waterways, how the city is divided — the map in prose)
- History (founding, how it came to be, the major turns that shaped it)
- The people & daily life
- Culture & faith (religion, festivals, civic identity)
- **Districts** — the city's quarters, each district's character, and the establishments within (Tier B/C)
- **Landmarks** — the great structures that become their own POI pages (Tier A)
- Factions present
- Status (Active / Contested / Occupied / Ruined / Lost / Unknown)
- Aliases (alternate names)
- Campaign appearances (session numbers + what happened there)
- If creating a restricted companion: secrets, hidden history, plot hooks — **and any undiscovered establishments/locations to stage** (see the staging mechanic below)

**Minor City (town / port)** — ask for:
- Parent Region
- Defining feature
- A brief description (1–3 sentences) — character, scale, role
- Government and Imperial Presence (one line each, if known)
- Notable establishments or landmarks within it
- Status
- Campaign appearances (session numbers + brief notes)
- If creating a restricted companion: secrets and/or undiscovered locations to stage

---

## Frontmatter

```yaml
---
Type: City
Region: "[[Parent Region]]"       # parent/map anchor — REQUIRED; lets the region hub discover this city
Defining Feature: <short phrase>
Population: <rough figure or band>
Government: <who rules and how>
Imperial Presence: <Heavy | Moderate | Light | None — and a word on the form it takes>
Importance: Major | Minor
Status: Active | Contested | Occupied | Ruined | Lost | Unknown
NoteIcon: city
cssclasses:
  - hide-header-underline-3
tags:
  - location
  - location/city
aliases: [AltName]
---
```

Rules:
- **`Region` is required** and is the doc's map anchor. Use the nearest mappable containing place — a named region (`"[[Gulf of Miriel]]"`) or, if there's no finer region, the continent (`"[[Valtorra]]"`). The region hub finds its cities by grepping `Region: "[[<Name>`, so this field must be set for the city to appear in its region's **Settlements & Sites**.
- Omit `Population`, `Government`, or `Imperial Presence` only if genuinely unknown — never write `???`.
- `Defining Feature` mirrors the other location subtypes; keep it to one crisp phrase.
- Aliases: YAML inline list `[Name1, Name2]`; omit the field entirely if there are none.

---

## Infobox

```markdown
> [!infobox|wikipedia]
> # City Name
> [![[Codex/Assets/Locations/Cities/City_Name_small.webp|cover hsmall]]](Codex/Assets/Locations/Cities/City_Name.webp)
> ###### Location Information
> Attribute |  Details |
> ---|---|
> Type | City |
> Region | [[Parent Region\|Display Name]] |
> Defining Feature | <short phrase> |
> Population | <figure> |
> Government | <who rules> |
> Imperial Presence | <Heavy / Moderate / Light / None> |
> ###### Status
> Attribute |  Details |
> ---|---|
> Status | <status> |
```

- The `Region` row is the reader's map reference — **always keep it**, even when other rows are omitted.
- Image path uses the **`Cities/`** subfolder with underscores, no spaces, in both the filename and the folder — `Codex/Assets/Locations/Cities/City_Name_small.webp`.
- See `location.md` for the universal infobox rules (pipe escaping, omitting unknown rows, image filename).

---

## Body — Major City

```markdown
**City Name** is a [defining feature] [in/on — its place within the region or continent]. [Second sentence: its scale, its role in the world, what makes it matter in Elandis.] [Optional third: the ruling power, or a defining tension.]

## Geography & Layout

[**Required first section — every location doc leads with this.** Open by placing the city on the map: which region or continent it sits in, what it's near, its setting (coast, river, mountains). Then lay out the city itself in prose — its walls and gates, major roads or causeways, waterways, and how it divides into quarters. This is the map in words; it sets up the Districts section below. Paint it, don't list it.]

## History

[The city's founding and the major turns that shaped it — how it came to be what it is today. Full paragraphs.]

## Government & Imperial Presence

[Who rules and how, and how heavily the [[Valtorran Empire]] leans on the place. Wikilink the ruler(s) and any governing body. For an occupied or governed city, the tension between local rule and Imperial control belongs here.]

## The People

[Who lives here, the demographic character (a human city, a cosmopolitan port, a dwarven hold), and what daily life looks like.]

## Culture & Faith

[Religion, festivals, civic traditions, and identity — what the city believes, celebrates, and prides itself on. Subsection a defining civic feature (a great market, a famous festival) when it warrants it.]

## Districts

[The heart of the hub. One `###` subsection per district/quarter. Lead each with the district's *character* — what it's for, who's there, how it feels — then catalogue its establishments inline. Tier B establishments get a `####` (or bold) sub-heading and full detail; Tier C are named in the prose. NPCs are described inline with the name linking out to a character page where one exists. When an establishment has graduated to its own page, make its sub-heading a wikilink — the inline detail stays put.]

### District Name

[The district's character in a sentence or two.]

#### Establishment Name *(type — quality)*

> [!example]+ Description
> Atmosphere and description of this establishment.

- **[[NPC Name]]** — their role here and a line of flavour.
- **Unpaged NPC** — described inline in full, no link (until they earn a page).

## Landmarks

[The city's POI map-hub. Wikilink the great structures that have (or will have) their own Point of Interest pages — each with a one-line gloss on what it is and where in the city it stands. This is the City's equivalent of a Region's **Settlements & Sites**. Verify every basename before linking.]

- **[[The Great Building]]** — <what it is, which district it heads, why it matters>

## Factions

[Factions and organisations that operate in the city — wikilink each to its faction page, with a one-line note on its presence and reach here. Don't restate the faction's roster; that lives on its own page.]

### [[The Bloody Nails|Campaign: The Bloody Nails]]

#### [[Session N - <Title>]]

[Narrative paragraph: what happened in the city during the session, and the party's role in it.]

## Trivia

- [A worldbuilding aside, a naming note, or a behind-the-scenes detail]
```

---

## Body — Minor City (town / port)

```markdown
**City Name** is a [defining feature] [in/on — region or continent]. [Second sentence: its role or character.] [Optional third: an atmospheric or historical note.]

## Geography & Layout

[**Required.** One to two paragraphs. Place the town on the map (region/continent, what it's near, its setting), then describe its layout and character — a market square, a harbour, the road it sits on. Wikilink any notable places within it inline.]

## Notable Places

[A light list of the establishments and landmarks worth knowing — bold or wikilink each with a one-line gloss. Promote any to their own POI page only when they earn it.]

### [[The Bloody Nails|Campaign: The Bloody Nails]]

#### [[Session N - <Title>]]

Brief summary of what happened here this session — one sentence or a short bullet.
```

The required first body section for a City is **`## Geography & Layout`**. The shared rules (world-focused opening, geography-first, session link format, Trivia is Major-only, public-only content) are in `location.md`.

---

## Restricted companion — secrets *and* a staging area for the undiscovered

A City restricted companion is created for the usual reasons (a `## Restricted` section in the stub, the DM asks for both, or restricted content surfaces in Step 3) **and for one city-specific reason: to stage locations the party hasn't discovered yet.**

The fun of a new city is exploring it. So the **public** city doc lists only what the party has actually discovered, while not-yet-found establishments and landmarks wait in the **restricted** companion. As the party explores, the DM **promotes** each discovered place from the restricted doc into the public hub. This means a city restricted doc may be created **even when there's no plot secret at all** — purely to hold undiscovered content.

In practice:
- For a city the party has fully explored (e.g. their home base), everything is public and **no restricted companion is needed** unless there's a genuine plot secret.
- For a city the party is about to enter, build the public doc with only the known/obvious places (gates, main roads, anything they'd see arriving), and stage the rest in the restricted doc under a clear `## Undiscovered` section, organised by district so promotion is a copy-paste.
- The base restricted-companion machinery (file path, the `> [!abstract] Public Entry:` callout, the `## DM Notes` block) is in `location.md`. The City adds the `## Undiscovered` staging section and may exist *solely* for it.

Restricted file path: `Codex - Restricted/Locations/Cities/<Name> - Restricted.md`.

### Restricted body heading set

Use this subtype's heading set, geography first, with the full truth woven in, plus the staging section:

`## Geography & Layout`, `## History`, `## Government & Imperial Presence`, `## The People`, `## Culture & Faith`, `## Districts`, `## Landmarks`, `## Factions`, then `## Undiscovered` (staged places awaiting promotion) and the shared `## DM Notes`.

---

## Image prompt framing

The shared painterly landscape style is in `location.md`. For a City, choose an *establishing cityscape* — the characteristic skyline or vista that says "this is the city": its walls and gates, its great buildings on the horizon, its harbour or the river through its heart. Convey scale and density, with the warm-against-cool, high-contrast lighting of the character art.

---

## Gold standard

`Codex/Locations/Cities/Val Miriel.md` — the prototype City entry, built from this spec: a `## Geography & Layout` spine (gates, the four causeway Ways, the river, the dock gradient), a `## Districts` hub with establishments inline and NPCs linked out, a `## Landmarks` section spoking to the great-building POIs, and an evergreen portrait that leaves the riots and other events to the Campaign section. Read it once published to match the quality bar. (The source DM notes live at `Val Miriel.md` in the vault root until migrated.)
