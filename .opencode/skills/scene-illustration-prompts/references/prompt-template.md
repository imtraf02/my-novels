# Prompt Template — ghép style + mô tả cảnh

Mẫu tham khảo cho Bước 3 của skill scene-illustration-prompts. Áp dụng cho mọi bộ truyện — không chứa nội dung cụ thể.

## Cấu trúc 1 prompt hoàn chỉnh

```text
{DÁN NGUYÊN VĂN toàn bộ nội dung bible/visual-style.md}

{ĐOẠN MÔ TẢ CẢNH — câu văn tự nhiên, gồm đủ 4 lớp:}
{1. Ai có mặt + ngoại hình đúng từng chữ theo character sheet}
{2. Hành động / biểu cảm / tư thế chính}
{3. Bối cảnh + chi tiết môi trường (được phép chi tiết hóa)}
{4. Bố cục gợi ý (nếu cần): close-up two-shot / wide establishing shot / low angle...}
```

## Quy tắc ghép

- Giữa style block và mô tả cảnh chỉ cách nhau một dòng trắng — không thêm tiêu đề, không đánh số, không giải thích.
- KHÔNG rút gọn/paraphrase style block. Copy y nguyên mỗi lần, kể cả các dòng IMPORTANT/Do not.
- Mô tả cảnh viết dạng đoạn văn liền mạch (3–6 câu), không dùng tag phân tách bằng dấu phẩy kiểu Midjourney.
- Không bao giờ yêu cầu chữ/caption trong ảnh (style đã cấm No text).

## Ví dụ cấu trúc (nội dung minh họa chung chung, không phải của truyện cụ thể)

```text
{visual-style.md nguyên văn dán tại đây}

An old sect elder with a thin frame, long white hair tied in a high bun with a wooden hairpin, wearing loose robes with faint cloud patterns, sits cross-legged on a raised platform inside a modest mountain hall. His eyes are closed, one hand resting on a small wooden seal beside him. Behind him stands a tall wooden cabinet stacked with herb baskets and hanging dried plants; sunlight falls through a round window onto the floor. Wide shot, slightly elevated angle showing the whole hall.
```

## Checklist trước khi ghi vào file prompts

- [ ] Style block nguyên văn 100%?
- [ ] Ngoại hình nhân vật khớp character sheet từng chữ (dáng/tóc/trang phục/phụ kiện)?
- [ ] Mỗi prompt đúng 1 beat có giá trị hình ảnh, không minh họa thoại trừu tượng?
- [ ] Đã kèm chú thích 1 dòng: cảnh này ứng với đoạn nào của chương?
- [ ] Số thứ tự prompt theo thứ tự xuất hiện trong chương?
