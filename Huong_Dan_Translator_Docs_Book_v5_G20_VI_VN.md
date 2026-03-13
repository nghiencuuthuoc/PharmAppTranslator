# Translator Docs Book v5 GUI + CLI Hướng dẫn sử dụng

Dành cho translator_docs_book_v5_g20_vi.py và translator_docs_book_v5_gui_g20_vi.py  
Gói ngôn ngữ G20 + tiếng Việt

March 13, 2026

> Tài liệu này giải thích cách cài đặt, chọn OCR, chọn ngôn ngữ, dùng GUI/CLI và rà soát đầu ra.

## Tổng quan

- Phiên bản này được thiết kế để dịch sách, tài liệu pháp quy, SmPC, PIL, dược điển, file Office, ebook, HTML, Markdown và văn bản thuần trong cùng một quy trình.
- Bản cập nhật hỗ trợ bộ ngôn ngữ định hướng G20 và bổ sung tiếng Việt. GUI phù hợp cho sử dụng hằng ngày, còn CLI phù hợp cho xử lý hàng loạt và chạy lặp lại theo lệnh.
- Tài liệu dưới đây tập trung vào cách vận hành, cài ứng dụng hỗ trợ, chọn ngôn ngữ dịch, chọn ngôn ngữ OCR và cách kiểm tra đầu ra.

## Điểm mới của bản cập nhật này

- Mở rộng lựa chọn ngôn ngữ dịch: Ả Rập, Đức, Anh, Tây Ban Nha, Pháp, Hindi, Indonesia, Ý, Nhật, Hàn, Bồ Đào Nha, Nga, Thổ Nhĩ Kỳ, Việt, Trung Quốc giản thể và Trung Quốc phồn thể.
- Alias OCR dễ nhập hơn. Ví dụ có thể gõ ja, zh-CN, zh-TW, vi, fr, ar hoặc mã Tesseract đầy đủ như jpn+eng.
- GUI hỗ trợ profile và khôi phục trạng thái phiên trước, thuận tiện cho các lô tài liệu lớn.
- Bảng có thể sắp xếp, tìm kiếm, xem trước, mở nhanh và menu chuột phải giúp rà soát kết quả nhanh hơn.

## Ngôn ngữ dịch được hỗ trợ

Chỉ dùng `auto` cho ngôn ngữ nguồn.

| Mã | Ngôn ngữ | Giá trị OCR gợi ý |
|---|---|---|
| ar | Ả Rập | `ara+eng` |
| de | Đức | `deu+eng` |
| en | Anh | `eng` |
| es | Tây Ban Nha | `spa+eng` |
| fr | Pháp | `fra+eng` |
| hi | Hindi | `hin+eng` |
| id | Indonesia | `ind+eng` |
| it | Ý | `ita+eng` |
| ja | Nhật | `jpn+eng` |
| ko | Hàn | `kor+eng` |
| pt | Bồ Đào Nha | `por+eng` |
| ru | Nga | `rus+eng` |
| tr | Thổ Nhĩ Kỳ | `tur+eng` |
| vi | Việt | `vie+eng` |
| zh-CN | Trung giản thể | `chi_sim+eng` |
| zh-TW | Trung phồn thể | `chi_tra+eng` |

## Ứng dụng hỗ trợ nên cài

- Khuyến nghị cài Tesseract OCR cho PDF scan và trang tài liệu dạng ảnh.
- Khuyến nghị cài LibreOffice cho file Office đời cũ như .doc, .xls, .ppt, .rtf, .odt, .ods và .odp.
- Khuyến nghị cài Calibre cho ebook như AZW, MOBI, PRC, FB2 và LIT.
- Khi dùng deep_translator / GoogleTranslator cần có kết nối internet.

## Gợi ý vị trí đặt ứng dụng

Nên đặt Tesseract trong thư mục Apps gần script, ví dụ:

`../Apps/Tesseract5.5.0/tesseract.exe`

`../Apps/Tesseract5.5.0/tessdata`



LibreOffice và Calibre có thể cài theo cách thông thường để chương trình tìm qua PATH hệ thống. Trên Windows, các thư mục cài đặt chuẩn cũng có thể được phát hiện.

## Định dạng đầu vào hỗ trợ

| Nhóm | Phần mở rộng | Ghi chú |
|---|---|---|
| Trích xuất trực tiếp | .pdf, .docx, .pptx, .xlsx, .xlsm, .xltx, .xltm, .epub, .html, .htm, .xhtml, .shtml, .md, .markdown, .mdown, .txt, .text, .csv, .tsv, .log, .json, .xml, .yaml, .yml | Đọc nội dung trực tiếp. |
| Tốt nhất qua Calibre | .azw, .azw3, .azw4, .mobi, .prc, .fb2, .lit | Được chuyển sang EPUB trước bằng ebook-convert. |
| Tốt nhất qua LibreOffice | .doc, .rtf, .odt, .xls, .ods, .ppt, .odp | Chuyển đổi trước rồi mới trích xuất. |

## Cách sử dụng GUI

1. **Khởi động**: Chạy python translator_docs_book_v5_gui_g20_vi.py --gui, hoặc mở file EXE đã đóng gói nếu bạn đã build sẵn.
2. **Chọn đầu vào và đầu ra**: Chọn một file hoặc cả thư mục. Sau đó chọn thư mục gốc đầu ra để lưu toàn bộ dự án đã dịch.
3. **Chọn ngôn ngữ**: Thiết lập Source Lang và Target Lang. Dùng auto khi thư mục có nhiều ngôn ngữ hoặc chưa biết chắc ngôn ngữ nguồn. Nếu muốn ra tiếng Việt thì chọn vi.
4. **Thiết lập OCR**: Dùng OCR Mode = auto cho PDF hỗn hợp, OCR Mode = all cho bản scan ảnh, hoặc OCR Mode = off cho tài liệu số sạch.
5. **Thiết lập ngôn ngữ OCR**: Có thể nhập ja, zh-CN, zh-TW, vi, fr, ar hoặc mã ghép như jpn+eng. Thiết lập này đặc biệt quan trọng với sách scan hoặc trang dược điển.
6. **Bắt đầu xử lý**: Nhấn Start. Hàng đợi, nhật ký, bảng tài liệu và bảng file giúp bạn theo dõi tiến trình.
7. **Rà soát kết quả**: Mở bilingual.md, target_only.md, full_target.txt, translation_bundle.json hoặc translation_report.json từ menu chuột phải hoặc nhắp đúp dòng.
8. **Tiếp tục công việc**: Profile lưu cấu hình. Ứng dụng cũng tự khôi phục trạng thái phiên trước để tiếp tục các lô lớn thuận tiện hơn.

## Mẹo dùng GUI hiệu quả

- F1 mở Help.
- Nhắp đúp vào dòng để mở file hoặc thư mục.
- Nhắp chuột phải để dùng các thao tác nhanh như Open File, Open Folder, Open Manifest, Open bilingual.md và Open translation report.
- Nhắp tiêu đề cột để sắp xếp.
- Dùng ô Search để lọc hàng đợi và danh sách kết quả.

## Cách sử dụng CLI

CLI phù hợp khi bạn cần xử lý hàng loạt ổn định, chạy lặp lại hoặc lưu lệnh mẫu để dùng lại.

**Mở giao diện GUI**

```bash
python translator_docs_book_v5_gui_g20_vi.py --gui
```

**Dịch cả thư mục sang tiếng Việt**

```bash
python translator_docs_book_v5_g20_vi.py "D:\InputBooks" --out "D:\Translated" --ocr auto --source-lang auto --target-lang vi
```

**Dịch PDF tiếng Nhật sang tiếng Anh bằng OCR toàn phần**

```bash
python translator_docs_book_v5_g20_vi.py "D:\Books\jp_book.pdf" --out "D:\Translated" --ocr all --ocr-lang ja --source-lang ja --target-lang en
```

**Dịch bản scan tiếng Trung sang tiếng Việt**

```bash
python translator_docs_book_v5_g20_vi.py "D:\Books\cn_scan.pdf" --out "D:\Translated" --ocr all --ocr-lang zh-CN --source-lang zh-CN --target-lang vi
```

**Kiểm tra nhận diện OCR runtime**

```bash
python translator_docs_book_v5_g20_vi.py --show-tesseract-info
```

**In danh sách định dạng và ngôn ngữ hỗ trợ**

```bash
python translator_docs_book_v5_g20_vi.py --list-supported-formats
```

## Cách chọn OCR đúng

- Dùng OCR Mode = auto khi file có thể vừa có text chọn được vừa có trang scan.
- Dùng OCR Mode = all cho SmPC scan, PIL scan, dược điển scan, PDF tiếng Nhật, tài liệu tiếng Trung dạng scan hoặc ảnh chụp trang giấy.
- Dùng OCR Mode = off cho DOCX, HTML, Markdown, TXT và nhiều PDF số sạch.
- Với tiếng Nhật dùng ja hoặc jpn+eng. Với tiếng Trung giản thể dùng zh-CN hoặc chi_sim+eng. Với tiếng Trung phồn thể dùng zh-TW hoặc chi_tra+eng. Với tiếng Việt dùng vi hoặc vie+eng.

## Thư mục đầu ra có gì

| Thư mục | Mục đích |
|---|---|
| 01_source | Bản sao file gốc khi bật Copy original file. |
| 02_extracted | Văn bản nguồn đã trích xuất và extracted_document.json. |
| 03_translation | full_target.txt, bilingual.md, target_only.md, translation_bundle.json. |
| 04_indexes | Chỉ mục segment và translation memory nếu bật. |
| 08_logs | translation_log.csv và các log lô xử lý. |
| 09_reports | translation_report.json và metadata manifest. |

## Quy trình gợi ý nên dùng

- SmPC tiếng Nhật hoặc dược điển scan sang tiếng Anh: OCR Mode = all, OCR Lang = ja, Source Lang = ja, Target Lang = en.
- Trang pháp quy tiếng Trung dạng scan sang tiếng Việt: OCR Mode = all, OCR Lang = zh-CN hoặc zh-TW, Source Lang = zh-CN hoặc zh-TW, Target Lang = vi.
- PIL tiếng Pháp hoặc tiếng Đức sang tiếng Việt: dùng OCR Mode = auto nếu PDF có text, hoặc all nếu là scan. Đặt Source Lang = fr hoặc de, Target Lang = vi.
- Thư mục hỗn hợp nhiều loại file: dùng Source Lang = auto, Target Lang theo ngôn ngữ mong muốn, và giữ OCR Mode = auto nếu thư mục không phải chủ yếu là scan ảnh.

## Xử lý sự cố thường gặp

- Không ra chữ OCR: kiểm tra lại Tesseract và chạy --show-tesseract-info.
- File Office đời cũ không xử lý được: cài LibreOffice và bảo đảm soffice có thể được tìm thấy.
- AZW hoặc MOBI không xử lý được: cài Calibre để có ebook-convert.
- Dịch bị lỗi ngắt quãng: tăng Retries và Retry Delay, đồng thời giữ mạng ổn định.
- Chọn sai ngôn ngữ OCR sẽ làm chất lượng giảm rất mạnh: đổi OCR Lang đúng với hệ chữ nguồn.

*Khi dùng cho công việc thật, nên luôn kiểm tra bilingual.md, target_only.md và translation_report.json trước khi xuất bản hoặc tái sử dụng nội dung đã dịch.*
