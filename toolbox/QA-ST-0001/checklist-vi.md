# ✔ DANH SÁCH KIỂM TRA CÓ THỂ IN — QA-ST-0001

**[← Quay lại Tiêu chuẩn Hoàn chỉnh](../../standards/vi/QA/QA-ST-0001.md)**

---

### **TRƯỚC KHI BẮT ĐẦU**

☐ Môi trường đã khai báo (in-house-preview / customer-preview / production)
☐ Thông tin đăng nhập đã ghi chú (ID + mật khẩu)
☐ Tên hiển thị đã xác minh (để kiểm tra thứ tự tên)

---

## **1. Bản dịch**

**Nếu bạn là DJIN Member bản địa của ngôn ngữ:**
☐ Bản dịch được xác thực bằng kiến thức bản địa
☐ DeepL/Takoboto được sử dụng làm hỗ trợ trong trường hợp nghi ngờ

**Nếu bạn là DJIN Member không phải bản địa:**
☐ Văn bản đầy đủ đã xác thực trong DeepL
☐ Từ đơn lẻ đã xác thực trong Takoboto

**Cho tất cả mọi người:**
☐ Thứ tự tên theo ngôn ngữ UI
☐ Avatar + Tên hiển thị đúng

---

## **2. Kiểm tra chính tả**

☐ Không có lỗi chính tả trong UI
☐ Không có lỗi chính tả backend hiển thị
☐ Bản dịch x→JA đã kiểm tra trong DeepL
☐ Từ đơn lẻ đã kiểm tra trong Takoboto

---

## **3. Dữ liệu Cơ bản**

☐ Không có placeholder ("aaa", "test", lorem ipsum)
☐ Không có gì xúc phạm
☐ Tên hư cấu phù hợp (JP/BR)

---

## **4. Bản dịch Giao diện**

☐ Các nút bằng ngôn ngữ đúng
☐ Không thiếu gì bằng pt-BR
☐ Không thiếu gì bằng tiếng Anh
☐ Thứ tự tên ok

---

## **5. Rò rỉ**

☐ Không có UUID hiển thị
☐ Không có ID nội bộ
☐ Không có stacktrace
☐ Không có gì như undefined/null/[object Object]
☐ Không có lỗi API thô
☐ Không có thông điệp kỹ thuật bị lộ

---

## **6. Bố cục**

Kiểm tra trong:

* ☐ Desktop
* ☐ Chiều rộng iPhone (~390px)

Kiểm tra:
☐ Không có gì tràn container
☐ Không có cuộn ngang
☐ Các nút nhấp được
☐ Danh sách tải

---

## **7. Luồng Chính**

Cho mỗi màn hình:
☐ Vào luồng chính (CTA)
☐ Tạo 1 mục
☐ Chỉnh sửa
☐ Xóa
☐ Luồng không đóng băng
☐ Bố cục không bị phá vỡ
☐ Điều hướng ok
☐ Không có cảnh báo xấu

---

## **8. Chính tả và Tin nhắn**

☐ Tin nhắn rõ ràng
☐ Không xấu hổ khi cho khách hàng xem
☐ Tiêu đề và mô tả tối thiểu chuyên nghiệp

---

## **9. Màu sắc và Thương hiệu**

☐ Không có màu ngoài tiêu chuẩn
☐ Không có Vuetify thô
☐ Không có độ tương phản xấu

---

## **10. Bằng chứng**

☐ 1 ảnh chụp màn hình mỗi màn hình
☐ 1 video ngắn về luồng chính
☐ Kiểm tra cuối cùng:

> "Tôi có thể cho khách hàng xem điều này mà không sợ không?"
> ☐ Nếu không → sửa / báo cáo

---

## **11. Phạm vi**

☐ Những gì được sửa nằm **trong** phạm vi
☐ Mọi thứ **ngoài** phạm vi đã được liệt kê là
**"Các mục ngoài phạm vi được xác định"**
☐ Không có gì quan trọng bỏ lỡ mà không có cảnh báo

---

## **12. Công thức (nếu có)**

☐ Đã kiểm tra xem có công thức hữu ích trong repo / vị trí được phép
☐ Nếu tôi không có quyền truy cập → đã làm thủ công
☐ Nếu công thức tồn tại → đã thực thi trong phạm vi

---

# **KẾT QUẢ CUỐI CÙNG**

### Chọn MỘT:

### ✔ Đầu ra 1 — Tài liệu + Chuyển giao

☐ Vấn đề đã liệt kê
☐ Bằng chứng đã đính kèm
☐ Nhiệm vụ đã tạo trong Jira
☐ Thông báo trong Slack / Nhiệm vụ
☐ Các mục ngoài phạm vi đã liệt kê

### ✔ Đầu ra 2 — Sửa + Ghi nhật ký

☐ Vấn đề đã sửa
☐ Bằng chứng đã đính kèm
☐ Thông báo trong Slack / Nhiệm vụ
☐ Các mục ngoài phạm vi đã liệt kê
