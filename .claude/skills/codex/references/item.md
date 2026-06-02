# Codex Category — Items

Item-specific workflow for the codex skill. Read this when the user is creating an item entry — a magic item, relic, weapon, focus, or artifact notable enough to warrant its own page.

An Item entry can be a **single named object** (a unique artifact like an amulet or a sword) or a **class of object** (a type of item many people bear, like an arcane focus). The body flexes to fit — a unique artifact leans on History and a Campaign section; a class of item leans on Creation and Cultural Significance. The gold standard `Codex/Items/Rhun'zar.md` is a class-of-object entry; read it for the quality bar.

## Vault locations

- **Public items:** `Codex/Items/<Name>.md` (flat folder — no per-item subfolder)
- **Restricted companion docs:** `Codex - Restricted/Items/<Name> - Restricted.md`
- **Root-level stubs:** `<Name>.md` at vault root (migration case)
- **Image assets:** `Codex/Assets/Items/` (published) and `x_Assets/Items/` (working copies). Filenames use underscores, no spaces, and **strip apostrophes** — `Rhun'zar` → `Rhunzar_small.webp` / `Rhunzar.webp`.

---

## Step 1 — Parse input

Extract from the user's message whatever they've already provided:
- Item **name**
- **Importance:** Major or Minor
- Whether a **restricted companion document** is also needed

If anything is missing, ask for it all in one message — don't ask one field at a time. Both name and importance are required before proceeding. A cursed, sentient, or plot-critical artifact is almost always **Major**.

---

## Step 2 — Check for existing files and research the item

Before asking for details, check the vault:

1. Does `Codex/Items/<Name>.md` already exist? If so, warn the user and ask whether they want to update/migrate rather than overwrite.
2. Does `<Name>.md` exist at the vault root? If so, read it — use its content to inform both the entry and whether a restricted companion is needed (see Stub File Format below).
3. Grep all synopsis files under `Campaigns/The Bloody Nails/Sessions/` for the item's name (and any short-form aliases). Items are often referred to obliquely ("the amulet", "the blade") — also grep for the bearer's name and any tied entity (a deity, forge, or faction) to catch appearances the item's own name would miss. Collect every matching snippet with its session number. Ignore hits inside `Transcript.md` files — never read those.
4. Glob for image files matching the item name in `x_Assets/Items/` and `Codex/Assets/Items/` (patterns: `Name*.webp`, `Name_no_apostrophe*.webp` — also check `*.png` in case a source hasn't been converted yet). If found, use the real filename in the infobox.

### Stub file format

A root-level stub may be freeform notes. If it contains a `## Restricted` section, treat everything before it as public information and everything under it as DM-only secrets. In this case, automatically create both files without asking — the DM structured it that way intentionally.

Example stub:
```
A silver amulet shaped like a spider, recovered from a sealed tomb. Worn by Vanya.

## Restricted
- Slowly corrupts its bearer
- The goddess Lo'achtah speaks through it, steering the bearer's choices
- Its grip tightens the longer it is worn
```

---

## Step 3 — Present research and gather details

**If a root stub was found OR synopsis mentions were found (migration mode):**

Present your findings in one message before asking anything:

```
**Research for [Name]**

Root stub: [content if any, or "empty"]

Synopsis appearances:
- Session N: [brief quote or summary of the relevant snippet]
- Session N: [...]

Current bearer (if known): [name]

Based on this, I'd suggest: [Major/Minor] — [one sentence reasoning].

What would you like to add before I generate the entry? Drop in any bullet notes —
appearance, properties, origin, who has held it, secrets, anything not in the synopses.
```

Wait for the user's notes, then proceed to generate. Don't ask a structured question list in migration mode — the user's notes are freeform and that's fine.

If the stub contained a `## Restricted` section, note that you'll create both files and confirm this is still what they want.

---

**If this is a fresh item with no existing files (creation mode):**

Ask for everything in **one message**. Only ask for what isn't already provided by the user.

**Major item** — ask for:
- Item Type (the descriptor — Amulet, Weapon, Wondrous Item, Cursed Artifact, Arcane Focus, etc.)
- Rarity (Common / Uncommon / Rare / Very Rare / Legendary / Artifact — or skip if it would spoil)
- Origin (who made it, where it came from)
- Current owner / bearer (who holds it now)
- Appearance (physical description — the richer the better)
- Properties (what it does — observed effects and, if known, the mechanics)
- History (its provenance — who forged it, who has wielded it, the deeds it has been part of)
- Connections (deities, factions, places, or characters tied to it)
- Status (Active / Lost / Destroyed / Dormant / Sealed / Unknown)
- Aliases (alternate names)
- Campaign appearances (session numbers + what happened)
- If creating a restricted companion: any curse, hidden powers, secret history, true purpose, or plot hooks tied to the item

**Minor item** — ask for:
- Item Type and Rarity (whatever is known)
- Origin and current owner
- A brief description (1–3 sentences) — appearance, what it does
- Status
- Campaign appearances (session numbers + brief notes)
- If creating a restricted companion: the secrets to document

---

## Step 4 — Generate the public document

### Frontmatter

```yaml
---
Type: Item
Item Type: <descriptor — Amulet, Weapon, Wondrous Item, Cursed Artifact, Arcane Focus>
Rarity: <Common | Uncommon | Rare | Very Rare | Legendary | Artifact>
Owner: "[[Current Bearer]]"
Origin: "[[Origin Place or Maker]]"
Connections:
  - "[[Tied Entity One]]"
  - "[[Tied Entity Two]]"
Importance: Major | Minor
Status: Active | Lost | Destroyed | Dormant | Sealed | Unknown
NoteIcon: item
cssclasses:
  - hide-header-underline-3
tags:
  - item
aliases: [ShortName, AltName]
---
```

Rules:
- Omit any field where the value is unknown — never write `???` or leave blanks.
- `Owner` is the current bearer (a single `"[[Name]]"`); use `Connections` (YAML list) for tied places, factions, or deities. Use either, both, or neither as fits the item — the Rhun'zar gold standard uses `Connections` and no `Owner`.
- **Don't spoil with metadata.** If naming the `Rarity` (e.g. "Artifact"), the `Status`, or the `Owner` would give away a secret the players don't know, omit that field from the public entry and carry it in the restricted companion instead.
- Aliases: YAML list `[Name1, Name2]`; omit the field entirely if there are no aliases.

### Infobox

```markdown
> [!infobox|wikipedia]
> # Item Name
> [![[Codex/Assets/Items/Item_Name_small.webp|cover hsmall]]](Codex/Assets/Items/Item_Name.webp)
> ###### Basic Information
> Attribute |  Details |
> ---|---|
> Type | Item |
> ###### Item Information
> Attribute |  Details |
> ---|---|
> Item Type | <descriptor> |
> Rarity | <rarity> |
> Owner | [[Current Bearer]] |
> Origin | [[Origin\|Display Name]] |
> ###### Status
> Attribute |  Details |
> ---|---|
> Status | <status> |
```

Rules:
- Escape pipes inside wikilinks within blockquotes using `\|` — this is an Obsidian rendering requirement.
- Omit rows for unknown values. Add **bespoke rows** when the item warrants — the Rhun'zar infobox adds `Used By` and `Materials`; an attuned item might add `Attunement`. Keep them under the `Item Information` heading.
- Image filename: underscores, no spaces, apostrophes stripped — `Item_Name_small.webp` / `Item_Name.webp`.
- If a real image was found in Step 2, use its actual filename; otherwise use the placeholder.

### Body — Major item

The section set **flexes to fit the item**. The opening paragraph and `## Description` → `#### Appearance` are always present; after that, use the sections that fit — `## Properties`, `## History` (or `## Creation` for a crafted class of item), `## Current Owner`, and any bespoke section the item warrants (e.g. `## Cultural Significance` for the Rhun'zar). Match the depth and free-form sectioning of the gold standard.

```markdown
**Item Name** is a [item type] [evocative opening clause — what it is and why it matters in Elandis]. [Second sentence: a key detail, its origin, or what makes it dangerous, coveted, or unique.]

## Description

#### Appearance

[Vivid prose. What the object looks like, its materials, scale, the impression it gives — and how it changes when active, if it does. Paint a picture, not a bullet list. 2–3 sentences minimum.]

## Properties

[What the item does. Lead with the observed, in-world effects — what those who have used or witnessed it have seen it do. If exact mechanics are known and public, state them plainly; keep curses, dormant powers, and hidden effects for the restricted companion.]

## History

[Provenance: who made it, where it came from, who has borne it before, and the deeds it has been part of. Full paragraphs. For a crafted class of item, rename to `## Creation` and describe how each is made.]

## Current Owner

[Who holds or wields it now, and how they came to have it. Wikilink the bearer.]

## [[The Bloody Nails|Campaign: The Bloody Nails]]

#### [[Session N - <Title>]]

[Narrative paragraph: how the item featured this session — found, used, lost, or its effect on its bearer.]

## Trivia

- [A worldbuilding aside, a naming note, or a behind-the-scenes detail]
```

### Body — Minor item

```markdown
**Item Name** is a [item type] [what it is and where it came from]. [Second sentence: its role or a defining property.] [Optional third sentence: a brief appearance or historical note.]

## Description

[Concise prose — one to three paragraphs covering appearance, what it does, and how it has intersected with the campaign. Focused on what is known.]

## [[The Bloody Nails|Campaign: The Bloody Nails]]

#### [[Session N - <Title>]]

Brief summary of how the item featured this session — one sentence or a short bullet.
```

### Rules that apply to both

- The **opening paragraph is world-focused** — describe what the item is in the world of Elandis. The party doesn't appear in the opening paragraph; their dealings with it belong in the Campaign section.
- **Separate the observed from the mechanical.** What characters have seen the item do is in-world prose; exact rules, DCs, and damage (if recorded) read as a clearly-marked aside or go to the restricted companion.
- **Session link format:** `#### [[Session N - <Title>]]` — direct basename link, no path, no alias. Each session file's basename is unique vault-wide, so Obsidian resolves it directly. Verify the exact basename (early sessions are zero-padded, e.g. `Session 08 - The High Road`).
- If no campaign appearances were provided, omit the Campaign section entirely.
- Trivia is Major-only.
- The public document contains only what the players currently know. If a restricted companion is also being created, secrets — curses, hidden powers, true origins — are omitted here and woven into the restricted version instead.

---

## Step 5 — Generate the restricted companion document (if needed)

Create this when: the stub file had a `## Restricted` section, the user asked for both files, or the user flagged restricted content during Step 3. Cursed, sentient, or deity-bound items almost always warrant one — the item's true nature is exactly the kind of thing the players shouldn't read.

Write to: `Codex - Restricted/Items/<Name> - Restricted.md` (create the `Codex - Restricted/Items/` folder if it doesn't exist yet).

### What the restricted document is

The restricted document is the **full-truth version** of the item article — the same structure as the public document, but with secrets woven naturally into the body. It is what the public article will become once those secrets are revealed to the players. When that day comes, the DM can replace the public file with this one (removing the `> [!abstract] Public Entry:` callout and the `## DM Notes` section).

This means:
- Appearance: includes any hidden aspect — marks that appear in moonlight, a sigil that only shows when the curse deepens.
- Properties: the true powers, including the curse, the dormant abilities, and the price of bearing it.
- History: the real provenance — who truly made it, its true purpose, and what it has done to past bearers.

A `## DM Notes` section at the bottom covers anything purely DM-side that won't ever belong in the public article — mechanical curse rules, session flags, plot hooks, the long-term arc the item drives.

### Restricted document structure

```markdown
[image prompt fenced code block]

[full frontmatter — same schema as public, plus any spoiler fields (true Rarity, Status, Owner) omitted from the public version]

> [!abstract] Public Entry: *[[Item Name]]*

[Infobox — same as public, with the spoiler rows restored]

[Opening paragraph — same as public, or expanded with the full truth if the public version was deliberately vague]

## Description

#### Appearance
[Full truth — including any hidden aspect]

## Properties
[The true powers, the curse, the dormant abilities, the price of bearing it]

## History
[The real provenance and true purpose, written as natural prose]

## Current Owner
[The bearer, and what the item is doing to them]

## [[The Bloody Nails|Campaign: The Bloody Nails]]

#### [[Session N - <Title>]]
[Same as public — campaign appearances are facts, not secrets]

## Trivia
[Same as public, if Major]

## DM Notes

- **True nature:** [What the item really is, not yet known to the party]
- **Curse / mechanics:** [The mechanical effects of bearing it, escalation rules]
- **Plot hooks:** [Ways the item might factor into future sessions]
- [Any other DM-side notes — session flags, the arc it drives, meta-context]
```

---

## Step 6 — Generate the image prompt

Place this at the **very top of each file**, before the frontmatter, in a fenced code block. Always generate it — even if an image already exists. Both files (public and restricted) get the same image prompt.

Items use the **same painterly art style as characters and locations** — so the whole wiki shares one look. An item is framed as an **object study**: the item as the focal subject (resting on a surface, held aloft, laid on cloth, glinting in a shaft of light) rather than a portrait or a landscape. Keep the portrait 3:4 framing so the thumbnail matches the rest of the wiki.

```
[STYLE]: Fantasy RPG item study. Bold painterly strokes, visible brushwork, digital painting aesthetic. Rich dramatic colour palette. NOT photorealistic — stylized like official D&D 5e module artwork.
[SUBJECT]: <the object — its form, materials, scale, decoration, and any glow or effect when active>
[COMPOSITION]: <how it is presented — e.g. "resting on dark velvet", "held up against firelight", "half-buried in tomb dust">
[MOOD]: <emotional tone — e.g. "ancient and coveted", "beautiful but quietly wrong">
[LIGHTING]: <dramatic, high-contrast lighting — e.g. "warm amber glow catching etched sigils", "cold light from within the gem">
[FORMAT]: Portrait, 3:4 aspect ratio
```

Keep the `[STYLE]` line identical across every item entry; only `[SUBJECT]`, `[COMPOSITION]`, `[MOOD]`, and `[LIGHTING]` change per item. Derive them from the item's appearance, materials, and nature, and make them specific — a good prompt conjures an exact object, not a generic fantasy trinket. Favour the warm-against-cool, high-contrast lighting of the character art.

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

## Gold standard

`Codex/Items/Rhun'zar.md` — a class-of-object entry: world-focused opening, `## Description` → `#### Appearance`, bespoke `## Creation` and `## Cultural Significance` sections, infobox with bespoke `Used By` / `Materials` rows, `Connections` frontmatter and no `Owner`, and a `## Notable Rhun'zar` bearer section in place of a single-artifact Campaign section. Read it to see the quality bar and the free-form sectioning to match. For a unique artifact, keep the `## History` / `## Current Owner` / Campaign sectioning shown in the body template above.
