# PharmApp Translator

Bộ công cụ desktop dùng để dịch sách, bài báo khoa học, tài liệu Office và kiểm tra lại các gói bản dịch sau khi xử lý.

PharmApp Translator phù hợp cho người dùng cần một quy trình rõ ràng:

1. **Dịch tài liệu nguồn** bằng **Translator Docs Book v5 GUI**
2. **Mở và kiểm tra gói kết quả** bằng **Translation Package Viewer v7**

Repository này phù hợp để đăng **release assets** cho các file `.exe` đã build sẵn.

---

## Các ứng dụng trong bộ release

### 1) Translator Docs Book v5 GUI
Ứng dụng này dùng để:
- thêm file hoặc thư mục vào hàng đợi
- chọn nơi đọc dữ liệu đầu vào và nơi lưu kết quả đầu ra
- chạy OCR khi cần
- dịch tài liệu sang bộ gói kết quả có cấu trúc rõ ràng
- lưu và nạp profile làm việc
- tiếp tục từ trạng thái lần chạy trước
- theo dõi tiến độ qua bảng tài liệu và log

### 2) Translation Package Viewer v7
Ứng dụng này dùng để:
- mở các thư mục kết quả đã dịch xong
- quét thư viện gói bản dịch
- đọc song song nguồn và đích
- tìm kiếm tài liệu và segment
- kiểm tra QA flags và số lượng lỗi
- sao chép prompt để AI review / fix từng đoạn
- lưu profile và khôi phục workspace lần trước

---

## Tính năng chính

- Chạy trực tiếp bằng **file EXE trên Windows**
- Giao diện **English / Vietnamese**
- Hỗ trợ giao diện **Light / Dark / System**
- Có **profile** để lưu cấu hình dùng lại
- Có **resume / restore previous session**
- Bảng dữ liệu **sort theo cột**
- Giao diện nhiều vùng làm việc
- Xử lý theo hàng đợi cho nhiều tài liệu
- Hỗ trợ review và QA bản dịch
- Chế độ đọc song ngữ song song
- Tìm kiếm trên tài liệu và segment đã dịch

---

## Gợi ý cấu trúc release

Khi đăng GitHub Release, có thể đóng gói như sau:

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

Hoặc tách thành các file ZIP riêng:

- `PharmAppTranslator_vX.Y_win64.zip`
- `Apps_Tesseract5.5.0_portable.zip`

---

## Cách đặt các Apps hỗ trợ cho bản EXE

### Tesseract OCR
Nếu người dùng cần OCR cho PDF scan hoặc tài liệu dạng ảnh, nên đặt Tesseract trong thư mục `Apps` gần bộ release.

Cách bố trí khuyến nghị:

```text
Release/
├─ translator_docs_book_v5_gui.exe
├─ translator_docs_book_viewer_v7_gui.exe
└─ ../Apps/Tesseract5.5.0/
```

Cách portable dễ dùng nhất:

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

Cách này giúp file EXE dễ tự nhận Tesseract hơn mà không cần người dùng cấu hình thủ công quá nhiều.

### Calibre
Nên cài Calibre nếu người dùng cần hỗ trợ các định dạng ebook như Kindle hoặc nhóm MOBI.

### LibreOffice
Nên cài LibreOffice nếu người dùng cần chuyển đổi các định dạng Office cũ trước khi dịch.

---

## Định dạng đầu vào phù hợp

Bản release này hướng đến các nhu cầu dịch tài liệu thực tế, với các định dạng thông dụng như:

- PDF
- DOCX
- PPTX
- XLSX
- EPUB
- HTML / HTM
- Markdown
- TXT / CSV / TSV / JSON / XML / YAML

Một số định dạng ebook hoặc Office cũ có thể cần thêm ứng dụng hỗ trợ ngoài.

---

## Hướng dẫn dùng nhanh

### Bước 1 — Chuẩn bị thư mục release
Tải bộ release và để hai file `.exe` cùng một chỗ.

Nếu cần OCR, đặt **Tesseract** vào đúng thư mục `Apps/Tesseract5.5.0/` như gợi ý.

### Bước 2 — Chạy ứng dụng dịch
Mở `translator_docs_book_v5_gui.exe`.

Quy trình cơ bản:
1. Chọn **Input Path**
2. Chọn **Output Path**
3. Thêm file hoặc thư mục
4. Chọn translator, source language, target language và OCR mode
5. Bấm **Start**

### Bước 3 — Kiểm tra kết quả
Mở `translator_docs_book_viewer_v7_gui.exe`.

Quy trình cơ bản:
1. Chọn **Library root** là thư mục chứa kết quả đã dịch
2. Bấm **Scan**
3. Chọn tài liệu
4. Đọc theo chế độ song song source/target
5. Dùng tab Search và QA để rà lỗi

---

## Gói kết quả đầu ra thường có gì?

Mỗi tài liệu sau khi dịch có thể tạo ra một gói kết quả có cấu trúc rõ ràng, thường gồm:

- bản gốc
- dữ liệu trích xuất
- bản song ngữ
- bản chỉ có ngôn ngữ đích
- file JSON bundle bản dịch
- log
- report
- manifest

Nhờ vậy, bộ release này không chỉ phục vụ dịch tài liệu mà còn phù hợp cho review, QA và lưu trữ lâu dài.

---

## Trường hợp sử dụng phù hợp

- bài báo khoa học
- sách và tài liệu hướng dẫn
- PDF kỹ thuật
- tài liệu nghiên cứu đa ngôn ngữ
- quy trình review nội bộ
- kiểm tra chất lượng bản dịch

---

## Video giới thiệu

Demo / giới thiệu:

- YouTube: https://youtu.be/KZjima0vD2A

---

## Gợi ý khi đăng GitHub Release

Tên release gợi ý:

```text
PharmApp Translator v1.0 - Windows EXE Release
```

Mô tả release ngắn gợi ý:

```text
Bản Windows portable của Translator Docs Book v5 GUI và Translation Package Viewer v7 để dịch tài liệu, mở gói kết quả, tìm kiếm và kiểm tra QA.
```

Các asset nên đính kèm:

- `translator_docs_book_v5_gui.exe`
- `translator_docs_book_viewer_v7_gui.exe`
- `README.md`
- `README.vi.md`
- gói `Apps/` nếu muốn phát hành kèm công cụ hỗ trợ

---

## Website và liên kết dự án

- https://www.nghiencuuthuoc.com
- https://www.pharmapp.dev

---

## License

Hãy bổ sung license của dự án trước khi public chính thức.

