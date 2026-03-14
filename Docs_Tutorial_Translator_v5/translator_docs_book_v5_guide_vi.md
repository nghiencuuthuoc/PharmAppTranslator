# Hướng dẫn khách hàng cuối – translator_docs_book_v5.exe

**Phiên bản tài liệu:** 1.0  
**Đối tượng:** người dùng cuối trên Windows  
**Mục tiêu:** dịch hàng loạt tài liệu bằng tệp thực thi dòng lệnh `translator_docs_book_v5.exe`

---

## 1. Tổng quan

`translator_docs_book_v5.exe` là công cụ dịch tài liệu đa định dạng theo lô. Công cụ có thể nhận **một tệp** hoặc **một thư mục**, trích xuất nội dung, OCR khi cần, dịch sang ngôn ngữ đích và xuất ra bộ kết quả gồm văn bản đích, bản song ngữ, log và báo cáo.

### Các nhóm định dạng thường dùng
- PDF
- Word (`.docx`)
- PowerPoint (`.pptx`)
- Excel (`.xlsx`)
- EPUB / ebook
- HTML / Markdown / TXT / CSV / JSON / XML / YAML

### Khi nào nên dùng công cụ này
- Dịch cả thư mục tài liệu kỹ thuật hoặc pháp lý
- Dịch dược điển, hồ sơ đăng ký, SMPC/PIL
- Tạo bản dịch hàng loạt để rà soát nội bộ
- Lưu lại log, chỉ mục và báo cáo cho QA

---

## 2. Điều kiện sử dụng

### Hệ điều hành
- Windows 10 hoặc Windows 11

### Cách chạy trong PowerShell
Nếu bạn đang đứng trong đúng thư mục chứa file EXE, hãy dùng:

```powershell
.\translator_docs_book_v5.exe
```

> Trong PowerShell, không nên gõ trần `translator_docs_book_v5.exe` khi file nằm ở thư mục hiện tại.

### Thành phần bổ trợ
- **Tesseract OCR**: cần thiết khi tài liệu PDF là dạng scan hoặc ảnh
- **LibreOffice**: hữu ích cho một số định dạng Office cũ
- **Calibre**: hữu ích cho một số định dạng ebook mở rộng

Nếu gói phát hành của nhà cung cấp đã đóng kèm các thành phần này thì bạn chỉ cần dùng. Nếu không, hãy nhờ bộ phận triển khai cài đặt.

---

## 3. Cú pháp cơ bản

```powershell
.\translator_docs_book_v5.exe "INPUT_PATH" --out "OUTPUT_PATH"
```

Trong đó:
- `INPUT_PATH`: đường dẫn tới **một file** hoặc **một thư mục**
- `--out`: thư mục gốc để lưu toàn bộ kết quả

### Ví dụ tối thiểu
```powershell
.\translator_docs_book_v5.exe "D:\Input" --out "D:\Output"
```

---

## 4. Khởi động nhanh theo tình huống

### 4.1. Dịch thư mục PDF/Office sang tiếng Việt
```powershell
.\translator_docs_book_v5.exe "D:\Regulatory\Input" --out "D:\Regulatory\Output_VI" --ocr auto --source-lang auto --target-lang vi
```

### 4.2. Dịch PDF scan tiếng Trung sang tiếng Việt
```powershell
.\translator_docs_book_v5.exe "D:\ChineseDocs" --out "D:\ChineseDocs_VI" --ocr all --ocr-lang chi_sim+eng --source-lang zh-CN --target-lang vi
```

### 4.3. Dịch PDF scan tiếng Nhật sang tiếng Anh
```powershell
.\translator_docs_book_v5.exe "D:\JP_PDF" --out "D:\JP_PDF_EN" --ocr all --ocr-lang jpn+eng --source-lang ja --target-lang en
```

### 4.4. Chạy thử 3 file đầu tiên
```powershell
.\translator_docs_book_v5.exe "D:\LargeInput" --out "D:\TestOutput" --max-files 3 --ocr auto --source-lang auto --target-lang vi
```

### 4.5. Chỉ trích xuất, không dịch
```powershell
.\translator_docs_book_v5.exe "D:\Input" --out "D:\ExtractOnly" --translator none
```

---

## 5. Các tham số quan trọng nhất

### 5.1. Đầu vào và đầu ra

| Tham số | Ý nghĩa | Khi nên dùng |
|---|---|---|
| `input_path` | File hoặc thư mục nguồn | Luôn bắt buộc khi chạy thật |
| `--out` | Thư mục kết quả | Luôn bắt buộc khi chạy thật |
| `--flat` | Không quét thư mục con | Khi chỉ muốn xử lý cấp hiện tại |
| `--max-files N` | Chỉ xử lý N file đầu tiên | Dùng để test nhanh |
| `--no-copy-original` | Không copy file gốc vào thư mục kết quả | Dùng khi muốn tiết kiệm dung lượng |

### 5.2. OCR

| Tham số | Ý nghĩa | Gợi ý |
|---|---|---|
| `--ocr off` | Tắt OCR | Chỉ dùng khi PDF có text thật |
| `--ocr auto` | OCR khi cần | Lựa chọn an toàn cho hầu hết trường hợp |
| `--ocr all` | OCR toàn bộ | Dùng cho PDF scan |
| `--ocr-lang ...` | Ngôn ngữ OCR | Ví dụ `chi_sim+eng`, `chi_tra+eng`, `jpn+eng` |
| `--ocr-min-native-chars N` | Ngưỡng phát hiện text native quá ít | Dùng nâng cao |
| `--tesseract-exe` | Đường dẫn `tesseract.exe` | Khi cần chỉ định rõ |
| `--tessdata-dir` | Thư mục `tessdata` | Khi cần chỉ định rõ |

### 5.3. Dịch

| Tham số | Ý nghĩa | Gợi ý |
|---|---|---|
| `--translator deep_translator` | Dùng bộ dịch mặc định | Thường dùng |
| `--translator none` | Không dịch, chỉ đi qua pipeline | Dùng để test trích xuất |
| `--source-lang` | Ngôn ngữ nguồn | `auto`, `zh-CN`, `zh-TW`, `ja`, `en`, `vi`... |
| `--target-lang` | Ngôn ngữ đích | Ví dụ `vi`, `en` |
| `--sleep-seconds` | Thời gian nghỉ giữa các chunk | Mặc định thường đủ |
| `--retries` | Số lần thử lại | Tăng khi mạng/bộ dịch không ổn định |
| `--retry-delay` | Thời gian chờ giữa lần thử | Dùng kèm `--retries` |
| `--max-chunk-chars` | Giới hạn độ dài mỗi chunk | Chỉ chỉnh khi có yêu cầu đặc biệt |
| `--keep-source-on-error` | Giữ nguyên text nguồn khi dịch lỗi | Hữu ích cho QA |

### 5.4. Chạy lại, bỏ qua hoặc ép dịch lại

| Tham số | Ý nghĩa |
|---|---|
| `--overwrite-translation` | Bỏ qua bản dịch cũ và dịch lại toàn bộ |
| `--no-skip-existing` | Vẫn xử lý dù tài liệu đã hoàn tất |
| `--retranslate-errors-only` | Chỉ dịch lại các đoạn lỗi |
| `--no-reuse-extraction` | Trích xuất lại từ đầu, không dùng dữ liệu cũ |

### 5.5. Kiểm tra cấu hình / môi trường

| Tham số | Ý nghĩa |
|---|---|
| `--show-config` | In cấu hình sau khi parse tham số rồi thoát |
| `--list-supported-formats` | In danh sách đuôi file hỗ trợ rồi thoát |
| `--show-tesseract-info` | In thông tin runtime của Tesseract rồi thoát |

---

## 6. Cấu trúc kết quả đầu ra

Mỗi tài liệu thường có một thư mục riêng trong `OUTPUT_PATH`. Bộ kết quả phổ biến gồm:

- `01_source` – bản sao file gốc
- `02_extracted/extracted_document.json` – dữ liệu trích xuất có cấu trúc
- `02_extracted/full_source.txt` – toàn bộ nội dung nguồn dạng text
- `03_translation/translation_bundle.json` – bản dịch theo từng segment
- `03_translation/full_target.txt` – toàn bộ nội dung đích
- `03_translation/bilingual.md` – bản song ngữ
- `03_translation/target_only.md` – bản đích
- `04_indexes/segment_index.csv` – chỉ mục segment
- `04_indexes/translation_memory.csv` – bộ nhớ dịch
- `08_logs/translation_log.csv` – log chi tiết
- `09_reports/translation_report.json` – báo cáo tài liệu
- `manifest.json` – siêu dữ liệu của tài liệu
- `batch_summary.json` – tóm tắt toàn bộ phiên chạy

### Nên kiểm tra file nào trước
1. `batch_summary.json` – xem tổng số file xử lý, fail, skip
2. `09_reports/translation_report.json` – xem chi tiết từng tài liệu
3. `08_logs/translation_log.csv` – xem segment nào lỗi
4. `03_translation/bilingual.md` – mở ra để kiểm tra nhanh chất lượng bản dịch

---

## 7. Quy trình sử dụng đề xuất cho khách hàng cuối

### Bước 1 – Chuẩn bị thư mục nguồn
- Đặt tài liệu vào một thư mục rõ ràng
- Tách riêng từng lô theo ngôn ngữ hoặc dự án nếu cần
- Tránh tên đường dẫn quá dài hoặc quá nhiều ký tự đặc biệt

### Bước 2 – Chạy thử trên số lượng nhỏ
Dùng `--max-files 3` hoặc chọn một thư mục con nhỏ để kiểm thử.

### Bước 3 – Chọn chế độ OCR phù hợp
- PDF text: `--ocr off` hoặc `--ocr auto`
- PDF scan: `--ocr all`
- Không chắc loại PDF: `--ocr auto`

### Bước 4 – Chạy thật trên toàn bộ lô
Sau khi kết quả thử đạt yêu cầu, bỏ `--max-files` và chạy toàn bộ.

### Bước 5 – Kiểm tra báo cáo và bản song ngữ
Mở `batch_summary.json`, `translation_report.json`, `bilingual.md` và `translation_log.csv`.

---

## 8. Các kịch bản gợi ý

### Kịch bản A – Dược điển tiếng Trung, PDF scan
Khuyến nghị:
- `--ocr all`
- `--ocr-lang chi_sim+eng`
- `--source-lang zh-CN`
- `--target-lang vi`

### Kịch bản B – SMPC/PIL tiếng Nhật
Khuyến nghị:
- `--ocr auto` hoặc `--ocr all`
- `--ocr-lang jpn+eng`
- `--source-lang ja`
- `--target-lang en`

### Kịch bản C – Bộ hồ sơ Word/PowerPoint/Excel nội bộ
Khuyến nghị:
- `--ocr off` hoặc `--ocr auto`
- `--source-lang auto`
- `--target-lang vi`

### Kịch bản D – Chạy QA hoặc rà lỗi
Khuyến nghị:
- `--keep-source-on-error`
- `--retranslate-errors-only`

---

## 9. Xử lý sự cố thường gặp

### 9.1. PowerShell báo không nhận ra tên EXE
Nguyên nhân thường gặp: chưa thêm `.\` trước tên file.

Đúng:
```powershell
.\translator_docs_book_v5.exe
```

### 9.2. Chạy nhưng kết quả OCR ít hoặc rỗng
- Kiểm tra bạn có đang dùng `--ocr off` không
- Kiểm tra Tesseract đã có sẵn chưa
- Thử `--show-tesseract-info`
- Thử `--ocr all`

### 9.3. Một số file bị bỏ qua
Có thể tài liệu đã được đánh dấu hoàn tất ở lần chạy trước. Thử:
```powershell
.\translator_docs_book_v5.exe "D:\Input" --out "D:\Output" --overwrite-translation --no-skip-existing
```

### 9.4. Chỉ muốn dịch lại phần lỗi
```powershell
.\translator_docs_book_v5.exe "D:\Input" --out "D:\Output" --retranslate-errors-only
```

### 9.5. Muốn xem cấu hình thực tế trước khi chạy
```powershell
.\translator_docs_book_v5.exe "D:\Input" --out "D:\Output" --ocr auto --source-lang auto --target-lang vi --show-config
```

---

## 10. Bộ lệnh mẫu khuyến nghị

### Mẫu 1 – Dịch toàn bộ thư mục sang tiếng Việt
```powershell
.\translator_docs_book_v5.exe "D:\Input" --out "D:\Output_VI" --ocr auto --source-lang auto --target-lang vi
```

### Mẫu 2 – Dịch PDF scan tiếng Trung sang tiếng Việt
```powershell
.\translator_docs_book_v5.exe "D:\ChinesePDF" --out "D:\ChinesePDF_VI" --ocr all --ocr-lang chi_sim+eng --source-lang zh-CN --target-lang vi
```

### Mẫu 3 – Dịch PDF scan tiếng Nhật sang tiếng Anh
```powershell
.\translator_docs_book_v5.exe "D:\JapanesePDF" --out "D:\JapanesePDF_EN" --ocr all --ocr-lang jpn+eng --source-lang ja --target-lang en
```

### Mẫu 4 – Chạy thử 5 file đầu
```powershell
.\translator_docs_book_v5.exe "D:\LargeBatch" --out "D:\LargeBatch_Test" --max-files 5 --ocr auto --source-lang auto --target-lang vi
```

### Mẫu 5 – Xem format hỗ trợ
```powershell
.\translator_docs_book_v5.exe --list-supported-formats
```

### Mẫu 6 – Kiểm tra thông tin Tesseract
```powershell
.\translator_docs_book_v5.exe --show-tesseract-info
```

---

## 11. Khuyến nghị vận hành

- Luôn chạy thử trên một tập nhỏ trước
- Với PDF scan, ưu tiên `--ocr all` nếu chất lượng text thấp
- Với thư mục lớn, tách theo dự án hoặc ngôn ngữ để dễ kiểm soát
- Luôn kiểm tra `batch_summary.json` sau mỗi lô
- Dùng `bilingual.md` để kiểm tra nhanh chất lượng bản dịch
- Nếu cần giữ lịch sử và khả năng truy vết, không tắt log và index

---

## 12. Liên hệ hỗ trợ nội bộ

Khi gửi ticket hoặc email hỗ trợ, nên đính kèm:
- Lệnh đã chạy
- `batch_summary.json`
- `translation_report.json`
- `translation_log.csv`
- 1–2 file đầu vào đại diện
- Ảnh chụp màn hình lỗi nếu có

---

## Phụ lục A – Danh sách tham số đầy đủ

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

## Phụ lục B – Lệnh được khuyến nghị nhất để bắt đầu

```powershell
.\translator_docs_book_v5.exe "D:\Input" --out "D:\Output" --ocr auto --source-lang auto --target-lang vi
```
