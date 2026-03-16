---
name: session-context
description: Use this skill when the user asks to generate session context for a D&D recap, wants to prepare a Gemini prompt for transcription recap, says "/session-context", asks to "generate context for session N", or wants to fill in the Session Context section of the recap prompt. Given a session number, reads the prep notes and previous synopsis to produce a paste-ready context block plus suggested updates to the standing recap prompt template.
---

# Session Context Generator

Generate a session-specific context block for pasting into the D&D session recap prompt, plus suggested updates to the standing prompt template.

## Why this matters

The recap prompt sends a raw (potentially error-filled) transcript to Gemini with a "Context Header" as the spelling source of truth. The `## Session Context` section is the only part that changes each session — it tells Gemini what happened this specific session, who the key NPCs are, and what terms to watch for. The better this section is, the more accurate and narrative-aware the recap will be.

The standing template's NPC/Locations sections also get stale over time. The skill flags when significant new permanent characters or places should be added, so the template stays current.

## Vault locations

- **Prep files:** `x_Session Prep/Campaigns/The Bloody Nails/Session <N> - <Title> - Prep.md`
- **Synopses:** `Campaigns/The Bloody Nails/Sessions/Session <N>/Synopsis.md`
- **Recap prompt template:** `x_Templates/Session - Recap - Prompt.md`

## Steps

### 1. Read the prep file

Glob for `Session <N> - * - Prep.md` in the prep directory. Read the full file. The NPC Quick Reference table (usually at the bottom) and scene headings are the most efficient sources — read them first to orient yourself.

### 2. Read the previous session's synopsis

Find and read `Campaigns/The Bloody Nails/Sessions/Session <N-1>/Synopsis.md`. The `## Summary` section is all you need — it gives Gemini the continuity context to understand where the party is coming from. If it doesn't exist, skip it gracefully.

### 3. Follow key wiki links (one level deep)

For `[[WikiLinks]]` pointing to central NPCs or locations in the prep, read the linked vault file. Focus on:
- Aliases and alternate names — these are the highest-value items for spelling correction, since players will say the name the character is *known by*, not necessarily what's in the prep
- Relationships that will affect how Gemini interprets dialogue
- Lore context central to understanding the session's events

Don't follow every link recursively — prioritise named characters with significant roles this session, and any location with its own vault note.

### 4. Read the current template

Read `x_Templates/Session - Recap - Prompt.md` to understand what's already in the standing NPCs and Locations sections. You need this to avoid duplicating what's already there and to identify what's missing.

### 5. Build the Session Context block

The goal is orientation and spelling correction — not a pre-told story. Gemini has the transcript; it doesn't need to know what happened. It needs to know *who* the names belong to and *how to spell them*. Keep every subsection as tight as possible.

Produce a `## Session Context` section with the following subsections:

**Previous Session:**
2–3 sentences only — just enough for Gemini to understand where the party is coming from and why they're in the current location. Draw from the previous synopsis's Summary section.

**Session Setting:**
One line: location, rough situation. e.g. `Session 46. The party enters Sumara, the hidden elven city in the Faewild, and attends a council meeting to present Ryo's royal claim.`

**Characters Present:**
NPCs who appear or are heavily discussed this session. Format:
`- Name / Alias: one-line role only.`

Keep it to name, alias(es), and role — nothing more. Aliases are the most important thing here since they're what players say aloud. Focus on NPCs *not already in the template's standing list*, plus any standing NPCs with new name reveals this session.

**Spelling Reference:**
A compact comma-separated list of proper nouns likely to be mangled by transcription software. Where a likely mishearing is obvious, note it in parentheses: `Syndrosa (not Sindrosa)`. This is the single most useful thing in the block — prioritise unusual names and multi-syllable fantasy terms.

### 6. Suggest template updates

Compare the session's significant NPCs and locations against the standing template. If recurring characters or places are missing from the template entirely, output a clearly marked suggestions block *outside* the main code block:

Only flag things that seem permanent — characters or places likely to recur in future sessions. Skip one-off encounters or minor NPCs.

## Output format

**Block 1** — A fenced code block containing the `## Session Context` markdown, ready to paste at the `....` placeholder in the template.

**Block 2** — A plain suggestions section outside the code block, clearly marked, listing any recommended additions to the standing template. The user reviews and approves these before applying.

If there are no template updates worth suggesting, omit Block 2 entirely.

## Example output structure

````markdown
## Session Context

**Previous Session:**
The party traversed the Faewild to reach Sumara — crossing the Gossamer Woods (where Ayana was hit by Gossamer Dust and de-aged to a child), the Briarshade forest, and the Liar's River (via a life-sized chess game against Uncle Grumble). They arrived at the foot of the Shimmering Peaks with child-Ayana in tow.

**Session Setting:**
Session 46. The party enters Sumara, the hidden elven city in the Faewild, and attends a council meeting to present Ryo's royal claim and Ayana's revelation about Kharazoth.

**Characters Present:**
- Ayana Syndrosa / Lady Syndrosa / Ayana Wynne: Former leader of the Circle of the Weave. True name revealed this session.
- Illythia Voss: Current leader of the Circle of the Weave. Ayana's former lover.
- Kaelen Vayne / Commander Vayne: Leader of the Circle of the Blade. De facto council head.
- Naivara Siannodel / Justiciar Naivara: Leader of the Circle of the Scales.
- Elrohir Gemflower / Archivist Elrohir: Leader of the Circle of the Scroll.
- Elder Silaqui Amastacia: Leader of the Circle of the Dawn.
- Warden Sylvaris: Leader of the Circle of the Root.
- Fenian / Master Artisan Fenian: Leader of the Circle of the Loom.
- Warden Caeryn: Lead arresting officer. Trained under Ayana.
- Warden-Elder Thessan: Caeryn's superior.
- Elder Pip Glimmermoss: Pixie healer. Reverses the Gossamer Dust on Ayana.
- Torgrun Brasswick: Dwarf tavern owner, from Glimmerforge.
- Syriel Brasswick: Torgrun's wife, an elf.
- Thenrel Arith: Elf road worker on the mountain approach.

**Spelling Reference:**
Syndrosa (not Sindrosa), Kharazoth (not Karazoth), Silmara (not Silmira), Illythia (not Ilithia), Siannodel (not Sianodel), Amastacia (not Anastacia), Gemflower (not Gem Flower), Thessan (not Thesson), Glimmerforge, Vanguard Wardens, Gossamer Dust, Locus Arcanum, Palisade Eternal, Luminarium, Oraculum, Verdant Vault, Rite of Ascension, Confluence of the Seven
````

---
## Suggested Template Updates

The following are missing from the standing recap prompt and seem likely to recur. Review and apply as you see fit.

**Add to NPCs section:**
- Illythia Voss: Leader of the Circle of the Weave in Sumara. Ayana's former lover.
- Kaelen Vayne: Leader of the Circle of the Blade. De facto council authority.
[...]

**Add to Locations section:**
- Sumara / The Shining City: Hidden elven city in the Faewild (Shimmering Peaks)
[...]
