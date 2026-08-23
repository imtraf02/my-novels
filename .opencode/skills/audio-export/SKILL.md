---
name: audio-export
description: Chuyển 1 chương truyện thành kịch bản text để gen audio TTS có biểu cảm — mỗi dòng một cụm thở, chèn tag [cười]/[thở dài]/[hắng giọng]. Skill chung, đường dẫn lấy từ bible/conventions.md của series.
---

# Audio export (kịch bản TTS)

Skill CHUNG — không phụ thuộc bộ truyện nào. Chỉ làm 2 việc: cắt dòng theo hơi thở và chèn tag biểu cảm. KHÔNG được viết lại văn.

## Input

- Một dự án có thể chứa nhiều series — xác định đúng series với người dùng nếu chưa rõ, rồi đọc `conventions.md` trong bible của series đó.
- File chương (mặc định: chương mới nhất theo đường dẫn bản thảo trong conventions).
- Nơi lưu: hàng "Kịch bản audio" trong bảng đường dẫn của conventions (mặc định: thư mục `audio/` nằm cạnh thư mục chapters, tên file `ch{ch}-audio.txt`).

## Format đầu ra

1. **Dòng tiêu đề:** `# CHAP {n}: {TÊN CHƯƠNG}` — viết thường hoá không cần, GIỮ nguyên dấu tiếng Việt.
2. **Mỗi dòng = một cụm thở:** tối đa ~12–15 âm tiết. Câu dài tách tại dấu phẩy hoặc ranh giới ngữ nghĩa. Câu đã ngắn thì giữ nguyên một dòng.
3. **Thoại:** giữ nguyên văn trong ngoặc kép `"..."`, mỗi câu một dòng. Thoại dài được tách nhiều dòng nhưng KHÔNG thêm/bớt/sửa một chữ nào.
4. **Tag biểu cảm** đứng RIÊNG một dòng, đặt ngay TRƯỚC câu nó áp dụng:
   - `[cười]` — đắc ý, nhẹ nhõm, sau punchline, tự mãn dễ thương
   - `[thở dài]` — mệt, than, chấp nhận số phận, đoạn suy tư chậm
   - `[hắng giọng]` — bối rối, vừa nhận ra điều lạ, chuẩn bị hỏi
   - Series có bộ tag riêng thì theo bible của series (ghi trong humor-style.md); skill mặc định dùng đúng 3 tag trên.
5. **Dòng trống** = ngắt cảnh lớn (chuyển địa điểm/POV). Trong cảnh thì liên tục, không chèn dòng trống giữa các câu ngắn.
6. **Số & đơn vị viết bằng chữ** cho tự nhiên: "ba trăm vạn", "mười ngày" — không để "300 vạn".
7. Tuyệt đối không: markdown in nghiêng/đậm, frontmatter, chú thích, emoji.

## Quy trình

1. Nạp conventions (Bước 0 giống các skill khác — đa series thì hỏi trước).
2. Đọc toàn bộ chương gốc.
3. Cắt dòng theo cụm thở. Truyện hài vốn kể câu ngắn — chủ yếu là tách những câu ghép dài.
4. Chọn chỗ gắn tag theo nghĩa cảnh; định mức: khoảng 3–8 tag cho chương 2.000 chữ, đặt ở beat cảm xúc THẬT, không rải đều máy móc, hai tag phải cách nhau ít nhất vài dòng.
5. Ghi file ra đường dẫn audio của conventions.
6. Báo cáo: tổng số dòng, số lượng từng loại tag, đường dẫn file đã ghi.

## Checklist cuối lượt

- [ ] Mọi câu thoại nguyên văn so với bản thảo?
- [ ] Không còn ký tự markdown (`*`, `_`)?
- [ ] Số liệu đã viết bằng chữ?
- [ ] Hai tag liên tiếp cách nhau > 3 dòng?
- [ ] Tiêu đề `# CHAP {n}: ...` đúng số chương?
