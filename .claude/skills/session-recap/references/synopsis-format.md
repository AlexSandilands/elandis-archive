# Synopsis Output Format

Exact format spec for the Session `<N> - <Title>.md` recap file. Saved directly to disk, no code-block wrapper.

## Structure

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

## Frontmatter notes

- `Session Date` and `Play Date` = the real-world date the user gave you
- `Party Level` = carry forward from the previous synopsis unless the transcript mentions a level-up
- `Location` = primary location of this session
- `Characters` = 2–3 most significant NPCs (not player characters)
- In-world date = carry forward from the previous synopsis; use the same day or advance by one if the transcript clearly shows time passing

## Summary rules — keep it tight

- **3 paragraphs** (not 4). Each paragraph 3–5 sentences. Aim for the length of the Gemini output, not a full prose retelling.
- Cinematic and engaging, but concise — hit the major beats without exhaustively narrating every exchange.
- Include specific plot twists, a key quote or two, major rewards, and the cliffhanger/resolution.
- Only state things that were established in the transcript.
- Wrap NPC names and major locations in `[[WikiLinks]]` on first mention in each paragraph.
- **In-world voice only.** Write the Summary as though it were a chronicle written within the world of Elandis. Use only in-world terminology and language — no numerical damage values (say "a devastating blow" not "45 damage"), no real-world game references (no "World of Warcraft raid", "Dexterity save", "Cone of Cold", "Phase 2"), no spell slot talk, no player names, no meta-game language. Describe what happened narratively: magic effects by their appearance, combat by its drama, mechanics by their fictional consequence. Spell names may appear only when they are recognisable as in-world magic (e.g. a moonbeam is a beam of moonlight). Save all mechanical detail, damage numbers, spell names, ability checks, and meta-commentary for the **Details** section.

## Details rules — one line per bullet

- One `###` section per major scene or act.
- Each bullet is one concise line — a fact, action, or beat. Avoid multi-sentence bullets.
- Bold labels for standout moments: `**Character Moment:**`, `**Reward Obtained:**`, `**Major Plot Twist:**`, `**Cliffhanger:**`, etc.
- Wrap NPC names and major locations in `[[WikiLinks]]` on first mention *in each section*.
- Only include what was established in the transcript.
