# Hướng dẫn sử dụng - translator_docs_book_v5_gui_g20_vi.exe

*Bản tiếng Việt*

## Tổng quan

translator_docs_book_v5_gui_g20_vi.exe là ứng dụng desktop GUI dùng để trích xuất văn bản từ sách và tài liệu văn phòng, dịch nội dung đã trích xuất, rồi sắp xếp kết quả vào một cấu trúc thư mục đầu ra rõ ràng.

Bản G20 + tiếng Việt này hướng tới các lựa chọn dịch gồm: Ả Rập, Trung Quốc giản thể, Trung Quốc phồn thể, Anh, Pháp, Đức, Hindi, Indonesia, Ý, Nhật, Hàn, Bồ Đào Nha, Nga, Tây Ban Nha, Thổ Nhĩ Kỳ và tiếng Việt.

Ứng dụng hỗ trợ hàng đợi đầu vào, lưu profile, tự khôi phục trạng thái phiên trước, danh sách tài liệu có tìm kiếm, preview, log, bảng sắp xếp theo cột và menu chuột phải để mở nhanh kết quả.

## Cách đặt file EXE và các app hỗ trợ

Để dùng ổn định hơn, nên đặt EXE trong thư mục app hoặc release và chuẩn bị các công cụ hỗ trợ như sau:

- **Tesseract OCR:** Nên có khi xử lý PDF scan. Ứng dụng thường dò theo cấu trúc đường dẫn tương đối như ../Apps/Tesseract5.5.0/tesseract.exe và ../Apps/Tesseract5.5.0/tessdata.

- **LibreOffice:** Nên cài nếu cần xử lý các định dạng Office cũ như .doc, .xls, .ppt, .odt, .ods, .odp và .rtf.

- **Calibre:** Nên cài nếu cần xử lý ebook như .azw, .mobi và các định dạng tương tự.

Bạn vẫn có thể dùng EXE khi thiếu một số công cụ, nhưng khả năng OCR và chuyển đổi định dạng sẽ bị giới hạn.

## Định dạng đầu vào được hỗ trợ

Chương trình có thể xử lý nhiều nhóm tài liệu khác nhau. Có thể hình dung theo các nhóm thực tế sau:

| Nhóm | Định dạng |
| --- | --- |
| Trích xuất trực tiếp | .txt, .csv, .tsv, .json, .xml, .yaml, .html, .htm, .md, .docx, .pptx, .xlsx, .epub, .pdf |
| Hỗ trợ best-effort với Calibre | .azw, .azw3, .azw4, .mobi, .prc, .fb2, .lit |
| Hỗ trợ best-effort với LibreOffice | .doc, .rtf, .odt, .xls, .ods, .ppt, .odp |

## Bắt đầu nhanh

1. Chạy translator_docs_book_v5_gui_g20_vi.exe.

1. Chọn UI Language và Appearance nếu cần.

1. Chọn Output Path.

1. Thêm một hoặc nhiều file, hoặc thêm cả thư mục.

1. Chọn Translator, Source Lang, Target Lang, OCR Mode và OCR Lang.

1. Nhấn Start.

1. Theo dõi tiến trình trong tab Log.

1. Sau khi xử lý xong, nhấn Refresh và xem kết quả trong Documents, Files và Preview.

1. Dùng Open Output để mở thư mục đầu ra gốc.

## Quy trình chính trong GUI

GUI được thiết kế cho quy trình dịch tài liệu theo lô, với phần hàng đợi đầu vào ở phía trước và phần rà soát kết quả ở phía sau.

### Input Queue

Hàng đợi đầu vào nhận cả file và thư mục.

Bảng có thể sắp xếp bằng cách nhắp vào tiêu đề cột.

Ô tìm kiếm sẽ lọc dữ liệu theo tên hoặc đường dẫn.

Nhắp đúp để mở file hoặc thư mục đang chọn.

Nhắp chuột phải để dùng các lệnh mở nhanh như open, open parent, copy path, copy name và remove selected.

### Settings

| Thiết lập | Ý nghĩa |
| --- | --- |
| Translator | Chọn bộ dịch. "deep_translator" là chế độ dịch thông thường; "none" phù hợp khi chỉ muốn test trích xuất. |
| Source Lang | Chọn ngôn ngữ nguồn của tài liệu, hoặc dùng auto khi chưa chắc. |
| Target Lang | Chọn ngôn ngữ đích. Bản build này hướng tới nhóm ngôn ngữ G20 và thêm tiếng Việt. |
| OCR Mode | off = không OCR; auto = OCR các trang có rất ít text gốc; all = OCR toàn bộ trang PDF. |
| OCR Lang | Nhập mã OCR của Tesseract, ví dụ jpn+eng, chi_sim+eng, chi_tra+eng, kor+eng, rus+eng, ara+eng, vie+eng. |
| Folder Style | auto ưu tiên tương thích với dữ liệu cũ, hash12 tạo thư mục duy nhất an toàn hơn, plain chỉ dùng tên nguồn. |
| Retries / Retry Delay | Dùng khi yêu cầu dịch bị lỗi tạm thời. |
| Max Chunk Chars | Điều khiển kích thước mỗi đoạn gửi đi dịch. Giá trị nhỏ hơn thường an toàn hơn khi job không ổn định. |
| Skip complete docs | Bỏ qua tài liệu đã có manifest hoàn chỉnh và đủ file dịch. |
| Overwrite translation | Buộc ghi đè bản dịch cũ. |
| Retranslate errors only | Giữ các đoạn đã thành công và chỉ dịch lại phần lỗi. |
| Copy original file | Sao chép file đầu vào vào 01_source để truy vết. |
| Recursive scan | Khi thêm thư mục, quét cả các file hỗ trợ nằm trong thư mục con. |

### Profile và khôi phục phiên trước

Profile lưu cả thiết lập dịch lẫn giao diện.

Bạn có thể load, save, save as, clone và delete profile.

Ứng dụng cũng lưu trạng thái phiên gần nhất, gồm bố cục cửa sổ, profile đang chọn, hàng đợi đầu vào, chuỗi tìm kiếm và tab cuối cùng; sau đó tự khôi phục khi mở lại chương trình.

### Search, Documents, Files, Preview và Log

Search lọc hàng đợi đầu vào, danh sách tài liệu đã xử lý và danh sách file đầu ra.

Documents hiển thị từng thư mục tài liệu đã xử lý cùng trạng thái, số segment, số lỗi và thời gian sửa đổi.

Files liệt kê toàn bộ file được tạo trong thư mục tài liệu đang chọn.

Preview xem trước nội dung text của các file như JSON, Markdown và TXT.

Log hiển thị tiến trình chạy và lỗi phát sinh.

Bạn có thể nhắp chuột phải trên danh sách tài liệu đã xử lý để mở trực tiếp thư mục tài liệu hoặc mở nhanh các file quan trọng như manifest.json, bilingual.md, target_only.md, full_target.txt, full_source.txt, translation_bundle.json và translation_report.json.

### Gợi ý cấu hình OCR

| Loại tài liệu | Gợi ý cấu hình |
| --- | --- |
| Tài liệu scan tiếng Nhật | Source: ja | OCR Lang: jpn+eng | Target thường dùng: en hoặc vi |
| Tài liệu scan tiếng Trung giản thể | Source: zh-CN | OCR Lang: chi_sim+eng | Target thường dùng: en hoặc vi |
| Tài liệu scan tiếng Trung phồn thể | Source: zh-TW | OCR Lang: chi_tra+eng | Target thường dùng: en hoặc vi |
| Tài liệu scan tiếng Hàn | Source: ko | OCR Lang: kor+eng | Target thường dùng: en hoặc vi |
| Tài liệu scan tiếng Nga | Source: ru | OCR Lang: rus+eng | Target thường dùng: en hoặc vi |
| Tài liệu scan tiếng Ả Rập | Source: ar | OCR Lang: ara+eng | Target thường dùng: en hoặc vi |
| Tài liệu scan tiếng Hindi | Source: hi | OCR Lang: hin+eng | Target thường dùng: en hoặc vi |
| Tài liệu scan tiếng Việt | Source: vi | OCR Lang: vie+eng | Target thường dùng: en hoặc vi |
| Pháp / Đức / Tây Ban Nha / Ý / Bồ Đào Nha / Thổ Nhĩ Kỳ / Indonesia | Chọn đúng Source Lang và cài gói ngôn ngữ Tesseract tương ứng khi cần OCR. |

## Cấu trúc thư mục đầu ra

Mỗi file nguồn sau khi xử lý sẽ được ghi vào một thư mục tài liệu riêng. Tên thư mục có thể ở dạng plain, hashed hoặc auto tùy theo Folder Style.

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

### Ý nghĩa từng thư mục và file

manifest.json: bản tóm tắt xử lý chính, gồm file nguồn, hash nguồn, ngôn ngữ nguồn và đích, cấu hình OCR, số segment và trạng thái cuối cùng của tài liệu.

01_source: bản sao tùy chọn của file gốc.

02_extracted/extracted_document.json: dữ liệu trích xuất có cấu trúc theo từng segment.

02_extracted/full_source.txt: toàn bộ text nguồn đã ghép lại để rà soát.

03_translation/translation_bundle.json: dữ liệu song song theo segment, trạng thái và metadata.

03_translation/full_target.txt: toàn bộ text đích đã ghép lại.

03_translation/bilingual.md: file Markdown song ngữ.

03_translation/target_only.md: file Markdown chỉ chứa ngôn ngữ đích.

04_indexes: index tìm kiếm theo segment và translation memory CSV.

08_logs/translation_log.csv: log dịch chi tiết ở mức segment.

09_reports/translation_report.json: báo cáo tập trung vào lỗi.

batch_summary_gui.json: file tổng hợp cho toàn bộ đợt chạy, nằm ở thư mục output gốc.

## Khuyến nghị sử dụng

- Chỉ dùng auto phát hiện ngôn ngữ khi bạn chưa chắc ngôn ngữ nguồn. Nếu đã biết trước, chọn trực tiếp thường sạch hơn.

- Với PDF scan, nên thử OCR Mode = auto trước. Chỉ dùng all khi text gốc trong PDF quá kém.

- Giữ Copy original file bật khi cần truy vết.

- Giữ Skip complete docs bật khi chạy lại theo kiểu bổ sung dần.

- Dùng Retranslate errors only khi lần chạy trước đã hoàn thành phần lớn segment và chỉ còn lỗi cục bộ.

- Sau mỗi lần chạy, nên rà manifest.json, translation_report.json, bilingual.md và full_target.txt trước khi công bố hoặc tái sử dụng bản dịch.

## Khắc phục sự cố

### OCR không hoạt động

Hãy kiểm tra Tesseract đã được cài và gói dữ liệu ngôn ngữ tương ứng đã có trong tessdata. Ví dụ OCR tiếng Nhật cần jpn, tiếng Việt cần vie, tiếng Trung giản thể cần chi_sim và tiếng Ả Rập cần ara.

### Một số file mở không tốt hoặc chuyển đổi lỗi

Nên cài LibreOffice cho các định dạng Office cũ và Calibre cho các định dạng ebook.

### Tài liệu bị bỏ qua ngoài ý muốn

Điều này thường xảy ra khi ứng dụng phát hiện thư mục tài liệu đó đã hoàn tất từ trước. Tắt Skip complete docs hoặc bật Overwrite translation nếu bạn muốn tạo lại từ đầu.

### Preview trống với một số file

Tab Preview chủ yếu dùng cho các đầu ra dạng text. Với file nhị phân, nên mở trực tiếp từ tab Files hoặc menu chuột phải của tài liệu.
