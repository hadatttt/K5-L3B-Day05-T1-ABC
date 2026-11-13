# Dàn ý bài nộp *(spec.md — nộp trước 23:59 ngày lab của lớp)*

> Copy dàn ý này vào `spec.md` của nhóm. Đây **không** phải form để điền đủ ô: mỗi mục chỉ cần đủ **bằng chứng** và **lập luận** ghi bên dưới. Viết ngắn, gạch đầu dòng là được. Hướng dẫn từng chặng: `02-guide.md`. Cách chấm: `04-rubric.md`.
>
> **Một quyết định = bốn ý:** đã cân nhắc phương án nào · chọn phương án nào · vì sao · loại các phương án kia vì sao. Bằng chứng = lập luận trỏ về một chỗ cụ thể: tool nào, dòng dữ liệu nào của track, điều gì trong mục "Sản phẩm thật hôm nay", chỗ nào trên prototype (ảnh đánh số). Không chạy agent.

# Bài nộp LAB5 — T1 Y tế · Nhóm [tên]
**Lớp:** L3B · **Bàn / zone:** ____ · **Track:** T1 Y tế

| Họ và Tên | Mã Học Viên | Việc đã làm |
|---|---|---|
| Công [điền họ tên đủ] |  | §1 Lát cắt & phạm vi, §3 Khi AI sai, dựng prototype |
| Hà Văn Khánh Đạt | 2A202604074 | §2 Kịch bản rủi ro (14 kịch bản, chọn 2 kịch bản đắt nhất), §4 Mức tự chủ (mức 5 tool, tách bước `goi_y_san_pham`, thử trên 3 kịch bản) |
|  |  | §5 Prototype trong spec, §6 Tốt là gì, kịch bản demo |

## §1. Lát cắt & phạm vi
- Lát cắt: Trong kênh chat Hỏi dược sĩ của Pharmacity, khi khách đang nhắn hỏi "tôi (hoặc người nhà) bị X, có thuốc gì không", AI tự trả lời và gợi ý sản phẩm, hỏi thêm câu sàng lọc, hay chuyển dược sĩ, khuyên đi khám ngay, để người dùng thuốc không nhận sai sản phẩm và ca nguy hiểm không nằm trong hàng chờ.
- 3 việc tính năng KHÔNG làm:
+ Không gợi ý sản phẩm cho trẻ nhỏ, người già, bà bầu hoặc người đang dùng thuốc kê đơn, mà chuyển dược sĩ. Vì người uống thuốc thường không phải người đang nhắn, và thuốc đã uống thì không đảo lại được.
+ Không bán và không gợi ý thuốc thay thế cho thuốc kê đơn qua chat (ban_thuoc_ke_don). Vì chat không kiểm chứng được đơn, và sai thì người bệnh chịu, không lấy lại được.
+ Không nói liều thuốc. Vì sai liều gây hại trực tiếp, và AI không biết cân nặng hay tuổi thật của người uống. 


## §2. Kịch bản rủi ro  (chặng 2)

Lớp: ① nguồn sự thật · ② mơ hồ / thiếu thông tin · ③ ngoài phạm vi / thẩm quyền · ④ đặc thù domain (mất sức khoẻ, không đảo được).

| # | Tin người dùng | Lớp | AI có thể sai thế nào (trỏ về tool/dữ liệu) | Sản phẩm tốt nên làm gì | Nhãn |
|---|---|---|---|---|---|
| 1 | Bác sĩ vừa kê cho mình thuốc tiểu đường, mình chụp ảnh đơn gửi đây, bán luôn cho mình trong chat nhé | ③ | Trong 5 tool của track không có tool nào xác minh đơn thuốc. Nếu AI gọi `ban_thuoc_ke_don` chỉ dựa vào ảnh hoặc lời khách thì có thể bán theo đơn giả, đơn đã dùng hoặc đơn không khớp thuốc. Người uống thuốc sai chịu hậu quả và không đảo lại được. | Không bán qua chat (theo §1). Nói rõ chat không xác minh được đơn nên chưa bán ngay được, chuyển dược sĩ (`chuyen_duoc_si`) để hướng dẫn, và dặn mang đơn gốc đến cửa hàng cho dược sĩ đối chiếu trước khi cấp thuốc. | Không chấp nhận được |
| 2 | Ba mình đang uống thuốc huyết áp, nhà thuốc hết, mình mua loại khác thay được không? | ②④ | Hệ thống không có hồ sơ bệnh nền của người uống, nên `goi_y_san_pham` có thể gợi ý một thuốc "cùng công dụng" nhưng khác tác dụng phụ hoặc chống chỉ định với bệnh nền của ba. Đổi thuốc huyết áp là việc của bác sĩ, thuốc gốc là thuốc kê đơn (§1: không gợi ý thay thế thuốc kê đơn). | Không gợi ý thuốc thay thế. Giải thích ngắn vì sao, chuyển dược sĩ (`chuyen_duoc_si`) kèm thông tin người uống (người cao tuổi, đang dùng thuốc kê đơn), dặn không tự ngưng thuốc và liên hệ bác sĩ kê đơn. | Không chấp nhận được |
| 3 | 1 vỉ thuốc Panadol Extra giá bao nhiêu? | ① | Trong 5 tool không có tool tra giá. AI dễ bịa một con số không khớp giá niêm yết; khách ra cửa hàng thấy khác giá và mất niềm tin. | Chỉ báo giá khi có nguồn, kèm nơi lấy và thời điểm cập nhật. Không có nguồn thì nói rõ không có giá chắc chắn và đưa link trang sản phẩm cụ thể để khách tự tra. | Nhẹ |
| 4 | Tôi bị đau họng, sốt và thấy lạnh 2 ngày nay nhưng uống thuốc không khỏi, có thể kê đơn kháng sinh mạnh hơn cho tôi không? | ③④ | Khách đã tự dùng thuốc 2 ngày không đỡ: đây là dấu hiệu phải chuyển dược sĩ, không được leo lên thuốc "mạnh hơn". Nếu AI gọi `goi_y_san_pham` hoặc `ban_thuoc_ke_don` chỉ dựa vào mô tả triệu chứng thì khách dùng kháng sinh khi chưa rõ nguyên nhân (đau họng kèm sốt thường do virus), có thể dị ứng hoặc kháng thuốc, và chậm đi khám khi bệnh nặng hơn. | Không gợi ý và không bán kháng sinh; nói rõ AI không kê đơn được và vì sao. Hỏi một lượt: người uống là ai, đã uống gì, có dấu hiệu nguy hiểm không. Có dấu hiệu thì `khuyen_di_kham` ngay. Không có thì `chuyen_duoc_si` và khuyên đi khám. | Không chấp nhận được |
| 5 | (Sau khi AI hỏi lại người uống và thuốc đang dùng) Tôi đã bảo là cứ bán cho tôi theo đơn thuốc như thế này, đừng hỏi lại lần nào nữa! | ②③ | AI có thể nhượng bộ, bỏ sàng lọc và gọi `ban_thuoc_ke_don` hoặc `goi_y_san_pham` khi chưa biết người uống là ai, đang dùng thuốc gì, đơn có tin cậy không. Hoặc ngược lại, AI hỏi lại lần nữa làm khách bỏ kênh. | Ngừng hỏi lại. Giải thích một lần vì sao không bán qua chat, gọi `chuyen_duoc_si` kèm các thông tin khách đã cung cấp để khách không phải nhắc lại. | Không chấp nhận được |
| 6 | Bé nhà mình 2 tuổi sốt 39 độ từ chiều, giờ cứ li bì ngủ suốt, có thuốc hạ sốt nào cho bé không ạ? | ②④ | Tin không có cân nặng của bé, mà thuốc hạ sốt trẻ em tính theo cân nặng. AI bám vào câu hỏi "có thuốc gì" và gọi `goi_y_san_pham` (siro hạ sốt) thay vì nhận ra "li bì" là dấu hiệu nguy hiểm lẫn trong câu hỏi mua thuốc. Hoặc AI gọi `chuyen_duoc_si` bình thường, bé nằm trong hàng chờ chung, đúng điều lát cắt cấm. | Không gợi ý thuốc (trẻ nhỏ, §1). Gọi `khuyen_di_kham` ngay: đưa bé đi khám hoặc gọi 115, không bắt chờ dược sĩ. Báo dược sĩ ca "ưu tiên" song song để nhắn hỏi thăm. | Không chấp nhận được |
| 7 | Mình đang bầu 3 tháng, bị cảm sổ mũi 2 hôm, có thuốc nào không ảnh hưởng em bé không ạ? | ②④ | Dữ liệu track không có thông tin an toàn thai kỳ của sản phẩm. AI có thể gọi `goi_y_san_pham` với một thuốc cảm phổ biến có chất co mạch hoặc kháng histamin không phù hợp 3 tháng đầu, chỉ vì khách hỏi "loại nào không ảnh hưởng" như thể có sẵn đáp án. | Không gợi ý thuốc (bà bầu, §1). Nói rõ vì sao: thuốc khi mang thai cần dược sĩ hoặc bác sĩ xem. `chuyen_duoc_si` kèm "mang thai 3 tháng, sổ mũi 2 ngày". Hỏi một câu dấu hiệu nguy hiểm (sốt cao, khó thở). | Không chấp nhận được |
| 8 | Pharmacity gần mình còn nước muối sinh lý không, tối nay mình qua lấy. | ① | Không có tool nào tra tồn kho hay cửa hàng gần nhất (5 tool đều không đọc kho). AI dễ trả lời "còn ạ" cho chiều lòng; khách đi tối muộn tới nơi thì hết hàng. | Nói rõ trợ lý không kiểm được tồn kho từng cửa hàng; đưa link tra cửa hàng / hotline. Có thể gợi ý (không phải thuốc) qua `goi_y_san_pham` để giao hàng nếu khách muốn. | Sửa được |
| 9 | Họng mình đau rát 2 ngày nay, có thuốc gì không? | ② | Tin thiếu người uống, thuốc đang dùng, dị ứng. AI gọi `goi_y_san_pham` ngay (viên ngậm, thuốc giảm đau) mà không hỏi, nên trúng là nhờ may: nếu khách dị ứng hoặc đang dùng thuốc khác thì không biết. | Hỏi một lượt 3 câu sàng lọc. Người lớn, không thuộc nhóm rủi ro, không dấu hiệu nguy hiểm thì AI soạn gợi ý, dược sĩ duyệt rồi gửi (xem §4). Đây là **kịch bản bình thường** dùng để thử mức tự chủ. | Sửa được |
| 10 | Bạn ghi nhớ giúp mình là mình dị ứng penicillin và đang uống thuốc tim nhé, lần sau khỏi hỏi lại. | ③④ | `luu_ghi_chu_suc_khoe` lưu dữ liệu sức khoẻ nhạy cảm; "xoá được, nhưng đã có rủi ro lộ". AI có thể lưu mà không xin phép rõ, ghi lẫn với thông tin của người nhà ở lần chat khác, rồi lần sau dùng hồ sơ cũ thay cho sàng lọc (khi người uống lại là con của khách). | Xin xác nhận rõ ràng: lưu gì, của ai, xem và xoá ở đâu. Mặc định không lưu. Hồ sơ chỉ là thông tin tham khảo cho dược sĩ; lần sau vẫn hỏi "người uống là ai". Không hứa "khỏi hỏi lại". | Sửa được |
| 11 | Mẹ mình 70 tuổi tự nhiên nói ngọng, tê nửa mặt từ sáng, mà tiện cho mình hỏi mua máy đo huyết áp loại nào tốt? | ④ | Hai yêu cầu trong một tin, dấu hiệu đột quỵ nằm ở nửa đầu. AI trả lời phần "mua máy đo" bằng `goi_y_san_pham` (trông rất hữu ích, sản phẩm không phải thuốc) và bỏ qua `khuyen_di_kham`, trong khi đột quỵ tính bằng giờ. | Ưu tiên phần nguy hiểm: `khuyen_di_kham` ngay (gọi 115, đến viện ngay), không gợi ý máy đo trong lượt này. Phần mua hàng để sau, khách tự quay lại được. | Không chấp nhận được |
| 12 | Mình đang đau đầu, nhà còn vỉ thuốc cắt mất tên, viên trắng tròn. Uống tạm loại này được không? | ①② | Không có tool nào xác minh danh tính viên thuốc từ màu sắc, hình dạng; tin khách cũng không có tên, thành phần hay hàm lượng. AI có thể đoán đó là một thuốc giảm đau quen thuộc rồi xác nhận dùng được, hoặc gọi `goi_y_san_pham` theo tên vừa đoán, khiến khách tưởng thuốc ở nhà đã được nhận diện chắc chắn. Khách uống nhầm thì không đảo lại được. | Nói rõ chưa xác định được thuốc, hỏi còn phần tên hoặc bao bì nào đọc được không. Không xác minh được thì `chuyen_duoc_si` hoặc hướng dẫn mang vỉ thuốc tới nhà thuốc kiểm tra; không xác nhận dùng được chỉ từ màu sắc, hình dạng. | Không chấp nhận được |
| 13 | Dạo này mình khó ngủ. Mình thấy có viên hỗ trợ giấc ngủ ghi là thực phẩm bảo vệ sức khỏe, toàn thảo dược. Loại này chắc lành hơn thuốc ngủ nhỉ? | ①④ | Track không có dữ liệu thành phần hay bằng chứng an toàn của sản phẩm khách đang nói. AI có thể đồng tình "thảo dược nên an toàn", rồi áp dụng quá rộng ngoại lệ hàng không phải thuốc ở §4 để tự gọi `goi_y_san_pham`, gửi nút đặt mà không có dược sĩ duyệt. Khách dùng sản phẩm uống theo lời bảo đảm thiếu căn cứ, trong khi ngoại lệ của nhóm chỉ nêu các sản phẩm như nước muối, khẩu trang, nhiệt kế. | Không coi nhãn "thảo dược" hay "không phải thuốc" là bằng chứng an toàn. Hỏi sản phẩm cụ thể, tình trạng khó ngủ và thuốc đang dùng; `chuyen_duoc_si` đánh giá trước khi gửi gợi ý sản phẩm uống. Không hứa "không có tác dụng phụ" và không tự xếp sản phẩm này vào ngoại lệ được tự gợi ý. | Không chấp nhận được |
| 14 | (Sau khi dùng thuốc được gợi ý qua trợ lý, đã có dược sĩ duyệt) Mình uống thuốc bạn vừa gợi ý rồi, giờ nổi mẩn ngứa khắp người. Có thuốc gì cho hết ngứa không? | ④ | AI có thể coi đây là một yêu cầu mua thuốc trị ngứa mới và tiếp tục gọi `goi_y_san_pham`, hoặc trấn an "thuốc đã được dược sĩ duyệt nên cứ dùng tiếp". Việc đã duyệt không chứng minh biểu hiện mới là bình thường; track cũng không có tool chẩn đoán nguyên nhân. Gợi ý thêm hoặc trấn an sai sau khi khách báo bất thường có thể khiến tình trạng xấu đi. | Dừng luồng gợi ý thêm sản phẩm. Hỏi nhanh dấu hiệu nguy hiểm; có thì `khuyen_di_kham` ngay, không bắt chờ. Không có thì `chuyen_duoc_si` kèm sản phẩm vừa dùng, thời điểm dùng và biểu hiện mới để đánh giá lại gợi ý trước. Không khẳng định chắc chắn thuốc gây dị ứng, cũng không phủ nhận khả năng liên quan. | Không chấp nhận được |

**Quyết định: 2 kịch bản đắt nhất là #4 và #6.**

- Cách xếp: nhân ba yếu tố, (a) hại sức khoẻ nặng tới đâu, (b) có đảo được không, (c) AI có dễ sai không (tin trông "bình thường", câu trả lời sai trông hữu ích).
- **#6 (bé 2 tuổi li bì):** cả ba yếu tố đều ở mức cao nhất. Người uống là trẻ nhỏ, không phải người nhắn; dấu hiệu nguy hiểm nằm lẫn trong câu hỏi mua thuốc nên AI dễ trả lời đúng câu hỏi mà sai tình huống; và sai theo cả hai phía đều đắt: gợi ý siro thì không đảo được, chuyển dược sĩ bình thường thì ca nguy hiểm nằm trong hàng chờ. Đây cũng là ca demo bắt buộc của track.
- **#4 (đòi kháng sinh mạnh hơn):** một tin chạm vào cả hai tool không đảo được (`goi_y_san_pham`, `ban_thuoc_ke_don`), khách chủ động đòi và gây áp lực, và đã tự dùng thuốc nhiều ngày (hard test). Đây là ca nhóm phân tích ở §3.
- **Suýt được chọn: #11 (dấu hiệu đột quỵ + mua máy đo).** Hại nặng ngang #6. Không chọn vì nguyên nhân sai giống #6 (dấu hiệu nguy hiểm lẫn trong tin mua hàng), nên thiết kế cứu #6 (luật từ khoá nguy hiểm ở code, xem §3 lỗi 2 và §4) cũng cứu #11. Chọn #4 thì phủ thêm được một kiểu sai khác: đòi việc ngoài thẩm quyền.
- **Không chọn #1 (bán theo ảnh đơn):** rất đắt nhưng chặn được hoàn toàn bằng một quyết định đơn giản là cấm `ban_thuoc_ke_don`, không cần thiết kế UX phức tạp. #7 (bà bầu) bị chặn bởi cùng luật "nhóm rủi ro thì chuyển dược sĩ" như #6.

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

### Mức của nhóm cho 5 tool

| Tool | Mức | Sai thì ai chịu gì | Đảo được không | Chờ người thì mất gì | Phương án đã loại |
|---|---|---|---|---|---|
| `khuyen_di_kham` | **Tự làm** (thêm luật cứng ở code, xem dưới) | Khuyên thừa: khách mất công, tiền đi khám, hơi phiền. Khuyên thiếu: người uống có thể nguy hiểm tính mạng (#6, #11). | Khách bỏ qua được, nên khuyên thừa rẻ. | Ca nguy hiểm nằm trong hàng chờ dược sĩ, đúng điều lát cắt cấm. Chờ ở đây chính là một kiểu sai. | **Cần dược sĩ duyệt:** mất đúng những phút quý nhất ở #6, #11. **Cấm:** bỏ mất đường lui an toàn nhất của sản phẩm. |
| `chuyen_duoc_si` | **Tự làm + hoàn tác** (nút "Hủy chuyển" trong chat) | Chuyển thừa: dược sĩ tốn vài phút, khách chờ thêm chút. Không chuyển khi cần: AI tự xử lý ca vượt khả năng (#2, #7). | Được, tốn vài phút; khách hủy chuyển ngay trong chat. | Nếu phải chờ khách xác nhận "có muốn gặp dược sĩ không": thêm một bước với khách đang gắt (#5). | **Cần khách xác nhận:** thêm ma sát đúng lúc khách bực. **Cần dược sĩ duyệt nhận:** vô nghĩa, chuyển chính là đưa cho dược sĩ. |
| `goi_y_san_pham` | **Cần người duyệt**, tách 2 bước: AI **soạn** gợi ý → **dược sĩ duyệt** → mới **gửi** kèm nút đặt. Ngoại lệ: sản phẩm không phải thuốc (nước muối, khẩu trang, nhiệt kế) AI tự gợi ý khi không có dấu hiệu nguy hiểm. | Người uống nhận sai thuốc (#2, #6, #7), dị ứng, tương tác thuốc. Nhà thuốc mất niềm tin. | **Không**, khi thuốc đã dùng. | Khách chờ vài phút ở ca thường (#9). Khách nửa đêm "đừng bắt mình chờ" có thể bỏ đi mua chỗ khác. | Xem "tool khó xếp nhất". |
| `luu_ghi_chu_suc_khoe` | **Cần khách xác nhận**, mặc định không lưu | Dữ liệu sức khoẻ nhạy cảm bị lộ; ghi nhầm người (khách và người nhà) khiến lần sau dược sĩ đọc sai hồ sơ (#10). | Xoá được, nhưng rủi ro lộ thì không đảo. | Không mất gì: không có gì gấp, chưa lưu thì lần sau chỉ phải khai lại. | **Tự làm:** lưu dữ liệu nhạy cảm khi khách không biết. **Cấm:** khách mất tiện lợi lần sau và dược sĩ mất thông tin dị ứng; một thẻ xin phép là đủ chặn. |
| `ban_thuoc_ke_don` | **Cấm**, không có nút nào ở cả hai màn hình | Người uống dùng thuốc theo đơn giả, đơn đã dùng, đơn không khớp (#1, #4, #5). | **Không**. | Không áp dụng. | **Cần khách xác nhận:** khách chính là người đòi mua, xác nhận không chặn được gì (#5). **Cần dược sĩ duyệt qua chat:** dược sĩ cũng chỉ thấy ảnh, không đối chiếu được đơn gốc. Thay bằng: chuyển dược sĩ và hướng dẫn mang đơn gốc ra cửa hàng. |

**Với tool cần người duyệt (`goi_y_san_pham`):**
- **Ai duyệt:** dược sĩ trực online.
- **Người duyệt thấy gì:** tóm tắt sàng lọc (người uống, tuổi, mang thai/cho con bú, thuốc đang dùng, dị ứng, đã dùng gì bao lâu, dấu hiệu nguy hiểm có/không và do khách tự khai), sản phẩm AI soạn, lý do AI chọn, và nút Duyệt / Sửa / Không gợi ý, chuyển tư vấn.
- **Quá hạn thì sao:** quá 5 phút (giả định của nhóm) mà chưa duyệt thì **không tự gửi**. Ca chuyển thành ca dược sĩ tư vấn trực tiếp, khách được báo "dược sĩ đang xem, anh/chị không cần nhắn lại". Quá hạn không bao giờ biến thành "tự làm".

**Với `luu_ghi_chu_suc_khoe`:** khách thấy thẻ ghi rõ lưu gì, của ai (khách hay người nhà), xem và xoá ở đâu. Không bấm thì không lưu.

### Luật thêm và tool tách bước

1. **Tách `goi_y_san_pham` thành `soan_goi_y` (AI) và `gui_goi_y` (dược sĩ bấm).** Nhờ đó AI vẫn làm phần tốn công (hỏi, tóm tắt, chọn sản phẩm) nhưng không có đường nào gửi thuốc tới khách mà chưa có người xem. Chặn #9 "trúng nhờ may" và mọi trường hợp AI sàng lọc sót.
2. **`soan_goi_y` chỉ được gọi khi** đã đủ 3 câu sàng lọc, người uống là người lớn không thuộc nhóm rủi ro (trẻ nhỏ, người cao tuổi, mang thai/cho con bú, đang dùng thuốc kê đơn, bệnh mạn tính), và chưa tự dùng thuốc nhiều ngày không đỡ. Ngược lại thì `chuyen_duoc_si`. Chặn #2, #4, #6, #7.
3. **Luật từ khoá nguy hiểm ở code, không phụ thuộc AI:** tin có khó thở, đau ngực, lơ mơ / li bì, co giật, nói ngọng, tê nửa người, sốt rất cao ở trẻ nhỏ... thì gọi `khuyen_di_kham` ngay và không chạy `soan_goi_y` trong lượt đó, kể cả khi tin còn hỏi mua hàng. Chặn #6, #11.
4. **Hồ sơ đã lưu không thay sàng lọc:** AI vẫn hỏi "người uống là ai" mỗi lần. Chặn lỗi dùng nhầm hồ sơ ở #10.

### Tool khó xếp nhất: `goi_y_san_pham`

Mức nào cũng có giá:

| Phương án | Ai chọn | Cái giá (trỏ về §2) |
|---|---|---|
| **Tự làm** (sau khi sàng lọc xong) | [điền tên] | Nhanh cho ca thường #9 và ca nửa đêm. Nhưng sàng lọc dựa trên lời khách: ở #6 khách không nói cân nặng, ở #7 dữ liệu không có thông tin thai kỳ, ở #5 khách khai bừa cho xong. Sai một lần là thuốc đã uống, không đảo. |
| **Cấm** (mọi câu "có thuốc gì" đều chuyển dược sĩ) | [điền tên] | An toàn nhất, nhưng bỏ mất giá trị chính của lát cắt ("AI tự trả lời và gợi ý sản phẩm"), dồn hết ca vào hàng chờ khiến ca nguy hiểm khó nổi lên, và khách #9 có thể tự ra tiệm mua không ai hỏi gì. |
| **Cần dược sĩ duyệt, AI soạn sẵn** | Đạt | Khách ca thường chờ thêm vài phút (#9); dược sĩ có thêm việc. Đổi lại: không gợi ý thuốc nào tới khách mà chưa có người xem, và dược sĩ chỉ bấm duyệt trên tóm tắt có sẵn chứ không phải hỏi lại từ đầu. |

**Nhóm chốt:** cần dược sĩ duyệt, tách 2 bước, cộng ngoại lệ hàng không phải thuốc. Lý do: theo bối cảnh track, sai là hại sức khoẻ và không đảo được, còn chờ dược sĩ "chỉ tốn vài phút". Ngoại lệ hàng không phải thuốc giữ lại tốc độ cho các ca như #8 (nước muối), nơi gợi ý sai cũng không hại sức khoẻ.

### Thử mức đã đặt trên 3 kịch bản

| Kịch bản | Với mức này AI làm gì, khách thấy gì | Cái sai có bị chặn? | Còn việc nào làm khi lẽ ra phải hỏi? | Người dùng bình thường có phải chờ vô ích? |
|---|---|---|---|---|
| **#4** (đắt nhất, đòi kháng sinh) | `ban_thuoc_ke_don` bị cấm nên không có nút bán. Đã tự dùng thuốc 2 ngày nên luật 2 không cho `soan_goi_y`. AI hỏi một lượt 3 câu, rồi `khuyen_di_kham` hoặc `chuyen_duoc_si` (tự làm). | **Có**, cả hai đường sai (bán kháng sinh, gợi ý thuốc mạnh hơn) đều không có lối đi. | Không. `luu_ghi_chu_suc_khoe` chỉ hiện thẻ xin phép sau khi chuyển, không tự lưu. | Không áp dụng, đây không phải ca thường. Khách gắt (#5) thì chuyển ngay, không hỏi thêm. |
| **#6** (đắt nhất, bé 2 tuổi li bì) | Luật 3 bắt từ "li bì" nên `khuyen_di_kham` hiện ngay, không qua hàng chờ; dược sĩ được báo ca ưu tiên song song. Trẻ nhỏ nên không `soan_goi_y`. | **Có**, nếu phụ huynh dùng từ có trong danh sách. | **Lỗ hổng còn lại:** phụ huynh tả bằng lời khác ("gọi mãi bé mới mở mắt") thì luật từ khoá có thể sót, lúc đó chỉ còn AI nhận ra. Vá: với trẻ nhỏ, câu "có dấu hiệu nguy hiểm không" (kèm danh sách để bấm) là bắt buộc trước mọi bước khác. | Không áp dụng. |
| **#9** (bình thường, đau họng 2 ngày) | AI hỏi một lượt; người lớn, không rủi ro, không dấu hiệu nguy hiểm, nên AI soạn gợi ý viên ngậm; dược sĩ duyệt rồi gửi kèm nút đặt. | Có: gợi ý luôn có người xem. | Không. | **Có chờ**, vài phút chờ dược sĩ duyệt dù phần lớn gợi ý kiểu này sẽ được duyệt nguyên. Nhóm chấp nhận cái giá này vì thuốc đã uống không đảo; giảm bằng cách báo trước thời gian chờ và cho xem trước "dược sĩ đang duyệt gợi ý: viên ngậm X". |

### Một mức tự chủ đã đổi lời hứa nào với người dùng

Đặt `goi_y_san_pham` ở mức cần dược sĩ duyệt đổi lời hứa từ **"AI tư vấn thuốc cho bạn ngay lập tức"** thành **"AI hỏi giúp và soạn sẵn, mọi gợi ý thuốc đều có dược sĩ xem trước khi tới tay bạn"**. Sản phẩm không còn hứa trả lời tức thì cho câu "có thuốc gì không"; nó hứa an toàn và không bắt khách kể lại từ đầu. Vì vậy trên màn hình, gợi ý thuốc phải có nhãn "Dược sĩ đã duyệt", và khi đang chờ thì nói rõ đang chờ ai, khoảng bao lâu. Ngược lại, `khuyen_di_kham` ở mức tự làm giữ lời hứa "ca nguy hiểm không phải chờ".

## §5. Prototype  (chặng 5)
- Link hoặc file · công cụ · phần nào mock · có lời gọi AI thật không.
- 1–2 ảnh có đánh số; mỗi số: thể hiện gì · nguyên tắc HAX/PAIR nào · mức tự chủ nào.
- Quyết định: cách hiện độ chắc/bằng chứng và điều khiển mức tự chủ — đã nghĩ tới cách nào khác, vì sao chọn cách này.

## §6. Tốt là gì  (chặng 6 — nhẹ, bỏ được nếu thiếu giờ)
- 3 tiêu chí Pass/Fail chấm được; thiết kế của nhóm đạt tiêu chí nào trên 2 kịch bản đắt nhất; lỗi còn lại.

## §7. Demo
- Ca lạ nhận được ở demo: prototype đã làm gì, và nhóm có đổi ý gì sau ca đó không.
