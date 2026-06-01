# Codex Lore Subtype — Deity

Deity-specific content for the codex skill. Read this **together with `references/lore.md`** (the shared lore workflow) when creating a Deity entry. This file holds only what's unique to Deities: the tier model and the public/restricted line it drives, the creation-mode questions, frontmatter, infobox, body templates, image framing, and gold standard. Everything else — migration-mode research, restricted-companion machinery, write order, and the shared lore rules — lives in `lore.md`.

A **Deity** is a god or divine being — a power that is *worshipped, prayed to, or reckoned divine*. Unlike a Concept (a timeless structure or force) or an Event (a happening), a deity is a *being* with a will, a portfolio of things it governs, and a relationship — present or lost — with the mortals who do or don't revere it. It is the one Lore subtype centred on a *person-like* figure, which is why it borrows the portrait framing of a Character for its art.

- **Public:** `Codex/Lore/<Name>.md`
- **Restricted:** `Codex - Restricted/Lore/<Name> - Restricted.md`

---

## The divine order — place the god in its tier first

Elandis has a specific, three-tier divine structure, and **the single most important thing a deity entry does is place its subject in that structure** — because the tier decides the entire shape of the public/restricted split. The full cosmology lives on the restricted [[World Tree]] and [[The Shattering]] pages; the short version:

1. **The [[World Tree]]** — the one genuinely transcendent god, above all others. (Already a Concept entry, not a Deity. A deity page never sits here.)
2. **The Gods of Old** — the ancient, *true* gods (the restricted cosmology calls them the **True Gods**; "Gods of Old" is the same tier, and the better in-world term for a deity page). Real powers, older than the Shattering, who by long habit do not reach directly into the world. Most are **forgotten** — their worship faded after the Shattering. *Selûne and Shar are Gods of Old.*
3. **The [[The Pantheon|Seven Divines]]** — the seven mortal champions the Gods of Old empowered at the end of the [[Chaos Wars]]. They ascended to lingering demigodhood, and as centuries passed the world forgot the old gods and gave its worship to these saviours instead. The dominant faith prays to the Seven, mistaking them for eternal gods. *Elaris Moonsong is a Seven Divine — and was Selûne's mortal champion.*

**This tier is itself a secret.** That the Seven are ascended mortals, that the Gods of Old stand behind them, that any of this hierarchy exists — none of it is public knowledge. Never state it on a public page. The public page reflects what the *world* believes; the restricted page carries the tier and its truths.

### The two archetypes (this is the whole game)

Which tier the god sits in produces one of two opposite public/restricted shapes. Settle which one you're writing before anything else:

- **A forgotten God of Old** (Selûne, Shar). The world barely remembers them — a scholar's footnote, a folk fragment, or (Shar) nothing but a name in a warning. So the **public page is thin and folkloric** — the faded memory, the half-understood myth — and the **restricted page is where the god comes alive**: that they are real, a true power, still capable of acting, and what they are doing now. The `## In Memory & Belief` section carries the gap, and is often the richest part of the public page precisely because so little is *known*.
- **A worshipped Seven Divine** (Elaris, Grumbar, and the rest of [[The Pantheon]]). The world reveres them as eternal gods, so the **public page is rich** — full portfolio, temples, clergy, holy days, relics, the works. The **restricted truth is the demotion**: that this "eternal god" was a mortal champion of the Shattering, a lingering demigod standing in for the distant Gods of Old, with a mortal life and death behind the divine mask. The truth most expands `## Overview`, `## Divinity`, and `## In Memory & Belief`.

A god may also have *no public face at all* (Shar): no temples, no clergy, no faith — perhaps only a single epithet a frightened priest let slip. Then `## Worship` shrinks to a sentence on that absence (or folds into `## In Memory & Belief`), and the entry is **almost entirely restricted**. Say so plainly rather than padding a public page that the world wouldn't have.

**When a forgotten god has been *supplanted by a successor* the world still worships** (Selûne by her ascended champion [[Elaris Moonsong|Elaris]]), two things follow, and both are easy to get wrong:
- The god's rites, relics, and holy days often **survive displaced into the successor's faith** — so a "forgotten" god's public `## Worship` can be genuinely *rich*, presented as the living faith's, with the true author revealed only in the restricted companion. Don't assume forgotten means an empty Worship section.
- The **specific link between the two** — that the successor was this god's own champion, and the era it happened — is itself part of the tier secret. The public page may say the faith now venerates the successor and the elder god is forgotten; it must **not** state that the successor was the god's champion, or pin the connection to a dateable event. That connection and its history belong only in restricted.

## Scope — the god, its faith, its champion

A Deity page is about *the god*. Three neighbours commonly tangle with it; keep the boundaries clean:

- **The god vs. its faith/church.** A god is a Deity; the organised religion that worships it (a temple, a holy order, a priesthood) is a **Faction**, and a specific temple building is a **Location**. Summarise the worship *on the deity page* (`## Worship`); spin the institution out to its own Faction/Location entry and link to it. (The High Sept, the Stoneheart — Locations; their clergy — potential Factions.)
- **The god vs. its mortal Chosen/champion.** A Chosen is a **Character**, not part of the deity. Selûne's champion [[Elaris Moonsong - Restricted|Elaris]] is his own page (and, being a Seven Divine, his own *Deity* page too). Reference the bond from the god's page; don't absorb the champion's biography into it.
- **The god vs. the event that defined it.** A god's defining deed (Selûne empowering her champion at the Shattering) is told *here in summary* as a bespoke section, with the fuller account left to the relevant Event or Character page — the same rule Concepts follow.

---

## Creation-mode questions

Ask only in creation mode (a fresh deity with no existing files). In migration mode, use the freeform presentation in `lore.md`. Ask for everything in **one message**, and only for what isn't already provided.

**Major Deity** — ask for:
- **Tier** — a God of Old, or one of the Seven Divines? (This sets the public/restricted split — see above. Confirm it first.)
- The one-line "what god is this" (the defining summary)
- Portfolio & domains — what they are the god *of*, and what they stand for (their values, not just their sphere)
- Worship — who reveres them, clergy/temples, holy days and rites, relics, prayers, iconography and holy symbol (or, if forgotten, what little of this survives — and whether anyone worships them at all)
- Myths & deeds — the god's defining stories and role: their place among the gods, their relationships to other deities, the deeds the faith tells of them (told here in summary)
- In memory & belief — how the world knows them *now*: revered as eternal, half-forgotten, mistaken for another, or unknown; folk understanding vs. the truth
- Status (see vocabulary below — Worshipped / Forgotten / Active / Withdrawn / Dead / Unknown)
- Aliases (alternate names, titles, epithets)
- Campaign appearances (session numbers + what happened)
- If creating a restricted companion: the tier truth (the demotion, or the living reality behind the forgotten myth), their true designs, hidden relationships, plot hooks

**Minor Deity** — ask for:
- Tier, and the one-line "what god is this"
- A brief account (a few sentences) — portfolio, and who (if anyone) reveres them
- How they're remembered / worshipped (one line), if notable
- Status
- Campaign appearances (session numbers + brief notes)
- If creating a restricted companion: the secrets to document

---

## Frontmatter

```yaml
---
Type: Lore
Category: Deity
Pantheon: <Gods of Old | The Seven Divines>          # the tier the world can place them in
Portfolio: <moon, light, forgiveness, wanderers>      # what they govern and stand for
Domains: <Knowledge, Life>                             # optional — D&D cleric domains
Symbol: <holy symbol / iconography>                   # optional — e.g. "A pair of eyes ringed by seven stars"
Chosen: "[[Champion Name]]"                            # optional — their mortal champion / Chosen
Revered by: <who worships them>                        # optional — e.g. "Sailors and wanderers" / "None openly"
Era: <evocative age phrase>                            # optional — a god is timeless; e.g. "Of the age before the Seven"
Related:
  - "[[The Pantheon]]"
Importance: Major | Minor
Status: Worshipped | Forgotten | Active | Withdrawn | Dead | Unknown
NoteIcon: lore
cssclasses:
  - hide-header-underline-3
tags:
  - lore
  - lore/deity
aliases: [AltName, Title]
---
```

Rules:
- **`Pantheon`** is the deity's orienting field — the tier the world can openly place them in (`Gods of Old` for an ancient god; `The Seven Divines` for an ascended one). It does *not* leak the secret (that the Seven are mortal, that the Gods of Old hide behind them) — that lives in restricted prose, not here.
- **`Status`** describes the god's present standing: `Worshipped` (an active public faith — the Seven), `Forgotten` (a lapsed god the world has lost — most Gods of Old), `Active` (moving in the world now — use on the *restricted* page when a "forgotten" god is in fact stirring, e.g. Selûne reaching for a Chosen), `Withdrawn`, `Dead`, or `Unknown`. A god's public and restricted pages may carry *different* Status values when the truth differs (public `Forgotten` → restricted `Active`).
- **`Chosen`** links the god's mortal champion if they have one; omit otherwise. **`Symbol`** anchors the iconography that the infobox image and `## Worship` will echo.
- `Era` is optional and evocative (a god is timeless), like a Concept — not a date. See `lore.md` for the shared frontmatter rules (omit unknowns; `Related`/`aliases` omitted when empty; `Related` must not leak a secret connection on the public page).

---

## Infobox

```markdown
> [!infobox|wikipedia]
> # Deity Name
> [![[Codex/Assets/Lore/Deity_Name_small.webp|cover hsmall]]](Codex/Assets/Lore/Deity_Name.webp)
> ###### Lore Information
> Attribute |  Details |
> ---|---|
> Type | Lore |
> Category | Deity |
> Pantheon | <Gods of Old / The Seven Divines> |
> Portfolio | <moon, light, forgiveness> |
> Domains | <Knowledge, Life> |
> Symbol | <holy symbol> |
> Chosen | [[Champion Name]] |
> Revered by | <who> |
> ###### Status
> Attribute |  Details |
> ---|---|
> Status | <status> |
```

- Always keep the `Category` and `Pantheon` rows — they orient the reader to what the god *is* and where it sits. Omit any other row whose value is unknown.
- See `lore.md` for the universal infobox rules (pipe escaping with `\|`, omitting unknown rows, real image filename when one was found).

---

## Body — Major Deity

```markdown
**Deity Name** is [the defining one-line — the god of what], [evocative clause on their place in the world of [[Elandis]]]. [Second sentence: their nature, their standing among the gods, or the gap between what they are and what the world believes.]

## Overview

[**Mandatory, leads the body.** The god in brief — what they are the god of, where they sit among the powers of the world, and how they are (or aren't) known — a reader's orientation before the detail. World-focused: describe the god as they exist in and over the world, not through the party. Full paragraphs.]

## Divinity

[**The heart of the article — what kind of god this is.** Their portfolio and the values beneath it (not just "the moon" but mercy, forgiveness, the protection of the weak), their place in the divine order as the world understands it, and their relationships to other gods (a twin, a rival, a consort, an enemy). Where the god has several facets, **nest them as `###` subsections** beneath `## Divinity` rather than spawning flat `##` headings. For a god whose true rank is a secret, this section gives the *world's* understanding; the truth waits for the restricted page.]

## Worship

[**The flexing middle — the faith, told from the deity's side.** Who reveres them and why; clergy, holy orders, and temples (summarised, with the institutions linked out to their own Faction/Location pages); holy days, rites, and festivals; relics and holy symbols; how the god is invoked and what the faithful ask of them. Group facets under `###` subsections (e.g. `### Holy Days & Rites`, `### Symbol & Iconography`, `### Temples & Clergy`). **For a forgotten god, gauge what actually survives** (see the archetypes above): if their rites live on *displaced into a successor's faith*, this section can still be rich — present it as the faith's, holding for restricted whose it truly is; if no faith survives at all, say so in a line and let the entry be almost entirely restricted, rather than inventing worship the world wouldn't have.]

## Myths & Deeds

[**Optional bespoke section** — the stories the world (or the faith) tells of this god: their defining deeds, their role in the great events, the legends that carry their name. Told here in summary, with fuller accounts linked out (an Event page, a Character's tale). For a god bound to a champion or a sibling-struggle, this is where that story lives in brief. Rename or split to fit; omit for a god with no mythology of note.]

## In Memory & Belief

[**Mandatory closer.** How the world knows this god *now* — revered as eternal, dwindled to folklore, conflated with another, or wholly forgotten; who keeps the faith and who has let it lapse; the gap between common understanding and the truth. **This is the signature Lore section and, for a deity, often the most load-bearing** — it is where a forgotten god's faded memory lives, and where a worshipped god's public face stands over the truth held in restricted. Present the world's belief here; hold the truth for the restricted companion.]

### [[The Bloody Nails|Campaign: The Bloody Nails]]

#### [[Session N - <Title>]]

[Narrative paragraph: how the god surfaced in the session — the vision, the priest's revelation, the mark left on a character — at the level the party understood it. The cosmic *why* stays in the restricted companion.]

## Trivia

- [A worldbuilding aside, a naming note, or a behind-the-scenes detail — Major only]
```

---

## Body — Minor Deity

```markdown
**Deity Name** is [the defining one-line — the god of what]. [Second sentence: their portfolio, or who reveres them.]

## Overview

[**Mandatory.** One to two paragraphs covering what they are the god of, their tier, and who (if anyone) worships them.]

## In Memory & Belief

[**Mandatory, can be one paragraph.** How they're remembered or worshipped, and by whom.]

### [[The Bloody Nails|Campaign: The Bloody Nails]]

#### [[Session N - <Title>]]

Brief summary of how they came up this session — one sentence or a short bullet.
```

The two mandatory body sections for a Deity are **`## Overview`** (leads) and **`## In Memory & Belief`** (closes). The shared rules (world-focused opening, straight Codex voice, session link format, Trivia is Major-only, public-only content) are in `lore.md`.

---

## Restricted body heading set

When a restricted companion is created (machinery in `lore.md`), use this subtype's heading set — the **same set as the public body** — with the full truth woven in:

`## Overview`, `## Divinity`, `## Worship`, `## Myths & Deeds` (if used), `## In Memory & Belief`

Where the truth goes depends on the archetype:
- **Forgotten God of Old:** the truth *expands a thin public page into a living one* — `## Overview` and `## Divinity` reveal that the god is real and what they truly are; a `## Worship`/`## Myths & Deeds` section can reveal what they are *doing now* (Selûne reaching for a Chosen because she fears a second Shattering); `## In Memory & Belief` reveals the truth beneath the forgetting. Update `Status` (often `Forgotten` → `Active`).
- **Worshipped Seven Divine:** the truth is the *demotion* — `## Overview` and `## Divinity` reveal they are an ascended mortal champion of the [[The Shattering|Shattering]], a lingering demigod, not an eternal god; their mortal life and death belong here; `## In Memory & Belief` reveals that the world prays to a saint mistaken for a god.

Keep the cosmology consistent with the restricted [[World Tree]] and [[The Shattering]] pages. Record deliberate mysteries and unanswered designs in `## DM Notes` rather than over-specifying them.

---

## Image prompt framing

**A deity is the one Lore subtype that breaks the 16:9 vista.** A god is a *figure*, so depict them as one — an **iconic divine portrait**, using the **same portrait style and 3:4 frame as a Character** rather than the painterly landscape the other Lore subtypes share. (The shared lore landscape block in `lore.md` does *not* apply to a Deity; use the block below.)

```
[STYLE]: Fantasy RPG character portrait. Bold painterly strokes, visible brushwork, digital painting aesthetic. Rich dramatic colour palette. NOT photorealistic — stylized like official D&D 5e module artwork.
[SUBJECT]: <the deity as an iconic divine figure — form, bearing, raiment, and the iconography/holy symbol that marks them>
[POSE]: <emblematic, godly — the pose that reads as divinity, e.g. "rising from moonlit water, arms open, stars wheeling at her brow">
[SETTING]: <a mythic backdrop that expresses their domain — celestial, elemental, or sacred>
[LIGHTING]: <dramatic lighting that carries their nature — radiant, shadowed, burning>
[FORMAT]: Portrait, 3:4 aspect ratio
```

Derive `[SUBJECT]`, `[POSE]`, `[SETTING]`, and `[LIGHTING]` from the god's portfolio, values, and iconography — and lean into the **awe** of a divine being. For a forgotten or unknowable god, let the image suggest mystery (a half-seen figure, a presence more than a person) rather than a literal mortal portrait. Keep the `[STYLE]` and `[FORMAT]` lines identical across every deity; only the middle lines change.

---

## Gold standard

`Codex/Lore/Selûne.md` (+ `Codex - Restricted/Lore/Selûne - Restricted.md`) — the gold standard for Deities, and specifically for a **forgotten God of Old**: a world-focused opening, `## Overview` lead, a `## Divinity` section on the moon/light/forgiveness portfolio and her standing among the gods, a `## Worship` section carrying the moon faith and its holy days (Silvernight, the Unshadowed, the Pardon) — *attributed by the world to her champion, not to her* — and an `## In Memory & Belief` that scopes how thoroughly she has been forgotten, with the truth (that she is a living God of Old, reaching directly into the world because she fears a second Shattering) held in the restricted companion. Note the public/restricted gap is the *whole entry*: the public page is a faded memory; the restricted page is a god in motion.

For the contrasting **no-worship** case, see `Codex/Lore/Shar.md` (+ its restricted companion) — a God of Old with no faith, no temples, and no public face at all (known only as "the Lady of Vengeance"), whose entry is almost entirely restricted: how to write a deity the world doesn't know it has. Match these bars.
```
