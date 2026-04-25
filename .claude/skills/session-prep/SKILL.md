---
name: session-prep
description: Use this skill when the user asks to "/session-prep", "prep session N", "generate prep for session N", "build the prep doc", or wants to create or fill in a D&D session prep document. Also trigger when the user says "prep the next session", "work on session N prep", or asks to turn a TODO list into a session plan. This skill reads the DM's TODO list from the existing draft prep file, reads recent synopses for narrative context, and produces a lightweight scene-based prep doc in the sparse Session 44 style — scenes with key beats and inline cheat sheets, with detailed lore pushed out to linked Codex docs.
---

# Session Prep Generator

Generate a lightweight, scene-based session prep document from the DM's draft prep file.

## Why this matters

The goal is a prep doc you can scan in two minutes before going live — a skeleton that gives you enough structure to avoid blank-spots while leaving room to improvise. Not a script. Session 46 was over-prepared: full NPC bios embedded, scripted dialogue blocks, exhaustive lore dumps. Session 44 is the gold standard: short bullet flows per scene, NPCs described in one line, detailed lore lives in linked Codex docs, cheat sheet tables appear *inside* the scene they belong to.

The draft prep file has two distinct input sections:
- **`## To Do`** — mechanical and admin tasks only (stream setup, Foundry asset creation, calendar, etc.). These are preserved as-is in the output.
- **`## Scenes`** — the DM's planning notes about what scenes to build. These are the source of intent for generating the scene content.

The synopses are the source of truth for what actually happened. Never trust the previous prep's narrative notes as fact — always verify against the synopsis.

## Vault locations

- **Prep files:** `x_Session Prep/Campaigns/The Bloody Nails/Session <N> - <Title> - Prep.md`
- **Synopses:** `Campaigns/The Bloody Nails/Sessions/Session <N>/Synopsis.md`
- **Codex characters:** `Codex/Characters/<Name>.md`
- **Codex locations:** `Codex/Locations/**/<Name>.md`
- **Legacy stubs:** vault root (many lore files still live here)

## Steps

### 1. Read the draft prep file

Glob for `Session <N> - * - Prep.md` in `x_Session Prep/Campaigns/The Bloody Nails/`. Read it.

- **`## To Do`** contains mechanical and admin tasks only — preserve these verbatim in the output.
- **`## Scenes`** contains the DM's planning notes: scene names, sub-scenes, and any thoughts or intentions they've jotted down. These are the source of intent for generating scene content.

If there is no draft file, ask the user for the session number and a brief description of what they want to cover. Create the file from scratch using the standard frontmatter. When creating from scratch, include an empty `## To Do` and an empty `## Scenes` section for the DM to fill in.

### 2. Read recent synopses — and cross-reference against the previous prep

Read `Synopsis.md` for sessions N-1 and N-2 from `Campaigns/The Bloody Nails/Sessions/`. The synopsis is the authoritative record of what actually happened at the table.

**Why this matters:** Prep notes often describe scenes that were planned but never ran, or include narrative beats written in the past tense that didn't actually occur. If you read only the prep, you'll confidently write false continuity into the new session. Always verify against the synopsis.

**Cross-reference process:**
- After reading both synopses and both previous prep files (if available), look for any scene, plot beat, or character moment that appears in the prep notes as a present fact ("Ayana and Illythia reunite", "the party learns X") but does not appear in the synopsis.
- If you find a discrepancy — something the prep described as happening, but the synopsis doesn't confirm — flag it. Don't assume it happened; don't assume it didn't. Ask the DM.

**Do not read transcript files** — synopses only. They're concise and accurate.

### 3. Collect questions before generating anything

Before writing a single scene, gather all open questions in one pass and ask them together. This is more efficient than interrupting the generation midway.

There are two categories of questions:

**Continuity questions** (from the cross-reference in Step 2): Any scene or plot beat from a previous prep that you cannot confirm happened based on the synopsis. Example: "The session 46 prep describes the Illythia/Ayana reunion in detail, but I don't see it in the synopsis. Did that scene happen?"

**Brainstorm questions** (from the `## Scenes` items): Any scene item that names a mechanic or encounter type but leaves the specifics undefined. Examples of underdeveloped items that need brainstorming:
- A puzzle is named but the text/answer/mechanic isn't specified
- A combat encounter lists enemies but not their behaviour, terrain, or twist
- A social encounter mentions a faction/group but not the shape of the conflict or what the players need to do
- A reveal moment is listed but the nature or delivery of the reveal isn't clear

For each underdeveloped item, ask a focused brainstorm question rather than inventing the details yourself. The DM has the creative vision; your job is to help structure it, not fill in the blanks unilaterally.

**Example brainstorm questions:**
- Cipher puzzle: "You've got a cipher puzzle in the Vault. What should the inscription text be, and what's the answer word the players need to spell out? Any constraint on the cipher alphabet, or should I suggest something based on the setting?"
- Combat: "For the stone guardians — how many, and do you want each one to have a distinct weakness/gimmick, or are they a uniform threat? Any specific environment or terrain in the chamber?"
- Social encounter: "The Confluence scene — is this structured as a formal debate (players are presenting evidence), a hostile interrogation, or something else? Do you want me to model the council members as having individual levers the players can pull?"

Once you have all questions, ask them in a **single message**. Group them clearly — continuity first, then brainstorm. Wait for answers before generating the prep.

### 4. Interpret the Scenes section

The `## Scenes` section contains the DM's raw planning notes — scene names, sub-scenes, and any thoughts or intentions they've jotted down. Each `###` heading in the DM's notes becomes a scene in the output. Group related sub-bullets under that scene.

The DM has already done the housekeeping/scene split — do not second-guess items between `## To Do` and `## Scenes`. Take each section at face value.

### 5. Check for Codex pages

For each NPC and location mentioned in scene items, check whether a Codex page exists:
- Glob `Codex/Characters/<Name>.md`
- Glob `Codex/Locations/**/<Name>.md`
- Also check vault root for legacy stubs: `<Name>.md`

Note what's missing. If an entity has no Codex page and there's not enough context to even write a 1-line inline description, add it to the Step 3 question list rather than asking separately.

### 6. Generate the prep document

Write the prep in the sparse format below. The guiding question for each scene is: *what does the DM need to know to run this confidently?* That's it. Not everything you could say — just what's needed.

**Format rules:**
- NPCs get one line inline: `**[[NPC Name]]** — brief manner/role`
- Cheat sheet tables go **inside** the scene they belong to, not collected at the bottom
- `> [!cite]+` Read Aloud callouts are the only long prose — use sparingly, only for moments that genuinely call for immersive flavour text
- Use callout types: `[!summary]`, `[!cite]`, `[!info]`, `[!question]`, `[!danger]`, `[!check]`
- For scenes with many entities (exploration, shopping, council meetings), add an inline table right there in the scene
- NPC Quick Reference table at the very end: NPC | Role | Manner | Key Line
- `## Notes` at the end for loose threads and reminders

**What to leave out:**
- Full NPC biographies or stat blocks (link to Codex instead)
- Scripted dialogue (bullet the key beats, not the words)
- Lore history dumps (link to Codex or a lore note)
- Redundant information that appears in multiple places

### 7. Write the file

Write to `x_Session Prep/Campaigns/The Bloody Nails/Session <N> - <Title> - Prep.md`. If the file already exists (the TODO source), overwrite it — the TODO items will be preserved in the `## To Do` section of the new doc.

Derive the session title from the primary scenario if not already in the filename. Use title case.

### 8. Offer Codex creation

After writing, list any NPCs or locations that need Codex pages. Offer to create them one at a time using `/codex`. Creating them now means all `[[wikilinks]]` in the prep will resolve correctly.

---

## Output format

```markdown
---
Session Date: YYYY-MM-DD
cssclasses:
  - hide-header-underline-3
tags:
  - session-prep
---

## To Do

- [ ] Stream Setup
- [ ] Set Session Date in Frontmatter
- [ ] Intro/Recap
- [ ] Update Calendar
[all items from the DM's ## To Do section preserved exactly as written]

## Recap

- [[Campaigns/The Bloody Nails/Sessions/Session N-1 - <Title>/Session N-1 - <Title>|Session N-1]]

## Scenario 1: <Name>

> [!summary]- Details
> - Where: [[Location]]
> - When: <timing relative to session start>
> - Key NPCs: [[NPC1]], [[NPC2]]

### Scene 1: <Name>

- Key beat / what happens
- What the players might do or discover

**[[NPC Name]]** — brief manner/role

> [!question] Trigger
> <condition that sets something in motion>
> > [!info]- Action
> > - <what happens as a result>

> [!cite]+ Read Aloud
> *<flavour text — only when a moment truly calls for it>*

### Scene 2: <Exploration / many-entity scene>

> [!example]+ Description
> <2-3 sentence atmosphere, what the party sees/feels>

| Location | What's Here | Proprietor | Key Detail |
|---|---|---|---|
| [[Place 1]] | goods / purpose | [[NPC]] | one interesting hook |
| [[Place 2]] | goods / purpose | [[NPC]] | one interesting hook |

- Scene flow bullets
- What the players can do here

## NPC Quick Reference

| NPC | Role | Manner | Key Line |
|---|---|---|---|
| [[Name]] | Role | 2-3 words | "One quote or key fact" |

## Notes

- Loose threads
- Reminders
```

---

## Gold standard reference

Session 44 (`x_Session Prep/Campaigns/The Bloody Nails/Session 44 - The Elven Archmage - Prep.md`) is the model to follow — short bullet flows, NPCs described inline in one sentence, triggers with nested actions, minimal read-aloud. Session 46 is the anti-pattern — too long, too scripted, full NPC bios embedded, lore dumps inline.
