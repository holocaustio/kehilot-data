# Yizkor Books Corpus

Source: Internet Archive collection `yiddishbookcenteryizkorbooks`, which mirrors the Yiddish Book Center / NYPL Yizkor book collection.

This directory is organized as:

```text
data/yizkor-books/
  manifest.json
  <country-or-region>/
    <town-or-subject>/
      <detected-language>/
        <internet-archive-id>-<title-slug>/
          metadata.json
          ia-metadata.json
          ocr.txt
          <internet-archive-id>.pdf
```

Language codes are machine-guessed from OCR/title text:

- `he`: mostly Hebrew-script Hebrew
- `yi`: mostly Yiddish in Hebrew script
- `he-yi`: mixed Hebrew/Yiddish
- `yi-latn`: romanized Yiddish / Latin-script Yiddish metadata
- `latin`: mostly Latin-script text
- `mixed`: unclear mixed-script text

Notes:

- `manifest.json` is the corpus index and should be treated as the primary inventory.
- Yiddish Book Center blocked scripted access to its index with HTTP 403, so the downloader uses Internet Archive advanced search for the collection.
- Most books include Internet Archive OCR as `_djvu.txt`. One item, `nybc314167`, had no IA OCR text file; its `ocr.txt` records that OCR is unavailable.
- IA place metadata is uneven. Some directories still contain subject-like names such as `jews-poland-radom`. A later canonicalization pass should normalize towns against JewishGen/YBC town names.
