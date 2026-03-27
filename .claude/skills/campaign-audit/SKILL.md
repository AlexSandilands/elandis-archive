---
name: campaign-audit
description: Use this skill when the user asks to "/campaign-audit", "audit a character", "check campaign references", "verify session appearances", or wants to validate that a character's Campaign sections match the actual session synopses. Also trigger when the user mentions fixing drift in character entries, checking for missing session appearances, or reconciling a character's page with synopses. This skill reads the character's Codex entry, cross-references every session synopsis, and produces a detailed accuracy report with optional fixes.
---

# Campaign Audit

Validate a character's Campaign appearance sections against the actual session synopses. Characters accumulate campaign sections over time and details drift — events get attributed to the wrong session, key moments are missed, or descriptions diverge from what actually happened. This skill catches all of that.

## When to use

Any time you need to verify whether a character's Codex entry accurately reflects their appearances across the campaign. The most common scenarios:

- A character page was just written or updated and needs a sanity check
- You're about to publish and want to make sure campaign sections are accurate
- The user asks to "audit" or "check" a character

## Vault locations

- **Character entries:** `Codex/Characters/<Name>.md`
- **Session synopses:** `Campaigns/The Bloody Nails/Sessions/Session <N>/Synopsis.md`
- **Session prep (spelling reference):** `x_Session Prep/Campaigns/The Bloody Nails/`

## Steps

### 1. Read the target character's Codex entry

Read the full character file. Extract:

- **Character name and aliases** — from frontmatter `aliases` field and any bold aliases in the text (e.g. "adopted the name **Ayana Wynne**"). You need all of these to search synopses effectively, since the character may be referred to differently across sessions.
- **Existing campaign session references** — look for the `### Campaign:` section and its `####` sub-headings, which link to specific session synopses. Note both the session number and the narrative content written for each appearance.
- **Key claims** — for each session entry, note the specific events, interactions, and details described. These are what you'll verify.

### 2. Search all synopses for appearances

Search across all synopsis files for the character's name and every known alias. Use grep to find mentions efficiently — do NOT read every synopsis file in full.

```
grep -rl "Character Name\|Alias1\|Alias2" Campaigns/The Bloody Nails/Sessions/*/Synopsis.md
```

This gives you the complete list of sessions where the character appears. Compare this against the sessions already documented in the character's entry.

**Metadata vs narrative appearances:** A character being listed in a synopsis's frontmatter `Characters` field or infobox does not necessarily mean they appear in the session. These metadata fields were sometimes populated from templates and may be inaccurate. Only count a character as appearing in a session if they are mentioned in the actual synopsis body text (`## Summary` or `## Details`). If a character appears only in frontmatter/infobox metadata but not in the narrative, ignore that session entirely — do not report it as a missing appearance.

### 3. Read and verify each referenced synopsis

For every session listed in the character's campaign section, read the synopsis (the `## Summary` and `## Details` sections are the key parts) and check:

- **Does the character actually appear?** Sometimes a session reference is wrong — the character was in a different session, or a scene was misattributed.
- **Are the events accurate?** Compare the specific claims in the character entry against what the synopsis describes. Look for:
  - Correct session attribution (did this event happen in Session 45 or 46?)
  - Accurate details (names, locations, actions, outcomes)
  - Missing context that changes the meaning
  - Embellishments that aren't supported by the synopsis
  - **Tone and severity** — does the entry soften, dramatise, or mischaracterise what happened? For example, if the synopsis says a character "lost her mental faculties" but the entry says she "lost her composure," that's a meaningful difference in severity. Similarly, if the synopsis describes something as dangerous but the entry calls it a "prank," that's an editorial liberty worth flagging.

Be thorough but fair — the character entry is a narrative summary, not a transcript. Minor rephrasing is fine. What matters is factual accuracy and faithful representation: who did what, where, in which session, and with what tone.

### 4. Read synopses for unlisted appearances

For sessions where the character appears (from Step 2) but has no entry in the character's campaign section, read the synopsis to understand:

- How significant is the appearance? (Named and active vs. briefly mentioned in passing)
- What happens to or around the character?
- Is this worth adding to the character's entry?

Minor mentions (e.g. "they passed through the market where [[Gemma]] was trading") may not need their own section. Significant interactions, plot developments, or character moments should be flagged as missing.

### 5. Produce the audit report

Present findings in three clear sections:

**Confirmed** — Session entries that accurately reflect the synopsis. Keep this brief — just note the session and a one-line confirmation.

**Discrepancies** — Details that don't match. For each:
- Which session
- What the character entry says
- What the synopsis says
- A suggested correction

Quote both sources so the user can see the mismatch without having to open files.

**Missing Appearances** — Sessions where the character appears but has no campaign section entry. For each:
- Which session
- Brief summary of the character's role/actions (from the synopsis)
- Recommended importance: suggest whether this warrants a new `####` session entry or is too minor

### 6. Offer to apply fixes

This step is not optional — always end the report by asking the user what they'd like to do next. The whole point of the audit is to lead to action, not just produce a document. Present these options:

1. **Fix discrepancies** — update the existing session entries with corrected details
2. **Add missing appearances** — write new `####` session entries for significant unlisted appearances
3. **Both**
4. **Neither** — just use the report as reference

When writing new session entries, match the style of the existing entries in the character's file. Look at how Ayana Syndrosa's campaign sections are written — concise narrative paragraphs that capture the character's key moments, interactions, and developments within that session. Each entry should feel like a self-contained summary of "what happened to this character in this session."

Format session links consistently:
```markdown
#### [[Campaigns/The Bloody Nails/Sessions/Session <N>/Synopsis|Session <N> — <Title>]]
```

The title should come from the synopsis or prep file name. If neither provides a clear title, derive one from the session's main event.

## Scope

This skill currently handles Characters only. The approach could extend to Locations, Factions, or any entity with campaign appearance tracking, but Characters are the priority — they have the most complex cross-references and the highest risk of drift.

## Important

- Do NOT read transcript files (`Transcript.md`) — they are massive and error-prone. Synopses are the source of truth.
- When searching for character mentions, always search for all known aliases. Players and synopses may use short names, titles, or adopted identities.
- If a character entry has placeholder content (e.g. `- [ ] Why did they appear`) rather than actual narrative, flag this as incomplete rather than as a discrepancy.
