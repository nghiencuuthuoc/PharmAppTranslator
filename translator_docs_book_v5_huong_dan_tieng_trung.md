# Hướng dẫn dịch tài liệu tiếng Trung bằng Translator Docs Book v5 GUI

**Mục đích**  
Tài liệu này giúp người dùng chọn đúng cấu hình khi dịch tài liệu tiếng Trung trong **Translator Docs Book v5 GUI**, đặc biệt với các file scan, PDF sách, dược điển, brochure kỹ thuật và tài liệu văn phòng có lẫn tiếng Anh.

---

## 1) Thiết lập tổng quát nên dùng

Khi xử lý tài liệu tiếng Trung, cấu hình nền tảng nên bắt đầu như sau:

- **OCR Mode** = `all`
- **OCR Lang** = chọn theo loại chữ Trung:
  - `chi_sim+eng` cho **giản thể**
  - `chi_tra+eng` cho **phồn thể**
- **Source Lang** = chọn theo loại văn bản:
  - `zh-CN` cho **Trung Quốc đại lục / giản thể**
  - `zh-TW` cho **Đài Loan / phồn thể**
- **Target Lang** = ngôn ngữ đích:
  - `vi` để dịch sang **tiếng Việt**
  - `en` để dịch sang **tiếng Anh**

**Khuyến nghị thực tế:**  
Với tài liệu scan hoặc PDF ảnh, nên để **OCR Mode = all** để hệ thống xử lý đầy đủ hơn các trang có chữ nằm trong ảnh, ảnh chụp, bản scan cũ hoặc PDF không có text layer sạch.

---

## 2) Phân biệt nhanh: giản thể hay phồn thể

### Giản thể
Thường gặp ở tài liệu từ **Trung Quốc đại lục**.  
Ví dụ các chữ:

- 中国药典
- 浓缩粉
- 制法
- 检查

**Thiết lập phù hợp:**
- **OCR Lang** = `chi_sim+eng`
- **Source Lang** = `zh-CN`

### Phồn thể
Thường gặp ở tài liệu từ **Đài Loan**, **Hong Kong**, hoặc một số tài liệu cũ.  
Ví dụ các chữ:

- 中國藥典
- 濃縮粉
- 製法
- 檢查

**Thiết lập phù hợp:**
- **OCR Lang** = `chi_tra+eng`
- **Source Lang** = `zh-TW`

---

## 3) Bảng cấu hình khuyến nghị

| Loại tài liệu | OCR Mode | OCR Lang | Source Lang | Target Lang |
|---|---|---|---|---|
| Tài liệu tiếng Trung giản thể dịch sang tiếng Việt | `all` | `chi_sim+eng` | `zh-CN` | `vi` |
| Tài liệu tiếng Trung giản thể dịch sang tiếng Anh | `all` | `chi_sim+eng` | `zh-CN` | `en` |
| Tài liệu tiếng Trung phồn thể dịch sang tiếng Việt | `all` | `chi_tra+eng` | `zh-TW` | `vi` |
| Tài liệu tiếng Trung phồn thể dịch sang tiếng Anh | `all` | `chi_tra+eng` | `zh-TW` | `en` |
| Tài liệu có tiếng Trung lẫn tiếng Anh chuyên ngành | `all` | `chi_sim+eng` hoặc `chi_tra+eng` | `zh-CN` hoặc `zh-TW` | `vi` / `en` |

**Lưu ý quan trọng:**  
Không nên ghép lệch cặp, ví dụ:
- `chi_sim+eng` nhưng lại chọn `zh-TW`
- `chi_tra+eng` nhưng lại chọn `zh-CN`

Phần mềm vẫn có thể chạy, nhưng chất lượng OCR và chất lượng dịch thường kém ổn định hơn, dễ sai thuật ngữ, sai phân đoạn câu hoặc nhận dạng nhầm ký tự.

---

## 4) Cấu hình nên dùng theo từng mục tiêu

### A. Dịch tài liệu tiếng Trung sang tiếng Việt
Dùng khi muốn tạo bản đọc nội bộ, bản tham khảo, tài liệu học thuật hoặc tài liệu kỹ thuật cho người đọc Việt Nam.

**Giản thể sang tiếng Việt**
```text
OCR Mode    = all
OCR Lang    = chi_sim+eng
Source Lang = zh-CN
Target Lang = vi
```

**Phồn thể sang tiếng Việt**
```text
OCR Mode    = all
OCR Lang    = chi_tra+eng
Source Lang = zh-TW
Target Lang = vi
```

### B. Dịch tài liệu tiếng Trung sang tiếng Anh
Phù hợp khi muốn chuẩn hóa nội dung để trao đổi quốc tế, đọc nhanh tài liệu chuyên ngành hoặc làm bước trung gian trước khi biên tập.

**Giản thể sang tiếng Anh**
```text
OCR Mode    = all
OCR Lang    = chi_sim+eng
Source Lang = zh-CN
Target Lang = en
```

**Phồn thể sang tiếng Anh**
```text
OCR Mode    = all
OCR Lang    = chi_tra+eng
Source Lang = zh-TW
Target Lang = en
```

---

## 5) Quy trình thao tác gợi ý trong GUI

### Bước 1. Chọn file nguồn
Chọn PDF, ảnh scan, tài liệu office, EPUB hoặc các định dạng được chương trình hỗ trợ.

### Bước 2. Kiểm tra loại chữ Trung
Quan sát nhanh vài chữ trên trang đầu:
- Nếu thấy dạng **中国 / 药 / 浓 / 体** -> thường là **giản thể**
- Nếu thấy dạng **中國 / 藥 / 濃 / 體** -> thường là **phồn thể**

### Bước 3. Đặt OCR Mode
Chọn:
```text
OCR Mode = all
```
Thiết lập này phù hợp cho phần lớn tài liệu scan, sách, dược điển, tài liệu PDF ảnh hoặc file có text layer không sạch.

### Bước 4. Chọn OCR Lang
- Tài liệu giản thể: `chi_sim+eng`
- Tài liệu phồn thể: `chi_tra+eng`

### Bước 5. Chọn Source Lang
- Giản thể: `zh-CN`
- Phồn thể: `zh-TW`

### Bước 6. Chọn Target Lang
- `vi` nếu muốn đọc và sử dụng bằng tiếng Việt
- `en` nếu muốn tạo bản tiếng Anh

### Bước 7. Chạy thử vài trang trước
Nếu tài liệu dài, nên chạy thử một phần nhỏ trước để đánh giá:
- chất lượng OCR
- thuật ngữ chuyên ngành
- cách xuống dòng
- độ sạch của bản dịch

Sau khi thấy ổn mới chạy toàn bộ tài liệu.

---

## 6) Khi nào nên để OCR Mode = all

Nên dùng **OCR Mode = all** trong các trường hợp sau:

- PDF là bản scan thật, không phải PDF text
- chữ nằm trong ảnh
- tài liệu cũ, mờ, nghiêng, lệch hoặc có nền không sạch
- sách scan nhiều cột
- dược điển, chuyên luận, sách có bảng, công thức, tiếng Anh xen tiếng Trung
- file office hoặc PDF sau chuyển đổi nhưng text layer bị lỗi

**Ưu điểm của chế độ này:**
- giảm nguy cơ bỏ sót vùng chữ
- phù hợp với tài liệu hỗn hợp ảnh + text
- hữu ích với tài liệu chuyên ngành có tiếng Anh đi kèm

---

## 7) Ví dụ thực tế: trang Dược điển Trung Quốc

Với trang như:

- **中国药典 2025 年版**
- có nội dung chuyên luận dược liệu
- có lẫn tiếng Anh như **POWDERED BUFFALO HORN EXTRACT**
- bố cục dạng sách scan

Thiết lập khuyến nghị là:

```text
OCR Mode    = all
OCR Lang    = chi_sim+eng
Source Lang = zh-CN
Target Lang = vi
```

Hoặc nếu cần bản tiếng Anh:

```text
OCR Mode    = all
OCR Lang    = chi_sim+eng
Source Lang = zh-CN
Target Lang = en
```

Đây là cấu hình phù hợp vì:
- trang dùng **chữ Trung giản thể**
- có **tiếng Anh đi kèm**
- tài liệu có đặc điểm của **bản scan sách chuyên ngành**

---

## 8) Mẹo để OCR và dịch sạch hơn

### Ưu tiên file nguồn rõ nét
- scan thẳng trang
- tránh nền xám đậm
- hạn chế bóng, nghiêng, méo
- độ phân giải đủ cao

### Với tài liệu có tiếng Anh xen tiếng Trung
Nên giữ phần `+eng` trong OCR Lang:
- `chi_sim+eng`
- `chi_tra+eng`

Điều này giúp phần mềm nhận dạng tốt hơn:
- tên hoạt chất
- tên Latin
- tiêu đề tiếng Anh
- từ viết tắt chuyên ngành
- thông số kỹ thuật

### Chạy thử trước khi chạy toàn bộ
Đặc biệt với:
- sách dày
- dược điển
- tiêu chuẩn
- brochure nhiều cột
- tài liệu có bảng

### Kiểm tra vài điểm sau khi dịch
- tên dược liệu
- tên hóa học
- hàm lượng, đơn vị
- số mục, số bảng
- tiêu đề và tên Latin
- các đoạn có trộn Trung - Anh

---

## 9) Lỗi thường gặp và cách xử lý

### Lỗi 1. Chữ OCR ra sai nhiều
**Nguyên nhân thường gặp:**
- chọn sai `chi_sim` / `chi_tra`
- file scan mờ
- trang lệch hoặc quá nhỏ
- ảnh có nền xấu

**Cách xử lý:**
- kiểm tra lại giản thể hay phồn thể
- ưu tiên `OCR Mode = all`
- dùng file scan rõ hơn nếu có

### Lỗi 2. Dịch đúng ít, sai nhiều ở thuật ngữ
**Nguyên nhân thường gặp:**
- OCR đầu vào chưa sạch
- tài liệu quá nhiều thuật ngữ chuyên ngành
- nhầm Source Lang

**Cách xử lý:**
- sửa lại cặp `OCR Lang` và `Source Lang`
- chạy thử vài trang trước
- ưu tiên xuất ra `en` nếu cần bản trung gian dễ hậu kiểm hơn

### Lỗi 3. Bản dịch bị lẫn tiếng Anh hoặc bỏ sót tiêu đề tiếng Anh
**Cách xử lý:**
- giữ `+eng` trong OCR Lang
- không chỉ dùng `chi_sim` hoặc `chi_tra` đơn lẻ nếu tài liệu có tiếng Anh xen kẽ

### Lỗi 4. Dùng đúng OCR Lang nhưng vẫn sai nhiều
**Khả năng cao do chất lượng scan**, không phải do lựa chọn ngôn ngữ.  
Khi đó cần ưu tiên cải thiện ảnh đầu vào hoặc xử lý lại file scan.

---

## 10) Cấu hình khuyên dùng để nhớ nhanh

### Trường hợp phổ biến nhất: tài liệu Trung Quốc đại lục
```text
OCR Mode    = all
OCR Lang    = chi_sim+eng
Source Lang = zh-CN
Target Lang = vi
```

### Khi muốn bản tiếng Anh
```text
OCR Mode    = all
OCR Lang    = chi_sim+eng
Source Lang = zh-CN
Target Lang = en
```

### Khi tài liệu là phồn thể
```text
OCR Mode    = all
OCR Lang    = chi_tra+eng
Source Lang = zh-TW
Target Lang = vi hoặc en
```

---

## 11) Kết luận

Đối với **Translator Docs Book v5 GUI**, khi dịch tài liệu tiếng Trung, cách chọn đúng nhất là:

- xác định trước tài liệu là **giản thể** hay **phồn thể**
- đặt **OCR Mode = all** cho tài liệu scan hoặc PDF ảnh
- ghép đúng cặp:
  - `chi_sim+eng` với `zh-CN`
  - `chi_tra+eng` với `zh-TW`
- chọn `vi` hoặc `en` theo nhu cầu đầu ra

Nếu gặp trang giống **中国药典 2025 年版**, nên coi đó là **giản thể**, và dùng:

```text
OCR Mode    = all
OCR Lang    = chi_sim+eng
Source Lang = zh-CN
Target Lang = vi hoặc en
```

Cấu hình đúng ngay từ đầu sẽ giúp OCR sạch hơn, dịch ổn định hơn và giảm đáng kể thời gian hậu kiểm.
