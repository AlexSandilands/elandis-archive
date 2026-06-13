# Codex Location Subtype — City

City-specific content for the codex skill. Read this **together with `references/location.md`** (the shared location workflow) when creating a City. This file holds only what's unique to Cities: the hub-and-spoke model, the creation-mode questions, frontmatter, infobox, body templates, and the gold standard. Everything else — research, migration-mode presentation, restricted-companion machinery, image prompt, write order, and the shared location rules — lives in `location.md`.

A City is a settlement — town, city, or port. Unlike a POI (a single site) it is itself a **hub**: the canonical at-a-glance page for the landmarks, establishments, and people within it, built on the tiered hub-and-spoke model below.

- **Public:** `Codex/Locations/Cities/<Name>.md`
- **Restricted:** `Codex-Restricted/Locations/Cities/<Name> - Restricted.md`

---

## The hub-and-spoke model — read this first

The city doc is the canonical hub for everything in the settlement. Three tiers of content:

- **Tier A — Landmark:** a great structure with its own interior, cast, and plot weight (players go *inside* it). → gets its **own Point of Interest page**; teased and wikilinked from the city doc's **Landmarks** section.
- **Tier B — Establishment:** a shop, tavern, or guildhall with flavour and a proprietor but no interior map. → stays **inline** under its district at full detail, with a plain-text heading.
- **Tier C — Mention:** a name with a line of colour. → named only in the district prose, no heading.

Rules that make the model work:

- **Graduation by link-out, not by moving content.** When a Tier B establishment earns a fuller page (recurring scenes, it becomes a graduated location), it stays inline **at the same level of detail** — the wikilink to its page goes in the **first sentence or two of its description**, never in the heading. **Establishment headings are always plain text** (just the name + the `*(type — quality)*` tag); a link in a heading reads awkwardly. Don't link an establishment at all until it has earned its own page — a thin root stub sharing the name doesn't count. (In the Val Miriel gold standard: River's Watch and Miriel's Rest are linked in their opening lines because they've graduated; The Coal, Fur and Fang, and Silverforge are unlinked.)
- **NPCs follow the same rule:** described inline in their establishment's bullets — the name is **not bolded**, links out to a character page where one exists, and is left plain text where it doesn't.
- **Landmarks and factions each get their own `###` subheading** so they show up in the document outline. As with establishments, the heading is plain text and the page link goes in the first sentence — landmarks (Tier A) and factions always link out, with the city doc noting their presence, never restating a roster.
- **Evergreen.** City docs are timeless portraits. Events ride in the **Campaign** section by default; only a genuinely transformative event graduates to its own short in-body section (DM's judgment per event).

---

## Creation-mode questions

Ask only in creation mode (a fresh settlement with no existing files). In migration mode, use the freeform presentation in `location.md`. Ask for everything in **one message**, and only for what isn't already provided.

**Major City** — ask for:
- Parent region (the `[[Region]]` it sits within) and where on the continent it lies
- Defining feature (the one-line "what is this city")
- Geography & layout (walls, gates, roads/causeways, waterways, docks, and how these divide it into districts — the richer the better)
- History (the founding and the turns that shaped it)
- Government & Imperial presence (who rules, how heavily the [[Valtorran Empire]] leans on the place)
- The people (demographics, daily life)
- Culture & faith (religion, civic identity, any defining fixture like a great market or festival)
- Districts and their establishments (Tier B shops/taverns with proprietors; Tier C mentions)
- Landmarks (Tier A great structures, each → its own POI page)
- Factions present
- Population and Status
- Aliases (alternate names)
- Campaign appearances (session numbers + what happened there)
- If creating a restricted companion: undiscovered locations to stage, plus any secrets / plot hooks

**Minor City / Town** — ask for:
- Parent region, and where it lies
- Defining feature
- A brief description (terrain, character, role, who rules)
- Notable establishments or landmarks within it
- Population and Status
- Campaign appearances (session numbers + brief notes)
- If creating a restricted companion: the secrets to document

---

## Frontmatter

```yaml
---
Type: City
Region: "[[Parent Region]]"
Defining Feature: <short phrase>
Population: <e.g. Hundreds of thousands>
Government: <who rules and how>
Imperial Presence: <none / light / heavy — and the lever>
Importance: Major | Minor
Status: Active | Contested | Ruined | Lost | Unknown
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
- **`Region` is required** — the parent region and the doc's map anchor; always set it, even if approximate.
- `Defining Feature`, `Population`, `Government`, and `Imperial Presence` are included when known — omit any row that genuinely isn't. (For a remote town beyond the Empire's reach, drop the `Imperial Presence` row entirely rather than writing "none".)
- Aliases: YAML inline list `[Name1, Name2]`; omit the field if there are none. See `location.md` for the universal location rules.

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
> Population | <count> |
> Government | <who rules> |
> Imperial Presence | <none / light / heavy — lever> |
> ###### Status
> Attribute |  Details |
> ---|---|
> Status | <status> |
```

- The `Region` row is the reader's map reference — **always keep it**, even when other rows are omitted.
- Image path uses the **Cities** subfolder, underscores, no spaces: `Codex/Assets/Locations/Cities/City_Name.webp` / `..._small.webp`.
- See `location.md` for the universal infobox rules (pipe escaping, omitting unknown rows, image filename).

---

## Body — Major City

```markdown
**City Name** is a [defining feature] in/on [parent region — where it sits in the world]. [One or two sentences on what it is, its scale, and what makes it matter in Elandis — its rulers, its trade, its faith. World-focused; the party does not appear here.]

## Geography & Layout

[**Required first section — every location doc leads with its geography.** Place the city on the map (region, continent, coast or river), then lay the map out in prose — the walls and gates, the main roads or causeways, the waterways, the docks, and how all of that divides the city into the districts the next section catalogues. Convey scale. Prose, not a bullet list, though a short list of the major avenues or quarters is fine.]

## History

[The founding and the major turns that made the city what it is today. Full paragraphs.]

## Government & Imperial Presence

[Who rules and how, and how heavily the [[Valtorran Empire]] leans on the place — the tension between local rule and Imperial control. Drop "& Imperial Presence" from the heading for a city beyond the Empire's reach.]

## The People

[Demographics and daily life — who lives here, the city's character, what an ordinary day turns on.]

## Culture & Faith

[Religion, festivals, civic traditions, identity. Give a defining civic fixture (a great market, a festival, a temple-quarter) its own `###` subsection when it warrants one — see the Val Miriel River Market.]

## Districts

[The hub's core. One `###` subsection per district.]

### District Name

[The district's character in a sentence or two, anchored to the landmark at its head.]

#### Establishment Name *(type — quality)*

[A plain description paragraph — atmosphere, what it sells or serves, what sets it apart. **No callout box.** The heading is plain text; if the establishment has its own page, wikilink it here in the first sentence or two, not in the heading.]

- [[NPC Name]] *(role)* — their place here and a line of flavour.
- Plain NPC Name *(role)* — plain text, unlinked, when they have no page yet.

[Tier C establishments are named in a line of district prose rather than given their own heading.]

## Landmarks

[The city's Point-of-Interest hub. One `###` subheading per Tier A great structure, so each appears in the outline. Heading is plain text; link the structure's POI page in the first sentence, with a one-line gloss on what it is and where in the city it stands.]

### Landmark Name

[The [[Landmark Page]] is <what it is, which district it heads, why it matters>.]

## Factions

[Factions and organisations operating in the city. One `###` subheading each — plain-text heading, link the faction page in the first sentence with a one-line note on its presence here. Don't restate rosters.]

### Faction Name

[The [[Faction Page]] <one-line note on its presence in the city>.]

## [[The Bloody Nails|Campaign: The Bloody Nails]]

#### [[Session N - <Title>]]

[Narrative paragraph: what happened in the city this session, and the party's role in it.]

## Trivia

- [A worldbuilding aside, a naming note, or a behind-the-scenes detail. (Major only.)]
```

---

## Body — Minor City / Town

```markdown
**Town Name** is a [defining feature] in/on [parent region]. [A sentence or two on what it is, who rules it, and its role in the world.]

## Geography & Layout

[**Required.** One to two paragraphs. Place the town on the map, then its layout and character. Wikilink any landmark or notable establishment within it inline.]

## [The People / History / a place-appropriate section]

[A town doesn't need the full Major heading set. Keep Geography & Layout first, then add only the sections the place earns — often a short Districts section or a single descriptive one.]

## [[The Bloody Nails|Campaign: The Bloody Nails]]

#### [[Session N - <Title>]]

Brief summary of what happened here this session — one sentence or a short bullet.
```

The required first body section for a City is **`## Geography & Layout`**. The shared rules (world-focused opening, geography-first, session link format, Trivia is Major-only, public-only content, and the definite-article naming convention) are in `location.md`.

---

## Restricted body heading set (standalone full entry only)

The default restricted companion is a **slim DM-reserve delta** — themed notes only, no body article (machinery in `location.md`). This heading set applies **only** to the standalone-full-entry exception (a complete not-yet-public entry drafted in restricted to move to the public Codex as-is later). In that case, use this subtype's heading set, geography section first:

`## Geography & Layout`, `## History`, `## Government & Imperial Presence`, `## The People`, `## Culture & Faith`, `## Districts`, `## Landmarks`, `## Factions`

**The restricted doc doubles as a staging area for undiscovered locations.** For a city the party hasn't fully explored, the *public* doc lists only what's been discovered; not-yet-found establishments and landmarks wait in the slim restricted doc — grouped by district under an `## Undiscovered Locations` (or similar) heading — and the DM **promotes** them into the public hub as the party finds them, preserving the fun of exploration alongside the usual DM-only plot truths. (The Val Miriel gold standard needs no restricted companion: the party explored it fully, and its remaining secrets live in the relevant character pages.)

---

## Image prompt framing

The shared painterly landscape style is in `location.md` — and **large settlements are the special case** called out there. A city is the one location type where you do **not** make `[SUBJECT]` specific: describe the *whole, not the parts*, never enumerate named buildings, streets, or causeways, demote landmarks to distant background texture, and sell scale through high aerial distance and atmospheric haze. The prompt should conjure one immense vista, not a checklist of structures. See the worked example at the top of the Val Miriel gold standard.

---

## Gold standard

`Codex/Locations/Cities/Val Miriel.md` — the prototype City. Tiered hub-and-spoke (four districts of inline Tier B establishments; the five Tier A landmarks and the two factions each promoted to its own `###` subheading and linked out, never rostered), the required `## Geography & Layout` first, plain-paragraph establishment blocks with plain-text headings and unbolded NPC bullets (page links woven into the description prose, not the heading), the definite-article naming convention applied throughout, a whole-not-parts city image prompt, and a multi-session Campaign section. Read it to see the exact quality bar to match.
