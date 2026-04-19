---
name: session-recap
description: Use this skill when the user asks to "/session-recap", "generate a recap for session N", "recap session N", "write up last session", "create the synopsis", or wants to produce a full session recap document from a transcript. Given a session number, gathers context from prep notes and previous synopses, requests permission to read the transcript, then produces a publication-ready Synopsis with a cinematic Summary and structured Details section, saved to the session folder. Also trigger when the user says "write the session write-up", "create session notes", or "generate the synopsis for session N".
---

# Session Recap Generator

Produce a complete, publication-ready session recap from a transcript — the full pipeline in one step.

## Why this exists

The previous workflow was: run session-context → paste into Recap prompt → paste transcript → send to Gemini. This skill does it all in-house: it gathers context (prep notes, previous synopsis, wiki links), asks your permission before touching the transcript, processes it, and writes the finished Synopsis file directly.

## Vault locations

- **Prep files:** `x_Session Prep/Campaigns/The Bloody Nails/Session <N> - <Title> - Prep.md`
- **Previous synopses:** `Campaigns/The Bloody Nails/Sessions/Session <N>/Synopsis.md` (or `Synopsis - Claude.md` if that exists)
- **Transcript:** `Campaigns/The Bloody Nails/Sessions/Session <N>/Transcript.md`
- **Recap prompt template:** `x_Templates/Session/Recap - Prompt.md`
- **Output:** `Campaigns/The Bloody Nails/Sessions/Session <N>/Synopsis - Claude.md`

---

## Steps

### 1. Determine the session number

Extract the session number from the user's prompt. If ambiguous, check the most recent session folder that has a Transcript.md but no Synopsis - Claude.md content.

### 2. Build the context header

The prep notes and vault files exist to help you **correct spelling and understand structure** — not to add lore. Read them with that purpose in mind.

**Read the prep file:**
Glob for `Session <N> - * - Prep.md` in the prep directory. Read it for:
- NPC names and aliases (for spelling correction only)
- Scene headings (to understand session structure)
- Locations (for correct spelling)

**Critical constraint — prep is for spelling, not facts:** The prep file contains the DM's planned content. Do not treat anything in it as something the players learned or experienced. Only include information in the recap that was clearly established *in the transcript itself* — things said aloud, witnessed directly, or explicitly confirmed by the DM. If you know from the prep that a vision represents Dondar's past, but the transcript only shows the players seeing a hooded dwarf walk out of a room, write what was seen — not what it means. When in doubt about whether something was actually revealed in the session, leave it out and flag it as a question for the DM.

**Read the previous session synopsis:**
Find `Campaigns/The Bloody Nails/Sessions/Session <N-1>/Synopsis*.md`. Read the full file — you need it both for:
- The `## Summary` section (2–3 sentence continuity context)
- The frontmatter (in-world date, party level — you'll need these in Step 3)

Skip gracefully if it doesn't exist.

**Follow key wiki links (one level deep):**
For `[[WikiLinks]]` in the prep pointing to central NPCs or locations, read the linked vault file for aliases and alternate names only. These help you recognise phonetic transcript mangling. Do not carry lore from these files into the recap unless it was spoken aloud in the session.

**Read the template:**
Read `x_Templates/Session/Recap - Prompt.md`. The "Context Header" contains the standing world context used for spelling reference.

**Build the session-specific context block:**
- **Previous Session:** 2–3 sentences — where the party is coming from.
- **Session Setting:** One line: session number, location, rough situation.
- **Characters Present:** NPCs with significant roles this session. Format: `- Name / Alias: one-line role.`
- **Spelling Reference:** Compact comma-separated list of proper nouns likely to be mangled. Note likely mishearings in parentheses.

### 3. Gather frontmatter information

Before reading the transcript, ask the user for two pieces of information:

> "Before I read the transcript, I need a couple of details for the frontmatter:
> 1. What was the session date? (e.g. 2026-03-28)
> 2. What's the YouTube video ID for the recording? (e.g. `K9zhEnc0p_4`) — leave blank if there isn't one yet."

While waiting, note the in-world date and party level from the previous synopsis's frontmatter. The in-world date for this session will typically be the same or the next day — confirm from the transcript if possible.

### 4. Request permission to read the transcript

Once you have the frontmatter details, ask:

> "Thanks. I'm ready to read the Session <N> transcript at `Campaigns/The Bloody Nails/Sessions/Session <N>/Transcript.md`. May I?"

**Do not read the transcript until the user confirms.**

### 5. Read and process the transcript

Once permission is granted, read the full `Transcript.md`.

**Read the entire file.** Transcripts are long. Do not stop partway through — the second half often contains the most important events. Keep reading until you reach the final line. A recap built on a partial transcript will be incomplete and misleading.

Keep in mind:
- The transcript typically **starts with a recap of the previous session** — skip this opening segment.
- There is typically **a break in the middle** — this is not the end. Continue reading past the break all the way to the final line.
- The transcript will be phonetically messy. Use your context header as the source of truth to correct names, spells, locations, and lore terms.
- **Only write what was in the transcript.** If a vision or event could mean something you know from the prep notes, describe only what was observable — what the players saw and heard. Do not explain or interpret beyond what was made explicit in the session.

### 6. Generate the Synopsis

Produce the recap in this exact format, saved directly to the file (no code block wrapper needed):

```markdown
---
Session Date: <YYYY-MM-DD>
cssclasses:
  - hide-header-underline-3
tags:
  - synopsis
---
> [!infobox|wikipedia]
> # Recording
> [![Title](https://img.youtube.com/vi/<VIDEO_ID>/maxresdefault.jpg)](https://www.youtube.com/watch?v=<VIDEO_ID>)
> # Basic Information
> Attribute |  Details |
> ---|---|
> Session # | <N> |
> Play Date | <YYYY-MM-DD> |
> Players | Deathmouse<br>JC<br>Kiwi<br>Lacer<br>Vael  |
> Party Level | <level> |
> # Session Details
> Attribute |  Details |
> ---|---|
> Date | [[Campaigns/The Bloody Nails/Calendar/...|<in-world date>]] |
> Location | [[<Location>]] |
> Characters | [[NPC1]]<br>[[NPC2]] |

## Summary

[Paragraph 1]

[Paragraph 2]

[Paragraph 3]

## Details

### <Scene Heading>

* <bullet>
...
```

If no YouTube video ID was provided, omit the `# Recording` section from the infobox entirely.

**Frontmatter notes:**
- `Session Date` and `Play Date` = the real-world date the user gave you
- `Party Level` = carry forward from the previous synopsis unless the transcript mentions a level-up
- `Location` = primary location of this session
- `Characters` = 2–3 most significant NPCs (not player characters)
- In-world date = carry forward from the previous synopsis; use the same day or advance by one if the transcript clearly shows time passing

**Summary rules — keep it tight:**
- **3 paragraphs** (not 4). Each paragraph 3–5 sentences. Aim for the length of the Gemini output, not a full prose retelling.
- Cinematic and engaging, but concise — hit the major beats without exhaustively narrating every exchange.
- Include specific plot twists, a key quote or two, major rewards, and the cliffhanger/resolution.
- Only state things that were established in the transcript.
- Wrap NPC names and major locations in `[[WikiLinks]]` on first mention in each paragraph.
- **In-world voice only.** Write the Summary as though it were a chronicle written within the world of Elandis. Use only in-world terminology and language — no numerical damage values (say "a devastating blow" not "45 damage"), no real-world game references (no "World of Warcraft raid", "Dexterity save", "Cone of Cold", "Phase 2"), no spell slot talk, no player names, no meta-game language. Describe what happened narratively: magic effects by their appearance, combat by its drama, mechanics by their fictional consequence. Spell names may appear only when they are recognisable as in-world magic (e.g. a moonbeam is a beam of moonlight). Save all mechanical detail, damage numbers, spell names, ability checks, and meta-commentary for the **Details** section.

**Details rules — one line per bullet:**
- One `###` section per major scene or act.
- Each bullet is one concise line — a fact, action, or beat. Avoid multi-sentence bullets.
- Bold labels for standout moments: `**Character Moment:**`, `**Reward Obtained:**`, `**Major Plot Twist:**`, `**Cliffhanger:**`, etc.
- Wrap NPC names and major locations in `[[WikiLinks]]` on first mention *in each section*.
- Only include what was established in the transcript.

### 7. Save the output

Write the full file (frontmatter + infobox + Summary + Details) to:
`Campaigns/The Bloody Nails/Sessions/Session <N>/Synopsis - Claude.md`

### 8. Offer the DM coaching analysis

After saving, ask:

> "Would you also like a DM coaching analysis? This gives critical feedback on pacing, player agency, spotlight management, and rates the session."

If yes, use the DM Coach prompt from `x_Templates/Session/Recap - Prompt.md` to produce the analysis. Save it to the same file under a `---` divider and `## DM Coaching` heading, or offer to save it separately.

### 9. Flag template updates

If significant recurring NPCs or locations appeared this session that are missing from the standing template's NPCs/Locations sections, note them as suggestions outside the main output. The user reviews and approves before applying.
