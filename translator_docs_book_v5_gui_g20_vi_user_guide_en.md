# User Guide - translator_docs_book_v5_gui_g20_vi.exe

*English edition*

## Overview

translator_docs_book_v5_gui_g20_vi.exe is a desktop GUI for extracting text from books and office documents, translating the extracted content, and organizing the results into a structured output folder.

The updated G20 + Vietnamese build is intended to work with these translation choices: Arabic, Chinese (Simplified), Chinese (Traditional), English, French, German, Hindi, Indonesian, Italian, Japanese, Korean, Portuguese, Russian, Spanish, Turkish, and Vietnamese.

The application supports a queue-based workflow, saved profiles, automatic state restore, searchable document lists, preview, logs, sortable tables, and right-click shortcuts for quickly opening outputs.

## Where to place the EXE and helper apps

For the smoothest experience, keep the EXE in your app or release folder and prepare helper tools like this:

- **Tesseract OCR:** Recommended for scanned PDFs. The app looks for a common relative layout such as ../Apps/Tesseract5.5.0/tesseract.exe and ../Apps/Tesseract5.5.0/tessdata.

- **LibreOffice:** Recommended for legacy Office files such as .doc, .xls, .ppt, .odt, .ods, .odp, and .rtf.

- **Calibre:** Recommended for ebook formats such as .azw, .mobi, and related formats.

The EXE can still be used without every helper tool, but OCR and some conversions will be limited.

## Supported input formats

The program can process multiple document families. Practical support can be grouped as follows:

| Category | Formats |
| --- | --- |
| Direct text extraction | .txt, .csv, .tsv, .json, .xml, .yaml, .html, .htm, .md, .docx, .pptx, .xlsx, .epub, .pdf |
| Best-effort with Calibre | .azw, .azw3, .azw4, .mobi, .prc, .fb2, .lit |
| Best-effort with LibreOffice | .doc, .rtf, .odt, .xls, .ods, .ppt, .odp |

## Quick start

1. Launch translator_docs_book_v5_gui_g20_vi.exe.

1. Choose UI Language and Appearance if needed.

1. Set Output Path.

1. Add one or more files, or add a whole folder.

1. Choose Translator, Source Lang, Target Lang, OCR Mode, and OCR Lang.

1. Click Start.

1. Watch the Log tab during processing.

1. After completion, click Refresh and review results in Documents, Files, and Preview.

1. Use Open Output to open the output root folder.

## Main workflow in the GUI

The GUI is designed for batch-oriented document translation, with the queue on the front end and processed outputs on the review side.

### Input Queue

The input queue supports both files and folders.

The table can be sorted by clicking column headers.

The search box filters queue items by name or path.

Double-click opens the selected file or folder.

Right-click provides quick actions such as open, open parent, copy path, copy name, and remove selected.

### Settings

| Setting | What it does |
| --- | --- |
| Translator | Select the translation engine. "deep_translator" is the normal translation mode; "none" is useful for extraction-only testing. |
| Source Lang | Choose the document source language, or use auto when unsure. |
| Target Lang | Choose the output language. This build is aimed at G20 languages plus Vietnamese. |
| OCR Mode | off = do not OCR; auto = OCR pages with very little native text; all = OCR all PDF pages. |
| OCR Lang | Enter the Tesseract OCR code, for example jpn+eng, chi_sim+eng, chi_tra+eng, kor+eng, rus+eng, ara+eng, vie+eng. |
| Folder Style | auto keeps compatibility with existing outputs, hash12 creates safer unique folders, plain uses only the source name. |
| Retries / Retry Delay | Used when translation requests fail temporarily. |
| Max Chunk Chars | Controls how much text is sent per translation chunk. Lower values may be safer for unstable jobs. |
| Skip complete docs | Skips documents that already have a complete manifest and translation outputs. |
| Overwrite translation | Forces the app to replace existing translations. |
| Retranslate errors only | Keeps successful segments and only retries failed ones. |
| Copy original file | Copies the input file into 01_source for traceability. |
| Recursive scan | When a folder is added, include supported files from subfolders. |

### Profiles and last-session restore

Profiles save both translation settings and UI preferences.

You can load, save, save as, clone, and delete profiles.

The app also saves the last session state, including window layout, selected profile, queue items, search text, and the last active tab, then restores that state the next time you open the application.

### Search, Documents, Files, Preview, and Log

Search filters the input queue, processed documents, and output files.

Documents shows each processed document folder with status, segment count, errors, and modification time.

Files lists every generated file inside the selected document folder.

Preview shows text previews for textual outputs such as JSON, Markdown, and TXT.

Log shows runtime progress and failures.

Right-click on the processed document list to open the document folder directly or jump to key files such as manifest.json, bilingual.md, target_only.md, full_target.txt, full_source.txt, translation_bundle.json, and translation_report.json.

### Recommended OCR combinations

| Document type | Recommended setup |
| --- | --- |
| Japanese scan | Source: ja | OCR Lang: jpn+eng | Typical targets: en or vi |
| Chinese Simplified scan | Source: zh-CN | OCR Lang: chi_sim+eng | Typical targets: en or vi |
| Chinese Traditional scan | Source: zh-TW | OCR Lang: chi_tra+eng | Typical targets: en or vi |
| Korean scan | Source: ko | OCR Lang: kor+eng | Typical targets: en or vi |
| Russian scan | Source: ru | OCR Lang: rus+eng | Typical targets: en or vi |
| Arabic scan | Source: ar | OCR Lang: ara+eng | Typical targets: en or vi |
| Hindi scan | Source: hi | OCR Lang: hin+eng | Typical targets: en or vi |
| Vietnamese scan | Source: vi | OCR Lang: vie+eng | Typical targets: en or vi |
| French / German / Spanish / Italian / Portuguese / Turkish / Indonesian | Use the matching source language and install the correct Tesseract language pack when OCR is needed. |

## Output structure

Each processed source file is written into its own document folder. The folder name may be plain, hashed, or auto-managed depending on Folder Style.

```text
output_root/
  batch_summary_gui.json
  <document_folder>/
    manifest.json
    01_source/
    02_extracted/
      extracted_document.json
      full_source.txt
    03_translation/
      translation_bundle.json
      full_target.txt
      bilingual.md
      target_only.md
    04_indexes/
      segment_index.csv
      segment_index.jsonl
      translation_memory.csv
    08_logs/
      translation_log.csv
    09_reports/
      translation_report.json
```

### What each folder and file is for

manifest.json: main processing summary, including source file, source hash, source and target language, OCR settings, segment counts, and final document status.

01_source: optional copy of the original file.

02_extracted/extracted_document.json: structured extracted content by segment.

02_extracted/full_source.txt: concatenated source text for review.

03_translation/translation_bundle.json: per-segment bilingual data, status, and metadata.

03_translation/full_target.txt: concatenated target text.

03_translation/bilingual.md: bilingual Markdown output.

03_translation/target_only.md: target-language Markdown output.

04_indexes: searchable segment indexes and translation memory CSV.

08_logs/translation_log.csv: low-level segment translation log.

09_reports/translation_report.json: error-focused summary report.

batch_summary_gui.json: summary file for the entire run, saved in the output root.

## Practical recommendations

- Use auto source detection only when you are unsure. If you know the source language, selecting it explicitly is usually cleaner.

- For scanned PDFs, prefer OCR Mode = auto first. Use all only when the native PDF text is poor.

- Keep Copy original file enabled when traceability matters.

- Keep Skip complete docs enabled for incremental reruns.

- Use Retranslate errors only when a previous run already completed most segments successfully.

- After a run, review manifest.json, translation_report.json, bilingual.md, and full_target.txt before publishing or reusing translated material.

## Troubleshooting

### OCR did not work

Check that Tesseract is installed and that the required language data exists in tessdata. For example, Japanese OCR needs jpn, Vietnamese OCR needs vie, Chinese Simplified OCR needs chi_sim, and Arabic OCR needs ara.

### Some files do not open or convert well

Install LibreOffice for old Office formats and Calibre for ebook formats.

### A document is skipped unexpectedly

This usually means the app detected an already completed document folder. Disable Skip complete docs or enable Overwrite translation if you want to force regeneration.

### Preview is empty for some files

The Preview tab is mainly for text-like outputs. Binary files should be opened directly from the Files tab or the document context menu.
