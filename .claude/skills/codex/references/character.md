# Codex Category — Characters

Character-specific workflow for the codex skill. Read this when the user is creating a character entry.

## Vault locations

- **Public characters:** `Codex/Characters/<Name>.md`
- **Restricted companion docs:** `Codex - Restricted/Characters/<Name> - Restricted.md`
- **Root-level stubs:** `<Name>.md` at vault root (migration case)
- **Image assets:** `Codex/Assets/Characters/` and `x_Assets/Characters/`

---

## Step 1 — Parse input

Extract from the user's message whatever they've already provided:
- Character **name**
- **Importance:** Major or Minor
- Whether a **restricted companion document** is also needed

If anything is missing, ask for it all in one message — don't ask one field at a time. Both name and importance are required before proceeding.

---

## Step 2 — Check for existing files and research the character

Before asking for details, check the vault:

1. Does `Codex/Characters/<Name>.md` already exist? If so, warn the user and ask whether they want to update/migrate rather than overwrite.
2. Does `<Name>.md` exist at the vault root? If so, read it — use its content to inform both the entry and whether a restricted companion is needed (see Stub File Format below).
3. Grep all synopsis files under `Campaigns/The Bloody Nails/Sessions/` for the character's name (and any short-form aliases). Collect every matching snippet with its session number. Ignore hits inside `Transcript.md` files — never read those.
4. Glob for image files matching the character name in `x_Assets/Characters/` and `Codex/Assets/Characters/` (patterns: `Name*.webp`, `First_Last*.webp` — also check `*.png` in case a source hasn't been converted yet). If found, use the real filename in the infobox.

### Stub file format

A root-level stub may be freeform notes. If it contains a `## Restricted` section, treat everything before it as public information and everything under it as DM-only secrets. In this case, automatically create both files without asking — the DM structured it that way intentionally.

Example stub:
```
Male elf, mid-30s. Merchant in Darmouth. Seems friendly but evasive.

## Restricted
- Actually an Imperial informant reporting to Commander Vayne
- Knows the location of a resistance safehouse
- Will cooperate with the party if his family is threatened
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

Based on this, I'd suggest: [Major/Minor] — [one sentence reasoning].

What would you like to add before I generate the entry? Drop in any bullet notes —
species, appearance, background, secrets, anything not in the synopses.
```

Wait for the user's notes, then proceed to generate. Don't ask a structured question list in migration mode — the user's notes are freeform and that's fine.

If the stub contained a `## Restricted` section, note that you'll create both files and confirm this is still what they want.

---

**If this is a fresh character with no existing files (creation mode):**

Ask for everything in **one message**. Only ask for what isn't already provided by the user.

**Major character** — ask for:
- Species, gender, pronouns, age
- Place (home location)
- Connections (factions, organisations, key relationships)
- Profession / title
- Status (Alive / Deceased / Unknown)
- Aliases (short names or alternate identities)
- Appearance (physical description — the richer the better)
- Personality (key traits, how they come across)
- Background / backstory
- Campaign appearances (session numbers + what happened)
- If creating a restricted companion: any secrets, hidden motivations, unrevealed connections, plot hooks

**Minor character** — ask for:
- Species, gender, pronouns, age (whatever is known)
- Place, connections, profession, status
- A brief description (1–3 sentences)
- Campaign appearances (session numbers + brief notes)
- If creating a restricted companion: the secrets to document

---

## Step 4 — Generate the public document

### Frontmatter

```yaml
---
Type: Character
Creature Type: Humanoid
Species: <species>
Gender: <gender>
Pronouns: <pronouns>
Age: <age>
Languages: <if known>
Place: "[[Place Name]]"
Connections:
  - "[[Connection One]]"
  - "[[Connection Two]]"
Profession: <profession>
Importance: Major | Minor
Status: Alive | Deceased | Unknown
NoteIcon: npc
cssclasses:
  - hide-header-underline-3
tags:
  - character
aliases: [ShortName, AlternateName]
---
```

Rules:
- Omit any field where the value is unknown — never write `???` or leave blanks
- Use YAML list format for Connections when there are multiple (as shown); inline string `"[[Name]]"` when there's only one
- Aliases: YAML list `[Name1, Name2]`; omit the field entirely if there are no aliases

### Infobox

```markdown
> [!infobox|wikipedia]
> # Character Name
> [![[Codex/Assets/Characters/First_Last_small.webp|cover hsmall]]](Codex/Assets/Characters/First_Last.webp)
> ###### Basic Information
> Attribute |  Details |
> ---|---|
> Type | Character |
> ###### Character Information
> Attribute |  Details |
> ---|---|
> Creature Type | Humanoid |
> Species | <species> |
> Gender | <gender>
> Pronouns | <pronouns> |
> Age | <age> |
> Languages | <languages> |
> Place | [[Place Name\|Display Name]] |
> Connections | [[Conn1]]<br>[[Conn2]] |
> Profession | <profession> |
> ###### Status
> Attribute |  Details |
> ---|---|
> Status | <status> |
```

Rules:
- Escape pipes inside wikilinks within blockquotes using `\|` — this is an Obsidian rendering requirement
- Omit rows for unknown values
- Image filename: underscores, no spaces — `First_Last_small.webp` / `First_Last.webp`
- If a real image was found in Step 2, use its actual filename; otherwise use the placeholder

### Body — Major character

```markdown
**Character Name** is a [species] [profession/role] [evocative opening clause — who they are and why they matter]. [Second sentence: a key detail, defining tension, or what makes them compelling.]

## Description

#### Appearance

[Vivid prose. Paint a picture — not a bullet list. Describe how they look, what they wear, how they carry themselves, what people notice first. 2–3 sentences minimum.]

#### Personality

[Character traits, emotional depth, how they come across in conversation, what drives them beneath the surface. 2–3 sentences minimum.]

## Biography

#### Background

[Origin, formative events, motivations, how they arrived at their current role. Full paragraphs. The richest section — use the backstory the user gave you, including only what's publicly known.]

## [[The Bloody Nails|Campaign: The Bloody Nails]]

#### [[Session N - <Title>]]

[Narrative paragraph: the character's key actions, decisions, and moments this session.]

## Trivia

- [A fun fact, a behind-the-scenes note, an origin story for the character's creation]
```

### Body — Minor character

```markdown
**Character Name** is a [species] [profession/role] of [[Place]]. [Second sentence: their role in the world or a defining trait.] [Optional third sentence: a brief physical or personality note.]

## Biography

[Concise prose. One to three paragraphs covering their role, recent actions, and how they have intersected with the campaign. Focused on what is known.]

## [[The Bloody Nails|Campaign: The Bloody Nails]]

#### [[Session N - <Title>]]

Brief summary of their appearance in this session — one sentence or a short bullet point.
```

### Rules that apply to both

- The **opening paragraph is world-focused** — describe who this character is in the world of Elandis. The party doesn't exist in the opening paragraph.
- **Session link format:** `#### [[Session N - <Title>]]` — direct basename link, no path, no alias. Each session file's basename is unique vault-wide, so Obsidian resolves it directly.
- If no campaign appearances were provided, omit the Campaign section entirely.
- Trivia is Major-only.
- The public document contains only what the players currently know. If a restricted companion is also being created, any secrets are omitted here and woven into the restricted version instead.

---

## Step 5 — Generate the restricted companion document (if needed)

Create this when: the stub file had a `## Restricted` section, the user asked for both files, or the user flagged restricted content during Step 3.

Write to: `Codex - Restricted/Characters/<Name> - Restricted.md`

### What the restricted document is

The restricted document is the **full truth version** of the character article — the same structure as the public document, but with secrets woven naturally into the body. It is what the public article will become once those secrets are revealed to the players. When that day comes, the DM can replace the public file with this one (removing the `> [!abstract] Public Entry:` callout and the `## DM Notes` section).

This means:
- Appearance/Personality: includes the full picture, not just the public-facing front
- Biography/Background: the real backstory, including hidden history and true motivations
- Campaign section: same as the public version (campaign appearances are facts, not secrets)

A `## DM Notes` section at the bottom covers anything that's purely DM-side and won't ever belong in the public article — plot hooks, mechanical notes, session planning, unrevealed connections that won't be revealed until much later.

### Restricted document structure

```markdown
[image prompt fenced code block]

[full frontmatter — same schema as public, same values]

> [!abstract] Public Entry: *[[Character Name]]*

[Infobox — identical to public version]

[Opening paragraph — same as public or expanded with full truth if the public version was deliberately vague]

## Description

#### Appearance
[Full truth — may differ from public if the character has a disguise or hidden aspect]

#### Personality
[Full truth — real motivations visible, not just the presented front]

## Biography

#### Background
[Complete backstory, secrets and all, written as natural prose]

## [[The Bloody Nails|Campaign: The Bloody Nails]]

#### [[Session N - <Title>]]
[Same as public]

## Trivia
[Same as public, if Major]

## DM Notes

- **Unrevealed connections:** [Links not yet known to the party]
- **Plot hooks:** [Ways this character might factor into future sessions]
- **Hidden motivations:** [What drives them that the party doesn't know yet]
- [Any other DM-side notes — mechanics, session flags, meta-context]
```

---

## Step 6 — Generate the image prompt

Place this at the **very top of each file**, before the frontmatter, in a fenced code block. Always generate it — even if an image already exists. Both files (public and restricted) get the same image prompt.

```
[STYLE]: Fantasy RPG character portrait. Bold painterly strokes, visible brushwork, digital painting aesthetic. Rich dramatic colour palette. NOT photorealistic — stylized like official D&D 5e module artwork.
[SUBJECT]: <race, gender, approximate age, most striking physical features, what they're wearing, their expression>
[POSE]: <what they're doing — e.g. "leaning against a stone pillar, arms folded, half-smile">
[SETTING]: <brief environment — e.g. "lamplit study lined with scrolls", "windswept city ramparts at dusk">
[LIGHTING]: <mood — e.g. "warm amber side-lighting, soft shadows", "cold blue moonlight, sharp contrast">
[FORMAT]: Portrait, 3:4 aspect ratio
```

Derive [SUBJECT], [POSE], [SETTING], and [LIGHTING] from the character's appearance, personality, profession, and home. Make them specific — a good prompt conjures an exact image, not a generic fantasy figure.

---

## Step 7 — Write the files

Assemble each document in this order:
1. Image prompt fenced code block
2. Frontmatter (YAML between `---` delimiters)
3. Infobox callout
4. Opening paragraph
5. Remaining body sections

Write each file to its correct path. Report all paths written when done.

If a root-level stub was detected in Step 2, ask the user to confirm deletion of the stub file — don't delete it automatically.

---

## Gold standard references

Read these if you want to see the exact style to match:

- **Major:** `Codex/Characters/Ayana Syndrosa.md` — literary prose, YAML list Connections, `\|` pipe escaping in the infobox, full campaign section, Trivia.
- **Minor:** `Codex/Characters/Warden Caeryn.md` — short 2–3 sentence opening, concise Biography prose (no Background sub-heading for Minor entries), bullet-style campaign entries. Ignore the `eWarden` typo at the start of that file — it's a source error.

These are the bar. Match them.
