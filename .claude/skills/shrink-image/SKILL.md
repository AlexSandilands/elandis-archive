---
name: shrink-image
description: Use this skill when the user asks to "/shrink-image", "shrink an image", "create a small version", "make a thumbnail", "resize a character image", or wants to generate the _small version of a Codex asset. Takes a full-size image and produces a 500px-wide thumbnail with the _small suffix, ready for use in Obsidian infoboxes.
---

# Shrink Image

Generate a `_small` thumbnail from a full-size Codex asset using ImageMagick. The small version is used in character infoboxes; the large version is what users navigate to when clicking the image.

## Convention

Every Codex asset has two files:
- `Name.png` — full-size (linked from the infobox, opened on click)
- `Name_small.png` — 500px-wide thumbnail (embedded in the infobox with `cover hsmall`)

Both live in `Codex/Assets/<Category>/` (e.g. `Codex/Assets/Characters/`).

## Steps

### 1. Identify the source image

If the user hasn't provided a path, ask: *"What's the path to the full-size image?"*

Accept any of:
- An absolute path (e.g. `/mnt/storage/Misc/Vaults/Elandis/Codex/Assets/Characters/Warden_Caeryn.png`)
- A vault-relative path (e.g. `Codex/Assets/Characters/Warden_Caeryn.png`)
- Just a filename — assume `Codex/Assets/Characters/` if no category is obvious

Resolve to an absolute path before proceeding.

### 2. Derive the output path

The small file goes in the same directory as the source, with `_small` inserted before the extension:
- `Warden_Caeryn.png` → `Warden_Caeryn_small.png`

### 3. Run ImageMagick

```bash
magick "<source_path>" -resize 500x "<output_path>"
```

`-resize 500x` sets width to 500px and calculates height to maintain aspect ratio — no squashing.

### 4. Confirm output

After running, report:
- Source dimensions (use `identify` to check before and after)
- Output path
- Output dimensions

Example:
```
Done. Warden_Caeryn_small.png created.
  Source:  1792×2400
  Output:  500×670
  Path:    Codex/Assets/Characters/Warden_Caeryn_small.png
```

### 5. Infobox reminder (if relevant)

If the user just created this for a new character entry, remind them the infobox embed should be:

```
[![[Codex/Assets/Characters/Name_small.png|cover hsmall]]](Codex/Assets/Characters/Name.png)
```
