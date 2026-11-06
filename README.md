# BÀI 9: XÂY DỰNG PROMPT 3 THÀNH PHẦN GIẢI MÃ THÔNG BÁO LỖI TRẠM SẠC CÙNG TRỢ LÝ AI

## PHẦN 1: THIẾT KẾ PROMPT 3 THÀNH PHẦN CHUẨN HÓA

### Câu 1. Vì sao câu hỏi ngắn khiến AI đưa ra câu trả lời sai lệch?

Câu hỏi: "AI ơi phần mềm trạm sạc của tôi bị hỏng rồi làm sao đây?" khiến AI trả lời sai lệch vì:

- Thiếu ngữ cảnh: Không cho AI biết đang sử dụng trạm sạc VoltCharge, hệ điều hành Windows 11 hay thiết bị nào đang gặp sự cố.
- Không cung cấp thông báo lỗi: AI không biết lỗi cụ thể là gì, không thể xác định nguyên nhân chính xác.
- Yêu cầu không rõ ràng: Không nói rõ muốn AI dịch lỗi, giải thích nguyên nhân hay hướng dẫn cách khắc phục.

Vì thiếu thông tin, AI có thể tự suy đoán nguyên nhân và đưa ra lời khuyên không phù hợp. Đây là hiện tượng AI Hallucination (ảo giác AI), tức là AI tạo ra thông tin nghe có vẻ hợp lý nhưng không đúng với tình huống thực tế.

### Câu 2. Soạn thảo Prompt 3 Thành phần hoàn chỉnh

Sử dụng công thức: Ngữ cảnh (Context) → Lỗi nguyên văn (Raw Error) → Yêu cầu (Instruction).

Prompt gửi cho ChatGPT/Gemini:

[***CONTEXT - NGỮ CẢNH***]

Tôi là nhân viên kỹ thuật mới, đang trực vận hành hệ thống trạm sạc xe điện VoltCharge tại Bến xe Miền Đông.

Thiết bị gặp sự cố là trạm sạc nhanh số 04, sử dụng hệ điều hành Windows 11. Khi khởi động phần mềm điều khiển trạm sạc, hệ thống đột ngột dừng hoạt động và hiển thị thông báo lỗi trên Terminal.

[***RAW ERROR - LỖI NGUYÊN VĂN***]

2026-09-21 21:15:30 [FATAL] ControllerDaemon failed to start.

System.UnauthorizedAccessException: Access to the path is denied.

InnerException: None. Process terminated with exit code 5 (0x00000005).

Suggestion: Run the application with elevated administrator privileges or verify NTFS file permissions.

[INSTRUCTION - YÊU CẦU]

1. Hãy dịch thông báo lỗi trên sang tiếng Việt đơn giản, dễ hiểu cho người mới học công nghệ thông tin.
2. Phân tích nguyên nhân gốc rễ khiến phần mềm không thể khởi động.
3. Đưa ra 3 bước khắc phục cụ thể trên Windows 11, ưu tiên cách an toàn và dễ thực hiện.
4. Nếu chưa đủ thông tin để xác định nguyên nhân, hãy nói rõ điều chưa chắc chắn và đề xuất cách kiểm tra, không tự suy đoán.

## PHẦN 2: GIẢI MÃ LỖI VÀ KỊCH BẢN KHẮC PHỤC

### Câu 3. Dịch và giải thích nguyên nhân gốc rễ của lỗi UnauthorizedAccessException

1\. Dịch thông báo lỗi

| Thông báo                        | Ý nghĩa tiếng Việt                                       |
| -------------------------------- | -------------------------------------------------------- |
| FATAL                            | Lỗi nghiêm trọng                                         |
| ControllerDaemon failed to start | Tiến trình điều khiển không thể khởi động                |
| UnauthorizedAccessException      | Lỗi không có quyền truy cập                              |
| Access to the path is denied     | Không được phép truy cập vào đường dẫn này               |
| InnerException: None             | Không có lỗi phụ bên trong được ghi nhận                 |
| Exit code 5                      | Mã lỗi 5, thường liên quan đến quyền truy cập bị từ chối |
| Run as Administrator             | Chạy bằng quyền Quản trị viên                            |

2\. Nguyên nhân gốc rễ

Lỗi xảy ra vì phần mềm VoltCharge muốn tạo hoặc ghi dữ liệu vào file:

`C:\Program Files\VoltCharge\data\session.log`

Tuy nhiên, thư mục Program Files là khu vực Windows bảo vệ. Phần mềm hiện tại không có đủ quyền để ghi dữ liệu vào đây.

Kết luận: Đây chủ yếu là lỗi phân quyền truy cập file trên Windows, không phải bằng chứng cho thấy trạm sạc bị hỏng phần cứng.

### Câu 4. Ba bước xử lý cụ thể trên Windows 11

Mục tiêu là cấp đúng quyền cần thiết để phần mềm có thể ghi dữ liệu vào file session.log.

Bước 1: Chạy phần mềm bằng quyền Administrator

1. Tìm biểu tượng phần mềm VoltCharge trên Desktop hoặc trong Start Menu.
2. Nhấn chuột phải vào biểu tượng phần mềm.
3. Chọn Run as administrator.
4. Nếu Windows hỏi quyền xác nhận, chọn Yes (nếu đây là phần mềm được đơn vị kỹ thuật cho phép).

Sau đó kiểm tra xem phần mềm có khởi động bình thường không.

Bước 2: Kiểm tra và cấp quyền ghi cho thư mục data

1. Mở File Explorer.
2. Truy cập đường dẫn:

`C:\Program Files\VoltCharge\`

3. Nhấn chuột phải vào thư mục `data` → chọn Properties.
4. Chọn tab Security → Edit.
5. Chọn đúng tài khoản Windows hoặc tài khoản dịch vụ chạy phần mềm VoltCharge.
6. Kiểm tra quyền Write (Ghi dữ liệu).
7. Nếu chưa có, nhờ quản trị viên cấp quyền Write hoặc Modify phù hợp cho tài khoản đó.
8. Chọn Apply → OK.

Lưu ý: Không cấp quyền Full Control cho Everyone hoặc Users một cách tùy tiện vì có thể khiến dữ liệu trạm sạc bị thay đổi trái phép.

Bước 3: Khởi động lại và kiểm tra hoạt động

1. Đóng phần mềm VoltCharge nếu đang mở.
2. Khởi động lại phần mềm bằng quyền phù hợp.
3. Kiểm tra xem trạm sạc số 04 có khởi động bình thường không.
4. Kiểm tra file `session.log` xem có ghi dữ liệu mới hay không.
5. Nếu vẫn xuất hiện lỗi Access is denied, báo quản trị viên kiểm tra quyền của tài khoản dịch vụ và nhật ký hệ thống.

Lưu ý an toàn: Vì đây là hệ thống trạm sạc thực tế, không tự ý thay đổi quyền thư mục hoặc khởi động lại dịch vụ điều khiển khi chưa được người phụ trách cho phép. Chỉ thử vận hành lại khi đã xác nhận an toàn và được phép.

### Câu 5. Bẫy an ninh: Xử lý chuỗi API_KEY trước khi gửi cho AI

Giả sử thông báo lỗi có chứa chuỗi:

`API_KEY: volt_secret_token_889922`

Cách xử lý đúng:

Trước khi dán thông báo lỗi vào ChatGPT hoặc Gemini, phải xóa hoặc che giấu chuỗi API Key và thay thế bằng nội dung giả lập.

Ví dụ:

Thông tin ban đầu:

`API_KEY: volt_secret_token_889922`

Sau khi che giấu:

`API_KEY: [REDACTED]`

Sau đó mới gửi phần nhật ký lỗi đã được làm sạch cho AI.

Vì sao phải làm như vậy?

- Bảo vệ thông tin bí mật: API Key giống như chìa khóa cho phép truy cập vào một dịch vụ hoặc tài khoản.
- Ngăn truy cập trái phép: Nếu người khác lấy được API Key, họ có thể sử dụng dịch vụ bằng quyền được cấp cho chủ sở hữu.
- Tránh rò rỉ dữ liệu: Thông tin bí mật không nên xuất hiện trong nội dung trò chuyện hoặc tài liệu chia sẻ không được phép.

Nếu API Key thật đã bị gửi lên AI hoặc bị lộ ở nơi khác, cần báo người quản lý và thu hồi (Revoke) hoặc thay thế khóa ngay.

Nguyên tắc: Tuyệt đối không gửi mật khẩu, API Key, Secret, mã OTP hoặc thông tin xác thực lên cửa sổ chat AI.

## PHẦN 3: TỔNG KẾT CUỐI BÀI

Qua bài tập, em rút ra được những kiến thức quan trọng:

1. Biết sử dụng công thức Prompt 3 Thành phần gồm Context, Raw Error và Instruction để đặt câu hỏi cho AI rõ ràng hơn.
2. Biết đọc và hiểu thông báo lỗi tiếng Anh, đặc biệt là lỗi UnauthorizedAccessException.
3. Hiểu được nguyên nhân lỗi Access is denied do phần mềm không có quyền ghi dữ liệu vào thư mục được bảo vệ.
4. Biết cách sử dụng Run as Administrator và kiểm tra quyền truy cập thư mục trên Windows 11.
5. Biết bảo vệ thông tin bí mật bằng cách che giấu API Key trước khi gửi nhật ký lỗi cho AI.
6. Không làm theo mọi hướng dẫn của AI một cách máy móc mà cần kiểm tra tính an toàn và chính xác trước khi thực hiện.
