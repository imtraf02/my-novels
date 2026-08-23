---
name: glossary-sync
description: Quét tên riêng/thuật ngữ qua frontmatter và grep, so với glossary của truyện (đường dẫn khai báo trong bible/conventions.md) — phát hiện thuật ngữ mới, chính tả lệch. Scale tới hàng nghìn chương bằng rg thay vì đọc file. Skill chung cho mọi bộ truyện, mỗi truyện một cấu trúc riêng.
---

# Đồng bộ bảng thuật ngữ (glossary sync)

Skill CHUNG — chỉ biết: quét tên riêng/thuật ngữ, so với `bible/glossary.md`.
Hoạt động với mọi bộ truyện, kể cả tiếng Việt có dấu. Ở quy mô 1.000+ chương, MỌI thao tác đếm/tra tìm dùng grep (`rg`), không đọc tuần tự.

## Input

- Phạm vi: 1 chương mới, hoặc toàn bộ bản thảo — đường dẫn lấy từ `conventions.md` trong bible của series. Không rõ → hỏi; mặc định chương mới nhất.
- Một dự án có thể chứa nhiều series (mỗi series một thư mục có `bible/` riêng) — không rõ series nào → hỏi người dùng.
- Bảng đối chiếu: đường dẫn glossary trong conventions.md (mặc định `bible/glossary.md`). Conventions không tồn tại mà mặc định cũng không thấy file → hỏi người dùng, đừng đoán.

## Các bước

1. **Nạp glossary** nếu tồn tại; giữ nguyên format sẵn có. Chưa có → đề xuất tạo khung:

   ```markdown
   # Glossary — <tên bộ truyện>

   ## Nhân vật
   | Thuật ngữ | Loại | Mô tả | Xuất hiện lần đầu |
   ```

2. **Thu ứng viên — rẻ trước, đắt sau**:
   - Tầng 1: frontmatter của (các) chương mới (`pov`, `characters_present`, `locations`, `key_events`, `new_characters`) — đã có sẵn danh sách thực thể, không cần đọc text.
   - Tầng 2: mục **Nhân vật xuất hiện / Nhân vật mới / Mốc thời gian-địa điểm** trong thư mục chapter summary theo conventions — thực thể đã được lọc sẵn, rẻ hơn đọc text gốc.
   - Tầng 3: text của chương mới — tên viết hoa giữa câu, từ trong ngoặc kép lúc xuất hiện đầu, "xưng hô + tên" (lão, sư huynh, tiểu thư... + tên), Họ + Tên nhiều âm tiết.
   - Tầng 4 (chỉ khi quét toàn bộ): `rg -o` rút mẫu trên rồi sort | uniq -c để đếm tần suất toàn repo — không mở file nào.

3. **So với glossary**, chia 3 nhóm:
   - **➕ Mới** — chưa có entry → đề xuất dòng mới (mô tả rút từ ngữ cảnh; không chắc thì `[?]`).
   - **⚠️ Lệch chính tả** — gần giống entry sẵn có nhưng khác dấu/thanh/ký tự ("Linh Kỳ" vs "Linh Khí"). Kiểm bằng cách `rg -i -n` từng biến thể có/không dấu trên toàn repo; liệt kê cặp so sánh + vị trí từng lần xuất hiện.
   - **🗑️ Lạc hậu** — có entry nhưng rg trả về 0 kết quả toàn repo → mới được coi là không còn dùng (chỉ báo cáo, KHÔNG đề xuất xoá).

4. **Báo cáo 3 nhóm**, mỗi phát hiện kèm số lần xuất hiện + `file:dòng` (grep trả sẵn). Sau đó hỏi có tự động ghi nhóm ➕ vào glossary không — chỉ sửa khi được xác nhận.

## Quy tắc

- Không bao giờ đọc tuần tự toàn bộ chapters; mọi phép đếm phải là grep.
- Từ tiếng Việt phổ thông dù lặp nhiều cũng không vào glossary.
- So ⚠️ bỏ qua hoa/thường và dấu thanh để tránh nhiễu.
- Không tự sửa chính tả trong chương; chỉ báo cáo.
- Khi thêm entry, điền cột "Xuất hiện lần đầu" = chương thấp nhất tìm thấy bằng `rg -l | sort`.
