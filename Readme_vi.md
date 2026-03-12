
# PharmAppTranslator: Bộ công cụ dịch tài liệu và kiểm tra bản dịch hướng dẫn sử dụng cho khách hàng

Bộ công cụ này gồm hai ứng dụng chạy độc lập bằng file `.exe`. Ứng dụng thứ nhất là **Translator Docs Book v5 GUI**, dùng để quét file hoặc thư mục, trích xuất nội dung, OCR khi cần, rồi tạo bộ hồ sơ bản dịch hoàn chỉnh. Ứng dụng thứ hai là **Translation Package Viewer v7**, dùng để mở lại các gói kết quả đã dịch, đọc song ngữ, tìm kiếm, rà lỗi QA và hỗ trợ kiểm tra chất lượng trước khi bàn giao hoặc lưu trữ.  

Điểm mạnh của bộ công cụ này là giao diện dành cho người dùng cuối: có **profile**, có **khôi phục trạng thái phiên làm việc**, có **bảng sắp xếp theo cột**, **nhắp đúp để mở file hoặc thư mục**, **menu chuột phải thao tác nhanh**, giao diện **EN/VI**, chế độ sáng/tối và bố cục nhiều vùng để làm việc liên tục với lượng tài liệu lớn. Cả hai ứng dụng đều có hotkey trợ giúp nhanh như `F1`, `Ctrl+Alt+D`, `Ctrl+Alt+S`, `Ctrl+Alt+L`, và `Ctrl+Q`.  

## 1) Hai file `.exe` dùng để làm gì?

### Translator Docs Book v5 GUI

Đây là ứng dụng dùng để **dịch tài liệu đầu vào**. Từ giao diện chính, người dùng chọn `Input Path`, `Output Path`, thêm file hoặc thêm thư mục, cấu hình bộ dịch, ngôn ngữ, OCR, rồi bấm `Start`. Ứng dụng hỗ trợ nhiều định dạng tài liệu như PDF, DOCX, PPTX, XLSX, EPUB, HTML, Markdown, TXT/CSV/TSV/JSON/XML/YAML; ngoài ra còn có thể xử lý thêm một số định dạng ebook và Office cũ thông qua công cụ hỗ trợ ngoài.  

### Translation Package Viewer v7

Đây là ứng dụng dùng để **mở lại gói kết quả đã dịch**. Người dùng chọn `Library root`, bấm `Scan`, sau đó xem danh sách tài liệu, danh sách segment, chế độ đọc song ngữ, tìm kiếm nội dung, rà lỗi QA, mở file gốc hoặc thư mục chứa kết quả. Viewer không phải là app để dịch tài liệu mới; nó được thiết kế để đọc các gói có `manifest.json`, `02_extracted`, `03_translation`, `04_indexes`, `08_logs`, `09_reports`.   

## 2) Cách chuẩn bị thư mục chạy từ file `.exe`

Để khách hàng dùng ổn định, nên đóng gói theo kiểu thư mục portable rõ ràng. Cách dễ dùng nhất là đặt hai file `.exe` trong một thư mục chạy riêng, và chuẩn bị thêm thư mục `Apps` cho công cụ OCR. Với build hiện tại, phần nhận diện Tesseract được cấu hình ưu tiên tìm theo các vị trí tương đối như `../Apps/Tesseract5.5.0/...`, `../../Apps/Tesseract5.5.0/...`, đồng thời vẫn có thể nhận từ biến môi trường hoặc từ `PATH`. 

Bạn có thể hướng dẫn khách hàng đặt thư mục như sau:

```text
PharmAppTranslator/
├─ Run/
│  ├─ translator_docs_book_v5_gui.exe
│  └─ translator_docs_book_viewer_v7_gui.exe
└─ Apps/
   └─ Tesseract5.5.0/
      ├─ tesseract.exe
      └─ tessdata/
```

Cách bố trí này phù hợp vì ứng dụng dịch có cơ chế dò `Tesseract` ở thư mục `../Apps/Tesseract5.5.0/` tính từ vị trí file chạy. Nếu khách hàng muốn tự chỉ đường dẫn, ứng dụng cũng có các tham số dành cho `tesseract-exe` và `tessdata-dir`, nhưng với người dùng phổ thông thì cách đặt thư mục như trên là dễ nhất.  

## 3) Các ứng dụng hỗ trợ cần chuẩn bị

### Tesseract OCR

Tesseract là thành phần gần như quan trọng nhất khi xử lý PDF scan hoặc PDF có lớp text quá kém. Ứng dụng hỗ trợ ba chế độ OCR là `auto`, `off`, `all`; mặc định ngôn ngữ OCR là `jpn+eng`. Nghĩa là nếu tài liệu là tiếng Nhật, tiếng Anh, hoặc PDF quét lẫn hai ngôn ngữ này, app có thể OCR trực tiếp. Với tiếng Việt hoặc ngôn ngữ khác, bạn nên chuẩn bị thêm bộ ngôn ngữ tương ứng trong thư mục `tessdata`.  

### Calibre

Calibre được dùng cho các định dạng ebook như `AZW`, `AZW3`, `AZW4`, `MOBI`, `PRC`, `FB2`, `LIT`. Theo code hiện tại, phần mềm sẽ tìm lệnh `ebook-convert` trong `PATH`, hoặc tìm bản cài đặt chuẩn của Windows trong `Program Files/Calibre2`. Nói đơn giản, với Calibre thì cách ổn định nhất là **cài Calibre chuẩn vào máy** thay vì chỉ chép thư mục rời.  

### LibreOffice

LibreOffice được dùng để đổi các định dạng Office cũ như `DOC`, `RTF`, `ODT`, `XLS`, `ODS`, `PPT`, `ODP` sang định dạng trung gian phù hợp hơn trước khi dịch. Theo code hiện tại, ứng dụng sẽ tìm `soffice` trong `PATH` hoặc trong vị trí cài đặt chuẩn của Windows. Vì vậy, nếu khách hàng thường làm với Office cũ, nên cài LibreOffice đầy đủ trên máy. 

## 4) Những định dạng file nào dùng tốt nhất?

Với người dùng cuối, nên chia thành hai nhóm dễ hiểu.

**Nhóm chạy trực tiếp, ổn định cao** gồm: PDF, DOCX, PPTX, XLSX/XLSM/XLTX/XLTM, EPUB, HTML/HTM/XHTML/SHTML, Markdown và các file text như TXT, CSV, TSV, LOG, JSON, XML, YAML/YML. Đây là các định dạng app đọc trực tiếp.  

**Nhóm cần công cụ hỗ trợ ngoài** gồm: AZW/MOBI và các ebook tương tự cần Calibre; DOC/RTF/ODT/XLS/ODS/PPT/ODP cần LibreOffice để chuyển đổi trước. Với khách hàng phổ thông, bạn nên ghi rõ rằng càng đưa tài liệu về DOCX, PDF text, EPUB hoặc HTML thì tốc độ và độ ổn định càng tốt.  

## 5) Cách sử dụng Translator Docs Book v5 GUI

Khi mở ứng dụng, khách hàng sẽ thấy phần đầu gồm chọn ngôn ngữ giao diện, profile, nút `Load`, `Save`, `Save As`, `Clone`, `Delete`, và chế độ giao diện `System/Dark/Light`. Bên dưới là vùng chọn `Input Path`, `Output Path`, các nút `Add Files`, `Add Folder`, `Clear Queue`, `Start`, `Refresh`, `Open Output`; phía dưới nữa là bảng hàng đợi, các thiết lập xử lý, tab `Documents`, `Preview`, `Log`, `Help`. Đây là giao diện dành cho thao tác theo lô chứ không chỉ từng file đơn lẻ.  

Quy trình dùng cơ bản như sau. Trước hết, chọn `Input Path` là file nguồn hoặc thư mục tài liệu. Sau đó chọn `Output Path` là nơi lưu kết quả. Có thể bấm `Add Files` để nạp một số file riêng lẻ, hoặc `Add Folder` để quét cả thư mục. Khi mọi thứ đã sẵn sàng, bấm `Start` để chạy. Trong quá trình chạy, tab `Log` sẽ hiển thị tiến độ dịch theo từng segment; khi hoàn tất, app tự làm mới danh sách tài liệu và lưu trạng thái phiên làm việc.  

Ở phần thiết lập, người dùng có thể chọn `Translator`, `Source Lang`, `Target Lang`, `OCR Mode`, `OCR Lang`, số lần thử lại, thời gian trễ, giới hạn ký tự mỗi đoạn, có ghi đè bản dịch hay không, có bỏ qua tài liệu hoàn tất hay không, có chỉ dịch lại các phần lỗi hay không, có sao chép file gốc vào gói kết quả hay không, và có quét đệ quy hay không. Hiện build này hỗ trợ rõ ràng hai lựa chọn translator là `deep_translator` và `none`.  

Với tài liệu PDF scan, nên để `OCR Mode = auto`. Với PDF ảnh hoàn toàn, có thể chuyển sang `all`. Nếu tài liệu đã có text tốt, có thể dùng `off` để chạy nhanh hơn. Nếu người dùng chủ yếu dịch Nhật–Anh hoặc Nhật–Việt qua lớp trung gian Anh, mặc định `jpn+eng` là hợp lý. Với tài liệu tiếng Anh bình thường, OCR thường không cần bật toàn phần trừ khi PDF quá xấu.  

Ứng dụng cũng hỗ trợ làm việc dài hơi nhờ **profile** và **resume**. Profile giúp lưu bộ thiết lập thường dùng như translator, OCR, ngôn ngữ, chunk size, giao diện. State giúp khôi phục hàng đợi, ô tìm kiếm, tab đang mở và nhiều giá trị của phiên trước. Đây là lý do app phù hợp cho người dùng phải xử lý thư mục tài liệu lớn nhiều ngày liên tục.  

## 6) Sau khi dịch xong sẽ thu được gì?

Mỗi tài liệu sẽ được tạo thành một **gói kết quả riêng**. Nếu bật sao chép file gốc, app sẽ lưu bản nguồn trong `01_source`. Phần trích xuất nằm trong `02_extracted`, phần bản dịch nằm trong `03_translation`, các file chỉ mục nằm trong `04_indexes`, log nằm trong `08_logs`, và báo cáo nằm trong `09_reports`. Viewer v7 cũng đọc chính các thư mục này để mở lại gói bản dịch.  

Trong gói kết quả, người dùng sẽ thấy các file quan trọng như `full_source.txt`, `full_target.txt`, `bilingual.md`, `target_only.md`, `translation_bundle.json`, `translation_log.csv`, `translation_report.json`, cùng với `manifest.json`. Đây là bộ hồ sơ rất tiện cho cả đọc nhanh, biên tập lại, kiểm tra QA, và lưu trữ lâu dài. `bilingual.md` phù hợp để đọc song ngữ, `target_only.md` phù hợp để đọc bản đích, `full_target.txt` phù hợp cho xử lý văn bản, còn `translation_bundle.json` thuận tiện cho các bước hậu kiểm sâu hơn.  

## 7) Cách sử dụng Translation Package Viewer v7

Sau khi đã có thư mục kết quả dịch, khách hàng mở **Translation Package Viewer v7** và chọn `Library root` là thư mục cha chứa các gói bản dịch. Bấm `Scan` để quét tài liệu. App chỉ nhận những thư mục có cấu trúc gói dịch hợp lệ, tức là có `manifest.json`, `02_extracted/extracted_document.json` và `03_translation/translation_bundle.json`. Sau khi quét xong, danh sách tài liệu sẽ hiện ở panel trái.  

Khi chọn một tài liệu, người dùng sẽ thấy danh sách segment và có thể chuyển sang tab `Reader` để đọc. Viewer hỗ trợ bốn chế độ xem: **song song đứng** (`side_by_side_vertical`), **song ngữ xếp dọc** (`stacked`), **chỉ nguồn** (`source`) và **chỉ bản dịch** (`target`). Trong thực tế, chế độ song song đứng là phù hợp nhất để biên tập và đối chiếu.  

Viewer còn có tab `Overview`, `Reader`, `Search`, `QA`, `Raw`, `Library`, `Help`, và vùng `Inspector`. `Inspector` hiển thị rất rõ tài liệu đang mở, ngôn ngữ nguồn–đích, trạng thái, số segment, số lỗi QA, vị trí `page/slide/sheet/chapter`, và cờ QA của đoạn đang chọn. Đây là phần rất hữu ích để khách hàng kiểm tra nhanh tài liệu mà không phải mở từng file JSON phía sau. 

Ở tab `Search`, nếu muốn tìm nhanh trong toàn bộ thư viện, người dùng nên bấm `Rebuild Index` sau khi `Scan`. App xây dựng chỉ mục tìm kiếm từ title, source ref, QA flags, error message, source text và target text, rồi cho phép tìm theo phạm vi `both`, `source`, `target`, `ref`, `qa`, `error`. Với thư viện lớn, đây là tính năng rất mạnh để tìm một thuật ngữ, một lỗi cụ thể, hoặc một đoạn đang có vấn đề.  

Ở tab `QA`, người dùng có thể rà các dòng có cờ lỗi hoặc cảnh báo. Viewer còn có các nút **Copy AI Prompt** và **Copy Fix Prompt** để sao chép prompt đánh giá hoặc prompt sửa câu dịch cho một segment cụ thể. Đây là điểm rất hữu ích khi bạn muốn kết hợp app với một AI chat bên ngoài để rà nhanh những đoạn khó.  

Tab `Library` hỗ trợ tìm thư mục và file, mở file hoặc mở thư mục cha. Theo thiết kế, app hỗ trợ **double click** để mở nhanh và có **menu chuột phải** cho các thao tác nhanh. Điều này rất thuận tiện khi khách hàng cần nhảy từ bản đọc sang file gốc, báo cáo, manifest hoặc log.  

## 8) Profile, lưu trạng thái và khôi phục phiên làm việc

Cả hai ứng dụng đều có cơ chế profile và khôi phục trạng thái, nhưng cách thể hiện hơi khác nhau.

Với **Translator Docs Book v5 GUI**, profile lưu các tham số dịch và giao diện; state lưu cả geometry cửa sổ, profile đang dùng, hàng đợi, từ khóa tìm kiếm, tab đang mở và các giá trị phiên gần nhất. Ứng dụng sử dụng thư mục dữ liệu riêng của người dùng trong `APPDATA` trên Windows hoặc vị trí tương đương trên macOS/Linux. Điều này giúp khách hàng tắt app rồi mở lại vẫn tiếp tục được công việc.  

Với **Translation Package Viewer v7**, app dùng một thư mục trạng thái riêng trong `APPDATA\PharmApp\TranslationPackageViewerV7`, có lưu `profiles` và `last_state`. App sẽ tự nạp lại trạng thái sau khi khởi động, gồm đường dẫn thư viện, profile, ngôn ngữ giao diện, giao diện sáng/tối, font, kích thước chữ, bộ lọc tài liệu, từ khóa tìm segment, chế độ reader và nhiều thông số khác. Điều này đặc biệt hữu ích khi khách hàng đang QA một thư viện lớn và phải dừng giữa chừng.   

## 9) Mẹo dùng thực tế cho khách hàng

Nếu mục tiêu là dịch hàng loạt tài liệu học thuật hoặc tài liệu kỹ thuật, cách tốt nhất là dùng **Translator Docs Book v5 GUI** để tạo gói dịch trước, sau đó dùng **Translation Package Viewer v7** để rà lại theo đợt. Làm như vậy sẽ tránh việc vừa dịch vừa sửa thủ công trong lúc app đang chạy.  

Nếu tài liệu là PDF scan, nên thử trước vài file để kiểm tra OCR. Nếu tài liệu là `.doc`, `.xls`, `.ppt` cũ, nên xác nhận LibreOffice đã cài đúng. Nếu tài liệu là ebook Kindle hoặc mobi, nên xác nhận Calibre đã cài và lệnh `ebook-convert` hoạt động bình thường. Đây là ba tình huống thường quyết định phần lớn việc chạy trơn tru hay không.  

Nếu khách hàng chỉ cần đọc kết quả, không cần cài Tesseract, Calibre hay LibreOffice cho máy Viewer. Các app hỗ trợ ngoài chủ yếu cần cho giai đoạn **trích xuất và dịch** ở Translator v5; còn Viewer v7 chủ yếu dùng để đọc gói đã tạo sẵn, tìm kiếm, QA và mở các file liên quan.  

---


