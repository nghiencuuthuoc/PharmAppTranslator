# Translator Docs Book v5 GUI + CLI User Guide

For translator_docs_book_v5_g20_vi.py and translator_docs_book_v5_gui_g20_vi.py  
G20 language pack + Vietnamese

March 13, 2026

> This guide explains setup, OCR, language selection, GUI/CLI usage, and output review.

## Overview

- This version is designed for translating books, regulatory documents, SmPC, PIL, pharmacopeia pages, office files, ebooks, HTML, Markdown, and plain text from a single workflow.
- It supports a G20-oriented translation language set and also adds Vietnamese. The GUI is suitable for day-to-day use, while the CLI is useful for repeatable batch jobs and scripted processing.
- The guide below focuses on operation, setup, language selection, OCR selection, and output review.

## What is new in this build

- Expanded translation language selection: Arabic, German, English, Spanish, French, Hindi, Indonesian, Italian, Japanese, Korean, Portuguese, Russian, Turkish, Vietnamese, Chinese Simplified, and Chinese Traditional.
- OCR language aliases are easier to enter. For example, you can type ja, zh-CN, zh-TW, vi, fr, ar, or a full Tesseract code such as jpn+eng.
- The GUI keeps profiles and restores the last session state, making it easier to resume large document batches.
- Sortable tables, search, preview, quick-open actions, and right-click actions make output review faster.

## Supported translation languages

Use `auto` only for the source language.

| Code | Language | Suggested OCR value |
|---|---|---|
| ar | Arabic | `ara+eng` |
| de | German | `deu+eng` |
| en | English | `eng` |
| es | Spanish | `spa+eng` |
| fr | French | `fra+eng` |
| hi | Hindi | `hin+eng` |
| id | Indonesian | `ind+eng` |
| it | Italian | `ita+eng` |
| ja | Japanese | `jpn+eng` |
| ko | Korean | `kor+eng` |
| pt | Portuguese | `por+eng` |
| ru | Russian | `rus+eng` |
| tr | Turkish | `tur+eng` |
| vi | Vietnamese | `vie+eng` |
| zh-CN | Chinese (Simplified) | `chi_sim+eng` |
| zh-TW | Chinese (Traditional) | `chi_tra+eng` |

## Recommended support apps

- Tesseract OCR is recommended for scanned PDFs and image-heavy pages.
- LibreOffice is recommended for legacy Office files such as .doc, .xls, .ppt, .rtf, .odt, .ods, and .odp.
- Calibre is recommended for ebook formats such as AZW, MOBI, PRC, FB2, and LIT.
- An internet connection is required when using deep_translator / GoogleTranslator.

## Suggested app placement

Place Tesseract in a nearby Apps folder when possible, for example:

`../Apps/Tesseract5.5.0/tesseract.exe`

`../Apps/Tesseract5.5.0/tessdata`



LibreOffice and Calibre can be installed normally and discovered from the system PATH. On Windows, standard installation folders also work.

## Supported input formats

| Category | Extensions | Notes |
|---|---|---|
| Direct extraction | .pdf, .docx, .pptx, .xlsx, .xlsm, .xltx, .xltm, .epub, .html, .htm, .xhtml, .shtml, .md, .markdown, .mdown, .txt, .text, .csv, .tsv, .log, .json, .xml, .yaml, .yml | Reads content directly. |
| Best via Calibre | .azw, .azw3, .azw4, .mobi, .prc, .fb2, .lit | Converted to EPUB first with ebook-convert. |
| Best via LibreOffice | .doc, .rtf, .odt, .xls, .ods, .ppt, .odp | Converted first, then extracted. |

## How to use the GUI

1. **Launch**: Run python translator_docs_book_v5_gui_g20_vi.py --gui, or open the packaged EXE if you have already built it.
2. **Choose input and output**: Select one file or a whole folder. Then choose the output root folder where translated projects will be stored.
3. **Select languages**: Set Source Lang and Target Lang. Use auto for mixed or unknown source language. For Vietnamese output, select vi.
4. **Set OCR**: Use OCR Mode = auto for mixed digital PDFs, OCR Mode = all for image scans, or OCR Mode = off for born-digital documents.
5. **Set OCR language**: You can enter ja, zh-CN, zh-TW, vi, fr, ar, or a compound code such as jpn+eng. This is especially important for scanned books or pharmacopeia pages.
6. **Start processing**: Press Start. The queue, log, document table, and file table help you monitor progress.
7. **Review results**: Open bilingual.md, target_only.md, full_target.txt, translation_bundle.json, or translation_report.json from the right-click menu or by double-clicking rows.
8. **Resume safely**: Profiles save settings. The application also restores the last session state, so large jobs can be resumed more comfortably.

## GUI productivity tips

- F1 opens Help.
- Double-click rows to open files or folders.
- Right-click tables for quick actions such as Open File, Open Folder, Open Manifest, Open bilingual.md, and Open translation report.
- Click table headers to sort.
- Use the search box to filter queue and output lists.

## How to use the CLI

The CLI is best when you want consistent batch processing, scheduled runs, or reusable commands.

**Launch GUI**

```bash
python translator_docs_book_v5_gui_g20_vi.py --gui
```

**Translate a whole folder to Vietnamese**

```bash
python translator_docs_book_v5_g20_vi.py "D:\InputBooks" --out "D:\Translated" --ocr auto --source-lang auto --target-lang vi
```

**Translate a Japanese PDF to English using full OCR**

```bash
python translator_docs_book_v5_g20_vi.py "D:\Books\jp_book.pdf" --out "D:\Translated" --ocr all --ocr-lang ja --source-lang ja --target-lang en
```

**Translate a Chinese scan to Vietnamese**

```bash
python translator_docs_book_v5_g20_vi.py "D:\Books\cn_scan.pdf" --out "D:\Translated" --ocr all --ocr-lang zh-CN --source-lang zh-CN --target-lang vi
```

**Show runtime OCR detection**

```bash
python translator_docs_book_v5_g20_vi.py --show-tesseract-info
```

**Print supported formats and languages**

```bash
python translator_docs_book_v5_g20_vi.py --list-supported-formats
```

## Choosing OCR correctly

- Use OCR Mode = auto when the file may contain both selectable text and scanned pages.
- Use OCR Mode = all for scanned SmPC, PIL, pharmacopeia scans, Japanese PDFs, Chinese scans, or photographed pages.
- Use OCR Mode = off for clean born-digital DOCX, HTML, Markdown, TXT, and many searchable PDFs.
- For Japanese, use ja or jpn+eng. For Simplified Chinese, use zh-CN or chi_sim+eng. For Traditional Chinese, use zh-TW or chi_tra+eng. For Vietnamese, use vi or vie+eng.

## What the output folder contains

| Folder | Purpose |
|---|---|
| 01_source | Original file copy (when Copy original file is enabled). |
| 02_extracted | Raw extracted source text and extracted_document.json. |
| 03_translation | full_target.txt, bilingual.md, target_only.md, translation_bundle.json. |
| 04_indexes | Segment index and translation memory, if enabled. |
| 08_logs | translation_log.csv and batch logs. |
| 09_reports | translation_report.json and manifest metadata. |

## Best-practice workflows

- Japanese SmPC or scanned pharmacopeia to English: OCR Mode = all, OCR Lang = ja, Source Lang = ja, Target Lang = en.
- Chinese scanned regulatory pages to Vietnamese: OCR Mode = all, OCR Lang = zh-CN or zh-TW, Source Lang = zh-CN or zh-TW, Target Lang = vi.
- French or German PIL to Vietnamese: OCR Mode = auto for searchable PDF, or all for scans. Set Source Lang = fr or de, Target Lang = vi.
- Mixed folders with many file types: use Source Lang = auto, Target Lang = your preferred language, and keep OCR Mode = auto unless the folder is mostly image scans.

## Troubleshooting

- No OCR text appears: verify Tesseract installation and run --show-tesseract-info.
- Legacy Office files fail: install LibreOffice and ensure soffice is available.
- AZW or MOBI cannot be processed: install Calibre so ebook-convert is available.
- Translation fails intermittently: increase Retries and Retry Delay, and keep the internet connection stable.
- Wrong OCR language reduces quality dramatically: change OCR Lang to match the source script.

*For production work, always inspect bilingual.md, target_only.md, and translation_report.json before publishing or reusing the translated content.*
