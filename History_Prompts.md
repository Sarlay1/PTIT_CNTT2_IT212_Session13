======================================================================
HISTORY_PROMPTS.TXT - AI-ASSISTED SYSTEM DESIGN (LOGITRACK SYSTEM)
Sinh viên thực hiện: Đỗ Tiến Đạt
======================================================================

[PROMPT 1] - Thiết lập vai trò, bối cảnh và phạm vi hệ thống (System Context & Role)
----------------------------------------------------------------------
Bạn là một Principal System Analyst và IT Consultant giàu kinh nghiệm. Tôi muốn bạn hỗ trợ tôi thiết kế một hệ thống mang tên "LogiTrack" - Nền tảng Quản lý Giao nhận & Logistics toàn diện.
Hệ thống bắt buộc phải có ít nhất 3 phân hệ chính: Quản lý đơn hàng & giá (Order & Pricing), Điều phối tài xế (Fleet & Dispatch), và Theo dõi thời gian thực (Tracking & Notification).
Có 3 Actors chính tham gia trực tiếp: Khách hàng gửi (Sender), Tài xế (Driver), và Điều phối viên (Dispatcher/Admin).
Trước hết, hãy viết cho tôi phần Tổng quan dự án (Project Overview) mục tiêu kinh doanh và mô tả tổng quát luồng đi của một đơn hàng từ lúc tạo đến lúc giao thành công. Yêu cầu viết ngắn gọn, chuyên nghiệp, không có lời thoại thừa của AI.


[PROMPT 2] - Khai thác chuyên sâu User Stories theo từng đối tượng (User Stories Specification)
----------------------------------------------------------------------
Dựa trên tổng quan hệ thống LogiTrack vừa thiết lập, hãy xây dựng danh sách User Stories chi tiết cho từng Actor (Sender, Driver, Dispatcher). Cấu trúc mỗi User Story cần tuân thủ format chuẩn: "As a [role], I want to [action], so that [benefit]". Trình bày kết quả dưới dạng một bảng biểu (Table) gồm các cột: ID, Actor, User Story, và Phân hệ (Module) tương ứng.


[PROMPT 3] - Chỉnh sửa nghiệp vụ thực tế & Thêm ràng buộc tính toán (Business Logic Refinement)
----------------------------------------------------------------------
Phần User Stories cơ bản đã tốt nhưng cần thực tế hơn. Trong phân hệ "Order & Pricing", hãy bổ sung thêm các tính năng mang tính thực tế cao sau đây vào danh sách User Stories:
1. Khách hàng (Sender) có thể áp dụng mã giảm giá (Discount Code) dạng phần trăm hoặc số tiền cố định.
2. Hệ thống phải tự động tính toán và cộng thêm phụ phí (Surcharge) động khi phát hiện các điều kiện bất lợi như: giao hàng vào giờ cao điểm (Peak hours) hoặc thời tiết xấu (Heavy rain/Storm).
   Hãy cập nhật và làm sâu sắc thêm các User Stories liên quan của cả Khách hàng và Quản trị viên hệ thống để phản ánh đúng logic này.


[PROMPT 4] - Thiết kế kiến trúc chức năng bằng sơ đồ Use Case (Functional Design - Use Case Diagram)
----------------------------------------------------------------------
Từ danh sách chức năng và User Stories hoàn chỉnh ở trên, hãy thiết kế một sơ đồ Use Case (Use Case Diagram) tổng thể cho hệ thống LogiTrack bằng ngôn ngữ mã nguồn Mermaid.
Yêu cầu:
- Sử dụng các `subgraph` để bao bọc và phân tách rõ ràng 3 phân hệ (Order & Pricing, Fleet & Dispatch, Tracking & Notification).
- Thể hiện rõ mối quan hệ kết nối (tương tác trực tiếp) từ 3 Actors (Sender, Driver, Dispatcher) đến các Use Case tương ứng của họ.
- Chỉ trả về đoạn mã Mermaid thuần túy nằm trong block code, không giải thích gì thêm.


[PROMPT 5] - Tối ưu hóa cấu trúc Use Case (Use Case Optimization)
----------------------------------------------------------------------
Sơ đồ Use Case bằng Mermaid vừa rồi nhìn chung khá đầy đủ, nhưng tôi muốn bạn tối ưu hóa lại cấu trúc logic. Hãy bổ sung thêm các quan hệ phụ thuộc hệ thống:
- Từ Use Case "Tạo đơn hàng" (Create Order), hãy thêm quan hệ <<include>> đến Use Case "Tính toán giá và phụ phí".
- Thêm một quan hệ <<extend>> từ Use Case "Tạo đơn hàng" sang Use Case "Áp dụng mã giảm giá" (vì không phải đơn hàng nào cũng có mã giảm giá).
  Hãy cập nhật lại mã nguồn Mermaid của sơ đồ Use Case theo đúng quy chuẩn phân tích thiết kế phần mềm này.


[PROMPT 6] - Thiết kế kiến trúc dữ liệu - Sơ đồ ERD (Data Architecture - ERD Diagram)
----------------------------------------------------------------------
Bây giờ chúng ta sẽ chuyển sang tầng dữ liệu. Hãy thiết kế mô hình thực thể mối quan hệ (ERD) cho hệ thống LogiTrack sử dụng cú pháp mã nguồn Mermaid.
Cơ sở dữ liệu tối thiểu phải có các thực thể (bảng): Users, Orders, Drivers, Shipments, TrackingLogs, và Discounts.
Yêu cầu cụ thể:
- Trong mỗi thực thể, định nghĩa rõ các trường (Attributes) quan trọng, xác định rõ thuộc tính nào là Khóa chính (PK) và Khóa ngoại (FK), kèm theo kiểu dữ liệu (int, string, float, datetime...).
- Thể hiện chính xác các mối quan hệ và bản số (Cardinality): Một-Một (1-1), Một-Nhiều (1-N), Nhiều-Nhiều (N-N) giữa các bảng. Ví dụ: Một Order có thể áp dụng 0 hoặc 1 mã Discount; Một Shipment có thể tạo ra nhiều dòng log vị trí trong TrackingLogs.


[PROMPT 7] - Tinh chỉnh lược đồ cơ sở dữ liệu (Database Schema Polish)
----------------------------------------------------------------------
Hãy kiểm tra kỹ lại sơ đồ ERD vừa tạo. Có một lỗ hổng logic vận hành: Bảng `Shipments` (Giao hàng) cần phải lưu lại lịch sử thay đổi trạng thái giao hàng cụ thể của tài xế (như: Đã lấy hàng, Đang giao, Đã giao, Giao thất bại) để phục vụ cho việc tracking thời gian thực.
Hãy bổ sung thêm trường `current_status` (string) vào bảng `Shipments` và thêm bảng `StatusHistory` để lưu vết chi tiết các mốc thời gian chuyển trạng thái (Timestamp) nhằm phục vụ báo cáo sau này. Cập nhật lại mã nguồn Mermaid của ERD.


[PROMPT 8] - Tổng hợp và Chuẩn hóa tài liệu đặc tả SRS (Final Assembly & SRS Formatting)
----------------------------------------------------------------------
Tuyệt vời. Bây giờ, hãy đóng vai trò là một Technical Writer chuyên nghiệp, tổng hợp toàn bộ các nội dung và sơ đồ chúng ta đã xây dựng qua các bước trên thành một bản tài liệu Đặc tả Yêu cầu Phần mềm (SRS - Software Requirements Specification) hoàn chỉnh.
Cấu trúc tài liệu phải được sắp xếp khoa học theo các chương:
Chương 1: Tổng quan dự án (Project Overview)
Chương 2: Danh sách User Stories chi tiết (Dạng bảng)
Chương 3: Kiến trúc chức năng hệ thống (Mô tả và Mã sơ đồ Use Case Mermaid đã tối ưu)
Chương 4: Kiến trúc dữ liệu hệ thống (Mô tả và Mã sơ đồ ERD Mermaid đã tinh chỉnh)

RÀNG BUỘC NGHIÊM NGẶT VỀ ĐỊNH DẠNG: Loại bỏ hoàn toàn tất cả các câu chào hỏi, lời dẫn, lời kết hoặc các câu hội thoại rác của AI (Ví dụ không được có: "Sure, here is the document...", "I hope this helps..."). Chỉ trả về nội dung tiêu đề tài liệu từ chương 1 cho đến hết để tôi có thể copy trực tiếp vào file báo cáo.
======================================================================