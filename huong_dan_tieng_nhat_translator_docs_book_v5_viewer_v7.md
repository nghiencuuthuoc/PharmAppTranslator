# Hướng dẫn sử dụng bộ công cụ dịch tài liệu tiếng Nhật

*Dành cho Dược điển Nhật, SmPC, PIL và tài liệu chuyên ngành bằng Translator Docs Book v5 GUI và Translation Package Viewer v7*

Bài viết này hướng dẫn cách sử dụng thực tế cho khách hàng khi làm việc với tài liệu tiếng Nhật, đặc biệt là **Dược điển Nhật**, **SmPC**, **PIL** và các tài liệu kỹ thuật chuyên ngành. Nội dung tập trung vào cách dùng file `.exe`, cách đặt các ứng dụng hỗ trợ, cách chọn cấu hình OCR phù hợp và cách kiểm tra lại bản dịch bằng Viewer.

## 1. Bộ công cụ này dùng để làm gì?

- Bộ công cụ gồm hai ứng dụng chạy bằng file .exe.
- Translator Docs Book v5 GUI dùng để quét file hoặc thư mục, trích xuất nội dung, OCR khi cần, dịch theo lô và tạo gói kết quả hoàn chỉnh.
- Translation Package Viewer v7 dùng để mở lại gói kết quả đã dịch, đọc song ngữ, tìm kiếm, rà lỗi QA và kiểm tra chất lượng trước khi bàn giao hoặc lưu trữ.

## 2. Tài liệu tiếng Nhật nào phù hợp nhất?

- Dược điển Nhật hoặc trích đoạn chuyên khảo từ Japanese Pharmacopoeia.
- SmPC tiếng Nhật, hồ sơ thông tin thuốc, tờ hướng dẫn sử dụng kiểu PIL.
- PDF scan từ tài liệu in giấy, file PDF có text sẵn, DOCX, HTML, EPUB và các tài liệu kỹ thuật Nhật – Anh hoặc Nhật – Việt.
- Tài liệu có xen tiếng Anh, số liệu, tiêu đề kỹ thuật hoặc bảng biểu.

## 3. Cách đặt các Apps hỗ trợ khi chạy từ file exe

- Để người dùng cuối chạy ổn định, nên để hai file exe trong một thư mục riêng và đặt bộ OCR Tesseract trong thư mục Apps ở cấp cha hoặc gần thư mục chạy.
- Cách bố trí gợi ý:
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
- Với ebook như AZW hoặc MOBI, nên cài Calibre trên máy. Với các định dạng Office cũ như DOC, XLS, PPT, nên cài LibreOffice để phần mềm tự chuyển đổi trước khi dịch.
- Nếu chỉ dùng Viewer để đọc lại kết quả đã dịch, thường không cần cài Tesseract, Calibre hoặc LibreOffice.

## 4. Chọn cấu hình đúng cho tài liệu tiếng Nhật

- Điều quan trọng nhất là xác định tài liệu thuộc loại scan hay không scan.
- Nếu là PDF scan hoặc chất lượng text rất kém, nên dùng OCR.
- Nếu là PDF có text sẵn hoặc DOCX/HTML/EPUB, nên ưu tiên đọc text trực tiếp để nhanh hơn và ít lỗi hơn.

## 5. Cấu hình khuyến nghị

Các cấu hình dưới đây phù hợp cho phần lớn dược điển Nhật, SmPC/PIL tiếng Nhật và tài liệu khoa học có xen tiếng Anh.

| Loại tài liệu | Source Lang | Target Lang | OCR Mode | OCR Lang | Khuyến nghị |
|---|---|---|---|---|---|
| Dược điển Nhật dạng scan | ja hoặc auto | vi hoặc en | all | jpn+eng | Ưu tiên OCR toàn phần để nhận lại chữ từ ảnh. |
| SmPC/PIL Nhật dạng scan | ja hoặc auto | vi hoặc en | all | jpn+eng | Phù hợp với PDF scan, photocopy, bản in cũ. |
| PDF tiếng Nhật có text sẵn | ja | vi hoặc en | off hoặc auto | jpn+eng | Nhanh hơn, ít lỗi hơn OCR toàn phần. |
| Thư mục nhiều file hỗn hợp | auto | vi hoặc en | auto | jpn+eng | Phù hợp khi chưa chắc tất cả đều là tiếng Nhật. |
| Tài liệu kỹ thuật cần rà soát thuật ngữ | ja | en | auto | jpn+eng | Tạo bản tiếng Anh trung gian để kiểm tra dễ hơn. |

## 6. Quy trình dịch bằng Translator Docs Book v5 GUI

- Bước 1: Mở app và chọn UI Language, Appearance, Profile nếu cần.
- Bước 2: Chọn Input Path là file nguồn hoặc thư mục chứa nhiều tài liệu.
- Bước 3: Chọn Output Path là nơi lưu kết quả.
- Bước 4: Có thể dùng Add Files để thêm vài file riêng lẻ hoặc Add Folder để quét cả thư mục.
- Bước 5: Thiết lập Translator, Source Lang, Target Lang, OCR Mode, OCR Lang, số lần thử lại, thời gian chờ và kích thước chunk.
- Bước 6: Bấm Start để bắt đầu. Tab Log sẽ hiển thị tiến độ từng tài liệu và từng segment.
- Bước 7: Khi hoàn tất, dùng Open Output để mở thư mục kết quả.

## 7. Khi nào nên dùng Source Lang = auto, và khi nào nên chọn ja?

- Nên dùng auto khi thư mục có nhiều tài liệu hỗn hợp hoặc bạn không chắc tất cả đều là tiếng Nhật.
- Nên chọn ja khi bạn chắc chắn tài liệu gốc là tiếng Nhật. Cách này thường giúp workflow rõ ràng hơn khi rà soát bản dịch.
- Target Lang nên chọn vi nếu mục tiêu là đọc hiểu nội bộ tại Việt Nam, hoặc en nếu mục tiêu là bản kỹ thuật trung gian để kiểm tra thuật ngữ.

## 8. Kết quả sau khi dịch gồm những gì?

- Mỗi tài liệu sẽ được lưu trong một thư mục riêng.
- Thông thường gói kết quả có các thư mục như 01_source, 02_extracted, 03_translation, 04_indexes, 08_logs và 09_reports.
- Các file hữu ích nhất cho người dùng cuối là bilingual.md, target_only.md, full_target.txt, translation_bundle.json, manifest.json và translation_report.json.

## 9. Cách dùng Translation Package Viewer v7 để kiểm tra tài liệu tiếng Nhật

- Mở app Viewer và chọn Library root là thư mục cha chứa các gói kết quả đã dịch.
- Bấm Scan để quét thư viện. Khi cần tìm kiếm mạnh hơn, bấm Rebuild Index.
- Chọn một tài liệu ở panel Documents, sau đó chọn segment tương ứng ở panel Segments.
- Dùng tab Reader để đọc nội dung. Chế độ Side by side vertical rất phù hợp để đối chiếu nguồn – đích. Bilingual stacked phù hợp khi muốn đọc liên tục theo đoạn. Source only và Target only hữu ích khi cần tập trung vào một phía.
- Dùng tab Search để tìm theo từ khóa, thuật ngữ hoạt chất, cảnh báo an toàn, tên tá dược hoặc cụm QA.
- Dùng tab QA để lọc các đoạn có vấn đề như đoạn quá dài, đoạn OCR yếu, đoạn còn cần kiểm tra thêm.
- Có thể dùng Copy Source, Copy Target, Copy AI Prompt hoặc Copy Fix Prompt để chuyển nhanh nội dung sang công cụ hỗ trợ biên tập.

## 10. Mẹo riêng cho dược điển Nhật, SmPC và PIL

- Với dược điển Nhật scan nhiều bảng và chuyên khảo dài, nên chạy thử 1–2 file trước để kiểm tra chất lượng OCR.
- Với PIL hoặc SmPC tiếng Nhật có nhiều cảnh báo, liều dùng và chống chỉ định, nên kiểm tra lại bằng Viewer theo từng đoạn quan trọng thay vì chỉ đọc toàn văn một lần.
- Nếu tài liệu có nhiều hình, bảng, công thức hoặc chữ rất nhỏ, nên cân nhắc OCR toàn phần và giảm Max Chunk Chars để chia đoạn dễ kiểm tra hơn.
- Nếu tài liệu có cả tiếng Nhật và tiếng Anh, giữ OCR Lang = jpn+eng thường là lựa chọn an toàn.

## 11. Các tình huống nên chọn cấu hình nào?

- PDF scan từ sách hoặc bản photocopy: OCR Mode = all, OCR Lang = jpn+eng.
- PDF text thông thường: OCR Mode = off hoặc auto.
- Tài liệu Nhật – Anh học thuật: Source Lang = ja, Target Lang = en.
- Tài liệu cần đọc hiểu nội bộ tại Việt Nam: Source Lang = ja, Target Lang = vi.
- Thư mục có nhiều nguồn ngôn ngữ lẫn nhau: Source Lang = auto, sau đó kiểm tra lại trong Viewer.

## 12. Các lỗi thường gặp và cách xử lý nhanh

- Không OCR được PDF scan: kiểm tra lại thư mục Tesseract, file tesseract.exe và thư mục tessdata.
- Mở ebook không được: cài Calibre.
- Mở DOC/XLS/PPT cũ không được: cài LibreOffice.
- Bản dịch đã xong nhưng muốn rà kỹ hơn: mở lại bằng Viewer, Scan lại thư viện, rồi dùng Rebuild Index và QA.
- Đang làm dở muốn tiếp tục sau: dùng profile, lưu trạng thái và mở lại phiên làm việc sau.

## 13. Khuyến nghị thực hành tốt

- Nên tách thư mục nguồn và thư mục kết quả rõ ràng.
- Nên chạy thử một ít tài liệu trước khi dịch hàng loạt cả thư mục lớn.
- Nên dùng Viewer để kiểm tra các đoạn thuộc phần chỉ định, chống chỉ định, liều dùng, cảnh báo, ADR, bảo quản và thành phần.
- Nên giữ bản song ngữ để đối chiếu, và chỉ dùng bản target_only khi đã kiểm tra lại các đoạn quan trọng.

## 14. Kết luận

- Nếu tài liệu là dược điển Nhật, SmPC hoặc PIL tiếng Nhật, bộ đôi Translator Docs Book v5 GUI và Translation Package Viewer v7 là quy trình làm việc hợp lý: dịch trước, kiểm tra sau, tìm kiếm được, QA được và rất phù hợp cho xử lý thư mục tài liệu lớn.
- Với tài liệu scan, hãy ưu tiên OCR đúng cấu hình. Với tài liệu không scan, hãy ưu tiên đọc text trực tiếp. Sau cùng, luôn dùng Viewer để rà lại các phần chuyên môn quan trọng trước khi phát hành hoặc sử dụng nội bộ.
