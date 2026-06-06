# 🏰 Elandis Wiki Launch Plan

**Goal:** Migrate and populate every root-level note into the Codex, and build a Codex skill reference for each entry type, so the player-facing wiki is ready.

**Target launch:** **Saturday 6 June 2026** (core complete and live; a thin tail of minor Points of Interest may finish 7–9 June).

---

## ⚙️ Working assumptions

- **~2h** on weekday evenings after work.
- **No work** Monday or Wednesday evenings.
- **~4h** on weekend days (Sat/Sun).
- **Quality bar:** full publication-quality on *every* entry — no light stubs. Deadline may slip slightly past 6 June for the long tail; that's accepted.
- Each file is done **with the `/codex` skill** (it researches synopses, gathers your notes, generates the entry, then you confirm stub deletion).
- **Total available before 6 June:** ~28 hours across 10 sessions.

---

## 📊 Scope at a glance

The 84 characters are already migrated and their stubs cleaned up. Remaining root content ≈ **126 files**:

| Category | Count | Notes |
|---|---|---|
| Skill references to write | 5 | locations, factions, items, lore, continents |
| Continents / World | 4 | Elandis, Valtorra, Faelon, Faewild |
| Stray characters | 2 | Valen Leafwhisper; Joffee (triage) |
| Cities | ~22 | 10 have content (reformat), ~12 empty (author) |
| Factions | ~17 | after de-duplication |
| Lore | ~17 | deities, events, cosmology, culture |
| Items | ~11 | weapons, artifacts, ships, materials |
| Regions | ~19 | forests, waters, geographic features |
| Points of Interest | ~30 | taverns, temples, districts, landmarks |

**Duplicates to merge (pick one canonical, fold in the other's content, delete the extra):**
- `Circle of Blades` ↔ `Circle of the Blade`
- `Pool of Reflection` ↔ `The Pool of Reflection`
- `Raven's Nest` ↔ `The Raven's Nest of Val Miriel`

**Watch for restricted content** during migration (a `## Restricted` section or `RESTRICTED CODEX ONLY` line in the stub → create a companion doc in `Codex - Restricted/`). Known so far: **Arkangel**.

> Category assignments below are a strong starting point, not gospel. Confirm the right Codex folder at migration time — a few files (Joffee, Tumbler's Crag, The Underrun, Locus Arcanum, The Maw) are genuinely ambiguous and tagged **triage**.

---

## 🔁 Per-file workflow (reuse every time)

For each file in a session:
- [ ] Run `/codex` → migrate `<Name>`
- [ ] Review the research it surfaces; add your DM notes
- [ ] Check all wikilinks resolve to real page names (no ghost pages)
- [ ] If the stub had restricted content, confirm the companion doc
- [ ] Confirm deletion of the root stub once the Codex entry is written

---

# 📅 The Schedule

## ✅ Day 1 — Sun 24 May (4h) · FOUNDATION
*Unblocks every later evening. Build the tooling first, then a few quick wins.*

- [x] **Write the 5 skill references** (mirror `.claude/skills/codex/references/character.md`):
  - [x] `references/locations.md` (cities, regions, points of interest — one ref, sub-types inside)
  - [x] `references/factions.md`
  - [x] `references/items.md`
  - [x] `references/lore.md` (deities, events, cosmology, culture)
  - [x] `references/continents.md`
- [x] **Update `codex/SKILL.md`** routing table + description so it dispatches to all categories (currently characters-only).
- [x] **Resolve the 3 duplicate pairs** (merge + delete extras).
- [ ] **Continents / World (4):**
  - [ ] Elandis *(world overview / top-level landing page)*
  - [ ] Valtorra
  - [ ] Faelon
  - [ ] Faewild
- [ ] **Stray characters (2):**
  - [ ] Valen Leafwhisper *(scout — use existing character ref)*
  - [ ] Joffee *(triage: confirm character vs location first)*

---

## ✅ Day 2 — Tue 26 May (2h) · MAJOR CITIES I
*Heavy reformats of your richest existing pages.*

- [x] Sumara, The Shining City
- [x] Val Miriel
- [x] Lighthaven

---

## ✅ Day 3 — Thu 28 May (2h) · MAJOR CITIES II

- [ ] Val Noren
- [ ] Point Blackrock
- [ ] Darmouth

---

## ✅ Day 4 — Fri 29 May (2h) · CITIES III + RESTRICTED

- [ ] Camaar
- [ ] Farhaven
- [ ] Ithilmara *(elven capital — short but has content)*
- [x] Arkangel *(flying city — has `RESTRICTED CODEX ONLY` content → create companion doc)*

---

## ✅ Day 5 — Sat 30 May (4h) · CITY STUBS (author from research)
*All empty — research synopses, generate, fill gaps with your notes.*

- [ ] Caer Nystral
- [ ] Glimmerforge
- [ ] Silverdeep
- [ ] Silverforge
- [ ] Skyreach
- [ ] Val Aerie
- [ ] Val Aran
- [ ] Val Luminor
- [ ] Val Solis
- [ ] Valfyria
- [ ] Miriel's Rest
- [ ] River's Watch
- [ ] Tumbler's Crag *(triage: city vs point of interest)*

---

## ✅ Day 6 — Sun 31 May (4h) · FACTIONS
*Mostly content-rich → reformat to the new faction template. The big two (Mawbreakers, Frostwarden Crews) eat the most time.*

Reformat (have content):
- [ ] The Mawbreakers
- [ ] The Frostwarden Crews
- [ ] The Frostwardens
- [ ] The Finegolds
- [ ] Veiled Cubs
- [ ] The Red Priests
- [ ] Silmara Family
- [ ] Circle of the Weave
- [ ] Circle of Blades *(canonical after Day 1 merge)*
- [ ] Valtorran Empire *(nation/faction)*
- [ ] [[Order of Ravens]]
- [ ] The Green Gryphons
- [ ] The Emberlight Vigil
- [ ] Hand of The Empire
- [ ] Eye of the Empire *(imperial spy network)*

Author (empty):
- [ ] Circle of the Dawn
- [ ] Shadow Serpents
- [ ] Vanguard Wardens

---

## ✅ Day 7 — Tue 2 Jun (2h) · LORE I — Pantheon & History

- [ ] Selûne *(deity)*
- [ ] Shar *(deity)*
- [ ] The Green Lady *(deity)*
- [ ] Torgar Earthshaker *(god of earth & stone)*
- [ ] Eldrin Starweaver *(god — note: not a character)*
- [ ] The Shattering *(world event)*
- [ ] Chaos Wars *(historical era)*
- [ ] Timeline *(world history overview)*

---

## ✅ Day 8 — Thu 4 Jun (2h) · LORE II — World, Cosmology & Culture

- [ ] The Confluence of the Seven
- [ ] The Winter Solstice *(holiday/event)*
- [ ] The Emerald Ceremony *(event)*
- [ ] Dwarven *(race/culture)*
- [ ] The Valtorran Elves *(race/culture)*
- [ ] Heartstone *(petrified World Tree root — landmark relic)*
- [ ] World Tree
- [ ] World Gates
- [ ] Locus Arcanum *(triage: lore concept vs site)*

---

## ✅ Day 9 — Fri 5 Jun (2h) · ITEMS

- [ ] Emberblade *(weapon)*
- [ ] Riftshard
- [ ] Dread's Hunger *(weapon)*
- [ ] Amulet of the Arachnid Queen
- [ ] Moonlit Aegis *(shield — currently untracked, `git add` it)*
- [ ] Belinda's Chest
- [ ] The Albatross *(Mawbreakers' flagship)*
- [ ] The Kraken *(ship/crew)*
- [ ] Gossamer Dust *(material)*
- [ ] Moonstone *(material)*
- [ ] Renite Steel *(material)*

---

## ✅ Day 10 — Sat 6 Jun (4h) · REGIONS + 🚀 LAUNCH PASS
*All empty/short — fast batch. Then run the pre-launch QA below and publish.*

Forests & wilds:
- [ ] Ancient Woods
- [ ] Whispering Woods
- [ ] Borealia Forest
- [ ] Farhaven Forest
- [ ] Bioluminescent Forest
- [ ] The Darkwood
- [ ] Gossamer Woods *(Faewild)*
- [ ] Briarshade *(Faewild)*
- [ ] Reveller's Glade *(Faewild)*
- [ ] Shimmering Peaks *(Faewild)*

Geographic features:
- [ ] Aeolian Chasm
- [ ] Vale of Eternal Night
- [ ] Isle of Erivin
- [ ] Frostway
- [ ] Gulf of Miriel
- [ ] Liar's River
- [ ] Luminor River
- [ ] The Maw *(whirlpool — triage: region vs landmark)*
- [ ] The Underrun *(triage: region vs point of interest)*

Then → **Pre-launch QA** (see checklist below) → **publish**.

---

## ⏭️ Overflow — Points of Interest (likely 7–9 Jun)
*~30 files, mostly empty. These are the long tail and the most likely to slip past launch. The taverns/temples your players actually frequent should jump the queue if time is tight.*

### Sun 7 Jun (4h) — POIs batch 1

Taverns, inns & shops:
- [ ] Rusty Nail
- [ ] The Gilded Crow
- [ ] The Fur and Fang
- [ ] The Red Leaf
- [ ] The Lion *(Inn)*
- [ ] Drunken Quay
- [ ] Gilded Grimoire *(magic shop — note: not an item)*
- [ ] Val Miriel River Market

Temples & religious sites:
- [ ] The Stoneheart *(large temple — 148 lines, allow extra time)*
- [ ] St. Avelines
- [ ] The High Sept

Sumara districts ("Ways"):
- [ ] The Royal Way
- [ ] The Military Way
- [ ] The Artisan Way
- [ ] The Divine Way

### Tue 9 Jun (2h) — POIs batch 2 + final review

Landmarks & structures:
- [ ] Royal Citadel of Sumara
- [ ] The Bastion
- [ ] The Miriel Bastion
- [ ] Valena's Bridge
- [ ] The Bridge of Stars
- [ ] The Portal
- [ ] The Theatre of Dreams
- [ ] Serenity Plaza
- [ ] The Emberspire
- [ ] The Ashen Forge
- [ ] The Coal
- [ ] Vault of Memories
- [ ] Pool of Reflection *(canonical after Day 1 merge)*
- [ ] The Raven's Nest of Val Miriel *(canonical after Day 1 merge — Order of Ravens HQ)*
- [ ] The Veiled Den
- [ ] Blackrock Shelters
- [ ] Goblin Lair
- [ ] Ruby Falls Goldmine

---

## 🚀 Pre-launch QA checklist
*Run on Day 10 (and again after the overflow days).*

- [ ] **No files left at vault root** except `CLAUDE.md`, `README.md`, `Scratch Notes.md`, and this plan.
- [ ] **Broken-link sweep** — no ghost/unresolved `[[wikilinks]]`.
- [ ] **Orphan check** — every Codex page is reachable from a landing/index page.
- [ ] **Category landing pages** exist (Characters, Locations, Factions, Items, Lore, Continents) and link their children.
- [ ] **Images** — each entry has its image prompt; generated art lives in `Codex/Assets/...`.
- [ ] **Restricted content** is in `Codex - Restricted/`, never leaked into a public page.
- [ ] **Spot-check 5 random pages** against the gold-standard formatting.
- [ ] **Publish/sync to the web wiki** (confirm the publish pipeline) and view as a player.
- [ ] `git add` + commit the migrated Codex.

---

## 🎯 If you fall behind

You chose full quality on everything, so the slip absorber is the **POI overflow (7–9 Jun)** — those are the least-trafficked pages. If a weekday session runs short, push that day's *empty* stubs (not the content reformats) into the next weekend's 4h block; the reformats are higher-value and should hold their slots.
