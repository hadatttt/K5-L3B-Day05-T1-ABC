# Prototype T1 · Hỏi dược sĩ

Mở `index.html` bằng trình duyệt, không cần cài gì. Toàn bộ dữ liệu là dựng.

- **Màn hình 1 (khách):** ca khó là kịch bản 4 (đòi kháng sinh). Nút mẫu: ca 4, ca 5 (khách gắt), ca lạ (bé sốt, lơ mơ).
- **Màn hình 2 (dược sĩ):** nhận ca chuyển kèm tóm tắt; thấy ca khách bỏ qua khuyến cáo đi khám.
- **Số cam 1, 2, 3:** G10, G11, PAIR Errors + Graceful Failure (xem chú thích cuối trang).

## AI thật (bonus)

Mở mục "Cấu hình AI thật", chọn Mistral (mặc định, model `mistral-small-latest`), Groq hoặc OpenRouter, dán API key, bật ô "Dùng AI thật". AI quyết định `ask / khuyen_di_kham / chuyen_duoc_si` và trả độ chắc + căn cứ; câu chữ khách thấy là mẫu đã duyệt, không do AI viết. Key chỉ nằm trong bộ nhớ tab, không lưu, không commit. Không bật hoặc gọi lỗi thì tự dùng luật mô phỏng.

Chụp 1–2 ảnh màn hình có số cam, lưu vào thư mục này để §5 của spec trỏ vào.
