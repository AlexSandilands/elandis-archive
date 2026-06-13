---
name: rename-grammar
description: Use this skill after renaming a vault page to drop a leading article — "The Frostwardens" → "Frostwardens", "The Maw" → "Maw", "The Albatross" → "Albatross". Trigger on "/rename-grammar", "I removed The from a page", "fix the grammar after renaming X", "I renamed X to drop the The, fix the links", "I dropped the leading The from X and the sentences are broken", or any time the user has renamed a page so its name no longer starts with an article and wants the referencing prose repaired. Obsidian auto-updates the link targets on rename but leaves the surrounding sentences missing their article (e.g. "We met [[Frostwardens]] yesterday"). This skill finds every reference across the vault and restores the article outside the brackets, matching the vault's page-naming convention. Do NOT use for creating entries (that's /codex) or for other kinds of rename.
---

# Rename Grammar Fixer

When a page is renamed to drop a leading article — `The Frostwardens` → `Frostwardens` — Obsidian rewrites every `[[The Frostwardens]]` link target to `[[Frostwardens]]`, but it cannot fix the prose. Sentences that read correctly because "The" lived *inside* the link now read broken because the article vanished:

- Before: `We met [[The Frostwardens]] yesterday.` → displays "We met The Frostwardens yesterday."
- After rename: `We met [[Frostwardens]] yesterday.` → displays "We met Frostwardens yesterday." ❌

This skill walks every reference and restores the article **outside** the brackets, the way the vault names pages:

- Fixed: `We met the [[Frostwardens]] yesterday.` ✅

This matches the vault convention (see `CLAUDE.md` / the `codex` skill): pages are bare proper nouns with no leading article, and the article is supplied in prose *outside* the wikilink — `the [[Frostwardens]]`, `The [[Order of Ravens]]`.

## Inputs

Establish two strings before doing anything:

- **New name** — the current (bare) page name, e.g. `Frostwardens`. This is what the user just renamed the page to. If unstated, ask, or infer from the page they point at.
- **Old name** — `The <New name>`, e.g. `The Frostwardens`.

The skill works whether or not the Obsidian rename has already run — Step 1 catches links in both the new bare form and any stragglers still in the old form.

## Step 1 — Find every reference

Search the whole vault for both link forms, excluding raw transcripts (never read or grep `Transcript.md`). Run from the vault root:

```bash
# New bare form (post-rename) — plain, aliased, and header links
grep -rn --include="*.md" "\[\[New Name\(\]\]\||#\)" . | grep -v "Transcript.md"

# Old form (any stragglers Obsidian did not rewrite)
grep -rn --include="*.md" "\[\[The New Name\(\]\]\||#\)" . | grep -v "Transcript.md"
```

In practice the simplest robust pass is to grep the bare token and eyeball the matches:

```bash
grep -rn --include="*.md" "\[\[Frostwardens" . | grep -v "Transcript.md"
grep -rn --include="*.md" "\[\[The Frostwardens" . | grep -v "Transcript.md"
```

Collect the full list of `file:line` hits. The link can appear as:

- Plain: `[[Frostwardens]]`
- Redundant self-alias: `[[Frostwardens|Frostwardens]]` — the rename leaves these behind (old `[[The Frostwardens|Frostwardens]]` → target rewritten, alias now repeats the target). Always collapse to plain.
- Aliased (genuine): `[[Frostwardens|Frostwarden]]`, `[[Frostwardens|the wardens]]`
- Header / block link: `[[Frostwardens#Crews|Fox Crew]]`

Any straggler still in the old `[[The Frostwardens...]]` form must **also** have its target rewritten to drop the `The` (Obsidian only rewrites links it indexed), in addition to the grammar fix below.

## Step 2 — Classify each occurrence and fix the grammar

Read the **whole line** (and enough of the surrounding sentence to judge) for each hit. Then apply the rules below. The goal is always: article **outside** the brackets, correct case for its sentence position.

### Plain link `[[Frostwardens]]`

This is the form that loses its article. Decide what sits immediately before it:

1. **Already has an article/determiner/possessive in front** — `the [[Frostwardens]]`, `a [[Frostwardens]]`, `their [[Frostwardens]]`, `eight [[Frostwardens]]`. Leave it; grammar is intact.
2. **Start of a sentence, heading, or list item** — `[[Frostwardens]] patrol the ice.` → `The [[Frostwardens]] patrol the ice.` Use capital **The** outside the brackets.
3. **Mid-sentence, article required** — `He joined [[Frostwardens]].` → `He joined the [[Frostwardens]].` Use lowercase **the** outside the brackets, even though the old link showed a capital "The". Lowercase mid-sentence is the improvement.
4. **Possessive** — `[[Frostwardens]]' lodge` → `the [[Frostwardens]]' lodge`. Article goes before, the possessive stays after.
5. **No article wanted** — genuinely attributive or list-label uses where English takes no article: `as Frostwardens` (rare), or an infobox/frontmatter/"See also" value where the bare page name is the convention. Leave these bare. When unsure whether prose wants an article, read it aloud — if "the" is needed for it to sound right, add it.

### Redundant self-alias `[[Frostwardens|Frostwardens]]` — always collapse

This is a **direct product of the rename**, not a rare incidental. When prose read `[[The Frostwardens|Frostwardens]]` (old target, bare display), Obsidian rewrites only the target on rename, leaving `[[Frostwardens|Frostwardens]]` — an alias that now exactly repeats its target. Always simplify these to plain `[[Frostwardens]]`, then apply the plain-link rules above (article outside the brackets, correct case for sentence position).

- `the mysterious "[[Frostwardens|Frostwardens]]"` → `the mysterious "[[Frostwardens]]"` (already has `the`, so just collapse).
- `five [[Frostwardens|Frostwardens]]` → `five [[Frostwardens]]` (determiner present, just collapse).
- `[[Frostwardens|Frostwardens]] patrol the ice.` → `The [[Frostwardens]] patrol the ice.` (collapse, then add sentence-start `The`).

Collapse them even in non-prose label contexts (infobox cells, "See also" lists) — the alias is pure redundancy there too. The collapse is global and mechanical: a single exact-match replace of `[[Name|Name]]` → `[[Name]]` across the vault is safe, then re-scan the plain hits for the article fix.

### Aliased link `[[Frostwardens|...]]` (genuine alias)

When the alias differs from the target, the displayed text is the alias, so the rename did **not** break the display. Do not touch the brackets. Only check whether the *surrounding* prose still reads correctly given the alias:

- `a former [[Frostwardens|Frostwarden]]` — reads fine, leave it.
- `old [[Frostwardens|Frostwarden]] sigils` — reads fine, leave it.

### Header / block links `[[Frostwardens#Crews|Fox Crew]]`

The display ("Fox Crew") is unaffected. Just ensure the target dropped its `The` (it will have, if Obsidian renamed). Fix surrounding article only if the prose needs it — usually it doesn't, because the display is a different noun phrase.

### Non-prose contexts — leave bare

Do **not** add articles inside: frontmatter fields, infobox table cells, tag lists, "Related"/"See also" link lists, or anywhere the bare page name is used as a label rather than a noun in a sentence. The bare name is correct there.

## Step 3 — Fix the renamed page itself

Obsidian renames the file and updates inbound links, but it does **not** touch the page's own contents. Open the renamed page (`Frostwardens.md`, and any restricted companion like `Codex-Restricted/Factions/Frostwardens - Restricted.md`) and reconcile:

- **H1 / title heading** — if it reads `# The Frostwardens`, decide with the user whether the title should stay `The Frostwardens` (some names keep the article as a display title even when the page name drops it) or become `Frostwardens`. Default to matching the new bare name unless the user wants the article kept as a display title.
- **Infobox `name` / title field** — same decision as the H1; keep them consistent.
- **Frontmatter `aliases`** — consider adding `The Frostwardens` as an alias so old-style `[[The Frostwardens]]` links and searches still resolve. Suggest this; don't force it.
- **Self-references in its own prose** — apply the Step 2 rules to any `[[Frostwardens]]` the page uses to refer to itself.

## Step 4 — Present and apply

1. Show the user a concise summary grouped by file: each occurrence, the before/after line, and a one-word reason (`sentence-start`, `mid-sentence`, `possessive`, `already-ok`, `alias-skip`, `label-skip`). Flag any you were unsure about so they can adjudicate.
2. On approval, apply the edits with exact-match replacements. Keep each edit minimal — change only the article and (for stragglers) the link target; never reflow or reword the sentence.
3. Re-run the Step 1 greps to confirm no `[[The Frostwardens` stragglers and no redundant `[[Frostwardens|Frostwardens]]` self-aliases remain, and that every `[[Frostwardens]]` now sits behind an article or is a deliberate bare label:

```bash
grep -rn --include="*.md" "\[\[The Frostwardens" . | grep -v "Transcript.md"      # stragglers
grep -rn --include="*.md" "\[\[Frostwardens|Frostwardens\]\]" . | grep -v "Transcript.md"   # redundant self-aliases
```

## Cautions

- Never read or grep `Transcript.md` files (per `CLAUDE.md`).
- Match the link token precisely — `[[Frostwardens` will not collide with a separate page like `Frostwarden Crews`, but double-check hits when the new name is a prefix of another page name.
- Article **outside** the brackets, always — never `[[the Frostwardens]]` or `[[The Frostwardens]]` (that recreates the problem).
- Prefer lowercase `the` mid-sentence; capital `The` only at sentence/heading/list-item start.
- This skill is for dropping a *leading article* on rename. For other renames, or for creating entries, use the appropriate skill instead.
