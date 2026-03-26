# mobible-cdn

Static assets for the [Mobible](https://github.com/ckhowell/mobible-05) Bible reader app. Served via [jsDelivr CDN](https://www.jsdelivr.com/).

## Contents

### `/bibles/` — 199 Bible translation SQLite databases

Each `.db` file contains a single table `{TranslationId}_verses` with columns: `book_id`, `chapter`, `verse`, `text`.

**CDN URL:**
```
https://cdn.jsdelivr.net/gh/ckhowell/mobible-cdn@v1/bibles/{TranslationId}.db
```

### `/fonts/` — 16 CJK font files (Japanese, Korean, Chinese SC, Chinese TC)

Noto Sans and Noto Serif in Regular (400) and Bold (700) weights for CJK scripts. Downloaded on demand when the user selects a CJK UI language.

**CDN URL:**
```
https://cdn.jsdelivr.net/gh/ckhowell/mobible-cdn@v1/fonts/{FontFileName}.ttf
```

## Versioning

Assets are pinned via git tags (`@v1`, `@v2`, etc.). jsDelivr caches aggressively per tag, so existing app installs continue working when new versions are published.

## Font Sources

CJK fonts are from [Google Fonts](https://fonts.google.com/noto) via `@expo-google-fonts` packages, licensed under [SIL Open Font License 1.1](https://scripts.sil.org/OFL).

## Bible Sources

Bible databases are from [bible_databases](https://github.com/ckhowell/bible_databases). See that repo for individual translation licences.

---

*Mobible — Chris Howell / Halfnine Design*
