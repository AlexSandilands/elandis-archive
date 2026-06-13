# 🏰 Elandis Wiki Launch Plan

**Goal:** Migrate and populate every remaining root-level note into the Codex so the player-facing wiki is ready.

**Target launch:** **Sunday 21 June 2026, 10:00 pm** (full quality on every entry; the POI long tail is the slip absorber).

> Revised 10 Jun 2026. The original 6 Jun target passed with the bulk of the work done — all 84 characters, the major cities, core factions, the pantheon, and a large batch of *new* pages not on the first list are already migrated. What remains is almost entirely empty 0-line stubs, which the `/codex` skill authors quickly from synopsis research.

---

## ⚙️ Working assumptions

- **~2h** on weekday evenings after work.
- **No work** Monday or Wednesday evenings.
- **~4h** on weekend days (Sat/Sun).
- **Quality bar:** full publication-quality on *every* entry — no light stubs.
- Each file is done **with the `/codex` skill** (it researches synopses, gathers your notes, generates the entry, then you confirm stub deletion).
- **Available before the 21 Jun 10pm deadline:** ~26 hours across 9 sessions (Thu 11 → Sun 21).

---

## 📊 Scope at a glance

~**104 entries** to author, almost all empty stubs. Plus a short housekeeping pass (6 stale deletes, 4 duplicate merges).

| Batch | Category | Count |
|---|---|---|
| 0 | Housekeeping (deletes + dup merges) | — |
| 1 | Continents | 3 |
| 2 | Pantheon / Deities | 7 |
| 3 | Characters | 11 |
| 4 | Factions | 8 |
| 5 | Cities & Towns | 14 |
| 6 | Regions & Wilds | 15 |
| 7 | Items | 8 |
| 8 | Institutions & Lore misc | 6 |
| 9 | POI — Taverns, Shops & Temples | 15 |
| 10 | POI — Landmarks & Structures | 17 |

---

## 🧹 Batch 0 — Housekeeping (do first, ~20 min)

**Stale leftovers — already migrated, root copy never deleted.** Glance at the Codex version, confirm it's the good one, then delete the root stub:
- [x] `Darmouth` → `Codex/Locations/Cities/Darmouth.md` *(root still has the old 152-line draft)*
- [x] `Point Blackrock` → `Codex/Locations/Cities/Point Blackrock.md` *(old 154-line draft)*
- [x] `Renite Steel` → `Codex/Items/Renite Steel.md`
- [x] `Shield Wall` → `Codex/Locations/Points of Interest/Shield Wall.md`
- [x] `Stonesworn` → `Codex/Factions/Stonesworn.md`
- [x] `Isle of Erivin` → `Codex/Locations/Regions/Erivan Island.md` *(renamed — delete the old stub)*

**Duplicate pairs — pick the canonical, fold in any content, delete the other:**
- [x] `Darkwood` ↔ `The Darkwood` → canonical region page
- [x] `Pool of Reflection` ↔ `The Pool of Reflection` → one POI
- [x] `Theater of Dreams` ↔ `The Theatre of Dreams` → one POI
- [x] `Raven's Nest` ↔ `The Raven's Nest of Val Miriel` → one POI (Order of Ravens HQ)

> ⚠️ Two items marked done in the old plan were **never actually migrated** — `River's Watch` and `World Gates` are back in the lists below.

---

## 🔁 Per-file workflow (reuse every time)

For each file in a session:
- [ ] Run `/codex` → migrate `<Name>`
- [ ] Review the research it surfaces; add your DM notes
- [ ] Check all wikilinks resolve to real page names (no ghost pages)
- [ ] If the stub had restricted content, confirm the companion doc in `Codex-Restricted/`
- [ ] Confirm deletion of the root stub once the Codex entry is written

---

## 🔒 Restricted content & the git subtree

**Decision:** keep the two-file split (`Codex/X.md` public + `Codex-Restricted/.../X - Restricted.md` private). With players contributing via a git subtree they clone the *actual files and history* — anything inline (stripped-at-publish DM sections, `%%secret%%` blocks) would land in the public repo's history and could never be redacted without rewriting it under contributors. File-level separation is the only safe boundary.

### Target structure

```
Elandis/                      ← private vault repo (the whole Obsidian vault)
├── Wiki/                     ← subtree root → public repo
│   ├── Codex/
│   └── Campaigns/
├── Codex-Restricted/         ← never leaves the private repo
├── x_Session Prep/
└── x_DM Toolkit/ ...
```

### The linking rule: restricted → public only

Public pages must **never** link into `Codex-Restricted/`. A dead `[[X - Restricted]]` link on the wiki advertises that a secret exists — the link text itself is the spoiler.

- Public pages link the plain name (`[[Elaris Moonsong]]`, `[[Vallarra Miriel]]`). If no public page exists yet, an unresolved link just reads as "page not written yet" — normal wiki behaviour.
- Restricted notes link freely to public pages.
- Nothing is lost in Obsidian: the backlinks panel on any public page surfaces its `- Restricted` companion, and the quick switcher finds it by name.
- Promotion stays clean: when a secret becomes table knowledge, fold content from `X - Restricted.md` into `X.md` (or `git mv` a restricted-only page into the Codex) — existing links already point at the right name.

**Known violations to fix before the subtree goes live** (public files currently linking `- Restricted` pages):
- [ ] `Codex/Characters/Vallania Miriel.md` *(frontmatter + connections table + biography)*
- [ ] `Codex/Characters/High Priest Oldir.md`
- [ ] `Campaigns/The Bloody Nails/Characters/Berberis.md`
- [ ] `Session 04 - To Free a Raven`
- [ ] `Session 20 - The Streets of Val Miriel`
- [ ] `Session 26 - A Midnight Romp`
- [ ] `Session 27 - The Wanted Dwarf`

### Naming convention inside `Codex-Restricted/`

Two kinds of file live there — keep the distinction deliberate:
- `X - Restricted.md` → a **permanent DM shadow page**; a public `Codex/X.md` with the same base name exists. The suffix avoids Obsidian name collisions and keeps `[[X]]` resolving to the public page.
- `X.md` (canonical name, e.g. `Forna.md`, `Hrothgar.md`) → a **not-yet-published entry**; no public counterpart. Promotion = `git mv` into `Codex/`.

So the suffix always means "a public page with this name exists."

### Migration notes (the `Wiki/` folder move)

- Wikilinks survive untouched — Obsidian resolves them vault-wide.
- ~176 files use path-style markdown links (`](Codex/Assets/...)` cover images). Do the move **inside Obsidian** with "automatically update internal links" on, then grep-sweep for any stragglers (`](Codex/` → `](Wiki/Codex/`).
- Check `publish.js` / `publish.css` for hardcoded `Codex/` paths.

### Leak guard (make the convention enforceable)

Add a pre-push hook or CI check on the public repo that **fails** if anything under `Wiki/` matches:
- `- Restricted]]`
- `Codex-Restricted/`
- `## DM Notes`

This turns "I try to remember" into "it can't leak."

---

# 📅 The Schedule

## Thu 11 Jun (2h) · HOUSEKEEPING + CONTINENTS + PANTHEON
*Clear the deck, then knock out the high-value top-level pages.*

- [x] Batch 0 housekeeping (deletes + dup merges)

**Batch 1 — Continents (3)** *(major top-level pages; the names are deceptive — these are landmasses)*
- [x] Aetheris *(central continent, site of The Shattering)*
- [x] Seraphon *(smaller northern continent, oldest cultures)*
- [x] Eldara *(largest continent, mercantile heart of the world)*

**Batch 2 — Pantheon / Deities (7)**
- [x] Mystra
- [x] Lathander
- [x] Tiamat
- [x] Grumbar *(elemental — earth)*
- [x] Istishia *(elemental — water)*
- [x] Kossuth *(elemental — fire)*
- [x] Forna *(triage — likely a deity; confirm at migration)*

---

## Fri 12 Jun (2h) · CHARACTERS

**Batch 3 — Characters (11)**
- [x] Ebon *(the Grand Raven — Order of Ravens)*
- [x] Elder Silaqui Amastacia
- [x] Justiciar Naivara Siannodel
- [x] Korvin Blackfeather
- [x] Master Artisan Fenian
- [x] Freya Ironsong
- [x] Thora Ironsong
- [x] Thorgar Ummal
- [x] Hilda Ummal
- [x] Hrothgar
- [x] Hvedra

---

## Sat 13 Jun (4h) · FACTIONS + CITIES & TOWNS

**Batch 4 — Factions (8)**
- [x] Cindercloaks
- [x] Circle of the Root
- [x] Circle of the Scales
- [x] Circle of the Scroll
- [x] Court of Fallen Leaves
- [x] Darkwood Vanguard
- [x] Emberlight Vigil
- [x] Skyguard

**Batch 5 — Cities & Towns (14)** *(the Luminor Plains farming towns make a natural sub-batch)*
- [ ] Shardcrest *(Imperial coastal city)*
- [ ] Nyrieth *(western port city)*
- [ ] Everfall *(cold northern city)*
- [ ] Silverforge
- [ ] Brightwater
- [ ] Valewatch *(watch-town)*
- [ ] Sabine *(Gulf of Miriel town)*
- [ ] River's Watch
- [ ] Isle of Solenne
- [ ] Redhaven *(Luminor Plains)*
- [ ] Nightstone *(Luminor Plains)*
- [ ] Hillcrest *(Luminor Plains)*
- [ ] Goldcrest *(Luminor Plains)*
- [ ] Ravencrest *(Luminor Plains)*

---

## Sun 14 Jun (4h) · REGIONS + ITEMS

**Batch 6 — Regions & Wilds (15)**

Forests & wilds:
- [ ] Whispering Woods
- [ ] Darkwood *(canonical after Batch 0 merge)*
- [ ] Gossamer Woods *(Faewild)*
- [ ] Reveller's Glade *(Faewild)*
- [ ] Shimmering Peaks *(Faewild)*

Geographic features:
- [ ] Vale of Eternal Night
- [ ] Frostway
- [ ] Liar's River
- [ ] Luminor River
- [ ] Luminor Plains
- [ ] Borealia Range *(mountains)*
- [ ] Silver Mountains
- [ ] Southern Highlands
- [ ] Xericana Sands *(desert)*
- [ ] The Underrun *(triage — region vs POI)*

**Batch 7 — Items (8)**
- [ ] Emberblade *(weapon)*
- [ ] Dread's Hunger *(weapon)*
- [ ] Riftshard
- [ ] Moonlit Aegis *(shield — `git add` if untracked)*
- [ ] The Kraken *(ship)*
- [ ] Gossamer Dust *(material)*
- [ ] Moonstone *(material)*
- [ ] Zephyr Cuffs

---

## Tue 16 Jun (2h) · INSTITUTIONS + LORE + TAVERNS (start)

**Batch 8 — Institutions & Lore misc (6)**
- [ ] Arcana Luminorium *(arcane academy, Val Luminor)*
- [ ] Imperial Academy
- [ ] Eternal Forge
- [ ] Red Bastion *(fortress in Val Miriel)*
- [ ] World Gates *(lore concept)*
- [ ] Fungrals *(triage — people/culture; appears in Bioluminescent Forest & Sumara)*

**Batch 9a — Taverns & shops (start, ~4)**
- [ ] Rusty Nail
- [ ] The Gilded Crow
- [ ] The Fur and Fang
- [ ] The Red Leaf

---

## Thu 18 Jun (2h) · TAVERNS (finish) + TEMPLES & WAYS

**Batch 9b — Taverns & shops (finish)**
- [ ] The Lion *(inn)*
- [ ] Drunken Quay
- [ ] Gilded Grimoire *(magic shop — not an item)*
- [ ] Val Miriel River Market

**Batch 9c — Temples & Sumara Ways (7)**
- [ ] The Stoneheart *(large temple — 148 lines of existing content, allow extra time)*
- [ ] St. Avelines
- [ ] High Sept
- [ ] The Royal Way
- [ ] The Military Way
- [ ] The Artisan Way
- [ ] The Divine Way

---

## Fri 19 Jun (2h) · POI LANDMARKS I  *(slip absorber begins here)*

**Batch 10a — Landmarks & structures (9)**
- [ ] Royal Citadel of Sumara
- [ ] The Bastion
- [ ] The Miriel Bastion
- [ ] Valena's Bridge
- [ ] The Bridge of Stars
- [ ] The Portal
- [ ] Theatre of Dreams *(canonical after Batch 0 merge)*
- [ ] Serenity Plaza
- [x] The Emberspire

---

## Sat 20 Jun (4h) · POI LANDMARKS II + POLISH

**Batch 10b — Landmarks & structures (8)**
- [ ] The Ashen Forge
- [ ] The Coal
- [ ] Vault of Memories
- [ ] Pool of Reflection *(canonical after Batch 0 merge)*
- [ ] Val Miriel - Governor's Keep
- [ ] Goblin Lair
- [ ] Ruby Falls Goldmine

Then, with remaining time:
- [ ] Image-prompt pass on any entry still missing art
- [ ] City / town maps (run `/city-map` where a sketch exists)
- [ ] Catch up on any batch that slipped

---

## Sun 21 Jun (4h, deadline 10pm) · 🚀 LAUNCH PASS

Run the Pre-launch QA below, then publish.

---

## 🚀 Pre-launch QA checklist

- [ ] **No files left at vault root** except `CLAUDE.md`, `README.md`, `Scratch Notes.md`, and this plan.
- [ ] Add location images taken from the parchment map to each location where relevant.
- [ ] City / town maps.
- [ ] Add landing page.
- [ ] Setup git subtree for codex *(structure + rules: see "Restricted content & the git subtree" above)*.
	- [ ] Move `Codex/` + `Campaigns/` under `Wiki/` (inside Obsidian), sweep `](Codex/` path links
	- [ ] readme
	- [ ] ensure anything that shouldn't be here is moved to restricted
	- [ ] Fix the public → restricted link violations (list in the subtree section)
	- [ ] Add the leak-guard check (pre-push hook or CI)
	- [ ] Review the Campaign Folder - Ensure no spoilers in player characters
- [ ] Review DMG Cities Properties
- [ ] **Broken-link sweep** — no ghost/unresolved `[[wikilinks]]`.
- [ ] **Orphan check** — every Codex page is reachable from a landing/index page.
- [ ] **Category landing pages** exist (Characters, Locations, Factions, Items, Lore, Continents) and link their children.
- [ ] **Images** — each entry has its image prompt; generated art lives in `Codex/Assets/...`.
- [ ] **Restricted content** is in `Codex-Restricted/`, never leaked into a public page.
- [ ] **Spot-check 5 random pages** against the gold-standard formatting.
- [ ] **Publish/sync to the web wiki** (confirm the publish pipeline) and view as a player.
- [ ] `git add` + commit the migrated Codex.

---

## 🎯 If you fall behind

Full quality on everything is the bar, so the slip absorber is **Batch 10 — POI Landmarks (Fri 19 / Sat 20)**: the least-trafficked pages. If a weekday session runs short, push that day's stubs into the next 4h weekend block; never sacrifice the continents, pantheon, factions, or cities — those are the high-value spine of the wiki and hold their slots.

The pacing (~4 entries/hr) matches what the earlier migration days actually hit, so the plan fits the 26 hours with thin slack — but it *is* thin. If you gain a Mon/Wed evening, spend it on Batch 10.
