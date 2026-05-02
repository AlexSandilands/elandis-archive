---
name: session-recap
description: Use this skill when the user asks to "/session-recap", "generate a recap for session N", "recap session N", "write up last session", "create the synopsis", or wants to produce a full session recap document from a transcript. Given a session number, gathers context from prep notes and previous synopses, requests permission to read the transcript, then produces a publication-ready Synopsis with a cinematic Summary and structured Details section, saved to the session folder. Also trigger when the user says "write the session write-up", "create session notes", or "generate the synopsis for session N".
---

# Session Recap Generator

Produce a complete, publication-ready session recap from a transcript — the full pipeline in one step.

## Why this exists

The previous workflow was: run session-context → paste into Recap prompt → paste transcript → send to Gemini. This skill does it all in-house: it gathers context (prep notes, previous synopsis, wiki links), asks your permission before touching the transcript, processes it, and writes the finished synopsis file directly.

## Vault locations

- **Prep file:** `x_Session Prep/Campaigns/The Bloody Nails/Session <N> - <Title> - Prep.md`
- **Session folder:** `Campaigns/The Bloody Nails/Sessions/Session <N> - <Title>/`
- **Previous synopsis:** `Campaigns/The Bloody Nails/Sessions/Session <N-1> - <Prev Title>/Session <N-1> - <Prev Title>.md`
- **Transcript:** `Campaigns/The Bloody Nails/Sessions/Session <N> - <Title>/Transcript.md`
- **Output (this session's synopsis):** `Campaigns/The Bloody Nails/Sessions/Session <N> - <Title>/Session <N> - <Title>.md`

The output file's name matches its parent folder — Obsidian convention.

## References

This skill ships with reference docs alongside `SKILL.md` in `references/`. Read them on demand:

- `references/context-header.md` — the standing world context (setting, players, locations, factions, NPCs). The spelling source of truth for transcript correction. **Read this in Step 2.**
- `references/synopsis-format.md` — the exact frontmatter + infobox + Summary/Details format spec the output must follow. **Read this in Step 6 before writing the recap.**
- `references/dm-coach-prompt.md` — the optional DM coaching analysis prompt. **Read this only if the user accepts the offer in Step 8.**

Keep `context-header.md` updated as the campaign evolves — Step 9 flags new recurring NPCs/locations that should be added.

---

## Steps

### 1. Determine the session number and title

Extract the session number from the user's prompt. Then resolve the full folder name by globbing `Campaigns/The Bloody Nails/Sessions/Session <N> - *` — the matched folder name (e.g. `Session 49 - The Silver Sage`) is also the title used for the output filename. If ambiguous, check the most recent session folder that has a `Transcript.md` but no matching `Session <N> - <Title>.md` synopsis yet.

### 2. Build the context header

The prep notes and vault files exist to help you **correct spelling and understand structure** — not to add lore. Read them with that purpose in mind.

**Read the prep file:**
Glob for `Session <N> - * - Prep.md` in the prep directory. Read it for:

- NPC names and aliases (for spelling correction only)
- Scene headings (to understand session structure)
- Locations (for correct spelling)

**Critical constraint — prep is for spelling, not facts:** The prep file contains the DM's planned content. Do not treat anything in it as something the players learned or experienced. Only include information in the recap that was clearly established *in the transcript itself* — things said aloud, witnessed directly, or explicitly confirmed by the DM. If you know from the prep that a vision represents Dondar's past, but the transcript only shows the players seeing a hooded dwarf walk out of a room, write what was seen — not what it means. When in doubt about whether something was actually revealed in the session, leave it out and flag it as a question for the DM.

**Read the previous session synopsis:**
Glob `Campaigns/The Bloody Nails/Sessions/Session <N-1> - *` to find the previous session folder, then read `Session <N-1> - <Prev Title>.md` inside it. Read the full file — you need it both for:

- The `## Summary` section (2–3 sentence continuity context)
- The frontmatter (in-world date, party level — you'll need these in Step 3)

Skip gracefully if it doesn't exist.

**Follow key wiki links (one level deep):**
For `[[WikiLinks]]` in the prep pointing to central NPCs or locations, read the linked vault file for aliases and alternate names only. These help you recognise phonetic transcript mangling. Do not carry lore from these files into the recap unless it was spoken aloud in the session.

**Read the standing context header:**
Read `references/context-header.md` (alongside this `SKILL.md`). It contains the standing world context (Setting, Players, Locations, Factions, NPCs) used as the spelling source of truth.

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

> "Thanks. I'm ready to read the Session <N> transcript at `Campaigns/The Bloody Nails/Sessions/Session <N> - <Title>/Transcript.md`. May I?"

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

Read `references/synopsis-format.md` for the exact output format spec — frontmatter shape, infobox layout, Summary rules (3 paragraphs, in-world voice, no game mechanics), and Details rules (one line per bullet, bold labels for standout moments).

Produce the recap following that spec, saved directly to the file (no code-block wrapper).

### 7. Save the output

Write the full file (frontmatter + infobox + Summary + Details) to:

`Campaigns/The Bloody Nails/Sessions/Session <N> - <Title>/Session <N> - <Title>.md`

The filename matches the parent folder name. If a file already exists at that path, ask before overwriting.

### 8. Offer the DM coaching analysis

After saving, ask:

> "Would you also like a DM coaching analysis? This gives critical feedback on pacing, player agency, spotlight management, and rates the session."

If the user says yes, read `references/dm-coach-prompt.md` and follow it to produce the analysis. Append the output to the synopsis file under a `---` divider and `## DM Coaching` heading, or offer to save it as a separate file alongside the synopsis if the user prefers.

### 9. Flag template updates

If significant recurring NPCs or locations appeared this session that are missing from the standing template's NPCs/Locations sections, note them as suggestions outside the main output. The user reviews and approves before applying.
