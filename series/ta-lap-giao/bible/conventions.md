# Conventions — Ta Chỉ Là Chưởng Môn Yếu Kê, Đệ Tử Sao Toàn Là Thiên Kiêu?

> Bản đồ cấu trúc RIÊNG của truyện này. Mọi skill (chapter-summary, continuity-check,
> glossary-sync, style-check, audio-export, scene-illustration-prompts) đọc file này TRƯỚC KHI chạy.
> Mục để trống = dùng mặc định.

## Đường dẫn

Ký hiệu: `{ch}` = số chương 4 chữ số, `{nn}` = số arc 2 chữ số.

| Mục | Giá trị |
|-----|---------|
| Bản thảo chương | `book-01/chapters/ch{ch}.md` |
| Chapter summary | `summaries/chapters/ch{ch}-summary.md` |
| Arc summary | `summaries/arcs/arc-{nn}.md` |
| Book summary | `summaries/books/book-N.md` |
| Master summary | `summaries/master-summary.md` |
| Glossary | `bible/glossary.md` |
| Style guide | `bible/style-guide.md` |
| Kịch bản audio | `book-01/audio/ch{ch}-audio.txt` |
| Prompt ảnh minh họa | `book-01/chapters/image-prompts/ch{ch}-prompts.md` |

## Bible gồm những file nào

characters.md, world.md, timeline.md, glossary.md, style-guide.md, humor-style.md, plan-bo-moi.md, word-substitutions.md, visual-style.md

## Quy ước

- Thể loại: hài hước / xuyên không / yếu kê lưu / hiểu lầm
- Số chương trong tên file: 4 chữ số (`ch0007`, không phải `ch7`)
- **Độ dài mỗi chương: ~4.000 ký tự** (3.800–4.500, tính cả khoảng trắng, không tính frontmatter) — đây là chuẩn duy nhất; bible file nào ghi độ dài khác đều quy về mốc này
- Tỷ lệ thoại theo arc: hài 50–70%, nghiêm trọng 35–55% (chi tiết ở humor-style.md)
- Thống nhất số đếm thuần Việt trong narration: "ba mươi sáu tông" (không dùng ghép "tam mươi lục"); giữ Hán Việt cho thứ tự: đại/nhị/tam/tứ đệ tử
- Độ dài 1 arc: ~30 chương
- Frontmatter FILE CHƯƠNG: `chapter, arc, title, pov, characters_present, locations, new_characters, key_events, timeline_notes`
- Frontmatter FILE SUMMARY: `chapter, arc, book`
- Format phần thân summary: theo `references/summary-format.md` của skill chapter-summary
