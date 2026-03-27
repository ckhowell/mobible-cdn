# How to Push mobible-cdn to GitHub

Run these commands from your terminal (not from Cowork).

## Step 1 — Create the repo on GitHub

```bash
gh repo create ckhowell/mobible-cdn --public --description "Static assets (Bible SQLite databases + CJK fonts) for the Mobible Bible reader app"
```

Or create it manually at https://github.com/new

## Step 2 — Initialise and push

```bash
cd /path/to/Mobible_05/mobible-cdn

git init
git branch -m main
git add README.md
git commit -m "Initial commit"

# Add bibles (199 files, ~969 MB — this will take a while)
git add bibles/
git commit -m "Add 199 Bible translation SQLite databases"

# Add fonts (16 files, ~145 MB)
git add fonts/
git commit -m "Add CJK font files (JP, KR, SC, TC) for on-demand loading"

git remote add origin https://github.com/ckhowell/mobible-cdn.git
git push -u origin main
```

**Note:** The bibles/ folder is ~969 MB. GitHub has a 100 MB per-file limit but all individual Bible .db files are well under that. The push may take a few minutes on a normal connection.

## Step 3 — Create the v1 tag

```bash
git tag v1
git push origin v1
```

This enables the versioned jsDelivr URLs:
```
https://cdn.jsdelivr.net/gh/ckhowell/mobible-cdn@v1/bibles/WEB.db
https://cdn.jsdelivr.net/gh/ckhowell/mobible-cdn@v1/fonts/NotoSansJP_400Regular.ttf
```

## Step 4 — Verify the CDN works

Wait 1-2 minutes for jsDelivr to index, then test:

```bash
curl -I "https://cdn.jsdelivr.net/gh/ckhowell/mobible-cdn@v1/bibles/WEB.db"
# Should return HTTP 200

curl -I "https://cdn.jsdelivr.net/gh/ckhowell/mobible-cdn@v1/fonts/NotoSansJP_400Regular.ttf"
# Should return HTTP 200
```

## Step 5 — Clean up Mobible_05

After pushing, you can safely:

1. Delete `Mobible_05/mobible-cdn/` (it's now on GitHub)
2. Delete `Mobible_05/bible_databases-master/` (superseded by the CDN repo)
3. Delete the oversized files from `assets/fonts/`:
   - All `NotoSansCJK*.ttf` files (~35 MB each)
   - All `NotoSerifCJK*.ttf` files (~58 MB each)
   - `SpaceMono-Regular.ttf`
4. Add `mobible-cdn/` and `bible_databases-master/` to `.gitignore` if not already

## Optional — Git LFS

If GitHub warns about large files or the push is very slow, you can enable Git LFS:

```bash
git lfs install
git lfs track "*.db"
git lfs track "*.ttf"
git add .gitattributes
git commit -m "Enable Git LFS for binary files"
git push
```

This is optional — all files are under 100 MB so standard git works fine.
