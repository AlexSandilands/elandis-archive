# Codex Category — Lore

Shared lore workflow for the codex skill. Read this when creating any lore entry — a historical event, a cosmological structure, a force, a phenomenon, a myth — **then read the subtype doc**, which holds the creation-mode questions, frontmatter, infobox, body templates, image-prompt framing, and gold standard for that subtype. This base holds everything the subtypes share.

| Subtype | What it is | Subtype reference | Status |
|---|---|---|---|
| **Event** | A discrete historical or cosmological happening with a place in time — a cataclysm, war, founding, pact, or turning point | `references/lore/event.md` | **Supported** |
| **Cosmology / Concept** | A timeless feature of how the world *is* — a cosmic structure, plane, force, phenomenon, or tradition | `references/lore/concept.md` | **Supported** |
| Deity | A god or divine being | *(not yet written)* | Not yet supported |

**Telling the subtypes apart:** if it *happened* (it has a *when* — you could place it on a timeline), it is an **Event**; if it *exists* (timeless — it is a thing the world is built from or contains), it is a **Cosmology / Concept**. A god or divine being is a **Deity** — that subtype isn't wired in yet; if the user wants one, tell them so and offer to write it as a Concept for now, or to hand-write it from `x_Templates/Codex/Lore.md`. (When Deity is added, write `references/lore/deity.md` mirroring the two existing subtype docs.)

**The Timeline is not a Lore entry.** `Timeline.md` is an index/chronology page that links *to* lore entries — it is not a templated lore article and is not produced by this skill. If the user wants to work on the Timeline, say so and treat it as a plain index page, not a codex entry.

## Vault locations

Both subtypes share one folder; the subtype is captured in the `Category` frontmatter field rather than in separate folders.

- **Public:** `Codex/Lore/<Name>.md`
- **Restricted companion:** `Codex - Restricted/Lore/<Name> - Restricted.md`
- **Root-level stubs:** `<Name>.md` at vault root (migration case)
- **Image assets:** `Codex/Assets/Lore/` (published) and `x_Assets/Lore/` (working copies). Underscores, no spaces — `World_Tree_small.webp` / `World_Tree.webp`.

---

## Step 1 — Parse input

Extract from the user's message whatever they've already provided:
- Lore **name**
- **Subtype:** Event or Cosmology / Concept (Deity is not yet supported). Infer from the subject — something that *happened* is an Event; something that *exists* timelessly is a Concept. Confirm if it's ambiguous.
- **Importance:** Major or Minor
- Whether a **restricted companion document** is also needed

If anything is missing, ask for it all in one message — don't ask one field at a time. Name, subtype, and importance are required before proceeding. If you're unsure whether something is an Event versus a Concept, say so and confirm — *the Sundering* (the act) is an Event; *the World Tree* (the thing) is a Concept; they often pair, and a single page usually covers the thing with its defining event summarised inside it (see the subtype docs on scope).

**Once the subtype is settled, read its reference doc now** (`references/lore/event.md` or `references/lore/concept.md`) and keep this base doc for the shared steps below.

---

## Step 2 — Check for existing files and research the lore

Before asking for details, check the vault:

1. Does `Codex/Lore/<Name>.md` already exist? If so, warn the user and ask whether they want to update/migrate rather than overwrite.
2. Does `<Name>.md` exist at the vault root? If so, read it — its content informs the entry and whether a restricted companion is needed (see Stub File Format below). Root lore stubs are often deep DM notes or brainstorm output; treat their lore as canon unless the synopses contradict them.
3. Grep all synopsis files under `Campaigns/The Bloody Nails/Sessions/` for the subject's name and its aliases. **Synopsis files are named `Session NN - <Title>.md`, not `Synopsis.md`** — search those and never read `Transcript.md`. Collect every matching snippet with its session number. Lore is often revealed in-world through a single scene (an archivist's tale, a vision, a god's chosen) — find those reveal moments, they anchor the public/restricted line.
4. **Reconcile attributions.** A stub may cite session numbers or names from memory; the synopses and existing Codex pages are the source of truth. If a stub places a reveal in Session N but the synopses place it elsewhere, trust the synopses and correct it, flagging the discrepancy to the user. Lore is dense with cross-references — verify each one.
5. Glob for image files matching the name in `x_Assets/Lore/` and `Codex/Assets/Lore/` (patterns: `Name*.webp`, `Name_with_underscores*.webp` — also check `*.png`). If found, use the real filename in the infobox path.

### Resolving links

Lore pages are dense with proper nouns — gods, heroes, places, other lore. Before writing each wikilink, resolve it to a real page:
- `find . -name "<Name>.md"` for an exact page.
- If a name doesn't resolve, grep for it as a frontmatter alias: `grep -rl "^  - <Term>$" --include="*.md" .` and link `[[Full Page Name|Display Term]]`.
- A figure who genuinely warrants their own page but doesn't have one yet may be linked as the intended target (this marks a page worth creating). Lore reliably spawns these — capture them for the user at hand-off rather than dropping them.

### Stub file format

A root-level stub may be freeform notes or brainstorm output. If it contains a `## Restricted` section, treat everything before it as public information and everything under it as DM-only secrets, and automatically create both files without asking — the DM (or the brainstorm skill) structured it that way intentionally. Lore is **secret-heavy**: the public article is the world's understanding (often folklore), and the restricted version holds the cosmic truth. A `## Codex To-Do` tail in a stub is a backlog note from brainstorming — **do not** fold it into the entry body; surface it to the user at hand-off (Step 7) as suggested follow-up entries.

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

[Any reconciled attributions, and the public/restricted line you read from the
reveal scenes — "the party learned X on-screen in Session N, but Y is still secret."]

Based on this, I'd suggest: [Major/Minor], Category: [Event / Cosmology] — [one sentence reasoning].

What would you like to add before I generate the entry? Drop in any bullet notes —
what it is or what happened, causes, consequences, how it's remembered, secrets, anything not in the synopses.
```

Wait for the user's notes, then proceed. Don't ask a structured question list in migration mode — the user's notes (especially brainstorm output) are freeform and that's fine.

If the stub contained a `## Restricted` section, note that you'll create both files and confirm this is still what they want.

**If this is a fresh lore entry with no existing files (creation mode):**

Ask for everything in one message, using the **creation-mode question list in the subtype doc** (`event.md` or `concept.md`). Only ask for what isn't already provided.

---

## Step 4 — Generate the public document

Assemble the **frontmatter, infobox, and body** from the templates in the subtype doc, observing these shared rules.

### Shared frontmatter base

Every lore entry carries this spine; the subtype doc specifies its own `Category`, `Status` vocabulary, and any extra fields.

```yaml
Type: Lore
Category: <Event | Cosmology>
Era: <when it happened, or its age — see subtype; omit if genuinely timeless and no evocative phrase fits>
Related:                      # optional — sibling lore pages this connects to
  - "[[World Tree]]"
Importance: Major | Minor
Status: <subtype vocabulary>
NoteIcon: lore
cssclasses:
  - hide-header-underline-3
tags:
  - lore
  - <lore/event | lore/cosmology>
aliases: [AltName]
---
```

- Omit any field whose value is unknown — never write `???` or leave blanks. `Related` and `aliases` are omitted entirely when empty.
- `Era` is load-bearing for Events (a date or age) and evocative-or-omitted for Concepts. `Related` is the lore-network field — link the other lore pages this one sits beside.
- **`Related` must not leak secrets on the public page.** List only connections the world (and the players) already know — a `Related` link is a visible cross-reference. A relationship that is itself restricted truth (e.g. the [[World Tree]] connection to [[The Shattering]], which the public page never mentions) belongs only in the *restricted* companion's `Related`, not the public one. The same goes for any in-body wikilink: don't link a page on the public side if the very connection is the secret.

### Universal infobox rules

- Use the `[!infobox|wikipedia]` callout. Escape pipes inside wikilinks within blockquotes using `\|` — Obsidian rendering requirement.
- Omit rows for unknown values, but **always keep the `Category` and `Era` rows** (they orient the reader to what kind of lore this is and when).
- Image path: underscores, no spaces — `Codex/Assets/Lore/Name_small.webp` / `Codex/Assets/Lore/Name.webp`. If a real image was found in Step 2, use its actual filename; otherwise use the placeholder (the user generates art from the prompt later).

### Rules that apply to all lore

- **The opening paragraph is world-focused** — describe the lore as it exists in the world of [[Elandis]]. The party doesn't appear in the opening; their dealings belong in the Campaign section.
- **`## Overview` always leads the body** (both subtypes) — the subject in brief, before the flexing middle.
- **`## In Memory & Belief` always closes the body** (both subtypes), before the Campaign and Trivia sections — *how the world knows this*: folklore, who believes or reveres it, conflicting tellings, what's commonly understood versus lost. This is the signature Lore section; never omit it (for a Minor entry it can be a single paragraph). It is also where the public/restricted gap lives most naturally — the public page gives the folk understanding, the restricted page the truth beneath it.
- **Use heading hierarchy — don't make every section a flat `##`.** A page that is nothing but top-level `##` headings reads uniform and list-like. Group related material under an umbrella `##` heading with `###` subsections beneath it: an Event's chronological beats nest under `## History`; a Concept's facets nest under `## Nature` or a bespoke umbrella. `## Overview` and `## In Memory & Belief` stay top-level; the flexing middle is where hierarchy earns its keep. The subtype doc shows the expected nesting. (Minor entries are short enough to stay flat.)
- **Tone is a straight, authoritative Codex voice** — not framed through any in-world narrator. The awe or mystery comes from the subject, not from a storyteller's perspective. (A Concept built on mystery should *lean into* the unknowable in plain declarative prose — see `concept.md`.)
- **Session link format:** `#### [[Session N - <Title>]]` — direct basename link, no path, no alias. Verify the exact basename (early sessions are zero-padded, e.g. `Session 08 - The High Road`).
- If no campaign appearances were provided, omit the Campaign section entirely.
- Trivia is Major-only.
- The public document contains only what the world currently understands. If a restricted companion is also being created, cosmic secrets are omitted here and woven into the restricted version instead.

---

## Step 5 — Generate the restricted companion document (if needed)

Create this when: the stub had a `## Restricted` section, the user asked for both files, or the user flagged restricted content during Step 3.

Write to: `Codex - Restricted/Lore/<Name> - Restricted.md`

### What the restricted document is

The restricted document is the **full-truth version** of the article — the same heading set as the public document for that subtype, but with the cosmic secrets woven naturally into the body. It is what the public article will become once those secrets are revealed. When that day comes, the DM can replace the public file with this one (removing the `> [!abstract] Public Entry:` callout and the `## DM Notes` section).

For lore the most common secret is **the truth beneath the myth** — what really happened versus what the world believes, the hidden cosmology, the connection to a current threat. Reveal it in the body (often expanding `## Overview`, the bespoke middle, and `## In Memory & Belief`), and update any frontmatter field the truth changes.

### Restricted document structure

```markdown
[image prompt fenced code block]

[full frontmatter — same schema as public, with any revealed fields corrected]

> [!abstract] Public Entry: *[[Lore Name]]*

[Infobox — same as public, with any concealed field now showing the truth]

[Opening paragraph — same as public, or expanded with the full truth if the public version was deliberately vague]

[Body — same heading set as the public body for this subtype (Overview, the bespoke middle, In Memory & Belief), with the full truth woven in.]

### [[The Bloody Nails|Campaign: The Bloody Nails]]

#### [[Session N - <Title>]]
[Same as public — campaign appearances are facts, not secrets]

## Trivia
[Same as public, if Major]

## DM Notes

- **Unrevealed truth:** [What this really is / what really happened, not yet known to the party]
- **Connections:** [Ties to current threats, factions, or other lore the players haven't drawn yet]
- **Plot hooks:** [Ways this lore might factor into future sessions]
- **Open threads:** [Deliberate mysteries and unresolved questions the DM is tracking]
```

---

## Step 6 — Generate the image prompt

Place this at the **very top of each file**, before the frontmatter, in a fenced code block. Always generate it — even if an image already exists. Both files (public and restricted) get the same prompt.

Lore uses the **same painterly style as the rest of the wiki**, in a **16:9 landscape** frame (the same `[STYLE]` line as locations). The subject differs by subtype — an Event is a frozen *dramatic moment*, a Concept is a mythic *vista* — and each subtype doc carries the framing note. The shared style block:

```
[STYLE]: Fantasy RPG landscape. Bold painterly strokes, visible brushwork, digital painting aesthetic. Rich dramatic colour palette. NOT photorealistic — stylized like official D&D 5e module artwork.
[SUBJECT]: <see subtype doc — an Event tableau, or a Concept vista>
[MOOD]: <the emotional tone the lore should evoke>
[LIGHTING]: <dramatic, high-contrast lighting>
[FORMAT]: 16:9 cinematic landscape
```

Keep the `[STYLE]` and `[FORMAT]` lines identical across every lore entry; only `[SUBJECT]`, `[MOOD]`, and `[LIGHTING]` change. Make them specific — a good prompt conjures one exact scene, not a generic fantasy backdrop.

---

## Step 7 — Write the files

Assemble each document in this order:
1. Image prompt fenced code block
2. Frontmatter (YAML between `---` delimiters)
3. Infobox callout
4. Opening paragraph
5. Remaining body sections

Write each file to its correct path. Report all paths written when done.

If a root-level stub was detected in Step 2, ask the user to confirm deletion of the stub file — don't delete it automatically. (Because the new Codex file shares the stub's basename, Obsidian resolves existing `[[Name]]` links to it once the duplicate root file is gone. If the stub had a different name than the Codex page, add the old name to `aliases` so links still resolve.)

If the stub carried a `## Codex To-Do` backlog (common from brainstorm hand-off), surface it to the user as a short checklist of suggested follow-up entries — each tagged new/update + Restricted, with a one-line of what it needs. Offer to create them next. Do not write the backlog into the published entry.
