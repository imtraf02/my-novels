---
name: style-check
description: Use this skill when the user wants their chapter/draft checked for word-choice and tone consistency — e.g. modern/thuần Việt words leaking into narration or other characters' dialogue when the setting calls for Hán Việt/cổ trang register, or a POV character's "allowed modern voice" bleeding into places it shouldn't. Triggers on phrases like "từ ngữ thì sao", "kiểm tra văn phong", "có từ nào bị lệch tông không", "rà lại cách dùng từ chương này". Also usable proactively right after Claude drafts or revises a chapter, before handing it back to the user. Works from bible/style-guide.md and bible/glossary.md — this skill is generic and not tied to any one story's specific characters or setting.
---

# Style & Word-Choice Check

Rà một đoạn/chương văn xem có từ ngữ bị lệch tông (đăng ký ngôn ngữ — register) so với quy tắc văn phong đã định cho truyện, và có thuật ngữ nào chưa nhất quán với glossary.

## Nguyên tắc cốt lõi

Không phải mọi từ hiện đại/thuần Việt đều là lỗi. Vấn đề là **từ đó xuất hiện đúng chỗ được phép hay không**. Trước khi rà bất kỳ chương nào, luôn đọc `bible/style-guide.md` để biết:
- Nhân vật/POV nào được phép dùng giọng hiện đại (thường là nhân vật xuyên không/trọng sinh, chỉ trong nội tâm hoặc lời tự thuật của chính họ)
- Những gì phải luôn giữ Hán Việt/cổ trang: lời kể khách quan (narration không thuộc về suy nghĩ ai), lời thoại của các nhân vật bản địa (không xuyên không)

Nếu `bible/style-guide.md` chưa có mục này, hỏi người dùng để xác lập trước, đừng tự suy đoán — quy tắc này khác nhau tùy truyện.

## Quy trình rà 1 chương

### Bước 1 — Xác định các "vùng giọng văn" trong chương
Đọc chương, phân loại từng đoạn:
- Nội tâm/suy nghĩ của nhân vật được phép giọng hiện đại → vùng ĐƯỢC PHÉP lệch tông
- Lời kể khách quan (narration) → vùng PHẢI giữ đúng tông đã định (thường cổ trang/Hán Việt)
- Lời thoại của nhân vật khác (không có đặc quyền giọng hiện đại) → vùng PHẢI giữ đúng tông

### Bước 2 — Quét từ ngữ lệch tông trong các vùng PHẢI giữ tông
Trước tiên, đọc `bible/word-substitutions.md` nếu có — đây là bảng tra modern↔cổ trang riêng của truyện, ưu tiên dùng thay thế có sẵn trong bảng này trước khi tự nghĩ ra phương án mới. Nếu file chưa tồn tại, đề xuất tạo mới (xem mẫu khởi tạo bên dưới).

Tìm từ/cụm từ mang sắc thái hiện đại, khẩu ngữ, hoặc quá thuần Việt so với nền cổ trang đã định — nhưng đang nằm lộn vào narration hoặc lời thoại nhân vật bản địa. Các nhóm hay gặp: đại từ nhân xưng (tôi/ông/mày-tao), thán từ (Ồ/Oke/Ừa), tính từ mô tả kiểu hiện đại/ngôn tình, cụm động từ nghe "công sở/quân sự hiện đại".

Với mỗi chỗ tìm được:
- Nếu đã có trong `word-substitutions.md` → dùng đúng phương án đã chốt, không tự bịa thêm
- Nếu chưa có → đề xuất 2-3 phương án thay thế giữ đúng tông cổ trang, ưu tiên giữ nguyên sắc thái/mức độ hài hước gốc, rồi hỏi người dùng có muốn thêm vào bảng để dùng nhất quán về sau không

### Bước 3 — Đối chiếu thuật ngữ với glossary
Với mọi danh từ riêng, tên cảnh giới/hệ thống tu luyện, đơn vị đo lường, chức vị... xuất hiện trong chương:
- Nếu đã có trong `bible/glossary.md` → kiểm tra viết đúng y hệt (kể cả dấu, cách viết hoa)
- Nếu chưa có → liệt kê ra để người dùng xác nhận thêm vào glossary (đừng tự ý thêm — có thể là biến thể cố ý)

### Bước 4 — Kiểm tra lặp từ gần nhau
Quét các từ/cụm lặp lại trong khoảng cách gần (cùng đoạn hoặc vài đoạn liên tiếp) làm giảm nhịp đọc — đặc biệt: động từ tường thuật (nói, nhìn, im lặng...), tính từ mô tả cảm xúc, chủ ngữ mở đầu câu liên tiếp. Xem `references/common-issues.md` để biết các loại lặp hay gặp.

### Bước 5 — Tổng hợp kết quả
Trình bày theo nhóm (không phải liệt kê tuần tự từng dòng):
1. Lệch tông (narration/lời thoại nhân vật khác bị lẫn giọng hiện đại)
2. Thuật ngữ chưa khớp glossary / thuật ngữ mới cần xác nhận
3. Lặp từ/cụm gần nhau

Với mỗi lỗi: trích câu gốc ngắn, giải thích ngắn gọn vì sao, đề xuất thay thế. Không viết lại toàn bộ chương trừ khi người dùng yêu cầu.

## Khi nào KHÔNG báo là lỗi

- Từ hiện đại nằm trong nội tâm/lời tự thuật của nhân vật có đặc quyền giọng hiện đại (đây là chủ đích, không phải lỗi)
- Từ lặp lại có chủ đích tu từ (điệp ngữ nhấn mạnh) — chỉ báo lặp khi rõ ràng là vô ý, làm nhịp đọc đều đều nhàm

## Xác lập word-substitutions.md lần đầu (nếu bible chưa có)

Nếu `bible/word-substitutions.md` chưa tồn tại, đề xuất tạo file này — đây là **dữ liệu sống** (bảng tra modern→cổ trang), khác với style-guide (quy tắc). Cấu trúc gợi ý: chia theo nhóm (đại từ nhân xưng, thán từ, tính từ, động từ...), mỗi dòng gồm từ hiện đại / từ cổ trang thay thế / ghi chú ngữ cảnh dùng. Bảng lớn dần theo từng chương được rà — mỗi lần tìm ra từ mới cần đổi, hỏi người dùng chốt phương án rồi thêm dòng mới vào bảng, không tự ý quyết định một mình.

## Xác lập style-guide lần đầu (nếu bible chưa có)

Nếu người dùng chưa có mục quy tắc giọng văn trong `bible/style-guide.md`, đề xuất thêm mục dạng:

```markdown
## Quy tắc giọng văn (register)
- Nhân vật có đặc quyền giọng hiện đại: [tên nhân vật] — chỉ trong nội tâm/lời tự thuật
- Lời kể khách quan: luôn Hán Việt/cổ trang
- Lời thoại nhân vật bản địa: luôn Hán Việt/cổ trang, không lẫn khẩu ngữ hiện đại
- Ngoại lệ (nếu có): [ví dụ nhân vật khác cũng xuyên không, hoặc bối cảnh đặc biệt]
```
