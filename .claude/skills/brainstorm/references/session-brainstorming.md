# Mode B — Session-prep brainstorming

`/session-prep` turns a decided TODO into a polished, scan-in-two-minutes prep doc. But it can only format what the draft already lists. This mode is the step before that: it sits with the DM, figures out **where the session is heading and what the players are likely to do**, **spots the prep gaps they haven't thought of**, and **lightly flags what's worth writing down versus what can be left to improv** so the DM doesn't sink hours into detail that never reaches the table. The output is an actionable prep checklist plus scene notes, written into the draft prep file for `/session-prep` to consume.

> Follow the three shared principles from `SKILL.md` throughout: the DM is in control, depth is adaptive, everything is grounded in canon. Never read `Transcript.md` files.

## The job, stated plainly

Riv's recurring failure mode is **over-prep** — sinking hours into writing exhaustive detail about every location the party might visit, most of which never gets used. A core part of this mode is helping counteract that: you're here to help write *less, and the right things*. Where it's obviously relevant, gently note what's worth writing down versus what's safe to improvise — a light reminder, not a running audit of every element. Riv stays in control of how much to prep; your job is to make the trade-off visible, not to police it.

At the same time, catch the opposite failure: a gap where the players will reasonably do something and the DM will be caught flat-footed with nothing to tell them. (Last session the party set out to gather information about the [[Veil of Eternal Night]]; that only works if the lore is actually prepped and ready to deliver.) Your job is to find those gaps before the table does.

## B1 — Identify the session and locate the draft prep file

Work out which session this is for.

- If the message names a number ("session 51"), use it.
- If it says "the next session", determine N: the latest `Synopsis.md` folder under `Campaigns/The Bloody Nails/Sessions/` tells you the last session played; the next session is one higher. Cross-check the prep folder. Confirm the number with the DM in your opening message rather than silently guessing if there's any ambiguity (duplicate/`XXX` draft files are common).

Locate the draft prep file:

```bash
ls "x_Session Prep/Campaigns/The Bloody Nails/" | grep "Session <N>"
```

- If a `Session <N> - <Title> - Brainstorm.md` already exists, that's your target — you're continuing a brainstorm. Read it.
- Otherwise look for the DM's skeleton, usually `Session <N> - XXX - Prep.md` (or a titled `- Prep.md` not yet brainstormed). Read it for any existing `## To Do` admin items and jotted scene intent — in B5 you'll turn it into the `- Brainstorm.md` draft.
- If nothing exists, you'll create the `- Brainstorm.md` draft in B5 from the standard template (frontmatter + `## To Do` with the standard admin items + `## Scenes`).

> **The brainstorm draft is its own file — `Session <N> - <Title> - Brainstorm.md`** — kept separate from the polished `- Prep.md` that `/session-prep` later produces, so your working notes and DM seeds survive. Never write the brainstorm into `- Prep.md`.

## B2 — Research where the party is and where they're heading

Before asking anything, reconstruct the situation. This is what lets you project what the players will do and walk in already knowing the gaps.

- **Read the previous synopsis** (`Campaigns/The Bloody Nails/Sessions/Session <N-1> - <Title>/Synopsis.md`) — the authoritative record of where the party ended up, what they decided, and what they said they'd do next. Read N-2 as well if N-1 leaves the direction unclear. **Synopses are truth; never trust a prior prep's narrative notes as fact** — preps describe what was *planned*, which often diverges from what happened.
- **Read the previous prep's `## Notes` / loose threads** (if present) for dangling hooks the DM already flagged.
- **Identify the likely destinations, NPCs, and subjects** the party will engage this session (e.g. "they're off to find [[the Silver Sage]]"; "they'll keep digging into the [[Veil of Eternal Night]]").
- **For each likely subject, check whether the lore actually exists to support it.** Glob/grep `Codex/` and the vault root:

  ```bash
  grep -rln "Silver Sage" <vault> --include="*.md" | grep -vi transcript
  ls Codex/Characters/ Codex/Locations/ 2>/dev/null | grep -i "<name>"
  ```

  A subject the players will interrogate but that has **no prepped lore behind it is a gap** — that's the Veil-of-Eternal-Night situation. Note these; they become both questions and checklist items.

Build a mental model: where is the party, what are the 2-3 most likely directions the session takes, and which of those are already supported by canon versus which need prep.

## B3 — Open with a situation brief, projected directions, and the gaps you already see

Lead with what you found — never with a cold question. Show the DM you understand where the session sits.

```
Here's where the party is coming into Session N:

- [where they ended last session, from the synopsis]
- [what they said they'd do next]
- [open threads still live]

The most likely shapes for this session:
1. [direction A — e.g. travel to the Sage through the forest]
2. [direction B — e.g. the players linger in the city chasing the Reclaimer rumours]

Gaps I can already see:
- [e.g. "they'll want to know what the Sage actually knows about the Veil — is that lore written down anywhere? I don't see a doc for it."]

Which way do you think they'll go — and is there anything you already know you want to happen?
```

Then ask your opening batch of questions (≤5, open-ended, natural prose — same rules as Mode A). Aim them at **direction and intent**, not detail yet: where's the session going, what does the DM want to land, what are they unsure about.

## B4 — Brainstorm the prep in rounds

This is the heart of the mode and it happens over several turns. As the shape of the session firms up, walk through it **scene by scene** (or beat by beat). For each prospective scene:

### (a) Classify the scene, then apply the right prep heuristic

Figure out what *kind* of scene it is and reason about what that kind actually needs:

- **Travel / journey** — Does anything happen en route, or is it a cutaway? If something might: suggest a **random-encounter table** and prepping **2-3 encounters** to populate it (mix of combat, social, and discovery — not all fights). Flag what each encounter would need (a map? a stat pick? just a description?). Most travel needs *one* table and a couple of light options, not a written-out gauntlet.
- **Combat** — What's the threat, and what does running it actually require? Typically: a **battle map** (call out explicitly: "this is a map you'll need to build in Foundry"), a **monster/stat selection** (suggest using a tool — e.g. a CR-appropriate lookup against the party level — rather than hand-writing stat blocks), **terrain or an environmental twist** that makes the fight interesting, and the **trigger/stakes**. Numbers and balance are real work; flag them.
- **Social / negotiation** — Who are the NPCs (one line each is enough), what does each one *want*, what's the shape of the conflict, and what do the players need to achieve or extract? The prep here is *levers and motivations*, not scripted dialogue.
- **Investigation / information-gathering** — This is the gap-prone one. What will the players ask about, and **is the information they'd uncover actually written down somewhere you can read it aloud?** If not, that lore is the prep. Identify the 2-4 facts/clues that need to exist and where they live.
- **Exploration of a place** — What can they find, who's there, what's the hook? A short table of points-of-interest beats paragraphs of description. (This is where over-prep bites hardest — see (b).)
- **Set-piece / reveal** — What's the reveal, how is it delivered, what's the trigger? One crisp beat, not a chapter.

### (b) Flag what's worth writing vs leaving to improv — lightly

As elements come up, keep a sense of which need to be on the page and which don't, and **surface that where it's obviously relevant** — not as a running audit of every line:

- **Worth writing** — things you can't reliably make up live: specific lore the players will extract, the answer to a puzzle, encounter stat selections and the map list, a number/name/date that must stay consistent, a secret or twist with moving parts, a clue chain that has to hang together.
- **Leave to improv** — things a competent DM invents at the table without missing a beat: ambient description, the look of a forest, minor NPC chatter, the texture of a market, transitional scenes, flavour. A one-line vibe note is plenty; no write-up needed.

When you notice the conversation drifting into prep that probably won't pay off — usually an elaborate location write-up for a place the party is just passing through — say so gently and move on:

> The party's only passing through the forest, so I'd keep it loose — an encounter table and a few bullets of atmosphere is probably enough rather than a full write-up. Up to you, though.

If the DM wants to develop a place into a real entry anyway, that's their call — just note it might fit better as a `/brainstorm` + `/codex` pass (Mode A) than buried in session prep. The default lean is toward *less*, but Riv decides.

### (c) Surface the concrete production tasks

As the worth-writing elements firm up, name the actual artifacts the DM will have to produce, because those are what eat time and get forgotten:

- **Maps** — "you'll need a battle map for the bridge fight" / "two maps: the forest road and the Sage's sanctum."
- **Monsters / stats** — "pick 2-3 CR-appropriate beasts for the forest table — want me to suggest some, or will you use a tool?"
- **Lore to have ready** — "write a short brief on what the Sage knows about the Veil, so you can deliver it live."
- **Handouts / props** — letters, maps shown to players, puzzle text, ciphers.
- **NPC one-liners** — name + manner + what they want, not a bio.

Keep the conversational rhythm of Mode A: fewer questions per turn after the opening batch, follow the threads, offer ideas they can take or leave, reconcile against canon, and **check in** ("want to keep going, or shall I write this up into the draft?") rather than deciding for them. Scale the number of rounds to the session's complexity.

## B5 — Write the brainstorm into the draft prep file

Write the results into the brainstorm draft — `Session <N> - <Title> - Brainstorm.md` (creating it from the standard template if it doesn't exist), mapping onto the sections `/session-prep` consumes: `## To Do`, `## Scenes`, `## Codex To-Do`, and `## Notes`. Keep the existing frontmatter; preserve any admin items already in `## To Do`.

```markdown
---
Session Date:
cssclasses:
  - hide-header-underline-3
tags:
  - session-prep
---

## To Do

[Preserve the standard admin items already present — Stream Setup, Set Session Date,
Intro/Recap, Update Calendar, etc. — verbatim.]

Then append the actionable prep checklist, GROUPED BY PREP TYPE, each item tagged
with the scene it serves:

**Maps**
- [ ] Forest road battle map — *Scene 2*
- [ ] The Sage's sanctum map — *Scene 3*

**Monsters / Encounters**
- [ ] Pick 2-3 CR-appropriate beasts for the forest random-encounter table — *Scene 2*

**Lore to have ready**
- [ ] Short brief: what the Silver Sage knows about the [[Veil of Eternal Night]] — *Scene 3*

**NPCs**
- [ ] [[Silver Sage]] one-liner: manner + what they want — *Scene 3*

**Handouts / Props**
- [ ] (only if any)

## Scenes

### Scene 1: <Name>
- Key intent / what this scene is for
- [the decided beats and ideas]
- [encounter approach if relevant: "random table, 2-3 options"]
- [worth-writing vs leave-loose, noted where it matters: "have the Veil lore brief ready; keep the forest description improv"]
- [gaps flagged: "needs the Veil lore brief — see checklist"]

### Scene 2: <Name>
- ...

## Codex To-Do

[Lore this brainstorm invented or advanced that needs a /codex pass before it reaches
the table. One checkbox per subject: entry name, (new/update + Restricted?), and a
one-line of what it needs. This is an authoring backlog, not table prep.]

- [ ] **[[Subject]]** *(new + Restricted)* — what it needs, in one line
- [ ] **[[Subject]]** *(update)* — what changed and why it now matters
```

Format rules for the write-up:

- **The `## To Do` checklist is the actionable list** the DM asked for: grouped by prep type (Maps, Monsters/Encounters, Lore to have ready, NPCs, Handouts/Props), each item tagged with its scene in italics. `/session-prep` preserves `## To Do` verbatim, so this checklist carries straight through into the finished doc.
- **`## Scenes` carries the intent** `/session-prep` formats into the polished scene flow. Use one `###` heading per scene — that's the structure `/session-prep` reads.
- **The `## Codex To-Do` is the lore backlog** the brainstorm generated — every new or advanced subject the players will interrogate that needs a real page behind it. List each as a checkbox: entry name, `(new/update + Restricted?)`, and a one-line of what it needs. This is *authoring* work, not table prep — it's the structured, trackable form of the lore-gap flag from B6, and the DM clears it with `/codex` before the session. Only include subjects that genuinely need writing; don't list every proper noun. (`/session-prep` should preserve this section verbatim, like `## To Do`.)
- **Note the worth-writing vs leave-loose calls where they matter.** Capture the ones that came up in conversation so the DM has a durable record of what not to over-prepare — but only where it's a real call, not on every bullet.
- **Capture decisions, not open questions.** No `TODO`/`???` litter inside the scene notes themselves (the `## To Do` checkboxes are the intended actionable items; that's different). If a thread genuinely stayed open, write it as a clear note ("Open: whether the Sage is hostile or wary").
- **Link established proper nouns** with `[[wikilinks]]` from what you confirmed in research.
- **Don't write the finished prose.** No read-aloud blocks, no cheat-sheet tables, no scripted beats — that's `/session-prep`'s job. You're producing the decided intent and the checklist, not the polished doc.
- **Name the draft `Session <N> - <Title> - Brainstorm.md`** — derive a working title from the primary scenario (title case). If you're working from an `XXX` (or untouched `- Prep.md`) skeleton, rename it to the `- Brainstorm.md` draft; don't leave the brainstorm in a `- Prep.md` file, since that's where `/session-prep` writes the polished doc.

## B6 — Hand off to session-prep (and flag any lore that needs writing first)

Tell the DM the brainstorm draft is filled and ready, and that they can run `/session-prep` to turn it into the polished scan-in-two-minutes doc. `/session-prep` writes that to a separate `Session <N> - <Title> - Prep.md` and leaves this `- Brainstorm.md` intact, so the working notes and DM seeds are kept. Don't run it yourself.

Crucially, **call out any lore gaps that should be filled before the session** — a subject the players will interrogate that has no Codex/lore doc behind it. These should already be captured as checkboxes in the **`## Codex To-Do`** section of the draft (B5); the handoff is where you surface them out loud. Suggest a quick `/brainstorm` (Mode A) + `/codex` pass on each, so the information actually exists to deliver at the table.

```
Filled in [path]. The prep checklist is grouped by type in ## To Do (maps, monsters, lore, NPCs) with each item tagged to its scene, and ## Scenes has the beat-by-beat intent — with the worth-writing-vs-improv calls noted where they matter, so you don't over-prep.

Two things flagged: you'll need [N maps] and a short lore brief on [subject] — that one has no Codex page yet, so consider a quick /brainstorm + /codex on it before the session so you've got something to read from.

And ## Codex To-Do lists the entries this brainstorm needs written — [Subject A], [Subject B] — clear them with /codex before the session.

Ready for /session-prep whenever you are.
```
