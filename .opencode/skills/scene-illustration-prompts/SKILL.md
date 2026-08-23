---
name: scene-illustration-prompts
description: Use this skill when the user wants a chapter turned into a set of image-generation prompts to illustrate it (for editing into video via CapCut or similar). Triggers on phrases like "làm ảnh cho chương này", "tách cảnh để vẽ", "prompt ảnh minh họa", "ghép video capcut". Reads bible/characters.md and bible/visual-style.md to keep character appearance and art style consistent across hundreds of generated images. Output is TEXT PROMPTS ONLY (for Gemini image generation) — this skill does not generate images itself.
---

# Scene Illustration Prompts (cho video CapCut)

Tách 1 chương thành các cảnh cần minh họa, sinh prompt ảnh hoàn chỉnh cho từng cảnh (dùng với Gemini image generation), giữ style cố định và ngoại hình nhân vật nhất quán qua toàn bộ truyện.

## Giả định cấu trúc repo

```
bible/
├── characters.md            ← mô tả text nhân vật (tính cách...) — bổ sung thêm mục "ngoại hình" (xem dưới)
├── visual-style.md           ← style prompt CỐ ĐỊNH của cả bộ truyện (chỉ set up 1 lần)
└── character-refs/           ← ảnh tham chiếu nhân vật đã tạo (do NGƯỜI DÙNG lưu về sau khi generate)

book-XX/chapters/
├── ch0001.md
└── image-prompts/
    └── ch0001-prompts.md     ← output của skill này
```

## Bước 0 — Xác lập visual-style.md (chỉ làm 1 lần cho cả truyện)

Nếu `bible/visual-style.md` chưa có, tạo file này chứa NGUYÊN VĂN style prompt người dùng đã chốt (không tự ý diễn giải lại/rút gọn — đây là style prompt đã được tinh chỉnh kỹ, giữ y nguyên câu chữ mỗi lần dùng). File này sẽ được dán vào ĐẦU mỗi prompt cảnh, không đổi giữa các chương.

## Bước 0b — Xác lập mô tả ngoại hình nhân vật (character sheet)

Vì style là monochrome/sepia (không phân biệt được bằng màu sắc), nhân vật PHẢI phân biệt được qua: dáng người, kiểu tóc, phụ kiện, hoa văn trang phục, đặc điểm riêng. Với mỗi nhân vật xuất hiện, thêm vào `bible/characters.md` mục:

```markdown
## [Tên nhân vật] — mô tả ngoại hình (cho ảnh minh họa)
- Dáng người: [VD: hơi mập tròn, thấp đậm / cao gầy]
- Tóc: [kiểu búi, độ dài, phụ kiện cài tóc]
- Trang phục: [loại áo/bào, hoa văn đặc trưng — mô tả bằng độ đậm/nhạt và họa tiết, KHÔNG dùng tên màu vì ảnh là 1 tông màu]
- Đặc điểm nhận diện riêng: [VD: luôn cầm quạt, có nốt ruồi, dáng đi khom lưng]
- Ảnh tham chiếu: [đường dẫn tới bible/character-refs/ nếu người dùng đã tạo và lưu về]
```

Nếu nhân vật chưa có mục này khi cần tạo prompt, DỪNG lại và hỏi người dùng bổ sung trước — không tự bịa ngoại hình, vì bịa sai sẽ khiến ảnh không nhất quán với các ảnh trước đó của cùng nhân vật.

## Quy trình tách 1 chương thành các cảnh

### Bước 1 — Đọc chương, xác định các "beat" cần minh họa
Không phải mọi đoạn đều cần ảnh. Chọn ra 3-8 khoảnh khắc (tùy độ dài chương) có giá trị hình ảnh cao nhất — ưu tiên: thay đổi bối cảnh, hành động rõ ràng (không phải nội tâm trừu tượng), khoảnh khắc cảm xúc cao, mở đầu/kết chương. Bỏ qua các đoạn thuần thoại/nội tâm không có hình ảnh cụ thể để vẽ.

### Bước 2 — Với mỗi beat, viết mô tả cảnh bằng câu văn tự nhiên (không phải tag rời)
Gemini xử lý tốt prompt dạng đoạn văn mô tả, không cần tag kiểu Midjourney. Mỗi mô tả cảnh gồm:
- Ai có mặt (dùng đúng mô tả ngoại hình đã chốt ở character sheet, không đổi từ ngữ giữa các chương)
- Đang làm gì, biểu cảm/tư thế chính (đơn giản, phù hợp phong cách tối giản của style)
- Bối cảnh/không gian (đây là phần được phép chi tiết — kiến trúc, đồ vật, cảnh quan)
- Bố cục gợi ý nếu cần (cận cảnh 2 người đối thoại / toàn cảnh sân đình / góc thấp nhìn lên...)

### Bước 3 — Ghép thành prompt hoàn chỉnh
Cấu trúc mỗi prompt = `[visual-style.md nguyên văn]` + `[mô tả cảnh từ bước 2]`. Xem `references/prompt-template.md` để có mẫu ghép cụ thể.

### Bước 4 — Xuất file
Lưu tất cả prompt của chương vào `book-XX/chapters/image-prompts/chXXXX-prompts.md`, đánh số theo thứ tự xuất hiện trong chương, mỗi prompt kèm 1 dòng chú thích ngắn (cảnh này minh họa đoạn nào) để dễ đối chiếu khi ghép video.

## Giữ nhân vật nhất quán qua hàng trăm ảnh (quan trọng nhất)

Vì đây là điểm dễ vỡ nhất khi làm cả nghìn chương, nhắc người dùng quy trình dùng Gemini:
1. Tạo 1 ảnh "chuẩn" cho mỗi nhân vật chính (theo đúng mô tả trong character sheet) — đây là ảnh tham chiếu gốc
2. Khi tạo các ảnh cảnh sau có nhân vật đó, đưa kèm ảnh tham chiếu gốc làm input cho Gemini cùng với prompt — Gemini sẽ giữ đặc điểm nhân vật khớp với ảnh mẫu thay vì tạo ngẫu nhiên lại
3. Nếu người dùng chưa có ảnh tham chiếu cho 1 nhân vật khi skill cần tạo prompt có nhân vật đó, nhắc họ nên tạo ảnh tham chiếu trước

Skill này chỉ sinh TEXT PROMPT — việc đưa ảnh tham chiếu vào Gemini là thao tác người dùng tự làm bên ngoài (ngoài phạm vi skill).

## Lưu ý

- Không tự ý thêm/bớt chi tiết ngoại hình nhân vật ngoài những gì đã chốt trong character sheet
- Style prompt trong `visual-style.md` giữ NGUYÊN VĂN, không diễn giải lại — kể cả khi thấy có thể viết gọn hơn
- Nếu người dùng muốn đổi bố cục (16:9, cận/toàn cảnh...) linh hoạt theo cảnh, ghi rõ trong phần bố cục của từng prompt, không áp cứng 1 kiểu cho mọi cảnh
