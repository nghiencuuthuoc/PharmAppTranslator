# End-User Guide – translator_docs_book_v5.exe

**Document version:** 1.0  
**Audience:** Windows end users  
**Purpose:** run batch document translation with the `translator_docs_book_v5.exe` command-line executable

---

## 1. Overview

`translator_docs_book_v5.exe` is a batch-oriented document translation tool. It can accept **a single file** or **an input folder**, extract content, perform OCR when needed, translate into a target language, and export a structured output package with translated text, bilingual output, logs, indexes, and reports.

### Common file groups
- PDF
- Word (`.docx`)
- PowerPoint (`.pptx`)
- Excel (`.xlsx`)
- EPUB / ebook
- HTML / Markdown / TXT / CSV / JSON / XML / YAML

### Typical use cases
- Batch translation of technical or regulatory document sets
- Pharmacopoeia, submission dossiers, SMPC/PIL packages
- Internal review packages with traceable output
- QA-oriented runs with logs and segment-level reports

---

## 2. Requirements

### Operating system
- Windows 10 or Windows 11

### How to run in PowerShell
If you are already in the folder that contains the EXE, use:

```powershell
.\translator_docs_book_v5.exe
```

> In PowerShell, do not rely on `translator_docs_book_v5.exe` alone when the file is in the current directory.

### Supporting components
- **Tesseract OCR**: required for scanned or image-based PDFs
- **LibreOffice**: useful for some legacy Office formats
- **Calibre**: useful for some extended ebook formats

If your software package already bundles these components, no extra setup is needed. Otherwise, ask your deployment or support team to install them.

---

## 3. Basic syntax

```powershell
.\translator_docs_book_v5.exe "INPUT_PATH" --out "OUTPUT_PATH"
```

Where:
- `INPUT_PATH`: path to **a file** or **a folder**
- `--out`: root folder for all generated output

### Minimal example
```powershell
.\translator_docs_book_v5.exe "D:\Input" --out "D:\Output"
```

---

## 4. Quick-start scenarios

### 4.1. Translate a mixed PDF/Office folder into Vietnamese
```powershell
.\translator_docs_book_v5.exe "D:\Regulatory\Input" --out "D:\Regulatory\Output_VI" --ocr auto --source-lang auto --target-lang vi
```

### 4.2. Translate scanned Chinese PDFs into Vietnamese
```powershell
.\translator_docs_book_v5.exe "D:\ChineseDocs" --out "D:\ChineseDocs_VI" --ocr all --ocr-lang chi_sim+eng --source-lang zh-CN --target-lang vi
```

### 4.3. Translate scanned Japanese PDFs into English
```powershell
.\translator_docs_book_v5.exe "D:\JP_PDF" --out "D:\JP_PDF_EN" --ocr all --ocr-lang jpn+eng --source-lang ja --target-lang en
```

### 4.4. Test only the first three files
```powershell
.\translator_docs_book_v5.exe "D:\LargeInput" --out "D:\TestOutput" --max-files 3 --ocr auto --source-lang auto --target-lang vi
```

### 4.5. Extract only, no translation
```powershell
.\translator_docs_book_v5.exe "D:\Input" --out "D:\ExtractOnly" --translator none
```

---

## 5. Most important options

### 5.1. Input and output

| Option | Meaning | When to use it |
|---|---|---|
| `input_path` | Source file or folder | Required for real processing |
| `--out` | Output root folder | Required for real processing |
| `--flat` | Do not scan subfolders recursively | Use when you want the current level only |
| `--max-files N` | Process only the first N files | Use for quick testing |
| `--no-copy-original` | Do not copy the original file into the output structure | Use to save disk space |

### 5.2. OCR

| Option | Meaning | Recommendation |
|---|---|---|
| `--ocr off` | Disable OCR | Use only for text-based PDFs |
| `--ocr auto` | OCR only when needed | Safest choice for most runs |
| `--ocr all` | OCR every page | Use for scanned PDFs |
| `--ocr-lang ...` | OCR language pack | Example: `chi_sim+eng`, `chi_tra+eng`, `jpn+eng` |
| `--ocr-min-native-chars N` | Threshold for low native text detection | Advanced usage |
| `--tesseract-exe` | Path to `tesseract.exe` | Use when you must point to a specific install |
| `--tessdata-dir` | Path to `tessdata` | Use when you must point to a specific install |

### 5.3. Translation

| Option | Meaning | Recommendation |
|---|---|---|
| `--translator deep_translator` | Use the default translator backend | Standard choice |
| `--translator none` | Skip translation and keep only extraction/output flow | Useful for extraction tests |
| `--source-lang` | Source language | `auto`, `zh-CN`, `zh-TW`, `ja`, `en`, `vi`, etc. |
| `--target-lang` | Target language | Example: `vi`, `en` |
| `--sleep-seconds` | Delay between translation chunks | Default is usually sufficient |
| `--retries` | Number of retry attempts | Increase if the service is unstable |
| `--retry-delay` | Delay between retries | Use together with `--retries` |
| `--max-chunk-chars` | Maximum chunk length | Change only for advanced tuning |
| `--keep-source-on-error` | Keep source text when translation fails | Helpful for QA review |

### 5.4. Reuse, skip, or force reprocessing

| Option | Meaning |
|---|---|
| `--overwrite-translation` | Ignore old translations and translate everything again |
| `--no-skip-existing` | Process documents even if a previous run marked them complete |
| `--retranslate-errors-only` | Retry only failed segments |
| `--no-reuse-extraction` | Re-extract content instead of using cached extraction |

### 5.5. Inspection and environment checks

| Option | Meaning |
|---|---|
| `--show-config` | Print the parsed runtime configuration and exit |
| `--list-supported-formats` | Print supported extensions and exit |
| `--show-tesseract-info` | Print Tesseract runtime information and exit |

---

## 6. Output structure

Each input document typically gets its own document folder inside `OUTPUT_PATH`. Common generated artifacts include:

- `01_source` – original file copy
- `02_extracted/extracted_document.json` – structured extracted data
- `02_extracted/full_source.txt` – full extracted source text
- `03_translation/translation_bundle.json` – segment-level translation bundle
- `03_translation/full_target.txt` – full translated output
- `03_translation/bilingual.md` – bilingual output
- `03_translation/target_only.md` – target-only output
- `04_indexes/segment_index.csv` – segment index
- `04_indexes/translation_memory.csv` – translation memory
- `08_logs/translation_log.csv` – detailed translation log
- `09_reports/translation_report.json` – per-document report
- `manifest.json` – document metadata
- `batch_summary.json` – batch-level summary

### Which files to check first
1. `batch_summary.json` – overall processed / skipped / failed counts
2. `09_reports/translation_report.json` – document-level details
3. `08_logs/translation_log.csv` – segment-level problems
4. `03_translation/bilingual.md` – quick human-readable review output

---

## 7. Recommended end-user workflow

### Step 1 – Prepare the input folder
- Place source documents in a clean folder
- Split by project or language if needed
- Avoid extremely long paths or unusual special characters

### Step 2 – Run a small pilot first
Use `--max-files 3` or a small subfolder before a full batch.

### Step 3 – Pick the right OCR mode
- Text PDF: `--ocr off` or `--ocr auto`
- Scanned PDF: `--ocr all`
- Mixed / unsure: `--ocr auto`

### Step 4 – Run the full batch
Once the pilot looks good, remove `--max-files` and run the full folder.

### Step 5 – Review the report and bilingual output
Open `batch_summary.json`, `translation_report.json`, `bilingual.md`, and `translation_log.csv`.

---

## 8. Suggested scenario presets

### Scenario A – Chinese pharmacopoeia, scanned PDF
Recommended:
- `--ocr all`
- `--ocr-lang chi_sim+eng`
- `--source-lang zh-CN`
- `--target-lang vi`

### Scenario B – Japanese SMPC/PIL package
Recommended:
- `--ocr auto` or `--ocr all`
- `--ocr-lang jpn+eng`
- `--source-lang ja`
- `--target-lang en`

### Scenario C – Internal Word/PowerPoint/Excel package
Recommended:
- `--ocr off` or `--ocr auto`
- `--source-lang auto`
- `--target-lang vi`

### Scenario D – QA / error follow-up
Recommended:
- `--keep-source-on-error`
- `--retranslate-errors-only`

---

## 9. Troubleshooting

### 9.1. PowerShell says the EXE is not recognized
Most common cause: you did not prefix the file with `.\`.

Correct:
```powershell
.\translator_docs_book_v5.exe
```

### 9.2. OCR output is poor or empty
- Check whether you are using `--ocr off`
- Check whether Tesseract is available
- Run `--show-tesseract-info`
- Try `--ocr all`

### 9.3. Some files are skipped
A previous run may have already marked those documents as complete. Try:
```powershell
.\translator_docs_book_v5.exe "D:\Input" --out "D:\Output" --overwrite-translation --no-skip-existing
```

### 9.4. Retry only failed parts
```powershell
.\translator_docs_book_v5.exe "D:\Input" --out "D:\Output" --retranslate-errors-only
```

### 9.5. Inspect the resolved runtime config before processing
```powershell
.\translator_docs_book_v5.exe "D:\Input" --out "D:\Output" --ocr auto --source-lang auto --target-lang vi --show-config
```

---

## 10. Recommended command templates

### Template 1 – Translate a folder into Vietnamese
```powershell
.\translator_docs_book_v5.exe "D:\Input" --out "D:\Output_VI" --ocr auto --source-lang auto --target-lang vi
```

### Template 2 – Translate scanned Chinese PDFs into Vietnamese
```powershell
.\translator_docs_book_v5.exe "D:\ChinesePDF" --out "D:\ChinesePDF_VI" --ocr all --ocr-lang chi_sim+eng --source-lang zh-CN --target-lang vi
```

### Template 3 – Translate scanned Japanese PDFs into English
```powershell
.\translator_docs_book_v5.exe "D:\JapanesePDF" --out "D:\JapanesePDF_EN" --ocr all --ocr-lang jpn+eng --source-lang ja --target-lang en
```

### Template 4 – Pilot run on the first five files
```powershell
.\translator_docs_book_v5.exe "D:\LargeBatch" --out "D:\LargeBatch_Test" --max-files 5 --ocr auto --source-lang auto --target-lang vi
```

### Template 5 – List supported formats
```powershell
.\translator_docs_book_v5.exe --list-supported-formats
```

### Template 6 – Check Tesseract runtime info
```powershell
.\translator_docs_book_v5.exe --show-tesseract-info
```

---

## 11. Operational recommendations

- Always start with a small pilot run
- For scanned PDFs, prefer `--ocr all` when the extracted text quality is poor
- For very large folders, split by project or language
- Always review `batch_summary.json` after each batch
- Use `bilingual.md` for quick quality checks
- Keep indexes and logs enabled unless you have a specific reason to disable them

---

## 12. Internal support handoff checklist

When opening a support ticket or escalation, include:
- the exact command you ran
- `batch_summary.json`
- `translation_report.json`
- `translation_log.csv`
- one or two representative source files
- a screenshot of the error if available

---

## Appendix A – Full option list

```text
input_path
--out
--flat
--max-files
--no-copy-original
--ocr {auto,off,all}
--ocr-lang
--ocr-min-native-chars
--translator {deep_translator,none}
--source-lang
--target-lang
--overwrite-translation
--no-skip-existing
--retranslate-errors-only
--keep-source-on-error
--sleep-seconds
--retries
--retry-delay
--max-chunk-chars
--folder-style {auto,hash12,plain}
--tesseract-exe
--tessdata-dir
--show-tesseract-info
--list-supported-formats
--show-config
--no-reuse-extraction
--no-write-indexes
--no-write-translation-memory
```

---

## Appendix B – Best first-run command

```powershell
.\translator_docs_book_v5.exe "D:\Input" --out "D:\Output" --ocr auto --source-lang auto --target-lang vi
```
