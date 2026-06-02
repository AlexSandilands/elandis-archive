---
name: codex
description: Use this skill when the user asks to "/codex", "create a character called X", "add a minor character", "create a location / point of interest / region / city / town called X", "create an item / artifact / magic item called X", "create a faction / organisation / guild / order / network called X", "add a local chapter / nest / cell of a faction", "create a lore / history / event entry", "write up the X war / cataclysm / the Shattering", "document a cosmological structure, plane, force, or phenomenon", "create a deity / god / goddess", "document a god or member of the pantheon", "make a new character, location, item, faction, or lore entry", "add a new codex entry", or wants to create, write, or generate any new character, location, item, faction, or lore page for the Elandis wiki. ALSO trigger when the user mentions a character, place (including a forest, gulf, mountain range, or plane), notable item/artifact, organisation/faction, or piece of lore (a historical event, a cosmological concept) that doesn't have a Codex page yet and asks to document, write up, or turn a stub into a proper entry. ALSO trigger when the user says "migrate [name]", "convert [name] to codex", or wants to move a root-level stub into the Codex folder. Supports Characters, Locations (Points of Interest, Regions, and Cities), Items, Factions (including Local Chapters), and Lore (Events, Cosmology / Concepts, and Deities). This skill researches the entry in the synopses, presents findings, gathers the DM's notes, and produces a complete, publication-ready Codex entry. When a restricted companion document is needed, it creates both files.
---

# Codex Entry Creator

Create publication-ready entries for the Elandis Codex wiki. Every output must look like it belongs in an official D&D lore compendium — polished, immersive, no placeholders.

The Codex covers multiple categories (characters, locations, factions, etc.). Each category has its own format, vault location, and workflow, kept in a dedicated reference doc. This SKILL.md routes to the right reference; the per-category file holds the full instructions.

## Step 1 — Identify the category

From the user's message, determine which kind of entry is being created.

| Category | Trigger phrases | Reference |
|---|---|---|
| Character | "character", "NPC", "minor/major character", a person's name, migrating a person stub | `references/character.md` |
| Location | "location", "point of interest", "POI", "region", "city", "town", "port", "place", a ruin/landmark/site/natural feature, a forest/gulf/mountain range/plane, a settlement, migrating a place stub | `references/location.md` |
| Item | "item", "magic item", "artifact", "relic", "weapon", "amulet", "focus", an object/trinket with story weight, migrating an item stub | `references/item.md` |
| Faction | "faction", "organisation", "guild", "order", "network", "house", "company", "cult", "rebel group", a named group that acts as a body, migrating a faction stub. ALSO "local chapter", "nest", "cell", "lodge" — a faction's branch in one city | `references/faction.md` |
| Lore | "lore", "history", "event", "cataclysm", "war", a cosmological structure/plane/force/phenomenon, a myth or tradition, a god/goddess/deity or a member of the pantheon, "the X war", "the Shattering"-style event, migrating a lore stub | `references/lore.md` |

**Currently supported:** Characters, Items, Factions (including Local Chapters), Locations of subtype **Point of Interest**, **Region**, and **City**, and Lore of subtype **Event**, **Cosmology / Concept**, and **Deity**. If the user asks for any other category, tell them it isn't supported yet and ask if they'd like a character, item, faction, location, or lore entry instead, or skip the skill.

If the category is ambiguous from the message, ask the user to confirm before loading a reference.

## Step 2 — Load the category reference

Read the reference file from the table above. It contains the full workflow for that category: vault paths, research steps, question lists, frontmatter schema, infobox layout, body templates, restricted-companion handling, image prompt format, and gold-standard examples to match.

**Locations are split to save context:** `references/location.md` is a slim shared base (workflow, research, restricted/image/write steps, universal rules). It routes to a per-subtype doc under `references/locations/` (`poi.md`, `region.md`) that holds that subtype's questions, frontmatter, infobox, and body templates. Read the base first, then the one subtype doc it points you to — never load both subtype docs.

**Lore is split the same way:** `references/lore.md` is the slim shared base. It routes to a per-subtype doc under `references/lore/` (`event.md`, `concept.md`, `deity.md`) holding that subtype's questions, frontmatter, infobox, and body templates. Read the base first, then the one subtype doc it points you to — never load more than that one subtype doc.

Follow the steps in the reference end-to-end. Do not improvise the format — match the reference exactly.

## Universal rules (apply to every category)

These rules hold regardless of category. The reference docs assume them.

- **No placeholders.** No `???`, no `- [ ]`, no `TODO`. If a value is unknown, omit the field. Every sentence must be real content.
- **Wikilinks** on first mention of every proper noun (character, place, faction, item). Before writing a wikilink, verify the exact page name with `find` or `ls` — don't assume the name. A wrong link creates a ghost page in Obsidian.
- **Alias lookup:** If a term in prose doesn't match any page name directly (e.g. "Empire", "Barak", "Gemma"), grep the vault for it as a frontmatter alias before leaving it unlinked: `grep -rl "  - <Term>" <vault>/ --include="*.md"`. If a match is found, write `[[Full Page Name|Display Term]]` — e.g. `[[Valtorran Empire|Empire]]`.
- **Page naming convention:** Vault pages use bare proper nouns without a leading article — `Veiled Cubs`, `Order of Ravens`, `Mawbreakers`. In prose, supply the article *outside* the brackets: `the [[Veiled Cubs]]`, `the [[Order of Ravens]]`. Never include "The" inside a wikilink unless that is literally how the page is named (e.g. `[[The Albatross]]` for the ship).
- **Transcripts are off-limits.** Never read `Transcript.md` files in session folders, even when grepping. Search synopses only.

## Adding a new category

When a new category needs to be supported:
1. Create `references/<category>.md` with the full workflow for that category (mirror the structure of `character.md`).
2. Add a row to the category table in Step 1 with its trigger phrases.
3. Update the skill description's trigger list if the new category introduces new phrases users will say.

The SKILL.md itself should stay slim — category-specific detail belongs in the reference, not here.
