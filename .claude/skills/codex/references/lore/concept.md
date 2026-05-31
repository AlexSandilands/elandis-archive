# Codex Lore Subtype — Cosmology / Concept

Concept-specific content for the codex skill. Read this **together with `references/lore.md`** (the shared lore workflow) when creating a Cosmology / Concept entry. This file holds only what's unique to Concepts: the creation-mode questions, frontmatter, infobox, body templates, image framing, and gold standard. Everything else — migration-mode research, restricted-companion machinery, write order, and the shared lore rules — lives in `lore.md`.

A **Cosmology / Concept** is a timeless feature of how the world *is* — a cosmic structure, a plane, a force, a phenomenon, or a tradition. Unlike an Event, it has no single *when*; it *exists*. Its page describes what it is, how it works, its nature, and (where it has one) the defining event in its history, told here in summary.

- **Public:** `Codex/Lore/<Name>.md`
- **Restricted:** `Codex - Restricted/Lore/<Name> - Restricted.md`

## Scope — the thing and its event

A Concept page covers *the thing*. Where the thing has a defining event (the [[World Tree]] and the Sundering), tell that event **here in summary** as a bespoke section, and link out to the fuller account if one exists (a hero's page, or a standalone Event page). Decide the boundary with the user: usually the Concept is primary and absorbs the event; split the event out only when it's large enough to carry its own article. Don't duplicate a full account on both pages.

## Embracing the unknowable

Some concepts are *meant* to resist explanation (the World Tree, the nature of the True Gods). When the DM has chosen deliberate mystery, **write into it, not around it**: state plainly what cannot be known, describe how the thing is spoken of and what it does rather than inventing a mechanism, and resist the urge to over-specify. Declarative prose about an unknowable thing reads as awe; a fabricated diagram reads as a betrayal of the design. The subtype's job here is restraint as much as description.

---

## Creation-mode questions

Ask only in creation mode (a fresh concept with no existing files). In migration mode, use the freeform presentation in `lore.md`. Ask for everything in **one message**, and only for what isn't already provided.

**Major Concept** — ask for:
- The one-line "what is this" (the defining summary)
- Nature — what it actually is, and how literally it should be described (or whether it's deliberate mystery)
- How it works / how it manifests — the way it touches the world and what it does
- Defining event or history — the moment or change that shaped it, if it has one (told here in summary)
- Significance — its place in the cosmos and why it matters
- In memory & belief — who knows of it, who reveres or fears it, what folklore surrounds it
- Status (Active / Withdrawn / Dormant / Lost / Unknown)
- Aliases (alternate names)
- Campaign appearances (session numbers + what happened)
- If creating a restricted companion: the cosmic truth, the hierarchy it sits in, hidden mechanics, plot hooks

**Minor Concept** — ask for:
- The one-line "what is this"
- A brief description (a few sentences) — what it is and how it works
- Who knows of it (one line), if notable
- Status
- Campaign appearances (session numbers + brief notes)
- If creating a restricted companion: the secrets to document

---

## Frontmatter

```yaml
---
Type: Lore
Category: Cosmology
Era: <evocative age phrase, or omit — "Primordial — predates the gods">   # optional for a Concept
Domain: <what realm of existence it governs or belongs to>                  # optional — e.g. "The cosmos entire", "Magic"
Revered by: <who holds it sacred>                                           # optional — e.g. "The Sumaran elves"
Related:
  - "[[The Shattering]]"
  - "[[World Gates]]"
Importance: Major | Minor
Status: Active | Withdrawn | Dormant | Lost | Unknown
NoteIcon: lore
cssclasses:
  - hide-header-underline-3
tags:
  - lore
  - lore/cosmology
aliases: [AltName]
---
```

Rules:
- `Era` is **optional** for a Concept (it's timeless) — include it only when an evocative age phrase fits ("Primordial"); otherwise omit. This is the key frontmatter difference from an Event, where `Era` is required.
- `Domain` and `Revered by` are optional flavour anchors — include the ones that fit, omit the rest.
- `Status` for a Concept describes its present state of being (`Active`, `Withdrawn`, `Lost`…), not a historical outcome.
- See `lore.md` for the shared frontmatter rules.

---

## Infobox

```markdown
> [!infobox|wikipedia]
> # Concept Name
> [![[Codex/Assets/Lore/Concept_Name_small.webp|cover hsmall]]](Codex/Assets/Lore/Concept_Name.webp)
> ###### Lore Information
> Attribute |  Details |
> ---|---|
> Type | Lore |
> Category | Cosmology |
> Era | <age phrase> |
> Domain | <what it governs> |
> Revered by | <who holds it sacred> |
> ###### Status
> Attribute |  Details |
> ---|---|
> Status | <status> |
```

- Always keep the `Category` row. Keep `Era` if one is set; omit it (and `Domain`/`Revered by`) when unknown.
- See `lore.md` for the universal infobox rules (pipe escaping, omitting unknown rows, image filename).

---

## Body — Major Concept

```markdown
**Concept Name** is [the defining one-line — what it is], [evocative clause on its place in the world of [[Elandis]]]. [Second sentence: its scale, its nature, or what makes it matter.]

## Overview

[**Mandatory, leads the body.** What this is, in brief — a reader's orientation before the detail. Full paragraphs.]

## Nature

[**The heart of the article.** What it actually is and how it works — its essence. For a concept built on deliberate mystery, this is where you embrace the unknowable (see the note above): state what cannot be known, describe how it is spoken of and what it does, and don't fabricate a mechanism. For a concrete concept (a tradition, a defined phenomenon), describe the mechanism clearly. When this section has several facets, **nest them as `###` subsections** beneath `## Nature` rather than spawning more flat `##` headings (e.g. `### A Thing Beyond Comprehension`, `### The Roots and the Planes`) — see the heading-hierarchy rule in `lore.md`.]

## <Bespoke sections>

[As many as the concept warrants, named to fit. For a structure with a defining event, a bespoke `## <Event>` umbrella tells that event in summary, with its beats as `###` subsections (e.g. `## The Sundering` holding `### The Cosmic Battle`, `### The Binding of the Silmara`, `### The Fall of the Sky`) and a link out to the fuller account. For a cosmic structure, a section on how it connects the world (e.g. `## The World Gates`); for a phenomenon, how it manifests. This is the flexing middle — group facets under umbrellas with `###` subsections rather than a long flat run of `##` headings, and match the depth of the gold standard.]

## In Memory & Belief

[**Mandatory closer.** Who knows of it, who reveres or fears it, and what folklore surrounds it — common understanding versus the truth, and how widely it's even known. This is the signature Lore section. For a concept known only to scholars or one people, say so, and present their understanding here; the deeper truth is held for the restricted page.]

### [[The Bloody Nails|Campaign: The Bloody Nails]]

#### [[Session N - <Title>]]

[Narrative paragraph: how the concept surfaced in the session — the reveal, the vision, the place the party reached — and what they learned of it.]

## Trivia

- [A worldbuilding aside, a naming note, or a behind-the-scenes detail — Major only]
```

---

## Body — Minor Concept

```markdown
**Concept Name** is [the defining one-line — what it is]. [Second sentence: how it works or where it fits.]

## Overview

[**Mandatory.** One to two paragraphs covering what it is and how it works together.]

## In Memory & Belief

[**Mandatory, can be one paragraph.** Who knows of it, and what's believed.]

### [[The Bloody Nails|Campaign: The Bloody Nails]]

#### [[Session N - <Title>]]

Brief summary of how it came up this session — one sentence or a short bullet.
```

The two mandatory body sections for a Concept are **`## Overview`** (leads) and **`## In Memory & Belief`** (closes). The shared rules (world-focused opening, straight Codex voice, session link format, Trivia is Major-only, public-only content) are in `lore.md`.

---

## Restricted body heading set

When a restricted companion is created (machinery in `lore.md`), use this subtype's heading set, with the full truth woven in:

`## Overview`, `## Nature`, `## <Bespoke sections>` (however many), `## In Memory & Belief`

The truth most often expands `## Nature` (what it really is, the hierarchy it sits in) and `## In Memory & Belief` (the gap between reverence and reality). Keep deliberate mysteries deliberate even here — the restricted page reveals what the DM knows, which for a truly unknowable thing may still be "this cannot be comprehended"; record the open threads in `## DM Notes` rather than inventing answers.

---

## Image prompt framing

The shared painterly landscape style and 16:9 format are in `lore.md`. For a Concept, choose a single **mythic, emblematic vista** — the image that captures the idea, not a moment in time. For a structure like the [[World Tree]], an awe-scaled, deliberately unpinnable vision (a colossal tree threading earth and sky, roots vanishing into cosmos) rather than a literal diagram. Convey scale, mystery, and the sense of something beyond comprehension; let the lighting carry reverence. For a concrete phenomenon, depict it manifesting in a characteristic setting.

---

## Gold standard

`Codex/Lore/World Tree.md` (+ `Codex - Restricted/Lore/World Tree - Restricted.md`) — the gold standard for Concepts: a world-focused opening, `## Overview` lead, a `## Nature` section that leans into deliberate mystery, bespoke middle sections (`## The World Gates`, `## The Sundering` told in summary with the fuller tale on [[Ryordan Silmara]]), and an `## In Memory & Belief` that scopes who even knows of it — with the cosmic hierarchy and the Material Plane's origin held in the restricted companion. Match this bar.
