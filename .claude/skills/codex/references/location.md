# Codex Category — Locations

Shared location workflow for the codex skill. Read this when creating any location entry, **then read the subtype doc** — it holds the creation-mode questions, frontmatter, infobox, body templates, and gold standard for that subtype, while this base holds everything the subtypes share.

| Subtype | What it is | Subtype reference | Status |
|---|---|---|---|
| **Point of Interest** | A single notable place — a ruin, landmark, natural feature, structure, or site within a larger region | `references/locations/poi.md` | **Supported** |
| **Region** | A broad geographic area — a forest, gulf, mountain range, or plane that contains settlements and sites | `references/locations/region.md` | **Supported** |
| City | A settlement — town, city, port | *(not yet written)* | Not yet supported |

**Telling the subtypes apart:** a whole forest, gulf, mountain range, or plane is a **Region**; a single ruin, landmark, or site *within* one is a **Point of Interest**; a settlement (town, city, port) is a **City**. A Region contains and links to the Cities and POIs inside it — it is both a lore article and the map-hub that ties its child places together. If the user wants a City, tell them that subtype isn't wired in yet and offer a Point of Interest or Region instead, or to hand-write it from `x_Templates/Codex/City.md`. (When City is added, write `references/locations/city.md` mirroring the two existing subtype docs.)

## Vault locations

Each subtype writes to its own folder; everything else (stubs, assets) is shared.

| Subtype | Public folder | Restricted folder |
|---|---|---|
| Point of Interest | `Codex/Locations/Points of Interest/<Name>.md` | `Codex - Restricted/Locations/Points of Interest/<Name> - Restricted.md` |
| Region | `Codex/Locations/Regions/<Name>.md` | `Codex - Restricted/Locations/Regions/<Name> - Restricted.md` |

- **Root-level stubs:** `<Name>.md` at vault root (migration case)
- **Image assets:** published under a subtype subfolder with **underscores, no spaces** — `Codex/Assets/Locations/Points_of_Interest/` for POIs, `Codex/Assets/Locations/Regions/` for Regions (working copies under `x_Assets/Locations/`). The infobox path must include this subfolder.

---

## Step 1 — Parse input

Extract from the user's message whatever they've already provided:
- Location **name**
- **Subtype:** Point of Interest or Region (City is not yet supported). Infer from the place — a whole forest/gulf/range/plane is a Region; a single ruin or landmark within one is a Point of Interest. Confirm if it's ambiguous.
- **Importance:** Major or Minor
- Whether a **restricted companion document** is also needed

If anything is missing, ask for it all in one message — don't ask one field at a time. Name, subtype, and importance are required before proceeding. If you're unsure whether something is a Point of Interest versus a Region (or a City), say so and confirm — a port town is a City, a whole forest is a Region, a single ruin or landmark within them is a Point of Interest.

**Once the subtype is settled, read its reference doc now** (`references/locations/poi.md` or `references/locations/region.md`) and keep this base doc for the shared steps below.

---

## Step 2 — Check for existing files and research the location

Before asking for details, check the vault:

1. Does the entry already exist in its subtype folder (`Codex/Locations/Points of Interest/<Name>.md` or `Codex/Locations/Regions/<Name>.md`)? If so, warn the user and ask whether they want to update/migrate rather than overwrite.
2. Does `<Name>.md` exist at the vault root? If so, read it — its content informs the entry and whether a restricted companion is needed (see Stub File Format below). Root location stubs are often already well-researched DM notes; treat their geography and lore as canon unless the synopses contradict them.
3. Grep all synopsis files under `Campaigns/The Bloody Nails/Sessions/` for the location's name (and any short-form aliases or the names of structures within it). Collect every matching snippet with its session number. Ignore hits inside `Transcript.md` files — never read those.
4. **Reconcile session attributions.** A root stub may cite session numbers from memory; the synopses are the source of truth. If the stub says an event happened in Session N but the synopses place it elsewhere, trust the synopses, correct it in the entry, and flag the discrepancy to the user.
5. Glob for image files matching the location name in `x_Assets/Locations/` and the subtype subfolder `Codex/Assets/Locations/Points_of_Interest/` or `Codex/Assets/Locations/Regions/` (patterns: `Name*.webp`, `Name_with_underscores*.webp` — also check `*.png`). If found, use the real filename **and its subtype subfolder** in the infobox path.

**Region** adds a hub-discovery research step (finding the child Cities/POIs to link) — see `references/locations/region.md`.

### Stub file format

A root-level stub may be freeform notes. If it contains a `## Restricted` section, treat everything before it as public information and everything under it as DM-only secrets. In this case, automatically create both files without asking — the DM structured it that way intentionally.

---

## Step 3 — Present research and gather details

**If a root stub was found OR synopsis mentions were found (migration mode):**

Present your findings in one message before asking anything:

```
**Research for [Name]**

Root stub: [summary of content, or "empty"]

Synopsis appearances:
- Session N: [brief quote or summary of the relevant snippet]
- Session N: [...]

[Any corrected session attributions — "the stub says X happened in Session N, but the synopses place it in Session M."]

Based on this, I'd suggest: [Major/Minor] — [one sentence reasoning].

What would you like to add before I generate the entry? Drop in any bullet notes —
geography, atmosphere, history, current state, secrets, anything not in the synopses.
```

Wait for the user's notes, then proceed. Don't ask a structured question list in migration mode — the user's notes are freeform and that's fine.

If the stub contained a `## Restricted` section, note that you'll create both files and confirm this is still what they want.

**If this is a fresh location with no existing files (creation mode):**

Ask for everything in one message, using the **creation-mode question list in the subtype doc** (`poi.md` or `region.md`). Only ask for what isn't already provided.

---

## Step 4 — Generate the public document

Assemble the **frontmatter, infobox, and body** from the templates in the subtype doc, observing these shared rules.

### Universal infobox rules

- Escape pipes inside wikilinks within blockquotes using `\|` — Obsidian rendering requirement.
- Omit rows for unknown values — but **always keep the parent row** (`Location` for a POI, `Continent`/`Plane` for a Region); it's the reader's map reference.
- Image path: underscores, no spaces, in **both the filename and the subtype subfolder** — `Codex/Assets/Locations/Points_of_Interest/Location_Name_small.webp` / `Codex/Assets/Locations/Points_of_Interest/Location_Name.webp` for a POI, and `Codex/Assets/Locations/Regions/...` for a Region. Never point the link at the bare `Codex/Assets/Locations/` folder.
- If a real image was found in Step 2, use its actual filename; otherwise use the placeholder (the user generates art from the prompt later).

### Rules that apply to all locations

- The **opening paragraph is world-focused** — describe the place as it exists in Elandis. The party doesn't appear in the opening paragraph; their deeds belong in the Campaign section.
- **Always anchor the place geographically, in a required first body section.** Every location leads its body with a mandatory geography section that places it on the map, then describes its physical setting — and it always comes first, even when the rest of the sectioning flexes:
  - **POI:** `## Location & Geography` — where the *point* sits relative to a known, mappable location (e.g. "north-east of [[Farhaven]]", "in the far south of [[Valtorra]], roughly 50 miles west of [[Darmouth]]"). Mirrors the infobox `Location` field.
  - **Region:** `## Geography & Landscape` — which continent or plane the *area* occupies, what it borders, and its rough extent, then the whole-area terrain and climate. Mirrors the infobox `Continent`/`Plane` field.

  The opening paragraph should gesture at the location too, but this section is where the map reference is guaranteed.
- **Session link format:** `#### [[Session N - <Title>]]` — direct basename link, no path, no alias. Each session file's basename is unique vault-wide, so Obsidian resolves it directly. Verify the exact basename (early sessions are zero-padded, e.g. `Session 08 - The High Road`).
- If no campaign appearances were provided, omit the Campaign section entirely.
- Trivia is Major-only.
- The public document contains only what the players currently know. If a restricted companion is also being created, secrets are omitted here and woven into the restricted version instead.

---

## Step 5 — Generate the restricted companion document (if needed)

Create this when: the stub had a `## Restricted` section, the user asked for both files, or the user flagged restricted content during Step 3.

Write to the subtype's restricted folder:
- POI: `Codex - Restricted/Locations/Points of Interest/<Name> - Restricted.md`
- Region: `Codex - Restricted/Locations/Regions/<Name> - Restricted.md`

### What the restricted document is

The restricted document is the **full-truth version** of the article — the same structure as the public document for that subtype, but with secrets woven naturally into the body. It is what the public article will become once those secrets are revealed. When that day comes, the DM can replace the public file with this one (removing the `> [!abstract] Public Entry:` callout and the `## DM Notes` section).

### Restricted document structure

```markdown
[image prompt fenced code block]

[full frontmatter — same schema as public, same values]

> [!abstract] Public Entry: *[[Location Name]]*

[Infobox — identical to public version]

[Opening paragraph — same as public, or expanded with the full truth if the public version was deliberately vague]

[Body sections — the same heading set as the public body for this subtype (listed under "Restricted body heading set" in the subtype doc), geography section first, with the full truth woven in. Hidden features, secret history, and concealed powers are written here as natural prose rather than held back.]

### [[The Bloody Nails|Campaign: The Bloody Nails]]

#### [[Session N - <Title>]]
[Same as public — campaign appearances are facts, not secrets]

## Trivia
[Same as public, if Major]

## DM Notes

- **Unrevealed history:** [What the place really is, not yet known to the party]
- **Plot hooks:** [Ways this place might factor into future sessions]
- **Hidden features:** [Secret passages, concealed dangers, things waiting to be found]
- [Any other DM-side notes — mechanics, session flags, meta-context]
```

---

## Step 6 — Generate the image prompt

Place this at the **very top of each file**, before the frontmatter, in a fenced code block. Always generate it — even if an image already exists. Both files (public and restricted) get the same prompt.

Locations use the **same painterly art style as characters** — so the whole wiki shares one look. Only the framing differs: a 16:9 landscape instead of a 3:4 portrait. The `[STYLE]` line must be identical to the character prompt's (just "portrait" → "landscape"); do **not** substitute a matte-painting, semi-realistic, or photoreal style.

```
[STYLE]: Fantasy RPG landscape. Bold painterly strokes, visible brushwork, digital painting aesthetic. Rich dramatic colour palette. NOT photorealistic — stylized like official D&D 5e module artwork.
[SUBJECT]: <the place — key visual features, scale, materials, any notable structures>
[MOOD]: <emotional tone — e.g. "vast, awe-inspiring, ancient", "desolate and haunted">
[LIGHTING]: <dramatic, high-contrast lighting — e.g. "low golden sun and long cool shadows", "shafts of pale light through deep gloom">
[FORMAT]: 16:9 cinematic landscape
```

Keep the `[STYLE]` line identical across every location entry; only `[SUBJECT]`, `[MOOD]`, and `[LIGHTING]` change per place. Derive those three from the place's geography, history, and current state, and make them specific — a good prompt conjures an exact vista, not a generic fantasy backdrop. Favour the warm-against-cool, high-contrast lighting of the character art. The subtype doc has a one-line note on **framing** (foreground a feature for a POI; a characteristic vista for a Region).

---

## Step 7 — Write the files

Assemble each document in this order:
1. Image prompt fenced code block
2. Frontmatter (YAML between `---` delimiters)
3. Infobox callout
4. Opening paragraph
5. Remaining body sections

Write each file to its correct path. Report all paths written when done.

If a root-level stub was detected in Step 2, ask the user to confirm deletion of the stub file — don't delete it automatically. (Because the new Codex file shares the stub's basename, Obsidian will resolve existing `[[Name]]` links to it once the duplicate root file is gone. If the stub had a different name than the Codex page, add the old name to `aliases` so links still resolve.)
