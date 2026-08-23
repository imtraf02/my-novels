---
name: continuity-check
description: So một chương với bible/ và lịch sử truyện ở quy mô 1.000+ chương — tra cứu phân tầng (master → arc → chapter summary → grep full text), không đọc tuần tự. Phát hiện mâu thuẫn nhân vật, thế giới, timeline, đồ vật. Skill chung cho mọi bộ truyện.
---

# Kiểm tra tính nhất quán (continuity check)

Skill CHUNG — không hard-code tên nhân vật hay luật thế giới.
Mọi quy tắc so sánh LẤY TỪ `bible/`; mọi sự kiện quá khứ tra qua tầng tóm tắt, không đọc lại nguyên văn.

## Input

- Thư mục series = thư mục chứa `bible/`. Dự án có thể chứa NHIỀU series (vd `series/<ten-bo>/`) — không rõ series nào → hỏi người dùng trước.
- Đọc `conventions.md` trong bible của series TRƯỚC khi chạy để biết cấu trúc riêng của truyện: đường dẫn bản thảo, các tầng summary, danh sách file bible. Chưa có conventions → dò thực tế, xác nhận với người dùng, rồi tạo.
- Chương cần kiểm tra (mặc định: chương mới nhất theo đường dẫn bản thảo trong conventions).

## Thang tra cứu (lookup ladder) — LUÔN đi từ trên xuống

Đường dẫn từng tầng lấy từ `bible/conventions.md` của truyện; bảng dưới gọi tên tầng, không ghim layout:

| Tầng | Nguồn | Dùng khi |
|------|-------|----------|
| 1 | Master summary | bức tranh toàn cảnh, hiện trạng |
| 2 | Book / arc summaries | sự kiện thuộc giai đoạn nào |
| 3 | Chapter summaries + frontmatter chương (`characters_present`, `locations`, `key_events`) | sự kiện cụ thể, ai có mặt ở đâu |
| 4 | Grep trên toàn bộ bản thảo | cần bằng chứng nguyên văn từng từ |
| 5 | Đọc nguyên văn 1 chương | cùng cực hiếm, chỉ khi grep trúng nhưng chưa đủ ngữ cảnh |

Ngân sách cứng: tối đa 5 chương nguyên văn/lượt kiểm. Vượt → dừng, báo người dùng nên chia nhỏ yêu cầu.

## Quy trình

1. **Đọc chương cần kiểm tra** (nguyên văn — đây là đối tượng bị soi).

2. **Đọc bible**: các file liên quan trực tiếp (`characters.md`, `world.md`, `timeline.md`...). Bible là nguồn sự thật, dung lượng nhỏ — được phép đọc trọn. Liệt kê file bible đã bỏ qua vào cuối báo cáo.

3. **Trích tuyên bố** từ chương: ngoại hình/tính cách/khả năng/trạng thái nhân vật, quan hệ, địa điểm & khoảng cách, tổ chức & lịch sử, luật hệ thống, mốc thời gian & tuổi, sở hữu đồ vật.

4. **Tra cứu từng tuyên bố theo thang ladder**:
   - Trước tiên tìm ở tầng 1–3. Thấy đủ → dừng, không xuống dưới.
   - Cần bằng chứng chính xác hơn → Grep tầng 4 với từ khóa rút từ tuyên bố: tên riêng, địa danh, tên vật phẩm, động từ đặc trưng. Dùng mẫu rộng trước (`rg -n -i`), thu hẹp sau nếu nhiễu.
   - Ghi lại tầng nào trả lời tuyên bố đó — báo cáo cần thể hiện chi phí tra cứu.

5. **Phân loại**:
   - 🔴 Mâu thuẫn trực tiếp — chương nói A, nguồn nói rõ không-A.
   - 🟡 Có thể mâu thuẫn — cần suy luận 2 bước; nêu cả hai cách hiểu.
   - 🟢 Bible chưa ghi — thông tin mới, không sai nhưng cần đồng bộ (gợi ý chạy chapter-summary/glossary-sync).

6. **Báo cáo**: mỗi mục gồm trích dẫn nguyên văn chương (`file:dòng`) vs trích dẫn nguồn (`file:dòng`, nêu rõ lấy từ tầng nào), mức độ, đề nghị xử lý. Cuối báo cáo: tổng 🔴🟡🟢 + việc cần làm theo ưu tiên + số liệu tra cứu (bao nhiêu tuyên bố dừng ở tầng nào).

## Quy tắc

- KHÔNG tự phán phía nào đúng — chỉ trình bày xung đột và đề xuất.
- Mọi phát hiện 🔴🟡 PHẢI có trích dẫn nguyên văn từ CẢ HAI nguồn.
- Bible mơ hồ ("khoảng", "có lẽ") ≠ mâu thuẫn trực tiếp.
- Twist được đánh dấu sẵn trong plot outline → chủ ý tác giả, không tính là lỗi.
- Với câu hỏi kiểu "X có từng làm Y không": trả lời bằng tầng thấp nhất có dữ liệu, kèm dẫn chứng; tuyệt đối không đọc hết chapters để trả lời.
