# Elandis Vault Organisation Plan

## Progress Checklist

### Phase 1: Infrastructure
- [x] Create folder structure (Codex/, Codex/Assets/, Codex - Restricted/ and all subfolders)
- [x] Create all 7 Codex document templates (Character, City, Region, POI, Faction, Lore, Item, Restricted)
- [x] `campaign-audit` skill — built and tested on Ayana Syndrosa
- [x] `shrink-image` skill — built (uses ImageMagick to generate 500px-wide `_small` thumbnails)
- [x] Warden Caeryn created as Minor character gold standard reference
- [x] Minor character format established (short opening paragraph + Biography + Campaign section with bullet-per-session)
- [x] Naming conventions documented (Section 8) — "The" rule, session title convention
- [ ] Update session prep template (x_Templates/Prep/Prep - Session.md)
- [x] `codex` skill — Characters only first, extend to other categories later
- [ ] `session-prep` skill (redesigned session prep)
- [ ] `synopsis-cleanup` skill
- [ ] Extend `codex` skill to other categories (City, Region, POI, Faction, Lore, Item)
- [ ] `migrate-to-codex` skill
- [ ] Update CLAUDE.md with new folder structure

### Phase 2: Batch Migration — Empty Files
- [ ] Migrate ~120 empty placeholder files as Minor entries via `migrate-to-codex`

### Phase 3: Content Migration — Non-Empty Files
- [ ] Major entities (~10-15 files: Empress Morganna, Sumara, Valtorran Empire, Ayana, Kharazoth, The Shattering, etc.)
- [ ] Minor entities with content (~30-40 files)
- [ ] Remaining files (~20-30)

### Phase 4: Synopsis Cleanup
- [ ] Run `synopsis-cleanup` on most recent 5-10 synopses

### Phase 5: Polish & Publish
- [ ] Name all sessions — add titles to every Synopsis frontmatter (see Section 8: Session Title Convention)
- [ ] Update `campaign-audit` skill to pull session titles from Synopsis frontmatter and apply them to Campaign section headings
- [ ] Backfill session titles in all existing Campaign sections (Ayana, future characters)
- [ ] Audit all wikilinks for broken links
- [ ] Create Codex.base index (via Obsidian GUI)
- [ ] Configure Obsidian Publish settings
- [ ] Final review pass
- [ ] Go live

---

## Context

The Elandis Obsidian vault has ~150+ lore files dumped at root level with no consistent structure, frontmatter, or formatting. The vault needs to be organised for publication via Obsidian Publish as a player-facing wiki, while keeping DM-only content private. This plan covers: folder structure, document standards, Claude Code skills for consistent content creation, session prep improvements, synopsis cleanup automation, image prompt generation, and a phased backfill strategy.

---

## 1. Folder Structure

```
Elandis/
  Codex/                              # PUBLIC - Canonical lore wiki
    Characters/
    Locations/
      Cities/                         # Darmouth, Val Miriel, Sumara
      Regions/                        # Gulf of Miriel, Shimmering Peaks
      Points of Interest/             # Ruby Falls Goldmine, The Stoneheart
    Factions/                         # The Valtorran Empire, The Finegolds
    Lore/                             # The Shattering, The Pantheon
    Items/                            # The Emberblade, Gossamer Dust
    Assets/                           # PUBLIC - Published images
      Characters/                     # Character portraits
      Locations/                      # Location artwork
      Factions/                       # Faction banners/symbols
      Lore/                           # Lore illustrations
      Items/                          # Item artwork
    Codex.base                        # Index using Obsidian Bases

  Campaigns/                          # PUBLIC - Canonical session recaps + transcripts
    The Bloody Nails/                 # Existing structure unchanged
      Sessions/
      Characters/
      Calendar/
      The Bloody Nails.md

  Codex - Restricted/                 # PRIVATE - DM-only lore (the restricted section)
    Characters/                       # e.g. "Gemma Finegold - Restricted.md"
    Locations/Cities/
    Locations/Regions/
    Locations/Points of Interest/
    Factions/
    Lore/
    Items/

  x_Session Prep/                     # PRIVATE - Unchanged
  x_DM Toolkit/                       # PRIVATE - Unchanged, expand over time
  x_Templates/                        # PRIVATE - Updated templates
  x_Assets/                           # PRIVATE - Raw/working assets, prompts, sketches
  .claude/                            # Skills and config
```

**Publishing rules:**
- `Codex/` and `Campaigns/` are published (including transcripts — players use them to search for session details)
- `Codex - Restricted/` is never published
- Everything prefixed `x_` is never published
- Images in `Codex/Assets/` are published alongside the wiki

**Assets structure:** Published images (character portraits, location artwork, etc.) live in `Codex/Assets/` mirroring the Codex category structure. Raw working files, sketches, and maps stay in `x_Assets/`. When an image is ready for the wiki, it moves from `x_Assets/` to the appropriate `Codex/Assets/` subfolder.

**Codex - Restricted/ convention:** Files named `<Entity Name> - Restricted.md`, linking back to the public Codex entry at the top. Contains: unrevealed backstories, secret motivations, upcoming plot hooks, hidden connections. Thematically styled as the "restricted section of the library" — DM-only lore that players shouldn't access yet.

---

## 2. Document Categories

| Category | Folder | Examples |
|---|---|---|
| Character | `Codex/Characters/` | Gemma Finegold, Empress Morganna, Torgrun |
| City | `Codex/Locations/Cities/` | Darmouth, Val Miriel, Sumara |
| Region | `Codex/Locations/Regions/` | Shimmering Peaks, The Darkwood |
| Point of Interest | `Codex/Locations/Points of Interest/` | Ruby Falls Goldmine, Serenity Plaza |
| Faction | `Codex/Factions/` | The Valtorran Empire, The Finegolds |
| Lore | `Codex/Lore/` | The Shattering, The Pantheon |
| Item | `Codex/Items/` | The Emberblade, Gossamer Dust |

---

## 3. Importance Levels

Two tiers: **Major** and **Minor**. Both must be publication-ready with no placeholders or prompts.

| Level | When to Use | What It Looks Like |
|---|---|---|
| **Major** | Core campaign entities. Players interact with them repeatedly. | Full wiki article: infobox, image, opening paragraph, Description (Appearance/Personality for characters), Biography/History, Campaign sections, Trivia. 500-2000 words. |
| **Minor** | Referenced entities, brief appearances, background world-building. | Infobox, image (if available), opening paragraph summary. No multi-section breakdown. Clean and complete, just concise. 100-300 words. |

**Key rule:** Both tiers are presentable on the public wiki. No `???`, no `- [ ]` checklists, no "TODO" markers. If information isn't known, it's simply omitted rather than shown as a placeholder.

---

## 4. Frontmatter Schemas

### Common Base (all categories)
```yaml
Type: <Category>           # Character, City, Region, POI, Faction, Lore, Item
Importance: Major | Minor
Status: Active | Deceased | Destroyed | Unknown | Disbanded
tags: []
aliases: []
cssclasses:
  - hide-header-underline-3
NoteIcon: <icon>
```

### Character
```yaml
Type: Character
Creature Type: Humanoid
Species: Human
Gender: Female
Pronouns: She/Her
Age: 24
Languages: Common, Dwarvish
Place: "[[Silverdeep]]"
Connections: "[[The Finegolds]], [[The Bloody Nails]]"
Profession: Merchant
Importance: Major
Status: Alive
NoteIcon: npc
tags: [character]
aliases: [Gemma]
```

### City
```yaml
Type: City
Region: "[[Gulf of Miriel]]"
Population: ~15,000
Government: Imperial Governor
Imperial Presence: Heavy
Importance: Major
Status: Active
NoteIcon: city
tags: [location, location/city]
aliases: []
```

### Region
```yaml
Type: Region
Continent: "[[Valtorra]]"
Defining Feature: Brief description
Importance: Minor
Status: Active
NoteIcon: region
tags: [location, location/region]
aliases: []
```

### Point of Interest
```yaml
Type: Point of Interest
Location: "[[Val Miriel]]"
Defining Feature: Brief description
Importance: Minor
Status: Active
NoteIcon: poi
tags: [location, location/poi]
aliases: []
```

### Faction
```yaml
Type: Faction
Leader: "[[Gemma Finegold]]"
Base: "[[Valtorra]]"
Alignment: Anti-Imperial
Importance: Major
Status: Active
NoteIcon: faction
tags: [faction]
aliases: []
```

### Lore
```yaml
Type: Lore
Era: Pre-Shattering | The Shattering | Post-Shattering | Modern
Related: "[[The Chaos Wars]]"
Importance: Major
Status: Active
NoteIcon: lore
tags: [lore]
aliases: []
```

### Item
```yaml
Type: Item
Item Type: Weapon | Armour | Artifact | Material | Consumable
Rarity: Common | Uncommon | Rare | Very Rare | Legendary
Owner: "[[Eryndor]]"
Origin: "[[Belinda Bubblegum]]"
Importance: Minor
Status: Active
NoteIcon: item
tags: [item]
aliases: []
```

---

## 5. Document Body Templates

**Design goal:** These should look like conventional wiki/fandom pages — polished, professional, immersive. Use Gemma Finegold as a starting reference but feel free to improve and embellish the structure to achieve better wiki quality. Every page should feel like it belongs in an official D&D lore compendium.

### Character - Major
Reference: `Codex/Characters/Gemma Finegold.md`

```markdown
> [!infobox|wikipedia]
> # Name
> [![[Codex/Assets/Characters/Name_small.png|cover hsmall]]](Codex/Assets/Characters/Name.png)
> ###### Basic Information
> (table)
> ###### Character Information
> (table)
> ###### Status
> (table)

Opening paragraph — concise, evocative summary of who this person is and why they matter.

## Description
#### Appearance
Vivid, prose-style physical description. Not a bullet list — paint a picture.
#### Personality
Character traits, attitudes, emotional depth. How they come across in conversation.

## Biography
#### Background
Origin, formative events, motivations, how they arrived at their current role.
### Campaign: [[The Bloody Nails]]
#### [[Session Link]]
Key interactions with the party, organised by session appearance.

## Trivia
Fun facts, voice notes, behind-the-scenes details.
```

### Character - Minor
Reference: `Codex/Characters/Warden Caeryn.md`

```markdown
> [!infobox|wikipedia]
> # Name
> [![[Codex/Assets/Characters/Name_small.png|cover hsmall]]](Codex/Assets/Characters/Name.png)
> (same table structure, omit unknown fields rather than leaving blank)

Opening paragraph — 2-3 sentences only. Who they are, their role in the world, one brief physical or personality note. No references to the player characters — this is purely who they are in the world.

## Biography

Concise prose covering their recent actions and how they have intersected with the campaign and the party. Not a full life story — focused on what is known and what has happened. One to three paragraphs.
```

### City - Major
```markdown
> [!infobox|wikipedia]   (optional — with city artwork)

## Details
- Population / Government / Imperial Presence / Defining Trait / Current Conflicts

### Overview
### History
### The People
### Culture and Beliefs
### Relations with the Empire

## Locations
### Key Locations
### Factions
### Merchants
### Taverns
```

### City - Minor
```markdown
## Details
- Population / Government / Defining Trait

### Overview
(1-2 paragraphs — enough to give a reader a clear sense of the place)
```

### Faction - Major
```markdown
Opening paragraph — who they are, what they stand for.

## Purpose & Goals
## Structure & Leadership
## Notable Members
## History
## Relations
### Campaign: [[The Bloody Nails]]
```

### Faction - Minor
```markdown
Opening paragraph summary.
## Notable Members (if applicable)
```

### Lore - Major
```markdown
Opening paragraph — what this is and why it matters.

## Overview
## Historical Context
## Significance
## Legacy / Current Impact
```

### Item - Major
```markdown
> [!infobox|wikipedia]   (with item artwork)

Opening paragraph — what it is, where it came from.

## Properties
## History
## Current Owner
```

### All categories follow the Major/Minor pattern — full sectioned article vs concise summary. Minor entries always have an infobox (where the category uses one) and a complete opening paragraph. No section should feel incomplete or stub-like.

---

## 6. Image Prompt Generation

Every skill that creates a Codex document should generate an image prompt at the top of the file in a code block. The user copies this into NanaBanana to generate the image, then places it in `Codex/Assets/<Category>/` and embeds it in the doc.

### Art Style Standard

Based on existing templates in `x_Templates/Assets - Character Picture Generation.md` and `x_Templates/Assets - Scene Generation Template.md`:

**Characters:**
```
[STYLE]: Fantasy RPG character portrait. Bold painterly strokes, visible brushwork, digital painting aesthetic. Rich dramatic colour palette. NOT photorealistic — stylized like official D&D 5e module artwork.
[SUBJECT]: <character description — race, gender, age, notable features, clothing, expression>
[POSE]: <pose/action — e.g. "leaning against a market stall, arms crossed, half-smile">
[SETTING]: <brief environment — e.g. "cobblestone market square, warm lantern light">
[LIGHTING]: <mood lighting — e.g. "golden hour side-lighting, deep shadows">
[FORMAT]: Portrait, 3:4 aspect ratio
```

**Locations:**
```
[STYLE]: Semi-realistic fantasy landscape. Digital matte painting, painterly textures, atmospheric perspective. Inspired by Jordan Grimmer / Raphael Lacoste. NOT photorealistic.
[SUBJECT]: <location description — key visual features, scale, materials>
[MOOD]: <emotional tone — e.g. "vast, awe-inspiring, ancient">
[LIGHTING]: <atmosphere — e.g. "diffused golden light through mist, overcast sky">
[FORMAT]: 16:9 cinematic landscape
```

The prompt is placed at the very top of the document in a fenced code block. Once the user generates and adds the image, they delete the prompt block.

**When to generate prompts:** Always — every Codex document gets an image prompt, regardless of category or importance level. Consistent artwork across the entire wiki is a priority.

**Prompt types by category:**
- **Characters**: Portrait prompt (3:4 aspect ratio)
- **Cities, Regions, POIs**: Landscape prompt (16:9 cinematic)
- **Factions**: Banner/emblem or group scene prompt (flexible aspect ratio)
- **Lore**: Thematic illustration prompt (16:9 cinematic)
- **Items**: Object/artifact prompt (1:1 square or 3:4)

---

## 7. Skills to Build

### 7.1 `codex` (Unified Codex Skill)
**Trigger:** `/codex` or "create a character/location/faction/etc."

A single skill that handles all Codex entry creation across every category. The user's input determines the category, and the skill adapts its prompts, frontmatter schema, body template, and image prompt style accordingly.

**Usage examples:**
- `/codex` — skill asks what you want to create
- `/codex add a minor character called Theren` — infers category + importance from input
- `/codex add a restricted character` — creates entry in `Codex - Restricted/`
- `/codex create a major city` — prompts for details using the City template
- `"create a faction called The Silver Covenant"` — natural language trigger

**Workflow:**
1. **Parse input** — extract what's provided (name, category, importance, restricted flag). Anything missing, ask.
2. **Determine category** — Character, City, Region, POI, Faction, Lore, or Item. If ambiguous, ask.
3. **Determine destination** — if "restricted" is mentioned, write to `Codex - Restricted/<Category>/`. Otherwise write to `Codex/<Category>/`.
4. **Prompt for details** — category-specific questions, scaled by importance:

   | Category | Major Prompts | Minor Prompts |
   |---|---|---|
   | **Character** | Species, gender, age, place, connections, profession, appearance, personality, backstory, party relationship | Brief description (1-3 sentences) |
   | **City** | Region, population, government, imperial presence, culture, key locations, factions, history | Region, defining trait, 1-2 paragraph overview |
   | **Region** | Continent, defining features, settlements, history, dangers | Continent, defining feature, brief overview |
   | **POI** | Parent location, defining feature, purpose, history | Parent location, defining feature, brief description |
   | **Faction** | Leader, base, alignment, purpose, structure, members, history | Leader, base, purpose, brief description |
   | **Lore** | Era, related topics, historical context, significance, legacy | Era, related topics, brief summary |
   | **Item** | Item type, rarity, owner, origin, properties, history | Item type, rarity, brief description |

5. **Generate document** — apply the correct frontmatter schema (Section 4) and body template (Section 5) for the category and importance level.
6. **Generate image prompt** — category-appropriate style (portrait for characters, landscape for locations, etc.) placed at top of file in a code block.
7. **Check for existing files** — if file exists at root or in Codex with content, migrate and reformat rather than overwriting.
8. **Check for existing images** — if an image already exists in `x_Assets/` or `Codex/Assets/` matching the name, link it in the infobox.
9. **Write file** — to the correct subfolder based on category and restricted flag.
10. **For restricted entries** — include a backlink to the public Codex entry at the top (e.g. `> Public entry: [[Character Name]]`), then sections for: Secret Backstory, Hidden Motivations, Unrevealed Connections, Upcoming Plot Hooks.

**Output paths by category and visibility:**

| Category | Public Path | Restricted Path |
|---|---|---|
| Character | `Codex/Characters/` | `Codex - Restricted/Characters/` |
| City | `Codex/Locations/Cities/` | `Codex - Restricted/Locations/Cities/` |
| Region | `Codex/Locations/Regions/` | `Codex - Restricted/Locations/Regions/` |
| POI | `Codex/Locations/Points of Interest/` | `Codex - Restricted/Locations/Points of Interest/` |
| Faction | `Codex/Factions/` | `Codex - Restricted/Factions/` |
| Lore | `Codex/Lore/` | `Codex - Restricted/Lore/` |
| Item | `Codex/Items/` | `Codex - Restricted/Items/` |

### 7.2 `session-prep` (Redesigned)
**Trigger:** `/session-prep`

**Format principles (learned from Session 44 vs 46):**
- Scene-focused with bullet points and callouts
- Brief inline NPC/location descriptions are fine (1-2 lines), but detailed lore lives in linked Codex docs
- Cheat sheet tables appear **within scenes** where relevant (e.g. a shopping scene gets a location/shop table right there), not all at the bottom
- Read-aloud text (`> [!cite]+`) is the only long prose
- Uses all existing callout templates: Action, Combat, Description, Quote, Read, Trigger, Trigger+Action, Details

**Improved prep structure:**
```markdown
---
Session Date: YYYY-MM-DD
cssclasses: [hide-header-underline-3]
tags: [session-prep]
---

## To Do
- [ ] Stream Setup
- [ ] Set Session Date in Frontmatter
- [ ] Intro/Recap
- [ ] Update Calendar

## Recap
- [[Previous Synopsis Link]]

## Scenario 1: <Name>

> [!summary]- Details
> - Where: [[Location]]
> - When: <timing>
> - Key NPCs: [[NPC1]], [[NPC2]]

### Scene 1: <Name>

> [!example]+ Description
> <2-3 sentences of atmosphere/setting>

- Key point 1
- Key point 2

**[[NPC Name]]** — brief 1-line description of manner/role here

> [!question] Trigger
> <condition>
> > [!info]- Action
> > - <what happens>

> [!cite]+ Read Aloud
> *<dramatic text>*

### Scene 2: Shopping / Exploration

> [!example]+ Description
> <atmosphere>

| Location | What's Here | Proprietor | Key Detail |
|---|---|---|---|
| [[Shop 1]] | Herbs, supplies | [[NPC]] | Fascinated by outsiders |
| [[Tavern]] | Food, gossip | [[NPC]] | Hasn't seen a dwarf in 100 years |

(scene details, triggers, etc.)

## NPC Quick Reference

| NPC | Role | Manner | Key Line |
|---|---|---|---|
| [[Name]] | Role | 2-3 words | "One quote" |

## Notes
- Loose threads, reminders
```

**What the skill does:**
1. Ask: session number, primary location, key scenarios/scenes, any new NPCs or locations
2. Read previous session synopsis for continuity
3. Read primary location's Codex page for reference
4. Check which referenced NPCs/locations have Codex pages; flag missing ones
5. Generate prep in the scene-based format above
6. Offer to create Minor entries for any undocumented entities via `/codex`

### 7.3 `synopsis-cleanup`
**Trigger:** `/synopsis-cleanup`

**Workflow:**
1. Read the raw synopsis (AI-generated from transcript)
2. Read the session prep (source of truth for names/spelling)
3. Read the recap prompt template (standing NPC/location reference)
4. Fix:
   - Wikibox metadata (session #, play date, in-world date, location, characters — all `[[wikilinked]]`)
   - Proper noun spelling (using prep NPC reference + template as ground truth)
   - Wrap all NPC names and locations in `[[wikilinks]]` on first mention per section
   - Clean up generic AI phrasing
5. Audit all `[[wikilinks]]` — check if target files exist in Codex or root
6. Output cleaned synopsis + list of entities needing Codex entries (offer to create Minor entries via `/codex`)

### 7.4 `migrate-to-codex`
**Trigger:** `/migrate-to-codex` or "migrate <filename>"

**Workflow:**
1. Read the root-level file
2. Classify category (Character/City/Region/POI/Faction/Lore/Item) based on content, filename, and context from vault references
3. Determine importance based on content volume (empty/minimal → Minor, detailed → Major)
4. If empty: search vault for `[[FileName]]` references in synopses/prep to gather context, generate a Minor entry
5. If non-empty: reformat into appropriate template, preserving all existing content, adding frontmatter
6. Always generate image prompt at top of file
7. Write new file in correct Codex subfolder
8. Set aliases to include the original filename so existing `[[wikilinks]]` still resolve
9. Prompt user to confirm deletion of old root file

**Batch classification heuristics:**
- Person names → Character
- Names with "Val ", "Forest", "River", geographic words → Location sub-type
- Names starting with "The " + collective noun → Faction
- Event names ("The Shattering") → Lore
- Object names → Item
- Ambiguous → ask user

### 7.5 `codex-audit`
**Trigger:** `/codex-audit` or "audit <character name>"

Validates that a Character's Campaign appearance sections are accurate against the actual session synopses. Characters accumulate campaign sections over time and it's easy for details to drift, get attributed to the wrong session, or for appearances to be missed entirely.

**Workflow:**
1. Read the target Character's Codex entry
2. Extract all Campaign session references (e.g. `Session 45`, `Session 46`)
3. Read each referenced synopsis and verify:
   - The character actually appears in that session
   - The events described in the character's entry match the synopsis
   - Key details (locations, other characters involved, outcomes) are accurate
4. Search all synopses for additional appearances not yet listed in the character's entry
5. Report:
   - **Confirmed:** Sections that match the synopses
   - **Discrepancies:** Details that don't match (with quotes from both sources)
   - **Missing appearances:** Sessions where the character appears but has no entry section
6. Optionally apply fixes (with user confirmation)

**Scope:** Initially Characters only, but could extend to Locations/Factions tracking their campaign appearances.

---

## 8. Naming Conventions

### "The" in Document Titles

**Rule:** If "The" is capitalised in natural prose, it is part of the proper name — include it in the filename. If it would be lowercase in a sentence, it is just an article — omit it.

| Category | Convention | Examples |
|---|---|---|
| **Events & ceremonies** | Keep "The" — it's part of the name | `The Emerald Ceremony.md`, `The Shattering.md`, `The Chaos Wars.md` |
| **Locations & structures** | Drop "The" — it's just an article | `Stoneheart.md`, `Liar's River.md`, `Ruby Falls Goldmine.md` |
| **Factions** | Keep "The" only if it's part of the self-given name | `The Bloody Nails.md` ✓ — `Valtorran Empire.md` (no "The") |
| **Characters** | N/A — character names don't have leading articles | — |

**In prose:** When linking mid-sentence where lowercase "the" is needed, use the pipe syntax: `[[Stoneheart|the Stoneheart]]`. For names that include "The", it will be capitalised as part of the proper noun: `during [[The Emerald Ceremony]]`.

### Session Title Convention

Campaign section headings use `Session N` only until all sessions have been formally named:

```markdown
#### [[Campaigns/The Bloody Nails/Sessions/Session 46 - The Shining City/Session 46 - The Shining City|Session 46]]
```

Once sessions are named, the title will be stored in each Synopsis's frontmatter and the display text updated to `Session N — Title`. The `campaign-audit` skill will be updated to read from frontmatter and apply titles automatically.

---

## 9. Existing Skills to Keep

- **`whisperx-prompt`** — No changes needed. Works well.
- **`session-context`** — No changes needed. Works well.

---

## 9. Template Updates

### Consolidate NPC Templates
Replace `x_Templates/NPC - Female.md` and `x_Templates/NPC - Male.md` with a single `x_Templates/Character.md` template. The skill handles gender-specific defaults.

### Update Town - City Template
Add full frontmatter schema from Section 4 to `x_Templates/Town - City.md`.

### Add New Templates
Create templates for: Region, Point of Interest, Faction, Lore, Item — matching the schemas and body structures defined above.

### Update Session Prep Template
Replace `x_Templates/Prep - Session.md` with the improved format from Section 7.6.

---

## 10. Additional Recommendations

### Codex Index Page
Create `Codex/Codex.base` using Obsidian's native Bases feature (`.base` files). Bases is a core Obsidian feature that works with Publish (unlike Dataview which is a plugin). It queries notes by frontmatter properties and renders as sortable/filterable tables.

Set up the Base to query all files in `Codex/` subfolders, displaying columns like Type, Species/Region, Status, Importance. Players can filter and browse the wiki from this single entry point. The `.base` file is configured via the Obsidian GUI — create it manually after the folder structure is in place.

### Tag Convention
Standardised nested tags for filtering:
- `character`, `location/city`, `location/region`, `location/poi`, `faction`, `lore`, `item`
- `importance/major`, `importance/minor`
- `campaign/the-bloody-nails`

### Update CLAUDE.md
Once structure is in place, update CLAUDE.md. Keep it very concise — just essential rules and folder pointers. Link to this plan or a reference doc for details rather than inlining everything. CLAUDE.md is loaded into every conversation context, so every line costs tokens.

---

## 11. Backfill Strategy & Timeline

### Phase 1: Infrastructure (Days 1-2)
- [ ] Create folder structure (all Codex/, Codex/Assets/, and Codex - Restricted/ subfolders)
- [ ] Create/update all 7 document templates
- [ ] Update session prep template
- [ ] Build all 4 skills
- [ ] Update CLAUDE.md with new structure docs

### Phase 2: Batch Migration — Empty Files (Days 3-5)
- [ ] Migrate ~120 empty placeholder files as Minor entries
- [ ] Use `migrate-to-codex` skill in batches of 20-30
- [ ] Each batch: auto-classify, generate frontmatter + 1-paragraph summary from vault context, generate image prompts
- [ ] Manual review per batch (spot-check, correct misclassifications)

### Phase 3: Content Migration — Non-Empty Files (Days 6-10)
- [ ] Migrate ~76 files with existing content
- [ ] Major entities first (~10-15 files: Empress Morganna, Sumara, The Valtorran Empire, Ayana Wynne, Kharazoth, The Shattering, etc.)
- [ ] Minor entities with content (~30-40 files: Darmouth, The Red Priests, etc.)
- [ ] Remaining files (~20-30)
- [ ] For Major entities: user provides creative input before skill generates

### Phase 4: Synopsis Cleanup (Days 8-12, overlapping)
- [ ] Run `synopsis-cleanup` on most recent 5-10 synopses
- [ ] Fix wikibox metadata, spelling, links
- [ ] Create any missing Codex entries flagged by the audit

### Phase 5: Polish & Publish (Days 13-14)
- [ ] Audit all `[[wikilinks]]` for broken links
- [ ] Create Codex.base index using Obsidian Bases (via GUI)
- [ ] Configure Obsidian Publish settings (include Codex + Campaigns, exclude x_ folders + Codex - Restricted)
- [ ] Final review pass on published content
- [ ] Go live

### Target: Publishable in ~2 weeks
With 1-2 hours per day of vault work, heavily assisted by the skills. The empty file migration (Phase 2) is mostly automated. The content migration (Phase 3) needs user creative input for Major entities.

---

## 12. Execution Order

**Note:** This plan will be saved to the vault as an actionable reference. The user will execute these steps manually, invoking Claude as needed for individual steps.

1. **Create folder structure** — mkdir all Codex/, Codex/Assets/, and Codex - Restricted/ subfolders
2. **Build templates** — create/update all document templates in x_Templates/
3. **Build skills** — create all 4 skills in .claude/skills/
4. **Update CLAUDE.md** — concise update with new folder pointers only
5. **Test skills** — run `/codex` on one entity per category to verify output
6. **Begin migration** — start with Phase 2 batch migration

---

## Critical File References

| File | Role |
|---|---|
| `Codex/Characters/Gemma Finegold.md` | Gold standard Character (Major) |
| `Sumara, The Shining City.md` | Gold standard City (Major) — to be migrated |
| `x_Templates/Town - City.md` | Existing city template — to be updated |
| `x_Templates/NPC - Female.md` | Existing NPC template — to be consolidated |
| `x_Templates/Assets - Character Picture Generation.md` | Art prompt style reference |
| `x_Templates/Assets - Scene Generation Template.md` | Location art prompt style reference |
| `x_Templates/Prep - Session.md` | Session prep template — to be redesigned |
| `x_Templates/Session - Recap - Prompt.md` | Recap prompt — used by synopsis-cleanup |
| `.claude/skills/session-context/SKILL.md` | Best-written existing skill — structural pattern for new skills |
| `x_Session Prep/.../Session 44 - The Elven Archmage - Prep.md` | Preferred prep style (sparse, scene-focused) |
