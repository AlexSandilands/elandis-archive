# Codex Category — Factions

Faction-specific workflow for the codex skill. Read this when the user is creating a faction entry — an organisation, network, order, guild, house, company, cult, or any group that acts as a body in the world.

A single reference covers **all kinds of faction**; the *kind* is captured in a `Category` field rather than in separate templates. Factions also have a lighter sub-document — a **Local Chapter** — for a faction's presence in one city (a Nest, a cell, a lodge). Chapter mode is described at the end of this doc.

## Vault locations

- **Public factions:** `Codex/Factions/<Name>.md`
- **Restricted companion docs:** `Codex - Restricted/Factions/<Name> - Restricted.md`
- **Local chapters:** `Codex/Factions/<Faction> — <City>.md` (restricted companion, if any: `Codex - Restricted/Factions/<Faction> — <City> - Restricted.md`)
- **Root-level stubs:** `<Name>.md` at vault root (migration case)
- **Image assets:** `Codex/Assets/Factions/` (published) and `x_Assets/Factions/` (working copies). Underscores, no spaces — `Order_of_Ravens_small.webp` / `Order_of_Ravens.webp`.

---

## Step 1 — Parse input

Extract from the user's message whatever they've already provided:
- Faction **name**
- **Category** — the kind of faction (criminal network, guild, religious order, noble house, military order, mercenary company, cult, rebel cell…). Free text; pick the phrase that best names what this group *is*.
- **Importance:** Major or Minor
- Whether a **restricted companion document** is also needed
- Whether this is a **Local Chapter** of a parent faction (see Chapter mode) rather than a top-level faction

If anything is missing, ask for it all in one message — don't ask one field at a time. Name and importance are required before proceeding; infer Category from the description and confirm if unsure.

---

## Step 2 — Check for existing files and research the faction

Before asking for details, check the vault:

1. Does `Codex/Factions/<Name>.md` already exist? If so, warn the user and ask whether they want to update/migrate rather than overwrite.
2. Does `<Name>.md` exist at the vault root? If so, read it — use its content to inform both the entry and whether a restricted companion is needed (see Stub File Format below). Root faction stubs are often well-developed DM notes; treat their lore as canon unless the synopses contradict them.
3. Grep all synopsis files under `Campaigns/The Bloody Nails/Sessions/` for the faction's name and its aliases. **Synopsis files are named `Session NN - <Title>.md`, not `Synopsis.md`** — search those and never read `Transcript.md`. Collect every matching snippet with its session number.
4. **Reconcile attributions.** A stub may cite session numbers, member names, or relationships from memory; the synopses and existing character pages are the source of truth. If the stub names a person who is actually a different page (e.g. a stub says "Barak Finegold" but the canonical character is `Barak Stormrider`), link the real page and flag the discrepancy to the user. If the stub places an event in Session N but the synopses place it elsewhere, trust the synopses and correct it.
5. Glob for image files matching the faction name in `x_Assets/Factions/` and `Codex/Assets/Factions/` (patterns: `Name*.webp`, `Name_with_underscores*.webp` — also check `*.png`). If found, use the real filename in the infobox path.

### Resolving member, ally, and place links

Factions are dense with proper nouns. Before writing each wikilink, resolve it to a real page:
- `find . -name "<Name>.md"` for an exact page.
- If a name doesn't resolve, grep for it as a frontmatter alias: `grep -rl "^  - <Term>$" --include="*.md" .` — many pages carry the page name as a bare noun and the short form as an alias (e.g. `The Mawbreakers` with alias `Mawbreakers`, `Valtorran Empire` with alias `Empire`). Write `[[Full Page Name|Display Term]]`.
- A name that resolves to a *different* character (same first name, wrong person) must **not** be linked — leave it as plain text. Verify identity, don't assume.
- A founder, former leader, or off-screen figure who genuinely warrants their own page but doesn't have one yet may be linked as the intended target (e.g. `[[Korvin Blackfeather]]`) — this marks a page worth creating, not an error. Use judgement: link people and groups that are clearly future codex entries; leave one-line operative names as plain text.

### Stub file format

A root-level stub may be freeform notes. If it contains a `## Restricted` section, treat everything before it as public information and everything under it as DM-only secrets. In this case, automatically create both files without asking — the DM structured it that way intentionally. (Factions are a common place for this: the public article is what the rebellion's allies and the party know; the restricted version reveals who really pulls the strings.)

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

[Any reconciled links or attributions — "the stub says 'Barak Finegold' but the
canonical character is Barak Stormrider; I've linked that page."]

Based on this, I'd suggest: [Major/Minor], Category: [kind] — [one sentence reasoning].

What would you like to add before I generate the entry? Drop in any bullet notes —
purpose, structure, history, members, relations, secrets, anything not in the synopses.
```

Wait for the user's notes, then proceed. Don't ask a structured question list in migration mode — the user's notes are freeform and that's fine.

If the stub contained a `## Restricted` section, note that you'll create both files and confirm this is still what they want.

**If this is a fresh faction with no existing files (creation mode):**

Ask for everything in **one message**. Only ask for what isn't already provided.

- Category (kind of faction)
- Purpose & goals — what they stand for, what they're working toward
- Structure & leadership — how they're organised, who leads, how authority flows (note if leadership is secret)
- Allegiance — their political stance (e.g. anti-Empire, Imperial loyalist, independent)
- Base — headquarters or seat of power, if any (many networks are decentralised)
- Notable members — key figures and their roles
- History — origins, turning points, how they reached their current position
- Relations — allies, enemies, uneasy truces with other powers
- Status (Active / Disbanded / Destroyed / Dormant / Hunted / Unknown)
- Aliases (alternate names)
- Campaign appearances (session numbers + what happened)
- If creating a restricted companion: secret leadership, hidden agendas, true allegiances, plot hooks

---

## Step 4 — Generate the public document

### Frontmatter

```yaml
---
Type: Faction
Category: <Criminal & Intelligence Network | Guild | Religious Order | Noble House | Military Order | Mercenary Company | Cult | ...>
Allegiance: <Anti-Empire resistance | Imperial loyalist | Independent | ...>
Leader: "[[Leader Name]]"
Base: <HQ — "[[Place]]" or a short phrase like "Decentralised network of Nests">
Importance: Major | Minor
Status: Active | Disbanded | Destroyed | Dormant | Hunted | Unknown
NoteIcon: faction
cssclasses:
  - hide-header-underline-3
tags:
  - faction
aliases: [AltName]
---
```

Rules:
- Omit any field where the value is unknown — never write `???` or leave blanks.
- **Secret leadership:** when a faction's true leader is concealed even from its own members, set `Leader: Identity concealed` (or name the public-facing figurehead) in the public frontmatter, and reveal the real leader only in the restricted companion. Don't expose the secret here.
- `Base`: a wikilink when the seat is one place; a short descriptive phrase when the faction is decentralised. Omit only if genuinely unknown.
- `Leader`/`Base` wikilinks use YAML list format when there are several; inline string `"[[Name]]"` for one.
- Aliases: YAML inline list `[Name1, Name2]`; omit the field entirely if there are none.

### Infobox

```markdown
> [!infobox|wikipedia]
> # Faction Name
> [![[Codex/Assets/Factions/Faction_Name_small.webp|cover hsmall]]](Codex/Assets/Factions/Faction_Name.webp)
> ###### Faction Information
> Attribute |  Details |
> ---|---|
> Type | Faction |
> Category | <category> |
> Allegiance | <allegiance> |
> Leader | <leader — [[Name]] or "Identity concealed"> |
> Base | <base> |
> ###### Status
> Attribute |  Details |
> ---|---|
> Status | <status> |
```

Rules:
- Escape pipes inside wikilinks within blockquotes using `\|` — Obsidian rendering requirement.
- Omit rows for unknown values.
- Image filename: underscores, no spaces — `Faction_Name_small.webp` / `Faction_Name.webp`, under `Codex/Assets/Factions/`. If a real image was found in Step 2, use its actual filename; otherwise use the placeholder.

### Body

Factions use a fixed three-section backbone, with bespoke sections slotted between **Structure & Leadership** and **History**. The mandatory sections are always present and always in this order; the bespoke ones flex to the faction (a criminal network gets *Known Nests* and *Operations*; a guild might get *Trade & Charter*; a religious order *Tenets & Rites*).

```markdown
**Faction Name** is a [category] [evocative clause — who they are and what they stand for in the world of [[Elandis]]]. [Second sentence: their defining tension, reach, or what makes them matter.]

## Purpose & Goals

[**Mandatory, leads the body.** What drives this faction — their mission, ambitions, and what they are working toward. Full paragraphs. For a group whose stance has shifted over time, capture both what they were and what they have become.]

## Structure & Leadership

[**Mandatory.** How the faction is organised, who leads it, and how authority flows. Use a bold-term list for a clear rank hierarchy, prose for looser structures. If leadership is secret, describe the *role* and how orders propagate without naming the person — the reveal lives in the restricted companion.]

[**Bespoke sections go here** — as many as the faction warrants, named to fit. Examples: `## Known Nests` / `## Chapters` (a table of local presences, linking to chapter docs), `## Operations` (notable jobs or campaigns), `## Symbols & Iconography`, `## Recruitment`, `## Tenets`, `## Holdings`. Match the depth and free-form sectioning of the gold standard.]

## History

[**Mandatory.** The faction's origins, founding figures, key turning points, and how they rose (or fell) to their current position. Full paragraphs.]

## Relations

[When applicable. How the faction interacts with other powers — allies, enemies, uneasy truces. A bold-term list per relationship reads well.]

### [[The Bloody Nails|Campaign: The Bloody Nails]]

#### [[Session N - <Title>]]

[Narrative paragraph: the faction's role in the session and the party's dealings with it.]

## Trivia

- [A worldbuilding aside, a naming note, or a behind-the-scenes detail — Major only]
```

#### Roster tables

- **Notable Members** — when a faction has named key figures, present them as a table: `| Member | Role | Notes |`. Link each member to their page (resolve per Step 2). This can be its own `## Notable Members` section or folded under Structure.
- **Sub-structure tables** — when a faction is organised into local chapters/cells, give them a bespoke table (e.g. `| City | Status | Key Figures |`). Keep the detail here **light** and link out to the chapter doc where one exists: `[[Order of Ravens — Val Miriel\|Val Miriel]]`. The chapter doc holds the local roster and operations; the main doc just orients the reader.

### Rules that apply to the body

- The **opening paragraph is world-focused** — describe the faction as it exists in Elandis. The party doesn't appear in the opening; their dealings belong in the Campaign section.
- **Session link format:** `#### [[Session N - <Title>]]` — direct basename link, no path, no alias. Verify the exact basename (early sessions are zero-padded, e.g. `Session 08 - The High Road`).
- If no campaign appearances were provided, omit the Campaign section entirely.
- Trivia is Major-only.
- The public document contains only what the players currently know. Secrets are omitted here and woven into the restricted companion instead.

---

## Step 5 — Generate the restricted companion document (if needed)

Create this when: the stub had a `## Restricted` section, the user asked for both files, or the user flagged restricted content during Step 3.

Write to: `Codex - Restricted/Factions/<Name> - Restricted.md`

### What the restricted document is

The restricted document is the **full-truth version** of the article — the same backbone as the public document, but with secrets woven naturally into the body. It is what the public article will become once those secrets are revealed. When that day comes, the DM can replace the public file with this one (removing the `> [!abstract] Public Entry:` callout and the `## DM Notes` section).

For factions the most common secret is **who really leads, and to what end** — a concealed Grand Master, a true allegiance behind a public front, a patron the rank and file never see. Reveal it in `Structure & Leadership` and `History`; set the `Leader` field to the real name.

### Restricted document structure

```markdown
[image prompt fenced code block]

[full frontmatter — same schema as public, but with the true Leader and any other revealed fields]

> [!abstract] Public Entry: *[[Faction Name]]*

[Infobox — same as public, but Leader (and any other concealed field) now shows the truth]

[Opening paragraph — same as public, or expanded with the full truth if the public version was deliberately vague]

[Body — same heading set as the public body (Purpose & Goals, Structure & Leadership, bespoke sections, History, Relations), with the full truth woven in: the real leader named in Structure & Leadership, hidden history in History, true allegiances in Relations.]

### [[The Bloody Nails|Campaign: The Bloody Nails]]

#### [[Session N - <Title>]]
[Same as public — campaign appearances are facts, not secrets]

## Trivia
[Same as public, if Major]

## DM Notes

- **Unrevealed leadership / connections:** [Who really runs it, ties not yet known to the party]
- **Hidden agenda:** [What the faction is really working toward beneath the public mission]
- **Plot hooks:** [Ways this faction might factor into future sessions]
- **Open threads:** [Unresolved questions the DM is tracking]
- [Any other DM-side notes — mechanics, session flags, meta-context]
```

---

## Step 6 — Generate the image prompt

Place this at the **very top of each file**, before the frontmatter, in a fenced code block. Always generate it — even if an image already exists. Both files (public and restricted) get the same prompt.

A faction is neither a person nor a place, so its art is its **heraldry** — the symbol the faction is known by, rendered as a **carved-stone emblem** in the same painterly tradition as the rest of the wiki (soft painterly brushwork, *not* flat vector). The crucial thing is that the emblem reads as a **symbol filling the frame, not a physical object in a scene**: the carved stone surface fills the square edge to edge, lit by flat even ambient light with **no directional source, no cast shadows, and no real-world props** (candles, tables, backgrounds) — anything that would make it look like a real tablet photographed on a desk rather than a faction's mark. Same painterly look as characters and locations; the differences are the subject (a symbol, not a figure or vista), the deliberately flat even lighting, and the 1:1 square format.

The emblem prompt has five blocks. `[STYLE]`, `[LIGHTING]`, and `[FORMAT]` are **fixed** — copy them verbatim for every faction. Only `[SUBJECT]`, `[BORDER]`, and `[MOOD]` change per faction (and `[BORDER]` only lightly).

```
[STYLE]: Fantasy RPG heraldic emblem. Soft painterly strokes, visible brushwork, digital painting aesthetic, rich but restrained colour palette. NOT photorealistic, NOT a flat inked vector logo, NOT a hard-outlined crest — stylized like a carved relief in official D&D 5e module artwork, the forms emerging from the stone through gentle modelling rather than bold outlines.
[SUBJECT]: <the faction's central device — the creature or object — displayed heraldically and carved in shallow, soft relief into a square slab of weathered dark grey stone that FILLS the entire frame edge to edge as a flat emblem (a symbol, not an object in a room). Describe the device's silhouette in concrete anatomical/structural terms so it reads unmistakably as what it is. The stone surface is richly textured: pitted, faintly cracked, age-worn, with subtle mottling. <Accent metal — e.g. tarnished silver leaf> catches the raised edges and tips, with faint hints of copper and rust in the hollows, set off against the cool grey stone.>
[BORDER]: a wide double frame carved into the stone — an outer raised border and an inner border line, with a plain, bare recessed channel between them. NO pattern, NO runes, NO letters, NO glyphs, NO symbols — clean carved stone only.
[MOOD]: <what the emblem should evoke — e.g. "secretive and watchful", "proud and martial", "ancient and devout">
[LIGHTING]: flat, even, ambient illumination — no directional light source, no cast shadows, no candle, no props, no background scene; the relief reads through carved depth alone
[FORMAT]: 1:1 square, the carved stone surface fills the frame as a centered emblem
```

Derive the device from the faction's identity — a raven for the Order of Ravens, a gryphon for the Green Gryphons. Make the device **specific and anatomically legible**: a good `[SUBJECT]` conjures one exact crest, not a generic fantasy badge, and spells out the silhouette so the species reads at a glance. (For the Order of Ravens this meant naming the corvid features explicitly — *"facing forward, broad rounded wings spread wide and raised in a symmetric upward V, head turned in sharp profile with a large heavy head, a thick wedge-shaped beak, and a shaggy ruff of throat hackles, the tail fanned downward in a broad wedge"* — because a plain "raven" rendered as a generic small bird. Do the equivalent for whatever the device is.)

Two lessons baked into the template above, learned tuning the Order of Ravens crest:
- **Keep the stone weathered.** Dropping the texture language gives a smooth, lifeless slate; "pitted, faintly cracked, age-worn, with subtle mottling" restores the carved-relic feel.
- **Keep the border plain.** A wide double frame reads well, but filling its channel with runes/glyphs/varied symbols clutters it. A bare recessed channel between two carved lines is the house style. If a faction genuinely warrants ornament, prefer a single simple repeating geometric motif (a chevron or notched fret) over runes or letters — never lettering or glyph-soup.

The `[STYLE]`, `[LIGHTING]`, and `[FORMAT]` lines stay identical for every faction; only `[SUBJECT]`, `[MOOD]`, and (lightly) `[BORDER]` change.

---

## Step 7 — Write the files

Assemble each document in this order:
1. Image prompt fenced code block
2. Frontmatter (YAML between `---` delimiters)
3. Infobox callout
4. Opening paragraph
5. Remaining body sections

Write each file to its correct path. Report all paths written when done.

If a root-level stub was detected in Step 2, ask the user to confirm deletion of the stub file — don't delete it automatically. (Because the new Codex file shares the stub's basename, Obsidian will resolve existing `[[Name]]` links to it once the duplicate root file is gone. If the stub had a different name than the Codex page, add the old name to `aliases` so links still resolve.)

---

## Chapter mode — a faction's local presence in one city

A **Local Chapter** is a faction's branch in a single city — the Order of Ravens' Nest in Val Miriel, a city's cell of the Green Gryphons, a guild's local lodge. It is a lightweight faction sub-document: the parent faction holds the purpose, full structure, and history; the chapter holds *local* detail — who runs it here, where it operates from, its roster, and its local jobs.

**When to use chapter mode:** the user asks for a specific city's branch of a faction ("the Val Miriel Nest", "Darmouth's Green Gryphons"), or a parent faction's roster table points at a chapter that's worth its own page. Keep the parent doc's mention of each chapter light and link out to these.

**Naming:** `<Faction> — <City>` with a spaced em dash — e.g. `Order of Ravens — Val Miriel`, `Green Gryphons — Darmouth`. In the parent doc and in prose, link with a display alias for the natural phrasing: `[[Order of Ravens — Val Miriel\|the Val Miriel Nest]]`. Add the natural phrasing as an `alias` on the chapter doc (e.g. `Val Miriel Nest`) so it resolves both ways.

**Paths:** `Codex/Factions/<Faction> — <City>.md` (restricted companion, if the local branch holds its own secrets: `Codex - Restricted/Factions/<Faction> — <City> - Restricted.md`).

### Chapter frontmatter

```yaml
---
Type: Faction
Category: Local Chapter
Parent Faction: "[[Order of Ravens]]"
City: "[[Val Miriel]]"
Leader: "[[Local Leader]]"
Base: "[[Local HQ]]"
Importance: Major | Minor
Status: Active | Abandoned | Destroyed | Compromised | Unknown
NoteIcon: faction
cssclasses:
  - hide-header-underline-3
tags:
  - faction
  - faction/chapter
aliases: [Natural Phrasing]
---
```

### Chapter infobox

```markdown
> [!infobox|wikipedia]
> # Faction — City
> [![[Codex/Assets/Factions/Faction_City_small.webp|cover hsmall]]](Codex/Assets/Factions/Faction_City.webp)
> ###### Chapter Information
> Attribute |  Details |
> ---|---|
> Type | Local Chapter |
> Parent Faction | [[Order of Ravens]] |
> City | [[Val Miriel]] |
> Leader | [[Local Leader]] |
> Base | [[Local HQ]] |
> ###### Status
> Attribute |  Details |
> ---|---|
> Status | <status> |
```

Always keep the **Parent Faction** and **City** rows — they are the chapter's anchors.

### Chapter body — slim template

No Purpose/Structure/History backbone (those live in the parent). A chapter leads with where it operates and who runs it.

```markdown
**Faction — City** is the [[Parent Faction]]'s presence in [[City]] — [one-line of what this branch is and does locally]. [Second sentence: its standing, reach, or current state in the city.]

## Overview & Base

[**Leads the body.** Where the chapter operates from and how it sits within the city — the front it hides behind, the entrance, any passphrase or concealment, the district. Then what this branch does locally and how it fits the city's politics.]

## Notable Members

| Member | Role | Notes |
|---|---|---|
| [[Local Leader]] | <local rank> | <one line> |

## Local Operations

[When applicable. The jobs, schemes, or events this branch has run locally — kept to what's local; campaign-wide operations stay on the parent doc.]

### [[The Bloody Nails|Campaign: The Bloody Nails]]

#### [[Session N - <Title>]]

[The party's dealings with this branch in the session.]
```

A chapter gets a restricted companion only if the *local* branch holds its own secrets (a double agent in the cell, a hidden local objective). The parent faction's secrets — its true leadership and grand agenda — stay on the parent's restricted doc, not duplicated here.

### Chapter image prompt

Same heraldic emblem prompt and 1:1 format as the parent (Step 6) — a chapter shares its parent's symbol, optionally inflected with a local detail (the city's colours, a local motif worked into the crest).

---

## Gold standard

- **Faction (Major, with restricted companion + chapter):** `Codex/Factions/Order of Ravens.md` + `Codex - Restricted/Factions/Order of Ravens - Restricted.md` — the three-section backbone, bespoke `Known Nests`/`Operations`/`Symbols` sections, a chapter roster table linking out, `Leader: Identity concealed` in public with the true Grand Raven revealed in the restricted version.
- **Local Chapter:** `Codex/Factions/Order of Ravens — Val Miriel.md` — the slim chapter template, Parent Faction/City anchors, local roster, and local operations.

These are the bar. Match them.
