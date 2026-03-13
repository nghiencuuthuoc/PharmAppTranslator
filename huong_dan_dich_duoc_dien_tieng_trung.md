# Hướng dẫn dịch dược điển tiếng Trung dạng scan bằng Translator Docs Book v5 GUI

## 1. Mục đích của bài hướng dẫn
Tài liệu dược điển tiếng Trung, chuyên luận, phụ lục, tiêu chuẩn kiểm nghiệm, bảng chỉ tiêu, bảng giới hạn tạp chất hoặc bảng điều kiện sắc ký thường được lưu dưới dạng PDF scan. Với loại tài liệu này, mục tiêu thực tế không chỉ là dịch được nội dung mà còn phải đọc được đúng thuật ngữ, giữ được số liệu, hiểu được cấu trúc bảng và giảm lỗi OCR.

Bài hướng dẫn này tập trung vào cách cấu hình Translator Docs Book v5 GUI để xử lý tài liệu tiếng Trung giản thể hoặc phồn thể, đặc biệt là các file scan có nhiều bảng.

## 2. Khi nào nên dùng cấu hình cho tiếng Trung?
Nên dùng cấu hình tiếng Trung khi tài liệu thuộc một trong các trường hợp sau:

- Dược điển Trung Quốc hoặc tài liệu chuẩn nội bộ viết bằng tiếng Trung.
- PDF scan từ sách, bản photocopy hoặc bản in cũ.
- Tài liệu có nhiều bảng thành phần, hàm lượng, giới hạn, điều kiện thử nghiệm.
- Tài liệu có lẫn chữ Hán, số liệu, ký hiệu Latin, tên hoạt chất hoặc tên thuốc thử bằng tiếng Anh.

## 3. Cấu hình khuyến nghị

### 3.1. Với tiếng Trung giản thể
- OCR Mode: `all` hoặc `auto`
- OCR Lang: `chi_sim+eng`
- Source Lang: `zh-CN`
- Target Lang: `vi` hoặc `en`

### 3.2. Với tiếng Trung phồn thể
- OCR Mode: `all` hoặc `auto`
- OCR Lang: `chi_tra+eng`
- Source Lang: `zh-TW`
- Target Lang: `vi` hoặc `en`

### 3.3. Ý nghĩa của từng lựa chọn
- `OCR Mode = all`: ép ứng dụng OCR toàn bộ trang. Phù hợp nhất với PDF scan dạng ảnh.
- `OCR Mode = auto`: chỉ OCR khi trang không có lớp text đủ tốt. Hợp với PDF trộn giữa scan và text.
- `chi_sim+eng` hoặc `chi_tra+eng`: ngoài tiếng Trung còn giữ khả năng nhận chữ Latin, con số, đơn vị, tên hóa chất và ký hiệu tiếng Anh.
- `Target Lang = vi`: phù hợp khi cần đọc hiểu nhanh bằng tiếng Việt.
- `Target Lang = en`: phù hợp khi cần tạo bản trung gian tiếng Anh để soát thuật ngữ chuyên môn.

## 4. Nên dịch thẳng sang tiếng Việt hay đi qua tiếng Anh?
Có hai chiến lược thực tế.

### Cách 1: Dịch thẳng Trung -> Việt
Phù hợp khi:
- Cần đọc nhanh nội dung.
- Tài liệu không quá nhiều thuật ngữ khó.
- Mục tiêu là hiểu ý chính, tra cứu nhanh chuyên luận hoặc đối chiếu tiêu chuẩn.

### Cách 2: Dịch Trung -> Anh -> hiệu đính sang Việt
Phù hợp khi:
- Tài liệu quá chuyên ngành.
- Có nhiều đoạn mô tả phép thử, điều kiện sắc ký, thuốc thử, định tính, định lượng, tạp chất liên quan.
- Cần QA kỹ trước khi sử dụng trong công việc nghiên cứu, đăng bài hoặc chuẩn hóa dữ liệu.

Khuyến nghị thực tế: với dược điển, nhiều nhóm người dùng sẽ dễ soát lỗi hơn nếu tạo bản tiếng Anh trước, sau đó mới hiệu đính sang tiếng Việt.

## 5. Quy trình thao tác trong Translator Docs Book v5 GUI

### Bước 1. Chuẩn bị file nguồn
Đặt các file PDF scan vào một thư mục riêng. Nên gom theo từng chủ đề hoặc từng cuốn để dễ theo dõi.

Ví dụ:
- `D:/PharmBook/Chinese_Pharmacopeia/Volume_1`
- `D:/PharmBook/Chinese_Pharmacopeia/Herbal_Monographs`

### Bước 2. Mở ứng dụng
Chạy file `translator_docs_book_v5_gui.exe`.

### Bước 3. Chọn thư mục đầu vào và đầu ra
- `Input Path`: chọn thư mục chứa PDF scan tiếng Trung.
- `Output Path`: chọn thư mục lưu kết quả dịch.

Nên dùng thư mục đầu ra riêng, ví dụ:
- `D:/PharmBook/Chinese_Pharmacopeia_Trans_v5`

### Bước 4. Chọn kiểu xử lý
Tại phần thiết lập phía dưới giao diện:
- Translator: chọn bộ dịch đang sử dụng trong app.
- Source Lang: chọn `zh-CN` hoặc `zh-TW`.
- Target Lang: chọn `vi` hoặc `en`.
- OCR Mode: chọn `all` nếu file là scan thuần ảnh; chọn `auto` nếu file là PDF hỗn hợp.
- OCR Lang: chọn `chi_sim+eng` hoặc `chi_tra+eng`.
- Max Chunk Chars: giữ mức vừa phải để mỗi đoạn không quá dài.
- Retries và Retry Delay: nên giữ giá trị an toàn nếu chạy nhiều file.

### Bước 5. Thêm file hoặc thêm cả thư mục
- `Add Files`: dùng khi muốn chọn một vài file mẫu.
- `Add Folder`: dùng khi muốn chạy cả thư mục.

Khuyến nghị: luôn chạy thử 1 đến 3 file trước để kiểm tra chất lượng OCR và hướng dịch.

### Bước 6. Bấm Start
Sau khi bấm `Start`, ứng dụng sẽ:
- Quét tài liệu.
- OCR từng trang nếu cần.
- Chia nội dung thành từng phần.
- Dịch và ghi log.
- Tạo gói kết quả đầu ra.

### Bước 7. Theo dõi quá trình chạy
- Bảng `Documents` giúp theo dõi trạng thái từng tài liệu.
- Tab `Preview` dùng để xem nhanh.
- Tab `Log` hiển thị segment đang chạy, lỗi OCR hoặc lỗi dịch nếu có.

## 6. Đặc thù của bảng scan trong dược điển tiếng Trung
Đây là điểm quan trọng nhất.

PDF bảng scan không phải lúc nào cũng giữ nguyên được cấu trúc ô bảng sau OCR. Trong nhiều trường hợp, ứng dụng sẽ đọc bảng theo từng dòng văn bản thay vì tái tạo bảng đẹp như file Excel gốc. Điều này là bình thường với tài liệu scan.

### Những gì thường vẫn làm tốt
- Đọc tên chỉ tiêu.
- Đọc số liệu, giới hạn, đơn vị.
- Đọc điều kiện thử nghiệm.
- Đọc ghi chú và tiêu đề cột nếu chất lượng scan đủ tốt.

### Những gì dễ phát sinh lỗi
- Lệch hàng giữa cột trái và cột phải.
- Gộp nhầm 2 dòng thành 1 dòng.
- Nhận sai ký tự gần giống nhau.
- Nhận sai dấu chấm thập phân, dấu phần trăm, đơn vị hoặc ký hiệu sắc ký.

Vì vậy, với bảng rất quan trọng, nên xem bản dịch như bản đọc hiểu trước, sau đó QA lại kỹ.

## 7. Cách giảm lỗi khi dịch bảng scan

### 7.1. Ưu tiên bản scan rõ
Nếu có nhiều bản PDF, hãy chọn bản:
- Độ phân giải cao hơn.
- Nền sạch hơn.
- Ít nghiêng, ít bóng mờ.
- Chữ đậm, cột rõ.

### 7.2. Giữ thêm tiếng Anh trong OCR
Nhiều bảng dược điển có:
- Tên hoạt chất Latin.
- Tên dung môi hoặc thuốc thử tiếng Anh.
- Đơn vị như mg, mL, %, ppm, pH.

Vì vậy `chi_sim+eng` hoặc `chi_tra+eng` thường tốt hơn chỉ dùng tiếng Trung đơn lẻ.

### 7.3. Chạy thử trên tài liệu mẫu
Không nên đưa ngay cả thư viện lớn vào chạy. Hãy thử bằng:
- 1 file có bảng đơn giản.
- 1 file có bảng phức tạp.
- 1 file có cả đoạn văn và bảng.

Sau đó mới chốt cấu hình chuẩn cho toàn bộ batch.

### 7.4. QA lại bằng Viewer
Sau khi dịch xong, nên mở bằng `translator_docs_book_viewer_v7_gui.exe` để rà.

## 8. Cách dùng Viewer để kiểm tra bản dịch tiếng Trung
Sau khi có kết quả dịch, mở Viewer và thực hiện như sau:

### Bước 1. Chọn Library root
Trỏ tới thư mục chứa các gói kết quả dịch.

### Bước 2. Bấm Scan
Viewer sẽ quét danh sách tài liệu đã hoàn thành.

### Bước 3. Chọn tài liệu cần kiểm tra
Xem theo từng tài liệu, từng trang hoặc từng segment.

### Bước 4. Chọn chế độ đọc phù hợp
Khuyến nghị:
- `side_by_side_vertical`: đọc song song nguồn và bản dịch theo 2 cột đứng.
- `stacked`: đọc nguồn ở trên, bản dịch ở dưới.

Với bảng hoặc trang nặng dữ liệu, chế độ song song đứng thường dễ kiểm tra hơn.

### Bước 5. Dùng QA và Search
- Tìm các cụm quan trọng như tên hoạt chất, giới hạn, đơn vị.
- Kiểm tra các đoạn dài bất thường.
- Soát các segment có dấu hiệu OCR chưa ổn.

## 9. Trường hợp nên chọn Target = English trước
Nên chọn `Target Lang = en` trước khi:
- Dịch chuyên luận định lượng hoặc sắc ký phức tạp.
- Có nhiều thuật ngữ dược điển chuẩn hóa.
- Cần trao đổi với nhóm kỹ thuật hoặc đối tác quen đọc tiếng Anh.
- Muốn dùng bản tiếng Anh làm bước trung gian để QA.

Sau khi có bản tiếng Anh ổn hơn, có thể hiệu đính sang tiếng Việt hoặc dùng AI/biên tập viên để hoàn thiện bản Việt.

## 10. Ví dụ cấu hình khuyến nghị theo tình huống

| Tình huống | OCR Mode | OCR Lang | Source | Target | Gợi ý |
|---|---|---|---|---|---|
| Dược điển Trung Quốc giản thể, PDF scan thuần ảnh | all | chi_sim+eng | zh-CN | vi | Dùng khi cần đọc nhanh tiếng Việt |
| Dược điển Trung Quốc giản thể, cần QA thuật ngữ kỹ | all | chi_sim+eng | zh-CN | en | Tạo bản Anh trung gian để kiểm tra |
| Dược điển Trung Quốc phồn thể | all | chi_tra+eng | zh-TW | vi | Dùng cho bản scan phồn thể |
| PDF hỗn hợp text + scan | auto | chi_sim+eng hoặc chi_tra+eng | zh-CN hoặc zh-TW | vi hoặc en | Chạy thử trước vài file |
| Bảng scan quan trọng cần đối chiếu kỹ | all | chi_sim+eng hoặc chi_tra+eng | đúng theo nguồn | en trước | Sau đó QA rồi hiệu đính Việt |

## 11. Kết quả đầu ra người dùng nên kiểm tra
Sau khi chạy xong, người dùng nên xem các thành phần sau trong gói kết quả:
- Bản song ngữ để đối chiếu.
- Bản đích để đọc liên tục.
- File log để biết tài liệu nào lỗi segment.
- Các báo cáo QA nếu có.

Nếu phát hiện một file bảng quá lỗi, nên quay lại chạy riêng file đó với cấu hình khác, thay vì chạy lại toàn bộ thư viện.

## 12. Kết luận
Với dược điển tiếng Trung dạng scan, điều quan trọng nhất không phải chỉ là bật dịch, mà là chọn đúng cấu hình OCR và đúng chiến lược đích.

Tóm tắt khuyến nghị:
- Trung giản thể: `chi_sim+eng`, `zh-CN`.
- Trung phồn thể: `chi_tra+eng`, `zh-TW`.
- PDF scan thuần ảnh: ưu tiên `OCR Mode = all`.
- Cần đọc nhanh: dịch sang `vi`.
- Cần QA kỹ thuật ngữ: dịch sang `en` trước.
- Với bảng quan trọng: luôn kiểm tra lại trong Viewer.

Nếu áp dụng đúng quy trình này, người dùng sẽ kiểm soát tốt hơn chất lượng bản dịch, đặc biệt với các bảng chỉ tiêu, chuyên luận và tài liệu dược điển có tính kỹ thuật cao.
