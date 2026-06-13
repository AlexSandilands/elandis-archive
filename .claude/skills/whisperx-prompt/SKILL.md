---
name: whisperx-prompt
description: This skill should be used when the user asks to "/whisperx-prompt", "generate a whisperx prompt", "make a transcription prompt for session", "create a dnd-transcribe prompt", or wants a WhisperX initial_prompt for a D&D session. Given a session number, reads the session prep notes from the Obsidian vault, extracts all proper nouns, and outputs a ready-to-use prompt string for dnd-transcribe.
---

# WhisperX Prompt Generator

Generate a compact, high-quality `initial_prompt` string for WhisperX to improve transcription accuracy of D&D session recordings.

## Why this matters

WhisperX uses `initial_prompt` as vocabulary context — a dense list of proper nouns that primes the model to recognise names it would otherwise mishear or mangle. The effective limit is ~224 tokens (~900 characters). Every character counts, so prioritise specificity over completeness.

## Vault location

Session prep files live at:
```
/mnt/storage/Misc/Vaults/Elandis/x_Session Prep/Campaigns/The Bloody Nails/
```
Files are named: `Session <N> - <Title> - Prep.md`

## Steps

### 1. Find and read the prep file

Glob for `Session <N> - * - Prep.md` in the prep directory. Read the full file.

### 2. Extract terms from the prep

Gather every proper noun in these categories:

- **NPCs** — full names, titles, and any aliases or alternate names mentioned in the text (e.g. if the prep reveals "Caeryn" is also called "Skyguard Caeryn", include both; if Ayana is revealed to have a secret name like "Lady Syndrosa", include that too). The NPC Quick Reference table at the bottom of most prep files is the most reliable source.
- **Locations** — place names from `[[WikiLinks]]`, scene headings, and descriptions. Include both the proper name and any colloquial shorthand used in the text.
- **Lore terms** — faction names, artefacts, historical events, spells, creatures, and world-specific vocabulary.

### 3. Follow key wiki links

For any `[[WikiLink]]` that points to a character, location, or lore note — especially ones that seem central to the session — read the linked vault file. Look for:
- Aliases and alternate names not in the prep (these are high-value: they're the names players will actually say)
- Related terms that appear in that note but not the prep

Don't follow every link recursively — one level deep is enough. Prioritise linked character notes and location notes over generic lore stubs.

### 4. Build the prompt

Assemble the final string using this structure:

```
D&D session in Valtorra. DM: Riv. Players: Kiwi (Dondar), Lacer (Kai), Deathmouse (Eryndor), JC (Ryo), Vael (Berberis/Vaeleran). Session <N> in <primary location/theme>. NPCs: <names>. Locations: <places>. Lore: <terms>.
```

**Prioritisation (if approaching the 900-char limit):**
1. NPCs with aliases (highest value — spoken names that Whisper needs to spell correctly)
2. Locations central to the session
3. Lore terms and faction names
4. Background locations / minor lore

**Do not include:** generic English words ("the Commons", "the road"), overly broad terms ("magic", "elf"), or session structure words ("Scene 1", "Read Aloud").

### 5. Output

Output the prompt as a single line wrapped in double quotes, followed by the character count (excluding the quotes). Format:

```
"<prompt text>"
```

This lets the user paste it directly into a fish shell command as an argument.

## Fixed header (always use exactly this)

```
D&D session in Valtorra. DM: Riv. Players: Kiwi (Dondar), Lacer (Kai), Deathmouse (Eryndor), JC (Ryo), Vael (Berberis/Vaeleran).
```

## Example — Session 46

```
"D&D session in Valtorra. DM: Riv. Players: Kiwi (Dondar), Lacer (Kai), Deathmouse (Eryndor), JC (Ryo), Vael (Berberis/Vaeleran). Session 46 in Sumara, the Shining City, Faewild. NPCs: Ayana Syndrosa, Lady Syndrosa, Illythia Voss, Kaelen Vayne, Naivara Siannodel, Elrohir Gemflower, Silaqui Amastacia, Fenian, Warden Sylvaris, Thenrel Arith, Skyguard Caeryn, Warden-Elder Thessan, Elder Pip Glimmermoss, Torgrun Brasswick, Syriel Brasswick, Lyris Thornweave, Sporryn, Ferethis, Arcanist Levvel. Locations: Shimmering Peaks, Heartstone Commons, Locus Arcanum, Luminarium, Palisade Eternal, Oraculum, Ironsward Canton, Royal Citadel, Verdant Vault, Liar's River, Glimmerforge. Lore: Kharazoth the Crimson Shadow, Chaos Wars, Gossamer Dust, Emerald Ceremony, Rite of Ascension, Skyguard, Ratha Silmara, Rhennaya Silmara, Crimson Empire."
```
*857 characters*
