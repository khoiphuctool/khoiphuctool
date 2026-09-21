# KhoiPhucTool

Phiên bản hiện tại: V7.49

KhoiPhucTool là ứng dụng Windows hỗ trợ khôi phục mật khẩu cho các tệp Office và Archive dưới dạng desktop tool, với khả năng chạy trên CPU hoặc tăng tốc bằng GPU thông qua Hashcat. Ứng dụng nhắm tới mục đích hỗ trợ kiểm thử, phục hồi dữ liệu hợp pháp và khôi phục mật khẩu đối với các tệp thuộc quyền sở hữu hoặc quản lý của người dùng.

## Mục tiêu

- Khôi phục mật khẩu cho file Office: Excel, Word, PowerPoint
- Hỗ trợ các định dạng archive phổ biến: RAR, ZIP, 7z
- Hỗ trợ các phương pháp tấn công: từ điển, brute-force, pattern, incremental
- Tích hợp GPU acceleration bằng Hashcat khi có thiết bị hỗ trợ
- Cung cấp giao diện tiếng Việt, dễ sử dụng và hỗ trợ đa luồng

## Tính năng chính

- Hỗ trợ file Office: .xlsx, .xls, .xlsb, .xlsm, .docx, .doc, .pptx, .ppt
- Hỗ trợ archive: .rar, .zip, .7z
- Tự động phát hiện định dạng tệp và kiểu mã hóa
- Hỗ trợ kiểm tra trước khi tấn công để ước lượng hiệu suất
- Hỗ trợ dictionary attack, mask attack, pattern attack và brute force
- Hỗ trợ tối ưu GPU qua Hashcat 7.1.2
- Hỗ trợ nhiều worker/thread để tăng hiệu suất và dễ dàng pause/resume
- Tự động xuất mật khẩu tìm được ra file TXT
- Đa dạng chế độ engine: Auto, CPU, GPU

## Hỗ trợ định dạng

### Office
- Excel: .xls, .xlsx, .xlsm, .xlsb
- Word: .doc, .docx
- PowerPoint: .ppt, .pptx
- VBA Macro / encrypted Office nội bộ

### Archive
- RAR 3, RAR 5
- ZIP (AES, standard)
- 7z (yêu cầu 7z.exe nếu dùng định dạng .7z)

## Yêu cầu hệ thống

### Cần thiết
- Windows 10/11
- Python 3.14 để build từ mã nguồn
- Truy cập bộ nhớ và ổ cứng đủ để lưu file khôi phục và checkpoint

### GPU (tùy chọn)
- Card đồ họa hỗ trợ GPU acceleration
- Cài đặt và đặt thư mục Hashcat cạnh file thực thi
- Cấu trúc đề xuất:

```text
dist/
  khoiphuctool.exe
  hashcat-7.1.2/
```

> Nếu muốn dùng GPU, hãy đảm bảo thư mục hashcat-7.1.2 nằm ở vị trí cùng cấp với file executable.

### 7z
- Đối với file .7z, cần cài đặt 7-Zip và có 7z.exe trong hệ thống.
- WinRAR không thể xử lý trực tiếp file .7z trong trường hợp cần mở archive encrypted.

## Cách chạy

### Chạy ứng dụng đã build
- Chạy file `khoiphuctool.exe`
- Hoặc đặt `hashcat-7.1.2` cạnh file exe nếu cần GPU acceleration

### Chạy từ mã nguồn
```bat
python khoiphuctool.PY
```

### Build ứng dụng
```bat
BUILD_KHOIPHUCTOOL.bat
```

Script build sẽ:
- kiểm tra Python 3.14
- compile `license_core.pyx`
- thực hiện PyInstaller build
- xuất file exe trong thư mục `dist/`

## Cấu trúc thư mục chính

```text
.
├── khoiphuctool.PY          # giao diện chính và engine chính
├── hashcat_engine.py        # tích hợp Hashcat
├── hashcat-7.1.2/          # Hashcat runtime
├── dictionary_generator.py  # sinh từ điển / charset
├── version.py               # phiên bản ứng dụng
├── BUILD_KHOIPHUCTOOL.bat   # build script
├── license_core.pyx         # mô-đun license/native
├── tests/                   # kiểm thử
├── WEB/                     # tài liệu và giao diện web/README
└── dist/                    # file build sau khi đóng gói
```

## Lưu ý pháp lý và trách nhiệm

⚠️ Phần mềm này chỉ được sử dụng cho các trường hợp hợp pháp, có quyền sở hữu hoặc quyền được phép kiểm thử, phục hồi dữ liệu, hoặc khôi phục mật khẩu cho tài sản kỹ thuật số của chính bạn.

- Không sử dụng để truy cập trái phép vào dữ liệu, tài khoản hoặc tệp của người khác
- Không sử dụng khi không có quyền hợp pháp
- Tác giả và người phát triển không chịu trách nhiệm đối với các hành vi vi phạm pháp luật hoặc sử dụng sai mục đích

## Ghi chú phát triển

- Phiên bản hiện tại đang được quản lý ở `version.py`
- Tính năng GPU và resume checkpoint được tích hợp trong các module liên quan như `hashcat_engine.py`, `hashcat_command_builder.py` và các worker module
- Nếu cần mở rộng khả năng hỗ trợ hoặc tối ưu hóa hiệu năng, nên giữ nguyên nguyên tắc: chạy ổn định trên CPU, tăng tốc tùy chọn bằng GPU khi có sẵn

## Liên hệ và đóng góp

Mọi góp ý, phản hồi hoặc yêu cầu cải tiến xin gửi qua kênh quản lý dự án hoặc thông tin liên hệ được lưu trong hệ thống nội bộ của dự án. Mục tiêu là giữ ứng dụng tối ưu, ổn định và an toàn hơn cho người dùng hợp pháp.

---

© KhoiPhucTool Team
