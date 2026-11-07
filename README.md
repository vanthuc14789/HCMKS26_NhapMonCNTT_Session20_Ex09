# SESSION 20 – BÀI TẬP: THỰC HÀNH PROMPT 3 THÀNH PHẦN
## PHẦN 1: THIẾT KẾ PROMPT 3 THÀNH PHẦN CHUẨN HÓA

### 1. Vì sao câu hỏi ngắn khiến AI trả lời sai?

Câu hỏi "AI ơi phần mềm trạm sạc của tôi bị hỏng rồi làm sao đây?" quá chung chung, không cung cấp thông tin về thiết bị, hệ điều hành và thông báo lỗi cụ thể.

Vì vậy, AI không xác định được nguyên nhân thực tế mà phải tự suy đoán. Đây là hiện tượng AI Hallucination (ảo giác AI), tức là AI đưa ra thông tin nghe có vẻ hợp lý nhưng không chính xác.

### 2. Prompt 3 thành phần hoàn chỉnh

[Context – Ngữ cảnh]

Tôi là nhân viên kỹ thuật trực ca đêm tại Bến xe Miền Đông, đang vận hành trạm sạc xe điện VoltCharge số 04 trên hệ điều hành Windows 11. Trạm sạc đột ngột dừng hoạt động khi khởi động phần mềm điều khiển.

[Raw Error – Lỗi nguyên văn]

```
[TERMINAL ERROR LOG - VOLTCHARGE CHARGER #04]
2026-09-21 21:15:30 [FATAL] ControllerDaemon failed to start.
System.UnauthorizedAccessException: Access to the path
'C:\Program Files\VoltCharge\data\session.log' is denied.
at System.IO.FileStream.ValidateFileHandle(SafeHandle handle)
at VoltCharge.Core.SessionManager.Initialize()
InnerException: None.
Process terminated with exit code 5 (0x00000005).
Suggestion: Run the application with elevated administrator privileges
or verify NTFS file permissions.
```

[Instruction – Yêu cầu]

Hãy đóng vai một kỹ sư hỗ trợ kỹ thuật, thực hiện các yêu cầu sau:

1. Dịch thông báo lỗi sang tiếng Việt đơn giản, dễ hiểu.
2. Phân tích nguyên nhân gốc rễ khiến phần mềm không thể khởi động.
3. Đưa ra 3 bước khắc phục cụ thể trên Windows 11.
4. Hướng dẫn kiểm tra quyền Administrator và quyền ghi file cho thư mục `data`.
5. Cảnh báo những thao tác nguy hiểm có thể ảnh hưởng đến hệ thống.

## PHẦN 2: GIẢI MÃ LỖI VÀ KỊCH BẢN KHẮC PHỤC

### 3. Dịch và giải thích nguyên nhân lỗi

Thông báo lỗi chính:

`UnauthorizedAccessException: Access to the path ... is denied`

Dịch nghĩa: Không được phép truy cập vào đường dẫn này.

Nguyên nhân:

Phần mềm VoltCharge muốn tạo hoặc ghi dữ liệu vào file `session.log` trong thư mục:

`C:\Program Files\VoltCharge\data\`

Tuy nhiên, Windows 11 đang chặn thao tác ghi file do tài khoản chạy phần mềm không có đủ quyền truy cập.

Mã lỗi `0x00000005` có nghĩa là Access Denied (bị từ chối truy cập).

Kết luận: Đây là lỗi phân quyền hệ thống Windows, không phải bằng chứng cho thấy dây điện hoặc phần cứng trạm sạc bị hỏng.

### 4. Ba bước khắc phục trên Windows 11

Bước 1: Chạy phần mềm bằng quyền Administrator

- Nhấn chuột phải vào biểu tượng VoltCharge.
- Chọn `Run as administrator`.
- Nếu Windows hỏi quyền, chọn `Yes`.
- Kiểm tra xem phần mềm có khởi động được không.

Bước 2: Kiểm tra và phân quyền ghi thư mục data

- Mở File Explorer.
- Truy cập `C:\Program Files\VoltCharge\`.
- Nhấn chuột phải vào thư mục `data`, chọn `Properties`.
- Chọn tab `Security`.
- Chọn đúng tài khoản hoặc nhóm chạy dịch vụ VoltCharge.
- Nhấn `Edit` và cấp quyền `Write` hoặc `Modify` nếu được quản trị viên phê duyệt.
- Nhấn `Apply` và `OK`.

Lưu ý: Chỉ cấp quyền cần thiết cho đúng tài khoản dịch vụ, không cấp `Everyone: Full Control` hoặc mở toàn quyền cho mọi người.

Bước 3: Khởi động lại và kiểm tra

- Khởi động lại phần mềm hoặc dịch vụ ControllerDaemon theo quy trình vận hành.
- Kiểm tra xem file `session.log` có được ghi dữ liệu không.
- Theo dõi màn hình Terminal để xác nhận lỗi đã hết.
- Chỉ đưa trụ sạc hoạt động trở lại khi kiểm tra an toàn điện và quy trình vận hành đạt yêu cầu.

### 5. Bẫy an ninh: Xử lý API_KEY

Nếu đoạn mã lỗi chứa chuỗi:

```
API_KEY: volt_secret_token_889922
```

Kỹ thuật viên phải thực hiện:

- Tuyệt đối không gửi nguyên chuỗi API Key lên ChatGPT hoặc Gemini.
- Xóa hoàn toàn giá trị bí mật hoặc thay bằng `[REDACTED]`.
- Chỉ gửi phần thông báo lỗi cần thiết để AI phân tích.
- Nếu API Key đã bị gửi lên AI hoặc xuất hiện ở nơi không an toàn, cần báo quản trị viên và thu hồi, tạo khóa mới.

Lý do: API Key là thông tin bí mật dùng để xác thực hệ thống. Nếu bị lộ, người khác có thể lợi dụng để truy cập trái phép, sử dụng dịch vụ hoặc gây thiệt hại cho dự án.

### 6. Ba nguyên tắc an toàn khi sử dụng AI

1. Không chạy lệnh mù quáng: Phải kiểm tra câu lệnh AI đưa ra trước khi thực hiện.
2. Chống ảo giác AI: Cung cấp đầy đủ ngữ cảnh và thông báo lỗi nguyên văn để AI không đoán mò.
3. Bảo vệ thông tin bí mật: Không gửi mật khẩu, API Key, mã OTP hoặc thông tin đăng nhập lên AI.
