# Prototype T1 · Hỏi dược sĩ

Mở `index.html` bằng trình duyệt, không cần cài gì. Toàn bộ dữ liệu là dựng.

- **Màn hình 1 (khách):** ca #12 (viên thuốc mất tên), cùng các nút mẫu #4 (đòi kháng sinh), #5 (khách gắt), #9 (đau họng, AI soạn để dược sĩ duyệt), ca bé sốt, lơ mơ. Bấm "Làm lại" trước khi đổi sang ca khác.
- **Màn hình 2 (dược sĩ):** nhận ca chuyển kèm tóm tắt; thấy ca khách bỏ qua khuyến cáo đi khám.
- **Số cam 1, 2, 3:** nguyên tắc của ca #4. **Số 4, 5, 6:** G2, G10, G9 của ca #12; **7, 8:** luồng duyệt ca #9 (xem chú thích cuối trang).

## Demo ca #12

1. Bấm "Làm lại" → "Ca 12: viên thuốc mất tên" → "Gửi". Chỉ ra trạng thái **④ Chưa xác định được thuốc**, câu dặn tạm chưa uống và nút **⑤ Bổ sung chữ trên vỉ**. Không có tên thuốc được đoán, thẻ sản phẩm hay phần trăm nhận diện.
2. Bấm "Bổ sung chữ trên vỉ", nhập dữ liệu dựng, chẳng hạn `…500 mg` và `Tôi, 30 tuổi`, rồi "Gửi thông tin cho dược sĩ". Phía dược sĩ thấy chữ nguyên văn, nhãn chưa xác minh và trạng thái chờ nhận. Bỏ trống là chưa cung cấp, không phải không dị ứng hay không có dấu hiệu nguy hiểm.
3. Bấm **⑥ Bổ sung / sửa thông tin**, sửa thành `…250 mg`, rồi gửi. Cùng mã ca được cập nhật và có nhãn thông tin vừa đổi. Bấm "Nhận ca" ở phía dược sĩ để thấy tin nhắn từ người hỗ trợ. Trước lúc nhận có thể "Hủy chuyển" và chuyển lại.
4. Thử nhánh "Tôi đã uống rồi": hướng dẫn liên hệ y tế hiện ngay, kể cả chưa thấy bất thường; form giờ/lượng đã uống có thể để trống và không cản tìm hỗ trợ. Nút gọi cấp cứu chỉ mở thông báo mô phỏng. Bấm "Tôi có dấu hiệu nguy hiểm" để xem ca khẩn.

Ảnh minh họa: [trạng thái và lựa chọn ban đầu](case12-screening.png), [sửa thông tin trên cùng hồ sơ](case12-handoff.png). Lời thoại và lập luận: [báo cáo §3 #12](../spec.md); giới hạn quyền: §4 luật 5.

Ca #12 chỉ nhận chữ khách gõ; không gửi ảnh hay nhận diện thuốc. Chuyển/nhận ca và hướng dẫn liên hệ y tế là mô phỏng, không kết nối người trực thật. Luật từ khóa nhận được các ca mẫu và một số cách nói khác, không thay thế đánh giá y tế hoặc hiểu mọi cách diễn đạt.

## AI thật (bonus)

Mở mục "Cấu hình AI thật", chọn Mistral (mặc định, model `mistral-small-latest`), Groq hoặc OpenRouter, dán API key, bật ô "Dùng AI thật". AI phân loại `ask / unknown_pill / soan_goi_y / khuyen_di_kham / chuyen_duoc_si` và trả độ chắc + căn cứ; câu chữ khách thấy là mẫu đã duyệt, không do AI viết. Key chỉ nằm trong bộ nhớ tab, không lưu, không commit. Không bật hoặc gọi lỗi thì tự dùng luật mô phỏng.

Ca #12 có thể gọi AI thật để phân loại ở lượt đầu, nhưng chốt chặn giữ trạng thái thuốc chưa xác minh và dùng lời thoại cố định. Các tin nối tiếp giữ cùng ngữ cảnh. Đã uống hoặc có dấu hiệu nguy hiểm thì hướng dẫn ngay, không chờ API. Không bật AI vẫn demo được đầy đủ; ảnh AI thật là bằng chứng của một lần chạy riêng, không phải mọi lượt đều gọi AI.
