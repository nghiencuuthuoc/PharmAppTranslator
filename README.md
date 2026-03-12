# PharmApp Translator

Desktop translation tools for books, scientific papers, Office files, and multilingual document packages.

PharmApp Translator is a practical Windows-first toolkit built for users who need to process large document collections with a clear workflow:

1. **Translate source documents** with **Translator Docs Book v5 GUI**
2. **Review completed translation packages** with **Translation Package Viewer v7**

This repository is intended to host the **release assets** for the ready-to-run `.exe` applications.

---

## Included apps

### 1) Translator Docs Book v5 GUI
Use this app to:
- add files or folders to a processing queue
- choose input and output locations
- run OCR when needed
- translate supported documents into structured translation packages
- save and reload work profiles
- resume from previous working state
- monitor progress through document tables and logs

### 2) Translation Package Viewer v7
Use this app to:
- open completed translation-package folders
- scan a translation library root
- review source and target text side by side
- search documents and segments
- inspect QA flags and issue counts
- copy AI review / fix prompts for selected segments
- save profiles and restore the previous workspace state

---

## Main features

- Ready-to-run **Windows EXE** workflow
- **English / Vietnamese** UI
- **Light / Dark / System** appearance
- **Profiles** for reusable settings
- **Resume / restore previous session** support
- **Sortable tables** and multi-pane layout
- Queue-based batch processing
- Document review and QA workflow
- Side-by-side bilingual reading modes
- Search across documents and translated segments

---

## Recommended release assets

For GitHub Releases, a clean package can look like this:

```text
PharmAppTranslator_Release/
├─ translator_docs_book_v5_gui.exe
├─ translator_docs_book_viewer_v7_gui.exe
├─ README.md
├─ README.vi.md
└─ Apps/
   └─ Tesseract5.5.0/
      ├─ tesseract.exe
      └─ tessdata/
```

You may also publish separate ZIP files if preferred:

- `PharmAppTranslator_vX.Y_win64.zip`
- `Apps_Tesseract5.5.0_portable.zip`

---

## Helper apps placement for EXE releases

### Tesseract OCR
If users want OCR support for scanned PDFs or image-based pages, place Tesseract in a nearby `Apps` folder.

Recommended layout:

```text
Release/
├─ translator_docs_book_v5_gui.exe
├─ translator_docs_book_viewer_v7_gui.exe
└─ ../Apps/Tesseract5.5.0/
```

In practice, the easiest portable layout is:

```text
MyTranslatorSuite/
├─ Run/
│  ├─ translator_docs_book_v5_gui.exe
│  └─ translator_docs_book_viewer_v7_gui.exe
└─ Apps/
   └─ Tesseract5.5.0/
      ├─ tesseract.exe
      └─ tessdata/
```

This makes it easier for the EXE build to detect Tesseract without extra manual setup.

### Calibre
Install Calibre if users need support for ebook formats such as Kindle / MOBI-family files.

### LibreOffice
Install LibreOffice if users need conversion support for older Office formats before translation.

---

## Supported input types

The release is designed for practical document translation workflows, including common formats such as:

- PDF
- DOCX
- PPTX
- XLSX
- EPUB
- HTML / HTM
- Markdown
- TXT / CSV / TSV / JSON / XML / YAML

Some legacy Office and ebook formats may require external helper applications.

---

## Quick start

### Step 1 — Prepare the release folder
Download the release assets and keep the two `.exe` files together.

If OCR is needed, place **Tesseract** inside the recommended `Apps/Tesseract5.5.0/` folder.

### Step 2 — Run the translator
Open `translator_docs_book_v5_gui.exe`.

Basic workflow:
1. Set **Input Path**
2. Set **Output Path**
3. Add files or folders
4. Choose translator, source language, target language, and OCR mode
5. Click **Start**

### Step 3 — Review the results
Open `translator_docs_book_viewer_v7_gui.exe`.

Basic workflow:
1. Set **Library root** to the translated output folder
2. Click **Scan**
3. Select a document
4. Review segments in side-by-side mode
5. Use Search and QA tabs to inspect issues

---

## Typical output package

Each translated document can generate a structured package containing files such as:

- source copy
- extracted text
- bilingual output
- target-only output
- translation bundle JSON
- logs
- reports
- manifest file

This makes the release suitable not only for translation, but also for auditing, review, and long-term archive workflows.

---

## Best use cases

- scientific articles
- books and manuals
- technical PDFs
- multilingual research documents
- internal review workflows
- translation QA and verification

---

## Video

Demo / presentation:

- YouTube: https://youtu.be/KZjima0vD2A

---

## Notes for GitHub release publishing

Suggested release title:

```text
PharmApp Translator v1.0 - Windows EXE Release
```

Suggested short release description:

```text
Portable Windows release of Translator Docs Book v5 GUI and Translation Package Viewer v7 for document translation, package review, search, and QA.
```

Suggested release assets:

- `translator_docs_book_v5_gui.exe`
- `translator_docs_book_viewer_v7_gui.exe`
- `README.md`
- `README.vi.md`
- optional `Apps/` helper package

---

## Website and project links

- https://www.nghiencuuthuoc.com
- https://www.pharmapp.dev

---

## License

Add the project license here before public release.

