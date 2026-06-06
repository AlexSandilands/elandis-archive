# Codex Lore Subtype — Culture

Culture-specific content for the codex skill. Read this **together with `references/lore.md`** (the shared lore workflow) when creating a Culture entry. This file holds only what's unique to Cultures: the creation-mode questions, frontmatter, infobox, body templates, image framing, and gold standard. Everything else — migration-mode research, restricted-companion machinery, write order, and the shared lore rules — lives in `lore.md`.

A **Culture** is the living (or lost) fabric of how a people exists — their customs, ceremonies, values, social structures, arts, and traditions. Unlike an Event, it has no single *when*; unlike a Concept, it is not a cosmic or metaphysical feature of the world — it is what a *people* does and is. Its page describes who these people are, what defines them, and how their way of life manifests in the world of [[Elandis]].

- **Public:** `Codex/Lore/<Name>.md`
- **Restricted:** `Codex - Restricted/Lore/<Name> - Restricted.md`

## Scope — the culture and the people who hold it

A Culture page covers *the way of life*. Where a culture is inseparable from a people, faction, or region that has its own page, cross-link rather than duplicate: describe the culture's customs here; let the people's page describe who they are and where they live. When a single ceremony or tradition is large enough to carry its own article, a standalone Culture entry is warranted — but most should be broad entries with the tradition as a subsection. Decide the boundary with the user: usually a Culture entry absorbs its most significant practices, linking out only to separately documented Events or Factions.

---

## Creation-mode questions

Ask only in creation mode (a fresh entry with no existing files). In migration mode, use the freeform presentation in `lore.md`. Ask for everything in **one message**, and only for what isn't already provided.

**Major Culture** — ask for:
- The people, civilization, or group this culture belongs to
- The one-line "what defines this culture" (its character, its animating value)
- Origin — where and when it emerged, and what shaped it into what it is today
- Core customs and practices — the defining traditions, ceremonies, or ways of life that mark someone as part of this culture
- Social structure — how the society is organised, hierarchies, roles, and bonds (if relevant to the culture)
- Art, craft, or expression — what they make, celebrate, or perform; what they leave behind
- Beliefs and values — what they hold sacred, what they fear or forbid, their moral framework
- How it's viewed from outside — how other peoples perceive, admire, distrust, or have been shaped by this culture
- Status (Active / Historical / Transformed / Lost)
- Aliases (alternate names for the culture or its people)
- Campaign appearances (session numbers + what surfaced in play)
- If creating a restricted companion: the secrets — hidden tensions, the truth behind a practice, what the culture conceals, the DM's read on where it is headed

**Minor Culture** — ask for:
- The people it belongs to and the one-line defining summary
- A brief description (a few sentences) — its most visible traits and a notable custom
- Status
- Campaign appearances (session numbers + brief notes)
- If creating a restricted companion: the secrets to document

---

## Frontmatter

```yaml
---
Type: Lore
Category: Culture
People: <the people or civilization — e.g. "The Sumaran Elves", "Valtorran commoners">   # required
Region: <homeland or primary home region>                                                   # optional
Era: <when it emerged or flourished, if historical — omit for living cultures>             # optional
Related:
  - "[[Sumara]]"
  - "[[Order of the Veil]]"
Importance: Major | Minor
Status: Active | Historical | Transformed | Lost
NoteIcon: lore
cssclasses:
  - hide-header-underline-3
tags:
  - lore
  - lore/culture
aliases: [AltName]
---
```

Rules:
- `People` is **required** — it anchors who this culture belongs to. Link the people's page if one exists: `"[[Sumaran Elves]]"`.
- `Region` is optional — include it when the culture is strongly tied to a specific homeland.
- `Era` is **optional** for a Culture (many are living) — include it only when the culture is historical (a lost people) or when an evocative phrase fits ("The Age of Sail", "Pre-Shattering Valtorra"). For an active culture, omit.
- `Status` describes the culture's present state: `Active` (practiced today), `Historical` (gone, but documented), `Transformed` (changed significantly from its origins), `Lost` (forgotten or eradicated).
- See `lore.md` for the shared frontmatter rules (omit unknowns, `Related`/`aliases` omitted when empty).

---

## Infobox

```markdown
> [!infobox|wikipedia]
> # Culture Name
> [![[Codex/Assets/Lore/Culture_Name_small.webp|cover hsmall]]](Codex/Assets/Lore/Culture_Name.webp)
> ###### Lore Information
> Attribute |  Details |
> ---|---|
> Type | Lore |
> Category | Culture |
> People | <people or civilization> |
> Region | <homeland> |
> Era | <age or period, if set> |
> ###### Status
> Attribute |  Details |
> ---|---|
> Status | <status> |
```

- Always keep the `Category` and `People` rows — they orient the reader. Omit `Region` and `Era` when not set.
- See `lore.md` for the universal infobox rules (pipe escaping, omitting unknown rows, image filename).

---

## Body — Major Culture

```markdown
**Culture Name** is [the defining one-line — what this culture is and who holds it], [evocative clause on its character or its place in the world of [[Elandis]]]. [Second sentence: what makes it distinctive, its animating value, or its reach.]

## Overview

[**Mandatory, leads the body.** Who these people are, the broad shape of their culture, and why it matters — a reader's orientation before the detail. Full paragraphs.]

## <Bespoke sections>

[As many as the culture warrants, named to fit. This is the flexing middle — group related aspects under umbrella `##` headings with `###` subsections rather than a flat run of headings. Natural umbrellas:
- `## Customs & Ceremony` — with `###` subsections per ceremony or practice
- `## Social Structure` — with `###` subsections for roles, hierarchies, bonds
- `## Craft & Expression` — with `###` subsections for art, music, building, language
- `## Beliefs & Taboos` — their values, what they hold sacred, and what they forbid
These are suggestions, not requirements — name them to match the subject. A culture defined by its warrior tradition might lead with `## The Way of the Blade`; one defined by mercantile life might open with `## The Merchant's Road`. Match the depth and structure of the gold standard.]

## In Memory & Belief

[**Mandatory closer.** How this culture is perceived from the outside — by neighbours, rivals, scholars, or history. How it is romanticised, misunderstood, or feared. For a living culture, what outsiders see versus what it actually is; for a lost one, how it is remembered and what has been forgotten. This is the signature Lore section. For a culture with something to hide, the surface perception lives here while the truth is held in restricted.]

## [[The Bloody Nails|Campaign: The Bloody Nails]]

#### [[Session N - <Title>]]

[Narrative paragraph: how the culture surfaced in the session — an encounter with its people, a ceremony witnessed, an artefact recovered — and what the party learned of it.]

## Trivia

- [A worldbuilding aside, a naming note, or a behind-the-scenes detail — Major only]
```

---

## Body — Minor Culture

```markdown
**Culture Name** is [the defining one-line — what this culture is and who holds it]. [Second sentence: its most notable trait or custom.]

## Overview

[**Mandatory.** One to two paragraphs covering who these people are, what defines their culture, and any notable customs together.]

## In Memory & Belief

[**Mandatory, can be one paragraph.** How they are perceived from outside — by neighbours, by history, by the wider world.]

## [[The Bloody Nails|Campaign: The Bloody Nails]]

#### [[Session N - <Title>]]

Brief summary of how it came up this session — one sentence or a short bullet.
```

The two mandatory body sections for a Culture are **`## Overview`** (leads) and **`## In Memory & Belief`** (closes). The shared rules (world-focused opening, straight Codex voice, session link format, Trivia is Major-only, public-only content) are in `lore.md`.

---

## Restricted body heading set (standalone full entry only)

The default restricted companion is a **slim DM-reserve delta** — themed notes only, no body article (machinery in `lore.md`). This heading set applies **only** to the standalone-full-entry exception. In that case, use this subtype's heading set:

`## Overview`, `## <Bespoke sections>` (however many), `## In Memory & Belief`

For a slim delta, the truth most often concerns hidden tensions within the culture (a dominant caste, a suppressed sect), the reality behind a practice (what a ceremony actually does versus what its participants believe), and where the culture is headed — capture those as themed reserve notes. Common delta headings: `## Hidden Tensions`, `## The Truth Behind [Practice]`, `## Where This Is Headed`, `## Plot Hooks`.

---

## Image prompt framing

The shared painterly landscape style and 16:9 format are in `lore.md`. For a Culture, depict a **characteristic scene of the culture in action** — not a portrait of one individual, but a scene that evokes the way of life: a ceremony in progress, a market or gathering, a craftsman's workshop at scale, a festival. Choose the scene that a traveller encountering this culture for the first time would remember. Favour warm communal light for living cultures; a cooler, more desolate palette for lost or transformed ones. The scene should feel like it belongs *in* the world, not staged for the viewer.

---

## Gold standard

No gold standard yet — the first Major Culture entry written with this template sets the bar. When one exists, record it here as: `Codex/Lore/<Name>.md` (+ restricted companion if applicable) — and note which aspects to match (opening structure, bespoke section choices, depth of `## In Memory & Belief`).
