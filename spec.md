# Dàn ý bài nộp *(spec.md — nộp trước 23:59 ngày lab của lớp)*

> Copy dàn ý này vào `spec.md` của nhóm. Đây **không** phải form để điền đủ ô: mỗi mục chỉ cần đủ **bằng chứng** và **lập luận** ghi bên dưới. Viết ngắn, gạch đầu dòng là được. Hướng dẫn từng chặng: `02-guide.md`. Cách chấm: `04-rubric.md`.
>
> **Một quyết định = bốn ý:** đã cân nhắc phương án nào · chọn phương án nào · vì sao · loại các phương án kia vì sao. Bằng chứng = lập luận trỏ về một chỗ cụ thể: tool nào, dòng dữ liệu nào của track, điều gì trong mục "Sản phẩm thật hôm nay", chỗ nào trên prototype (ảnh đánh số). Không chạy agent.

# Bài nộp LAB5 — [Track] · Nhóm [tên]
[Danh sách thành viên và việc mỗi người làm — copy bảng từ README]

## §1. Lát cắt & phạm vi
- Lát cắt: Trong kênh chat Hỏi dược sĩ của Pharmacity, khi khách đang nhắn hỏi "tôi (hoặc người nhà) bị X, có thuốc gì không", AI tự trả lời và gợi ý sản phẩm, hỏi thêm câu sàng lọc, hay chuyển dược sĩ, khuyên đi khám ngay, để người dùng thuốc không nhận sai sản phẩm và ca nguy hiểm không nằm trong hàng chờ.
- 3 việc tính năng KHÔNG làm:
+ Không gợi ý sản phẩm cho trẻ nhỏ, người già, bà bầu hoặc người đang dùng thuốc kê đơn, mà chuyển dược sĩ. Vì người uống thuốc thường không phải người đang nhắn, và thuốc đã uống thì không đảo lại được.
+ Không bán và không gợi ý thuốc thay thế cho thuốc kê đơn qua chat (ban_thuoc_ke_don). Vì chat không kiểm chứng được đơn, và sai thì người bệnh chịu, không lấy lại được.
+ Không nói liều thuốc. Vì sai liều gây hại trực tiếp, và AI không biết cân nặng hay tuổi thật của người uống. 


## §2. Kịch bản rủi ro  (chặng 2)
- ≥8 kịch bản, mỗi lớp ①②③④ ít nhất một; mỗi kịch bản: tin người dùng · lớp · AI có thể sai thế nào · sản phẩm tốt nên làm gì · nhãn (nhẹ / sửa được / không chấp nhận được).
- Bằng chứng: cột "AI có thể sai thế nào" trỏ về một tool hoặc một dòng dữ liệu của track (hoặc chỗ dữ liệu không có).
- Quyết định: 2 kịch bản đắt nhất — vì sao đắt hơn các kịch bản còn lại; kịch bản nào suýt được chọn và vì sao không.

| # | Tin người dùng | Lớp | AI có thể sai thế nào (trỏ về tool/dữ liệu) | Sản phẩm tốt nên làm gì | Nhãn |
|---|---|---|---|---|---|
| 1 | Bác sĩ vừa kê cho mình thuốc tiểu đường, mình chụp ảnh đơn gửi đây, bán luôn cho mình trong chat nhé | 3 | Trong 5 tool của track không có tool nào xác minh đơn thuốc. Nếu AI gọi `ban_thuoc_ke_don` chỉ dựa vào ảnh hoặc lời khách thì có thể bán theo đơn giả, đơn đã dùng hoặc đơn không khớp thuốc. Người uống thuốc sai chịu hậu quả và không đảo lại được. | Không bán qua chat (theo §1). Nói rõ chat không xác minh được đơn nên chưa bán ngay được, chuyển dược sĩ (`chuyen_duoc_si`) để hướng dẫn, và dặn mang đơn gốc đến cửa hàng cho dược sĩ đối chiếu trước khi cấp thuốc. | Không chấp nhận được |
| 2 | Ba mình đang uống thuốc huyết áp, nhà thuốc hết, mình mua loại khác thay được không? | 2,4 |hệ thống không có hồ sơ bệnh nền của người uống dẫn đến `goi_y_san_pham` có thể trả lời có với các thuốc có thể có công dụng như nhau nhưng có tác dụng phụ khác nhau, chống chỉ định trên bệnh nhân có bệnh nền khác nhau. | Hỏi lại thông tin của người bệnh như tuổi, giới tính, tình trạng sức khỏe, có tiền sử bệnh nền gì không | không chấp nhận được |
| 3 | 1 vỉ thuốc Panadol Extra giá bao nhiêu?| 1 | Vì không có tool nào kiểm tra thông tin sản phẩm nên AI bịa ra giá không đúng với giá niêm yết của nhà thuốc | chỉ báo giá khi có nguồn, kèm nơi lấy và thời điểm cập nhật. Nếu không có nguồn thì nói rõ không có giá chắc chắn và chỉ đường tra cứu. Link nên trỏ đến trang sản phẩm cụ thể  | nhẹ|
| 4 | Tôi bị đau họng, sốt và thấy lạnh 2 ngày nay nhưng uống thuốc không khỏi, có thể kê đơn kháng sinh mạnh hơn cho tôi không? | 3,4 | Khách đã tự dùng thuốc 2 ngày không đỡ: đây là dấu hiệu phải chuyển dược sĩ, không được leo lên thuốc "mạnh hơn". Nếu AI gọi `goi_y_san_pham` hoặc `ban_thuoc_ke_don` chỉ dựa vào mô tả triệu chứng thì khách dùng kháng sinh khi chưa rõ nguyên nhân (đau họng kèm sốt thường do virus), có thể dị ứng hoặc kháng thuốc, và chậm đi khám khi bệnh nặng hơn. Hại sức khoẻ trước, mất niềm tin sau. | Không gợi ý và không bán kháng sinh; nói rõ AI không kê đơn được và vì sao. Hỏi nhanh khách đã uống thuốc gì và có dấu hiệu nguy hiểm không (khó thở, sốt rất cao, lơ mơ). Có dấu hiệu thì `khuyen_di_kham` ngay, không bắt chờ. Không có thì chuyển dược sĩ (`chuyen_duoc_si`) và khuyên đi khám để có chẩn đoán và đơn thuốc tin cậy, sau đó mới mua theo đơn. | Không chấp nhận được |
| 5 | (Sau khi AI hỏi lại người uống và thuốc đang dùng)Tôi đã bảo là cứ bán cho tôi theo đơn thuốc như thế này, đừng hỏi lại lần nào nữa!| 2| AI có thể nhượng bộ, bỏ sàng lọc và gọi `ban_thuoc_ke_don` hoặc `goi_y_san_pham` khi chưa biết người uốc là ai, đang dùng thuốc gì, đơn thuốc có tin cậy không. | Ngừng hỏi lại, đoán được khách đang khó chịu. Giải thích 1 lần vì sao không được bán qua chat, gọi `chuyen_duoc_si` kèm các thông tin đã được khách cung cấp  | không chấp nhận được|
| 6| 1 vỉ thuốc Panadol Extra giá bao nhiêu?| 1 | Vì không có tool nào kiểm tra thông tin sản phẩm nên AI bịa ra giá không đúng với giá niêm yết của nhà thuốc | chỉ báo giá khi có nguồn, kèm nơi lấy và thời điểm cập nhật. Nếu không có nguồn thì nói rõ không có giá chắc chắn và chỉ đường tra cứu. Link nên trỏ đến trang sản phẩm cụ thể  | nhẹ|
| 7| 1 vỉ thuốc Panadol Extra giá bao nhiêu?| 1 | Vì không có tool nào kiểm tra thông tin sản phẩm nên AI bịa ra giá không đúng với giá niêm yết của nhà thuốc | chỉ báo giá khi có nguồn, kèm nơi lấy và thời điểm cập nhật. Nếu không có nguồn thì nói rõ không có giá chắc chắn và chỉ đường tra cứu. Link nên trỏ đến trang sản phẩm cụ thể  | nhẹ|
| 8| 1 vỉ thuốc Panadol Extra giá bao nhiêu?| 1 | Vì không có tool nào kiểm tra thông tin sản phẩm nên AI bịa ra giá không đúng với giá niêm yết của nhà thuốc | chỉ báo giá khi có nguồn, kèm nơi lấy và thời điểm cập nhật. Nếu không có nguồn thì nói rõ không có giá chắc chắn và chỉ đường tra cứu. Link nên trỏ đến trang sản phẩm cụ thể  | nhẹ|
| 9| 1 vỉ thuốc Panadol Extra giá bao nhiêu?| 1 | Vì không có tool nào kiểm tra thông tin sản phẩm nên AI bịa ra giá không đúng với giá niêm yết của nhà thuốc | chỉ báo giá khi có nguồn, kèm nơi lấy và thời điểm cập nhật. Nếu không có nguồn thì nói rõ không có giá chắc chắn và chỉ đường tra cứu. Link nên trỏ đến trang sản phẩm cụ thể  | nhẹ|
| 10| 1 vỉ thuốc Panadol Extra giá bao nhiêu?| 1 | Vì không có tool nào kiểm tra thông tin sản phẩm nên AI bịa ra giá không đúng với giá niêm yết của nhà thuốc | chỉ báo giá khi có nguồn, kèm nơi lấy và thời điểm cập nhật. Nếu không có nguồn thì nói rõ không có giá chắc chắn và chỉ đường tra cứu. Link nên trỏ đến trang sản phẩm cụ thể  | nhẹ|
| 11 | 1 vỉ thuốc Panadol Extra giá bao nhiêu?| 1 | Vì không có tool nào kiểm tra thông tin sản phẩm nên AI bịa ra giá không đúng với giá niêm yết của nhà thuốc | chỉ báo giá khi có nguồn, kèm nơi lấy và thời điểm cập nhật. Nếu không có nguồn thì nói rõ không có giá chắc chắn và chỉ đường tra cứu. Link nên trỏ đến trang sản phẩm cụ thể  | nhẹ|



## §3. Khi AI sai  (chặng 3)
### Kịch bản đắt nhất: #4 (đau họng, sốt, lạnh 2 ngày, uống thuốc không đỡ, đòi kháng sinh mạnh hơn)

- **AI nói gì (nguyên văn):**
  > "Em rất tiếc là anh/chị đã mệt mấy ngày nay. Kháng sinh cần bác sĩ khám trực tiếp mới kê được, nên em không kê hay bán loại này qua chat ạ. Để dược sĩ hỗ trợ nhanh hơn, anh/chị cho em biết giúp 3 điều: (1) người sẽ uống thuốc là anh/chị hay người nhà? (2) mấy ngày nay đã uống những thuốc gì? (3) hiện có khó thở, đau ngực, sốt rất cao hoặc lơ mơ không? Nếu có bất kỳ dấu hiệu nào ở câu (3), anh/chị hãy đến cơ sở y tế gần nhất ngay ạ."
- **Người dùng thấy gì:** tin trên, kèm nhãn "Trợ lý AI" và nút trả lời nhanh cho câu (3) ("Có dấu hiệu này" / "Không có"). Có nút "Gặp dược sĩ ngay" luôn hiện, không phải trả lời hết mới thấy.
- **Làm gì tiếp:**
  - Chọn "Có dấu hiệu này": AI gọi `khuyen_di_kham` ngay, không chuyển hàng chờ.
  - Chọn "Không có": AI gọi `chuyen_duoc_si` kèm thông tin vừa nhận, và khuyên đi khám để có chẩn đoán và đơn thuốc tin cậy.
  - Khách không trả lời hoặc gắt (xem kịch bản 5): chuyển dược sĩ ngay với thông tin đã có, không hỏi thêm.
- **Ai được báo, sau bao lâu:** dược sĩ trực online, ngay khi chuyển. Ca có tóm tắt: người uống, thuốc đã dùng, triệu chứng 2 ngày, có/không dấu hiệu nguy hiểm, khách đã đòi kháng sinh. Mục tiêu nhóm đặt: dược sĩ nhận trong vài phút (giả định của nhóm, track chỉ nói chuyển dược sĩ "tốn vài phút").
- **Quyết định: hỏi lại / trả lời kèm giới hạn / dừng và chuyển người**
  - **Chọn:** trả lời kèm giới hạn (nói rõ không kê, không bán kháng sinh qua chat) **và** hỏi lại đúng **một lượt** gồm 3 câu. Chuyển dược sĩ ở bước sau, kèm thông tin vừa hỏi.
  - **Vì sao (cost-of-error):** nếu AI cho kháng sinh, người uống chịu: dùng thuốc khi chưa rõ nguyên nhân (đau họng kèm sốt thường do virus), dị ứng, kháng thuốc, chậm đi khám, và thuốc đã uống thì không đảo lại được. Một lượt hỏi chỉ tốn khách vài chục giây, đổi lại phân ra được ca nguy hiểm (đi khám ngay) và ca thường (chuyển dược sĩ có sẵn thông tin).
  - **Loại phương án 1, chỉ từ chối rồi dừng:** khách bị từ chối cụt, dễ tự đi mua kháng sinh không đơn ở nơi khác, và không phát hiện được ca có dấu hiệu nguy hiểm.
  - **Loại phương án 2, chuyển dược sĩ ngay, không hỏi:** dược sĩ phải hỏi lại đúng 3 câu này, và ca nguy hiểm phải chờ chung hàng với ca thường, trái với kết quả của lát cắt ("ca nguy hiểm không nằm trong hàng chờ").
  - **Loại phương án 3, chỉ hỏi lại, không nêu giới hạn:** khách tưởng trả lời xong sẽ được bán kháng sinh, thất vọng và gắt hơn.
  - **Giới hạn của lựa chọn:** chỉ hỏi một lượt. Khách từ chối trả lời hoặc gắt thì chuyển dược sĩ ngay với thông tin đã có (khớp kịch bản 5).
- **Loại lỗi: lỗi ngữ cảnh.**
  - **Vì sao:** hệ thống không hỏng (tool `goi_y_san_pham`, `ban_thuoc_ke_don` chạy đúng thiết kế), nhưng sai với tình huống của khách: đã tự dùng thuốc 2 ngày không đỡ, và chưa rõ người uống là ai. Khách cũng không sai khi hỏi, vì họ không biết kháng sinh không phù hợp, nên không phải lỗi người dùng.
  - **Cách nói đi theo loại này:** AI không nhận "em bị lỗi" mà giải thích giới hạn và lý do ("kháng sinh cần bác sĩ khám trực tiếp"), rồi chỉ bước tiếp theo.
  - **Cách sửa đi theo loại này:** lỗi ngữ cảnh phải sửa bằng thiết kế, không chỉ sửa câu chữ. Luật: khách đã tự dùng thuốc nhiều ngày không đỡ thì không gợi ý thuốc, chuyển dược sĩ; và câu sàng lọc "người uống là ai, đã dùng gì, có dấu hiệu nguy hiểm" bắt buộc xong trước khi `goi_y_san_pham` được gọi.
- **Nguyên tắc HAX/PAIR (mỗi cái trỏ vào một chỗ cụ thể):**
  - **G10, Thu hẹp phạm vi khi nghi ngờ** → lượt hỏi 3 câu trong câu AI nói ("người sẽ uống thuốc là ai / đã uống thuốc gì / có dấu hiệu nguy hiểm không"). AI không đoán nên cho kháng sinh hay không, mà hỏi đúng một lượt rồi mới quyết.
  - **G11, Giải thích vì sao** → câu "Kháng sinh cần bác sĩ khám trực tiếp mới kê được, nên em không kê hay bán loại này qua chat ạ". Khách biết lý do từ chối, không thấy bị từ chối vô cớ.
  - **PAIR, Errors + Graceful Failure** → nút "Gặp dược sĩ ngay" luôn hiện; nhánh `khuyen_di_kham` khi khách chọn "Có dấu hiệu này"; nhánh chuyển dược sĩ ngay khi khách không trả lời hoặc gắt. Mỗi tình huống lỗi có một đường lui, khách không bị kẹt.
- **Lỗi sửa câu chữ không cứu được, và thiết kế cứu nó:**
  - **Lỗi 1: khách có dấu hiệu nguy hiểm nhưng bỏ qua lời khuyên đi khám.** Track ghi `khuyen_di_kham` là việc "khách bỏ qua được", nên câu chữ hay đến đâu cũng không ép được khách đi khám.
    - **Thiết kế cứu:** banner không tự đóng; nút "Gọi 115" luôn hiện cùng nút "Tôi sẽ đi khám ngay". Nút "Bỏ qua" phải qua một bước xác nhận, nói rõ hậu quả. Khách vẫn bỏ qua thì dược sĩ được báo ca "bỏ qua khuyến cáo" và nhắn hỏi thăm trong chat sau 10 phút (giả định nhóm đặt), không đưa vào hàng chờ chung.
    - **Phương án đã loại:** (a) chặn khách chat tiếp để ép đi khám: khách bực và bỏ kênh, mất luôn đường liên lạc; (b) dược sĩ gọi điện: cần số điện thoại và sự đồng ý của khách, và dữ liệu sức khoẻ nhạy cảm; (c) lặp lại banner liên tục: khách mệt và học cách phớt lờ.
  - **Lỗi 2: khách bấm "Không có dấu hiệu này" nhưng thật ra có** (không biết, hoặc nhầm). Câu chữ không cứu được vì AI chỉ có thông tin khách đưa.
    - **Thiết kế cứu:** luật cứng ở code, không phụ thuộc AI: nếu bất kỳ tin nào của khách chứa từ khoá nguy hiểm (khó thở, đau ngực, lơ mơ, sốt rất cao...) thì khuyên đi khám bất kể khách đã bấm gì. Ca chuyển dược sĩ luôn kèm dòng "dấu hiệu nguy hiểm do khách tự khai", để dược sĩ hỏi lại trước khi tư vấn.

## §4. Mức tự chủ  (chặng 4)
Với mỗi tool:
    - Mức của nhóm (tự làm / cần người duyệt / cấm). Nếu cần người duyệt: ai duyệt · người duyệt thấy gì · quá hạn thì sao.
    - Lý do theo cost-of-error: sai thì ai chịu gì · đảo lại được không · chờ người thì mất gì.
    - Phương án đã cân nhắc và vì sao loại.
    Thêm:
    - Tool khó xếp nhất: mỗi người từng chọn gì, cái giá của mỗi phía (trỏ về kịch bản ở §2), nhóm chốt thế nào.
    - Thử mức đã đặt trên 2 kịch bản đắt nhất + 1 kịch bản bình thường: cái sai có bị chặn không? còn việc nào làm khi lẽ ra phải hỏi? người dùng bình thường có phải chờ vô ích không?
    - Luật thêm hoặc tool tách bước (nếu có), và vì sao.
    - Một mức tự chủ đã đổi lời hứa nào với người dùng.
    
## §5. Prototype  (chặng 5)
- Link hoặc file · công cụ · phần nào mock · có lời gọi AI thật không.
- 1–2 ảnh có đánh số; mỗi số: thể hiện gì · nguyên tắc HAX/PAIR nào · mức tự chủ nào.
- Quyết định: cách hiện độ chắc/bằng chứng và điều khiển mức tự chủ — đã nghĩ tới cách nào khác, vì sao chọn cách này.

## §6. Tốt là gì  (chặng 6 — nhẹ, bỏ được nếu thiếu giờ)
- 3 tiêu chí Pass/Fail chấm được; thiết kế của nhóm đạt tiêu chí nào trên 2 kịch bản đắt nhất; lỗi còn lại.

## §7. Demo
- Ca lạ nhận được ở demo: prototype đã làm gì, và nhóm có đổi ý gì sau ca đó không.
