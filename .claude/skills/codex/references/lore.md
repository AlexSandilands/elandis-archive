# Codex Category — Lore

Shared lore workflow for the codex skill. Read this when creating any lore entry — a historical event, a cosmological structure, a force, a phenomenon, a myth — **then read the subtype doc**, which holds the creation-mode questions, frontmatter, infobox, body templates, image-prompt framing, and gold standard for that subtype. This base holds everything the subtypes share.

| Subtype | What it is | Subtype reference | Status |
|---|---|---|---|
| **Event** | A discrete historical or cosmological happening with a place in time — a cataclysm, war, founding, pact, or turning point | `references/lore/event.md` | **Supported** |
| **Cosmology / Concept** | A timeless feature of how the world *is* — a cosmic structure, plane, force, phenomenon, or tradition | `references/lore/concept.md` | **Supported** |
| **Deity** | A god or divine being — a power that is worshipped, prayed to, or reckoned divine | `references/lore/deity.md` | **Supported** |

**Telling the subtypes apart:** if it *happened* (it has a *when* — you could place it on a timeline), it is an **Event**; if it *exists* (timeless — it is a thing the world is built from or contains), it is a **Cosmology / Concept**; if it is a *being* that is worshipped or reckoned divine (a god, a goddess, a member of the pantheon), it is a **Deity**. The line between a Concept and a Deity is *being vs. structure* — the [[World Tree]] is a Concept (a cosmic structure, even though the elves revere it); Selûne is a Deity (a god with a will and a portfolio). When in doubt, ask.

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
- **Subtype:** Event, Cosmology / Concept, or Deity. Infer from the subject — something that *happened* is an Event; something that *exists* timelessly is a Concept; a *worshipped or divine being* is a Deity. Confirm if it's ambiguous.
- **Importance:** Major or Minor
- Whether a **restricted companion document** is also needed

If anything is missing, ask for it all in one message — don't ask one field at a time. Name, subtype, and importance are required before proceeding. If you're unsure whether something is an Event versus a Concept, say so and confirm — *the Sundering* (the act) is an Event; *the World Tree* (the thing) is a Concept; they often pair, and a single page usually covers the thing with its defining event summarised inside it (see the subtype docs on scope).

**Once the subtype is settled, read its reference doc now** (`references/lore/event.md`, `references/lore/concept.md`, or `references/lore/deity.md`) and keep this base doc for the shared steps below.

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

Based on this, I'd suggest: [Major/Minor], Category: [Event / Cosmology / Deity] — [one sentence reasoning].

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
Category: <Event | Cosmology | Deity>
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
  - <lore/event | lore/cosmology | lore/deity>
aliases: [AltName]
---
```

- Omit any field whose value is unknown — never write `???` or leave blanks. `Related` and `aliases` are omitted entirely when empty.
- `Related` wikilinks must use the **block list** format shown in the template above (each `- "[[Name]]"` on its own line). Never pack multiple wikilinks into one quoted string or an inline array — Obsidian will not resolve them.
- `Era` is load-bearing for Events (a date or age), evocative-or-omitted for Concepts, and optional for Deities (which orient on `Pantheon` instead — see `deity.md`). `Related` is the lore-network field — link the other lore pages this one sits beside.
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

Create this when: the stub had a `## Restricted` section, the user asked for a restricted doc, or the user flagged restricted content during Step 3.

Write to: `Codex - Restricted/Lore/<Name> - Restricted.md`

### What the restricted document is

The restricted document holds **only the DM-reserve delta** — the cosmic truth beneath the myth, the hidden cosmology, the ties to current threats, and the plot hooks deliberately kept *out* of the public entry. It is **not** a copy of the public article. The public entry stays the single source of truth for what the world understands; the restricted doc carries just the reserve, in a lightweight notes format that's quick to jot and edit and detailed enough to fold into the public entry later, when the truth is revealed.

For lore the most common secret is **the truth beneath the myth** — what really happened versus what the world believes, the hidden cosmology, the connection to a current threat. That is exactly the kind of reserve this doc holds. Lore is secret-heavy, so this delta is often substantial — keep all of it, but don't re-state the folk version the public page already carries.

**Do not duplicate the public doc.** No copied frontmatter, infobox, body prose, session logs, or image prompt. If a fact already appears in the public entry, it does not belong here. The public doc owns the world's understanding; the restricted doc owns the cosmic truth beneath it.

> **Exception — standalone full entry.** Sometimes the DM writes a *complete* entry in restricted first, before any of it is public, intending to move it to the public Codex as-is later. Only when the user explicitly says this is a not-yet-public full entry, build the full public-style article here (full frontmatter, infobox, body using the subtype's heading set, image prompt — Steps 4 & 6) instead of the slim delta. The slim delta below is the default.

### Restricted document structure (slim delta — the default)

```markdown
---
Type: Lore
tags:
  - dm-notes
---

> [!abstract] Public Entry: *[[<Lore Name>]]*

## <Theme heading>
- The cosmic truth, hidden cosmology, ties to current threats — concise notes, or prose where the DM authored richer reserve lore.

## <Another theme>
- ...
```

Guidance:
- Group the reserve material under a few clear `##` headings that fit the content — e.g. `The Truth`, `Hidden Cosmology`, `What Really Happened`, `Connections`, `Plot Hooks`, `Open Threads`. Don't force a fixed heading set; use what the secrets call for.
- Prefer concise bullets, **but lore reserve is often rich authored prose** (the cosmic truth) — keep substantial passages as prose under a heading rather than flattening them. Never discard authored detail.
- A relationship that is itself restricted truth (e.g. the [[World Tree]]–[[The Shattering]] link the public page never mentions) belongs here, not on the public page.
- Keep `[[wikilinks]]` on proper nouns. Frontmatter is just `Type` + the `dm-notes` tag. No infobox, no image prompt, no duplicated session log.

---

## Step 6 — Generate the image prompt

Place this at the **very top of the public file**, before the frontmatter, in a fenced code block. Always generate it — even if an image already exists. The slim restricted doc gets no image prompt; only a standalone full restricted entry carries one.

Most Lore uses the **same painterly style as the rest of the wiki**, in a **16:9 landscape** frame (the same `[STYLE]` line as locations). The subject differs by subtype — an Event is a frozen *dramatic moment*, a Concept is a mythic *vista* — and each subtype doc carries the framing note. **The Deity subtype is the exception:** a god is a *figure*, so it uses a Character-style **portrait (3:4)** rather than the landscape block below — see `deity.md` for the deity image block. The shared landscape block (Events and Concepts):

```
[STYLE]: Fantasy RPG landscape. Bold painterly strokes, visible brushwork, digital painting aesthetic. Rich dramatic colour palette. NOT photorealistic — stylized like official D&D 5e module artwork.
[SUBJECT]: <see subtype doc — an Event tableau, or a Concept vista>
[MOOD]: <the emotional tone the lore should evoke>
[LIGHTING]: <dramatic, high-contrast lighting>
[FORMAT]: 16:9 cinematic landscape
```

Keep the `[STYLE]` and `[FORMAT]` lines identical across every Event and Concept entry; only `[SUBJECT]`, `[MOOD]`, and `[LIGHTING]` change. Make them specific — a good prompt conjures one exact scene, not a generic fantasy backdrop. (Deities use the portrait block in `deity.md` instead.)

---

## Step 7 — Write the files

Assemble the **public document** in this order:
1. Image prompt fenced code block
2. Frontmatter (YAML between `---` delimiters)
3. Infobox callout
4. Opening paragraph
5. Remaining body sections

Assemble the **slim restricted doc** (if any) in its own order: minimal frontmatter (`Type` + `dm-notes` tag) → a `> [!abstract] Public Entry: *[[<Name>]]*` callout → themed reserve sections. No H1 title (Obsidian shows the note title already), no image prompt, no infobox. (A standalone full restricted entry instead follows the public order above.)

Write each file to its correct path. Report all paths written when done.

If a root-level stub was detected in Step 2, ask the user to confirm deletion of the stub file — don't delete it automatically. (Because the new Codex file shares the stub's basename, Obsidian resolves existing `[[Name]]` links to it once the duplicate root file is gone. If the stub had a different name than the Codex page, add the old name to `aliases` so links still resolve.)

If the stub carried a `## Codex To-Do` backlog (common from brainstorm hand-off), surface it to the user as a short checklist of suggested follow-up entries — each tagged new/update + Restricted, with a one-line of what it needs. Offer to create them next. Do not write the backlog into the published entry.
