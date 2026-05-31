# Codex Lore Subtype — Event

Event-specific content for the codex skill. Read this **together with `references/lore.md`** (the shared lore workflow) when creating an Event. This file holds only what's unique to Events: the creation-mode questions, frontmatter, infobox, body templates, image framing, and gold standard. Everything else — migration-mode research, restricted-companion machinery, write order, and the shared lore rules — lives in `lore.md`.

An **Event** is a discrete historical or cosmological happening with a place in time: a cataclysm, war, founding, pact, or turning point. It has a *when*, causes that led to it, and a legacy that outlasts it.

- **Public:** `Codex/Lore/<Name>.md`
- **Restricted:** `Codex - Restricted/Lore/<Name> - Restricted.md`

## Scope — event vs. the thing it changed

An Event page tells *what happened*. Where an event is bound up with a structure or place (the Sundering and the [[World Tree]]; a war and a region), decide with the user which page is primary. Usual rule: a **Concept** page covers the thing and summarises its defining event inside it; a standalone **Event** page is warranted when the happening is large enough to carry its own article (as [[The Shattering]] is). Don't duplicate a full event account on both pages — summarise on one, link to the other.

---

## Creation-mode questions

Ask only in creation mode (a fresh event with no existing files). In migration mode, use the freeform presentation in `lore.md`. Ask for everything in **one message**, and only for what isn't already provided.

**Major Event** — ask for:
- Era / when it happened (a date, an age, or "lost to history")
- The one-line "what was this" (the defining summary)
- Background — the world before, and the causes that led to it
- What happened — the course of the event itself, its key moments and figures
- Outcome & aftermath — how it ended, and the consequences that persist into the present
- Legacy — what it left behind that still shapes the world (ruins, relics, scars, institutions)
- In memory & belief — how the world remembers it now: common knowledge, folklore, who takes it seriously, conflicting tellings
- Status (Historical / Ongoing / Mythologised / Lost)
- Aliases (alternate names)
- Campaign appearances (session numbers + what happened)
- If creating a restricted companion: the truth beneath the myth, hidden causes, ties to current threats, plot hooks

**Minor Event** — ask for:
- Era / when, and the one-line "what was this"
- A brief account (a few sentences) — cause, what happened, consequence
- How it's remembered (one line), if notable
- Status
- Campaign appearances (session numbers + brief notes)
- If creating a restricted companion: the secrets to document

---

## Frontmatter

```yaml
---
Type: Lore
Category: Event
Era: <"~2,500 years ago" | "The Age of Chaos" | "Lost to history">
Outcome: <short phrase — the event's result, e.g. "Tiamat banished; the breach sealed">   # optional
Related:
  - "[[World Tree]]"
  - "[[Riftshard]]"
Importance: Major | Minor
Status: Historical | Ongoing | Mythologised | Lost
NoteIcon: lore
cssclasses:
  - hide-header-underline-3
tags:
  - lore
  - lore/event
aliases: [AltName]
---
```

Rules:
- `Era` is **required** for an Event — it is the field that makes it an event. Use the best available: a rough date, a named age, or "Lost to history" when deliberately undated.
- `Outcome` is optional — a one-line result of **this** event, not of a later one that resolved it. Pin it to the event the page is actually about: the [[The Shattering|Shattering]] is the *breach* (its outcome is the world torn open and flooded with magic and monsters) — it is **not** the banishment and sealing that came five centuries later at the [[Chaos Wars|end of the war]]. Don't borrow a downstream event's result. Omit if the event is ongoing or its result is the whole article.
- See `lore.md` for the shared frontmatter rules (omit unknowns, `Related`/`aliases` omitted when empty).

---

## Infobox

```markdown
> [!infobox|wikipedia]
> # Event Name
> [![[Codex/Assets/Lore/Event_Name_small.webp|cover hsmall]]](Codex/Assets/Lore/Event_Name.webp)
> ###### Lore Information
> Attribute |  Details |
> ---|---|
> Type | Lore |
> Category | Event |
> Era | <when> |
> Outcome | <short phrase> |
> ###### Status
> Attribute |  Details |
> ---|---|
> Status | <status> |
```

- Always keep the `Category` and `Era` rows — they orient the reader. Omit `Outcome` if unknown.
- See `lore.md` for the universal infobox rules (pipe escaping, omitting unknown rows, image filename).

---

## Body — Major Event

```markdown
**Event Name** is [the defining one-line — what happened and when], [evocative clause on why it still matters to the world of [[Elandis]]]. [Second sentence: its scale, its cost, or the shape it left on the present.]

## Overview

[**Mandatory, leads the body.** The event in brief — what happened, when, and why it matters — as a reader's orientation before the detail. Full paragraphs.]

## History

[**Umbrella for the chronological account — don't leave the narrative beats as a flat run of `##` sections.** Group them as `###` subsections beneath this single `## History` heading. The three beats below are the typical set; name and split them to fit the event (a multi-phase war might warrant four or five `###` beats, a single founding only one or two).]

### The World Before

[The world before, and the causes that led to the event. What was the age that ended? What pressures, ambitions, or forces set it in motion? This is where the *before* lives — the lost world the event destroyed or transformed. Rename to fit (`### The World Before`, `### Origins`, `### The Road to War`).]

### The <Event>

[**Bespoke-named — the heart of the article.** The course of the event itself: its key moments, turning points, and figures. Name this subsection for the event (`### The Chaos Wars`, `### The Sacrifice of the Seven`, `### The Sundering`) and split into several bespoke `###` subsections when the event has distinct phases. This is the equivalent of a faction's flexing middle — give it the depth the event warrants.]

### Aftermath & Legacy

[How it ended and what it left behind that still shapes the present — the scars, ruins, relics, institutions, or ongoing consequences. For an event whose consequences are still in motion (a sealed breach that leaks, a foe who survived), say so plainly; the live thread belongs here in summary, with the secret detail saved for the restricted companion.]

## In Memory & Belief

[**Mandatory closer.** How the world remembers the event now — common knowledge versus folklore, who takes it seriously (and who treats it as a campfire tale), and how the tellings differ. This is the signature Lore section. Where the public account is a romanticised or garbled version of the truth, that gap is the heart of this section — present the folk version here and hold the truth for the restricted page.]

### [[The Bloody Nails|Campaign: The Bloody Nails]]

#### [[Session N - <Title>]]

[Narrative paragraph: how the event surfaced in the session — the reveal, the vision, the scholar's tale — and what the party learned of it.]

## Trivia

- [A worldbuilding aside, a naming note, or a behind-the-scenes detail — Major only]
```

---

## Body — Minor Event

```markdown
**Event Name** is [the defining one-line — what happened and when]. [Second sentence: its cause or its consequence.]

## Overview

[**Mandatory.** One to two paragraphs covering cause, what happened, and consequence together.]

## In Memory & Belief

[**Mandatory, can be one paragraph.** How it's remembered, if at all — and by whom.]

### [[The Bloody Nails|Campaign: The Bloody Nails]]

#### [[Session N - <Title>]]

Brief summary of how it came up this session — one sentence or a short bullet.
```

The two mandatory body sections for an Event are **`## Overview`** (leads) and **`## In Memory & Belief`** (closes). The shared rules (world-focused opening, straight Codex voice, session link format, Trivia is Major-only, public-only content) are in `lore.md`.

---

## Restricted body heading set

When a restricted companion is created (machinery in `lore.md`), use this subtype's heading set — the **same set as the public body** — with the full truth woven in:

`## Overview`, `## History` (with `### The World Before`, the bespoke `### <Event>` beats, and `### Aftermath & Legacy` nested beneath it), `## In Memory & Belief`

The truth most often expands `### The World Before` (the real cause), the bespoke beats (what actually happened versus the record), `### Aftermath & Legacy` (consequences still in motion — a foe who survived, a seal that leaks), and `## In Memory & Belief` (the truth beneath the folk version).

---

## Image prompt framing

The shared painterly landscape style and 16:9 format are in `lore.md`. For an Event, capture **the event mid-happening** — a dramatic moment rather than a static place: motion, stakes, the instant everything changed. Favour a **wide shot that conveys scale** over a tight hero-moment — for a world-scale cataclysm, pull back so the catastrophe dominates and the hosts read as a tide of tiny figures, rather than zooming on individuals (for [[The Shattering]], a colossal rift tearing the sky and bleeding red light over masses and monstrous hordes spread across the land — no discernible figures). Favour the warm-against-cool, high-contrast lighting of the rest of the wiki.

---

## Gold standard

`Codex/Lore/The Shattering.md` (+ `Codex - Restricted/Lore/The Shattering - Restricted.md`) — the gold standard for Events: a world-focused opening, `## Overview` lead, then a `## History` umbrella holding the chronological beats as `###` subsections (`### The World Before` — the Lost Age and the Dragon Queen's aim; the bespoke `### The Chaos Wars` and `### The Sacrifice of the Seven`; `### Aftermath & Legacy` — the Riftshards and the reset), and an `## In Memory & Belief` that presents the folk myth while the restricted companion carries the cosmic truth. Note the antagonist is unnamed on the public page ("the Dragon Queen") with the true name ([[Tiamat]]) held in restricted. Match this bar.
