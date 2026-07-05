You are helping the user add a new recipe video to the cooking page of their Jekyll personal website (hotsushi.github.io).

## How the system works

Recipe videos live in `_reels/`. Each file generates:
- A tile on `/cooking/` (thumbnail + title + tags)
- A shareable detail page at `/cooking/reels/<filename>/`

The tile and detail page are driven entirely by the front matter in the reel file. No other files need to be touched.

## Step 1 — Ask the user these questions (all required)

1. **Embed code** — "Paste the embed code (YouTube iframe, Instagram blockquote, TikTok iframe, or any other platform)"
2. **Dish name** — "What's the dish called?"
3. **Tags** — "How would you tag it?" (see taxonomy below — pick one from each group)

If any answer is missing, ask before proceeding.

## Step 2 — Determine the platform

Detect from the embed code:
- Contains `instagram.com` → `platform: instagram`
- Contains `youtube.com` or `youtu.be` → `platform: youtube`
- Contains `tiktok.com` → `platform: tiktok`
- Anything else → `platform: other`

## Step 3 — Get the thumbnail

**YouTube**: Extract the video ID from the embed URL (the part after `/embed/` and before `?`).
Fetch the thumbnail: `https://img.youtube.com/vi/<VIDEO_ID>/maxresdefault.jpg`
Save to: `assets/hobbies/img/<slug>.jpg`

**Instagram / TikTok / other**: Search online (Unsplash or similar) for a high-quality food photo matching the dish name. Show it to the user and confirm before saving.

Save thumbnail to: `assets/hobbies/img/<slug>.jpg`
where `<slug>` is the dish name lowercased, spaces replaced with hyphens (e.g. `chicken-karahi`, `lehsuni-malai-eggs`).

## Step 4 — Create the reel file

Filename: `_reels/<VIDEO_ID>.md` (use the video ID from the embed URL as the filename)

```yaml
---
layout: reel
title: <Dish Name>
platform: <instagram|youtube|tiktok|other>
thumbnail: /assets/hobbies/img/<slug>.jpg
tags: [<category>, <difficulty>]
embed: |
  <paste the full embed code here, indented by 2 spaces>
---
```

## Tag taxonomy

**Category** (pick one — shown in warm/nature tones):
- `curry` — any curry, karahi, gravy dish
- `appetizer` — starters, snacks, eggs, small plates
- `dessert` — sweets, drinks, kheer, halwa

**Difficulty** (pick one — color-coded):
- `easy` — under 30 min, minimal technique (shown in blue)
- `medium` — moderate prep or technique (shown in yellow/amber)
- `hard` — complex, multi-step, long cook time (shown in red)

Tags render as colored pills on the tile. CSS classes are `tag-<tagname>` and are already defined in `_includes/timelines/cooking.html`.

## Step 5 — Restart the server and verify

```bash
pkill -f "jekyll serve"
bundle exec jekyll serve --port 4000 --detach
```

Then check:
- `http://localhost:4000/cooking/` — new tile appears with thumbnail and tags
- `http://localhost:4000/cooking/reels/<VIDEO_ID>/` — detail page loads with embed

## Step 6 — Commit and push

Always commit and push using the PAT token at `/Users/sraikar/OSS/github.pat.token`:

```bash
git -c user.email="sushant.s.raikar@gmail.com" add _reels/<file>.md assets/hobbies/img/<slug>.jpg
git -c user.email="sushant.s.raikar@gmail.com" commit -m "Add <Dish Name> reel"
PAT=$(cat /Users/sraikar/OSS/github.pat.token | tr -d '[:space:]')
git push "https://${PAT}@github.com/HotSushi/hotsushi.github.io.git" master
```

## Reference — existing reels

| File | Dish | Platform | Tags |
|---|---|---|---|
| `_reels/DZc50UHIW4o.md` | Chicken Karahi | instagram | curry, medium |
| `_reels/WnfzPwgPUro.md` | Lehsuni Malai Eggs | youtube | appetizer, curry, easy |
