---
name: process-wiki-image
description: Use this skill when the user asks to "/process-wiki-image", "process a character image", "convert a new character image", "make WebP versions", or wants to turn a source PNG into the published WebP pair (full + thumbnail) for a Codex asset. Takes a full-size source image, produces a quality-95 full WebP (max 1000px wide) and a quality-85 300px thumbnail WebP, and archives the original PNG outside the vault.
---

# Process Wiki Image — Source PNG → Published WebP Pair

Convert a freshly generated source image (typically a NanaBanana-style PNG) into the WebP pair used by the published Codex, and archive the original outside the vault.

## Convention

Every Codex asset has two WebPs published in the vault and one archived original:

- `<Codex/Assets/<Category>/Name.webp>` — max 1000px wide, quality 95 (linked from the infobox, opened on click)
- `<Codex/Assets/<Category>/Name_small.webp>` — 300px-wide thumbnail, quality 85 (embedded in the infobox with `cover hsmall`)
- `<archive root>/<Name>.png` — lossless source PNG, kept outside the vault for reprocessing

**Default archive root for character images:** `/mnt/storage/Misc/DnD/The Bloody Nails/Art/Characters/NPCs/`

If processing a different asset category (locations, items, etc.), ask the user for the archive root rather than assuming.

WebP at q95 is visually indistinguishable from the source PNG for AI-generated painterly art and is roughly 10× smaller. Q85 at 500px is enough for retina-quality infobox display.

## Steps

### 1. Identify the source image

If the user hasn't provided a path, ask: *"What's the path to the source PNG?"*

Accept any of:
- An absolute path
- A vault-relative path (e.g. `Codex/Assets/Characters/Warden_Caeryn.png`)
- Just a filename — assume `Codex/Assets/Characters/` if no category is obvious

Resolve to an absolute path before proceeding.

### 2. Derive output paths

Given source `Codex/Assets/Characters/Warden_Caeryn.png`:
- Full WebP:  `Codex/Assets/Characters/Warden_Caeryn.webp`
- Thumb WebP: `Codex/Assets/Characters/Warden_Caeryn_small.webp`
- Archive:    `<archive root>/Warden_Caeryn.png`

Before continuing, check that no file already exists at the archive destination — if it does, skip the archive step silently (the source is already safely stored).

### 3. Generate the WebPs

```bash
magick "<source>" -resize 1000x\> -quality 95 "<full_webp>"
magick "<source>" -resize 300x -quality 85 "<thumb_webp>"
```

`-resize 1000x\>` caps width at 1000px but won't upscale images already smaller than that. `-resize 300x` sets width to 300px; both calculate height to maintain aspect ratio.

### 4. Archive the source PNG

If a file already exists at the archive destination, skip this step — the original is already stored safely.

Otherwise:

```bash
mv "<source>" "<archive_root>/"
```

### 5. Confirm output

Use `identify` (ImageMagick) and `ls -lh` to check dimensions and file sizes — don't reach for Python when shell tools suffice.

Report the source dimensions, both output paths and sizes, and the archive path:

```
Done. Warden_Caeryn processed.
  Source:   1792×2400 PNG, 8.8M  → archived to /mnt/storage/Misc/DnD/The Bloody Nails/Characters/NPCs/Warden_Caeryn.png
  Full:     1000×1339 WebP q95, 800K  → Codex/Assets/Characters/Warden_Caeryn.webp
  Thumb:    300×402   WebP q85, 24K   → Codex/Assets/Characters/Warden_Caeryn_small.webp
```

### 6. Infobox reminder (if relevant)

If the user just created this for a new character entry, remind them the infobox embed should be:

```
[![[Codex/Assets/Characters/Name_small.webp|cover hsmall]]](Codex/Assets/Characters/Name.webp)
```
