---
name: brainstorm
description: Use this skill when the user wants to brainstorm, flesh out, develop, or workshop the details of a D&D vault entry through conversation — before it gets formatted into a finished Codex page. Triggers on "/brainstorm", "brainstorm the X note", "let's flesh out X", "develop the X entry", "help me come up with details for X", "I want to work on the X note", or any time the user points at a thin or empty note — a character, location, item, faction, event, or lore concept — and wants to figure out what it should contain. ALSO trigger when the user says they want to brainstorm or develop an idea before running /codex on it. This skill searches the vault for everything already established about the subject, presents that canon, then asks adaptive open-ended questions — a few for a minor note, several rounds for an important one — and writes the gathered ideas into the note as organized DM notes (using the ## Restricted convention for secrets) so /codex can turn it into a polished entry. This is the front-end to /codex: reach for it whenever a source note is too thin for codex to work from, and the DM wants to develop it collaboratively rather than hand over a finished brief.
---

# Brainstorm — Develop a Vault Entry Through Conversation

The `/codex` skill turns a note full of details into a polished, publication-ready wiki entry. But it can only work with what's already in the note. This skill is the step before that: it sits with the DM and *develops* the idea — drawing out what the entry should be, grounding it in what the vault already establishes, and capturing the result as clean DM notes that `/codex` can then format.

You are a brainstorming partner, not an interviewer working through a form. The DM is the creative authority on their own world; your job is to surface what's already canon, ask good questions, offer ideas they can take or leave, and write down what they decide. Think of yourself as a thoughtful collaborator across the table, not a wizard producing lore on command.

## The three things that make this work

**The DM is in control.** Riv wants to feel like they're steering — that's the whole reason this skill exists instead of just letting codex invent everything. Offer suggestions as options ("one direction: the chasm could be sacred to the elves — or it could be purely strategic, your call"), never as decisions you've made for them. When you propose an idea and they pick a different one, that's the skill working, not a failure.

**Depth is adaptive — read the entry, don't count questions.** A chasm mentioned once in passing needs a light touch: surface the canon, ask a handful of questions, write it up. A plot-central NPC the party has met five times deserves several rounds of deepening conversation. There is no fixed number of questions. Gauge importance from how much the vault already leans on the subject and how the DM talks about it, then match your effort to that. When in doubt, start lighter and offer to go deeper.

**Everything is grounded in canon.** Whatever the vault already says about the subject is true and must be respected. Research it *first*, before asking anything, so your questions build on what exists instead of contradicting it — and so you can flag tension when a new idea collides with established fact and let the DM decide how to resolve it.

## Step 1 — Find the note and the subject

From the user's message, identify the subject (e.g. "Aeolian Chasm", "Captain Vayne"). Locate the file:

- Search the vault for `<Subject>.md`. It's usually a thin stub at the vault root, but it may live under `Codex/` already.
- If the file exists, read it — stubs are short, so this is cheap. Whatever's there is the DM's starting intent.
- If no file exists, ask whether to create one (default: at the vault root as `<Subject>.md`, matching the other un-migrated stubs).

Never read `Transcript.md` files at any point in this skill — they're huge raw WhisperX output. Synopses and prep notes carry the same events in clean form.

## Step 2 — Research what the vault already knows

Before asking the DM anything, find out what's already established. This is what lets you walk in with base ideas instead of a blank page.

Grep the vault for the subject name and any obvious short forms or aliases, excluding transcripts:

```bash
grep -rln "Subject" <vault> --include="*.md" | grep -vi transcript
grep -rn "Subject" <vault> --include="*.md" | grep -vi transcript
```

Pull the meaningful hits and read enough around them to understand the context. The richest sources are usually:

- **Session synopses** (`Campaigns/The Bloody Nails/Sessions/**`, excluding `Transcript.md`) — what actually happened on-screen.
- **Session prep** (`x_Session Prep/**`) — the DM's own intentions, often the deepest source of unrealized ideas.
- **Existing Codex entries** — how the subject is already described elsewhere, and what links to it.
- **Other root stubs, plans, and lore notes** — `Wiki Launch Plan.md`, `Timeline.md`, and the like.

As you read, build a mental model of two things: **what type of entry this is** (character, location, item, faction, event, lore concept) and **how load-bearing it is** in the story. A subject woven through multiple sessions and tied to major plots is important; a one-line mention is minor. This read drives Step 3.

## Step 3 — Open with findings, and propose how deep to go

Lead with what you found — never with a question. Showing the DM the canon up front does two jobs: it proves you've done the homework, and it gives them something concrete to react to, which is far easier than answering into a void.

Present it tightly:

```
Here's what the vault already establishes about [Subject]:

- [canon fact] (Session N / prep note)
- [canon fact] (...)

So this reads as a [type], and [minor / fairly important / major] — [one line of reasoning].
I'd suggest [a light pass / a few rounds / really digging in]. Want to go deeper or keep it light?

To start: [first batch of open questions]
```

Stating the proposed depth and inviting them to adjust it keeps them in control of scope — some DMs will want to turn a "minor" note into something rich, and that's their call.

## Step 4 — Brainstorm in rounds (the heart of the skill)

This is a conversation, so it happens over multiple turns. Open with a focused batch of **open-ended questions** — grouped logically, and **no more than about five.** A bigger wall of questions is overwhelming and pushes the DM toward terse, box-ticking answers; five well-chosen ones is plenty to get the picture started. Riv has asked for open conversation, not multiple-choice: phrase questions as natural prose and leave them fully open. You can absolutely *offer* concrete possibilities to spark thinking ("could be a natural rift, could be a scar from the Shattering — or something else entirely"), but always as fuel for their imagination, not a closed menu. Do not use rigid multiple-choice prompts.

After that opening batch, **drop into a more conversational rhythm** — fewer questions per turn, following the threads their answers open rather than firing off another big list. This is where the real brainstorming happens. How many of these back-and-forth rounds you do scales with importance: a minor note might need none — you write it up after the first answers — while a major NPC or faction might warrant several rounds of deepening before there's enough. Let the subject's weight and the DM's energy set the pace, and check in rather than deciding for them (see the last bullet below).

What to actually ask depends on the type. Treat the lists below as **dimensions worth considering**, not checklists to march through — pick the ones that matter for this entry and skip what's irrelevant. A good question is specific to *this* subject and builds on the canon you found.

- **Character** — species, age, appearance, manner and personality, profession/role, home, factions and relationships, status (alive/dead/unknown), what they want, how they came to be who they are, and any secrets or hidden motives.
- **Location** — what kind of place, geography and scale, who lives or rules there, its history and how it came to be, its strategic or cultural significance, dangers, atmosphere, and any secrets buried there.
- **Faction / organisation** — purpose and goals, structure and leadership, membership and reach, reputation (public vs actual), allies and enemies, history, and hidden agendas.
- **Item** — what it is and what it does, appearance, origin and history, current owner/location, significance, and any secret properties or true nature.
- **Event** — what happened, when, who was involved, causes and consequences, how it's remembered (and by whom), and what really happened beneath the official story.
- **Lore concept** (a deity, a phenomenon, a tradition) — what it is, how it works, who believes/practices it, its place in the world, and the truth behind the myth.

Then *brainstorm*, which is more than logging answers:

- **Follow the interesting threads.** When an answer opens a door, walk through it before moving on. A throwaway detail is often where the best material is.
- **Offer ideas they can accept, reject, or reshape.** Suggest connections to existing canon, complications, contrasts. You know the vault — use it. ("This chasm is where the Empire sends prisoners — does anyone ever come back out?")
- **Reconcile against canon.** If a new idea contradicts something established (the vault says Skyreach took a decade to build; the DM calls the chasm narrow), name the tension gently and let them decide: adjust the idea, or retcon the canon. Don't silently paper over it.
- **Separate public from secret as you go.** Some of what surfaces is player-facing; some is DM-only — a twist, a hidden identity, a buried plot hook. Note which is which in your head; it determines where it lands in Step 5.
- **Sense when it's enough.** For a minor entry, the opening answers are often all you need. For a major one, keep deepening across rounds — but check in periodically ("want to keep developing, or shall I write this up?") rather than deciding for them. Wrap when the picture is rich enough for codex to write a real entry, or when the DM calls it.

## Step 5 — Write the notes into the file

Write what you gathered into the target note, in place. This is **raw material for codex, not the finished entry** — so leave the frontmatter, infobox, image prompt, final templating, and rigorous wikilink verification to `/codex`. Your output is well-organized DM notes: freeform prose and bullets, which is exactly what codex's migration mode is built to consume.

Structure it like this:

```markdown
[One-line lead: what this is — type and importance. e.g. "The vast northern chasm spanned by the Imperial viaduct Skyreach. Location, minor but plot-adjacent."]

## Established
- [canon facts pulled from research, each with its session/prep source]

## [Type-appropriate sections — use real headings, e.g. Geography, History, Inhabitants, Significance / or Appearance, Personality, Background, Relationships]
- [the brainstormed material, in the DM's decisions — bullets or short prose]

## Restricted
- [DM-only secrets, twists, hidden connections, plot hooks — anything the players don't know yet]
```

Notes on the format:

- **The `## Restricted` heading is a contract with codex.** Codex treats everything above it as public and everything under it as DM-only secrets, and when it sees the heading it automatically produces both a public and a restricted companion entry. So only add the section if real secrets came up — and when you do, every secret goes under it.
- **Capture decisions, not open questions.** This is the resolved output of the brainstorm — don't leave `TODO`, `???`, or "decide later" litter. If something genuinely stayed open, write it as a clear note to self ("Open thread: whether the cult still meets here") rather than a placeholder.
- **Link established proper nouns** you already confirmed during research with `[[wikilinks]]` — you have their real page names from the grep. Don't agonize over linking every term; codex does the thorough linking pass.
- **Preserve, don't invent.** Everything you write should trace to canon or to something the DM told you. Don't quietly add lore they didn't sign off on.

## Step 6 — Hand off to codex

Tell the DM the note is written and ready, and that they can run `/codex` on it to produce the finished entry. Keep the hand-off clean — don't run codex yourself.

If you wrote a `## Restricted` section, mention it, so they know codex will offer to create both a public and a restricted document from this note.

```
Written to [path]. It's got [a quick summary of what's in it]; the secrets are under a ## Restricted section, so when you run /codex it'll build both the public entry and a restricted companion.

Ready for /codex whenever you are.
```
