# Format chuẩn cho chapter summary

Lưu tại `summaries/chapters/chXXXX-summary.md`. Dùng số chương 4 chữ số để sort đúng thứ tự (ch0850, không phải ch850).

```markdown
---
chapter: 850
arc: 29
book: 3
---

**Tóm tắt:** [2-4 câu, sự kiện chính xảy ra trong chương, theo thứ tự thời gian trong chương]

**Nhân vật xuất hiện:** A, B, C
**Nhân vật mới:** [để trống nếu không có]

**Thay đổi trạng thái quan trọng:**
- [VD: A phát hiện bí mật của B → ảnh hưởng tới quan hệ A-B từ đây]
- [VD: C bị thương nặng, chưa rõ sống/chết]

**Mốc thời gian/địa điểm:** [nếu chương này xác lập điều gì mới, VD: "3 ngày sau sự kiện chương 847", "bối cảnh chuyển sang Thành Lạc Dương"]

**Móc nối chương sau:** [1 câu — chương này để lại câu hỏi/mâu thuẫn gì cần giải quyết]
```

## Ví dụ

```markdown
---
chapter: 850
arc: 29
book: 3
---

**Tóm tắt:** An lẻn vào thư viện cấm để tìm manh mối về cái chết của sư phụ.
Cô phát hiện cuốn nhật ký ghi lại việc Long — người cô tin tưởng nhất — từng
là đệ tử của kẻ thù. Bị lính canh phát hiện, An buộc phải bỏ trốn mà chưa kịp
đọc hết.

**Nhân vật xuất hiện:** An, Long (nhắc tên qua nhật ký, không xuất hiện trực tiếp), lính canh (không tên)
**Nhân vật mới:** (không có)

**Thay đổi trạng thái quan trọng:**
- An biết được quá khứ của Long nhưng chưa xác nhận được, tạo nghi ngờ
- Thư viện cấm giờ bị siết an ninh chặt hơn sau vụ đột nhập

**Mốc thời gian/địa điểm:** Thư viện cấm, hoàng cung Lạc Dương, đêm khuya

**Móc nối chương sau:** An sẽ đối mặt Long — hỏi thẳng hay giấu bí mật?
```

## Quy tắc viết summary

- Khách quan, không lẫn giọng văn tiểu thuyết (không ẩn dụ, không mô tả cảm xúc hoa mỹ — chỉ nêu sự kiện)
- Ưu tiên NHỮNG GÌ THAY ĐỔI (trạng thái nhân vật, quan hệ, thông tin người đọc/nhân vật khác biết) hơn là mô tả hành động bề mặt
- Nếu chương chủ yếu là thoại/nội tâm không có sự kiện lớn, ghi rõ "chương chuyển tiếp, không có thay đổi trạng thái lớn" thay vì cố bịa ra sự kiện
- Giữ dưới 200 từ phần tóm tắt chính, kể cả với chương dài
