---
tags:
  - meta
  - campaign
---

# Renaming Plan — Pick Up In Another Session

## Goal

Restructure every session folder under `Campaigns/The Bloody Nails/Sessions/` to the **Option C (folder-note) convention**: folder and inner synopsis file share the same name.

**Before:**
```
Sessions/Session 01/
  ├─ Art/
  ├─ Synopsis.md
  └─ Transcript.md
```

**After:**
```
Sessions/Session 01 - The Rusty Nail/
  ├─ Art/
  ├─ Session 01 - The Rusty Nail.md      ← renamed from Synopsis.md
  └─ Transcript.md
```

## Why

1. **Unique filenames across the vault** — currently all 48 synopsis files are called `Synopsis.md`, which collapses the quick switcher, graph view, and backlinks into a mess of duplicates.
2. **Folder-note convention** — folder and main doc share a name. Plays well with the [Folder Notes](https://github.com/LostPaul/obsidian-folder-notes) plugin (click folder → opens the note). Even without the plugin, it reads cleanly in the file tree.
3. **Session # + title both visible at a glance** — satisfies the "wiki navigability" requirement.
4. **Transcripts and Art stay siblings** — session folder remains the container for all session-related files.

## What to do

For each row in the table below:

1. Rename the folder: `Sessions/Session NN/` → `Sessions/Session NN - <Chosen Title>/`
2. Rename the inner file: `Synopsis.md` → `Session NN - <Chosen Title>.md` (same name as the folder)
3. Leave `Art/` and `Transcript.md` untouched inside.

Session `10.5` uses `10.5` literally (e.g. `Session 10.5 - Diverging Paths/`).

## ⚠️ Wikilink migration (DO NOT SKIP)

A vault-wide scan found **109 `[[...Synopsis]]` wikilinks across 71 files** that currently point at the old paths. After renaming, all of these will break unless updated.

Breakdown of link shapes to handle:
- **Full-path links** like `[[Campaigns/The Bloody Nails/Sessions/Session 01/Synopsis]]` — need both the folder segment AND the final segment updated.
- **Bare `[[Synopsis]]` links** — currently ambiguous; rely on Obsidian's context resolution. Need to be rewritten to the new unique filename, e.g. `[[Session 01 - The Rusty Nail]]`.
- **Aliased links** like `[[...Synopsis|Session 1]]` — preserve the alias, update the target.

Files with the heaviest link count (check these first): `Codex/Characters/Gemma Finegold.md` (13), `Codex/Characters/Barak Stormrider.md` (12), `Codex/Characters/King Marius Noren.md` (6), `Codex/Characters/Ayana Syndrosa.md` (5).

Also present across: the ~48 session prep notes under `x_Session Prep/Campaigns/The Bloody Nails/`, ~15 character notes at vault root and in `Codex/Characters/`, `Campaigns/The Bloody Nails/The Bloody Nails.md`, the skill files under `.claude/skills/`, and a few templates/toolkit docs.

**Recommended approach:** Ask Claude to enable Obsidian's "Use [[Wikilinks]]" + "Automatically update internal links" setting before doing the renames through Obsidian itself — Obsidian will fix most links for free. Alternatively, scripted `mv` + regex replace across the vault, then manually verify the heavy-link files listed above.

## Safety checklist before starting

- [ ] **Commit or back up the vault first.** (Git state was not confirmed in the previous session — verify `git status` in the vault root, or make a manual copy.)
- [ ] **Close Obsidian** during scripted renames, or perform the renames *through* Obsidian one at a time to let it auto-fix links.
- [ ] **Delete or archive the `.bak` file** `Codex/Characters/Ayana Syndrosa.md.bak` — contains stale `Synopsis` links that won't be useful after the rename.
- [ ] **Keep the `Session Title Proposals.md` sibling file** for historical reference, or delete it once this is done — it's superseded by this document.

## Verification after renaming

- [ ] All 48 session folders match pattern `Session NN - <Title>/` (or `Session 10.5 - ...`).
- [ ] Each folder contains exactly one `.md` file whose name matches the folder.
- [ ] `Art/` and `Transcript.md` still present and untouched.
- [ ] Grep the vault for `[[.*Synopsis` — should return zero matches (apart from this document and the proposals sibling).
- [ ] Open 3–4 character notes from the heavy-link list above and spot-check that backlinks resolve.

---

# Chosen Titles

| #    | Chosen                      |
| ---- | --------------------------- |
| 01   | The Rusty Nail              |
| 02   | Midnight Fangs              |
| 03   | The Streets of Darmouth     |
| 04   | To Free a Raven             |
| 05   | The Baited Ambush           |
| 06   | The Goblin Lair             |
| 07   | Grakthor Falls              |
| 08   | The High Road               |
| 09   | The Veiled Den              |
| 10   | The Coastal Cave            |
| 10.5 | Diverging Paths             |
| 11   | The Tale of Salla the Brave |
| 12   | How to Start a Rebellion    |
| 13   | Waves, Wings and Sails      |
| 14   | The Devil's Wish            |
| 15   | Operation Skyreach          |
| 16   | The Fall of Skyreach        |
| 17   | A New Journey Begins        |
| 18   | The Old Forest              |
| 19   | Blood and Sorrow            |
| 20   | The Streets of Val Miriel   |
| 21   | The Governor's Daughter     |
| 22   | Inferno at Serenity Plaza   |
| 23   | Ruby Falls Goldmine         |
| 24   | Nelfandris The Banished     |
| 25   | The Chimera                 |
| 26   | A Midnight Romp             |
| 27   | The Wanted Dwarf            |
| 28   | The Underrun                |
| 29   | Lighthaven Awaits           |
| 30   | The Darkwood Ambush         |
| 31   | The Emberlight Vigil        |
| 32   | The Road to Point Blackrock |
| 33   | A Camp Alight               |
| 34   | Mourning Bells              |
| 35   | The Frostway                |
| 36   | General Korvas              |
| 37   | March of the Dead           |
| 38   | A Trail of Blood            |
| 39   | The Stoneheart              |
| 40   | General Blackmarsh          |
| 41   | Reclaim the Reclaimer       |
| 42   | Liberation of Val Noren     |
| 43   | The Shield of the North     |
| 44   | The Elven Archmage          |
| 45   | Pieces on a Board           |
| 46   | The Shining City            |
| 47   | Confluence of the Seven     |
| 48   | The Vault of Memories       |
