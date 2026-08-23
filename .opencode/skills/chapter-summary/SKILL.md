---
name: chapter-summary
description: Use this skill whenever the user finishes writing/editing a chapter of their novel and wants it summarized, indexed, or synced into the story bible. Triggers on phrases like "tóm tắt chương này", "cập nhật bible", "xong chương X rồi", "lưu tóm tắt", or any request to process a completed chapter file in a multi-chapter novel repo (especially long-running series with hundreds/thousands of chapters). Also use proactively after Claude itself finishes drafting or heavily revising a chapter for the user, to keep summaries/bible/timeline in sync without being asked each time.
---

# Chapter Summary & Bible Sync

Xử lý 1 chương vừa hoàn thành: sinh tóm tắt, gắn metadata, và đồng bộ vào story bible (nhân vật/timeline/glossary) — theo cấu trúc phân cấp để scale tới hàng nghìn chương mà không cần đọc lại toàn bộ lịch sử truyện.

## Khi nào dùng
- Người dùng vừa viết/sửa xong 1 file chương và muốn tóm tắt + cập nhật bible
- Người dùng hỏi "chương trước nói gì", "arc này tóm tắt sao" → đọc summary/arc tương ứng thay vì đọc full chapter
- Chuẩn bị viết chương mới → dùng bước "Nạp ngữ cảnh trước khi viết" bên dưới để chỉ nạp phần cần thiết, không nạp cả nghìn chương

## Cấu trúc repo — KHÔNG giả định, đọc từ bible/conventions.md

Mỗi bộ truyện có một cấu trúc riêng. Skill này KHÔNG hard-code đường dẫn nào cả.

### Bước 0 — Nạp cấu trúc của truyện (làm trước mọi bước khác)
1. Xác định thư mục SERIES: một dự án có thể chứa NHIỀU bộ truyện (vd `series/<ten-bo>/`, mỗi series có `bible/` riêng). Người dùng không nêu tên series mà dự án có >1 thư mục chứa `bible/` → hỏi trước khi làm gì cả.
2. Đọc `conventions.md` trong bible của series đó — bản đồ cấu trúc RIÊNG của truyện này: đường dẫn bản thảo, chỗ lưu chapter/arc/master summary, schema frontmatter, độ dài 1 arc, danh sách file bible.
3. Xử lý:
   - **Có conventions.md** → dùng đúng như nó ghi, kể cả khi khác hoàn toàn ví dụ bên dưới.
   - **Chưa có** → dò thực tế (Glob `**/ch*.md`, `**/summaries/**`, ...) rồi XÁC NHẬN với người dùng trước khi chạy; sau khi chốt, tạo `conventions.md` ghi lại để các lần sau và các skill khác khỏi hỏi lại.

Ví dụ MỘT cấu trúc phổ biến — chỉ minh hoạ, không phải chuẩn bắt buộc:

```
<novel-repo>/
├── bible/
│   ├── conventions.md   ← bản đồ cấu trúc của truyện này
│   ├── characters.md
│   ├── world.md
│   ├── timeline.md
│   └── glossary.md
├── book-XX/
│   └── chapters/chXXXX.md          ← nội dung chương (có frontmatter, xem dưới)
└── summaries/
    ├── chapters/chXXXX-summary.md   ← format xem references/summary-format.md
    ├── arcs/arc-NN.md              ← gộp summary của 1 khoảng arc_size chương
    └── master-summary.md           ← tóm tắt toàn truyện, vài trang
```

## Quy trình xử lý 1 chương vừa xong

### Bước 1 — Đọc chương
Đọc file chương vừa hoàn thành. Không cần đọc các chương khác trừ khi cần đối chiếu 1 chi tiết cụ thể.

### Bước 2 — Gắn/cập nhật frontmatter cho chương
Thêm vào đầu file chương (nếu chưa có) hoặc cập nhật:

```yaml
---
chapter: 850
arc: 29
title: "..."
pov: "Tên nhân vật kể chuyện/góc nhìn chính"
characters_present: [A, B, C]
locations: ["..."]
new_characters: []       # nhân vật lần đầu xuất hiện
key_events: ["..."]      # 1-3 sự kiện quan trọng nhất, ngắn gọn
timeline_notes: ""       # nếu chương này xác lập/thay đổi mốc thời gian
---
```
Metadata này là thứ các skill khác (continuity-check, glossary-sync) sẽ quét thay vì đọc full text — nên ưu tiên chính xác và súc tích hơn là đầy đủ.
Schema trường ở trên là MẶT ĐỊNH — nếu conventions.md khai báo schema khác cho truyện này thì theo conventions.

### Bước 3 — Sinh chapter summary
Xem `references/summary-format.md` cho format chuẩn. Tóm tắt ngắn (100–200 từ), tập trung: chuyện gì xảy ra, ai thay đổi trạng thái/quan hệ, có sự kiện nào ảnh hưởng chương sau. Lưu vào thư mục chapter summary đã khai báo trong conventions.md.

### Bước 4 — Cập nhật bible NẾU có thay đổi thực chất
Chỉ sửa `bible/` khi chương vừa xong làm thay đổi trạng thái lâu dài — không phải mọi chương đều cần:
- `characters.md`: nhân vật mới xuất hiện, chết, học kỹ năng mới, quan hệ đổi
- `timeline.md`: mốc thời gian mới được xác lập
- `glossary.md`: thuật ngữ/tên riêng mới lần đầu xuất hiện

Dùng str_replace/edit trực tiếp vào đúng mục liên quan trong bible — không viết lại toàn bộ file.

### Bước 5 — Cập nhật arc summary
Gộp arc theo kích thước khai báo trong conventions.md (mặc định ~20-30 chương nếu không ghi) — xem thư mục arc summary hiện có theo conventions, hoặc tạo mới nếu chương này mở arc mới. Thêm 1-2 câu tóm tắt chương này vào arc đang mở — arc summary không phải là ghép các chapter summary lại, mà là tóm tắt gọn hơn nữa ở tầm nhìn cao hơn.

### Bước 6 — Cập nhật master-summary.md (chỉ khi đóng 1 arc)
Không cập nhật mỗi chương. Khi 1 arc kết thúc, thêm 1 đoạn ngắn (3-5 câu) vào master summary (đường dẫn theo conventions.md) tóm tắt arc đó ở tầm truyện.

## Nạp ngữ cảnh trước khi viết chương mới

Khi người dùng chuẩn bị viết chương tiếp theo, KHÔNG đọc hết các chương cũ. Đường dẫn dưới đây lấy từ conventions.md. Nạp theo thứ tự ưu tiên, dừng khi đã đủ:
1. Master summary
2. Arc summary hiện tại (arc gần nhất)
3. 2-3 chapter summary gần nhất
4. Phần liên quan trong các file bible nhân vật & timeline (theo danh sách file trong conventions.md) — chỉ nhân vật/mốc thời gian sẽ xuất hiện trong chương sắp viết
5. Chỉ đọc full text chương cũ nếu cần trích dẫn/đối chiếu chi tiết cụ thể (dùng grep tìm từ khóa thay vì đọc tuần tự)

## Khi truyện đã rất dài (hàng trăm/nghìn chương)

- Không bao giờ đọc tuần tự nhiều file chương để tìm thông tin — grep từ khóa trên thư mục chapter summary (theo conventions) hoặc trên metadata frontmatter trước
- Nếu cần tìm "lần cuối nhân vật X xuất hiện là chương nào" → grep `characters_present` (hoặc trường tương đương khai báo trong conventions) trong frontmatter của các file chương/summary, không load nội dung
- Nếu thư mục arc summary đã nhiều (>15-20 file), cân nhắc thêm 1 tầng nữa: volume summary gộp nhiều arc — đề xuất đường dẫn với người dùng, chốt xong thì ghi vào conventions.md

## Lưu ý

- Không tự ý viết lại/diễn giải lại nội dung chương — chỉ tóm tắt sự kiện khách quan
- Nếu phát hiện mâu thuẫn với bible khi đọc chương (tên sai, mốc thời gian lệch...) trong lúc tóm tắt, báo cho người dùng ngay, đừng tự ý "sửa cho khớp" — đó là việc của skill continuity-check, không phải chapter-summary
- Giữ giọng tóm tắt trung lập, không lẫn văn phong tiểu thuyết vào summary
