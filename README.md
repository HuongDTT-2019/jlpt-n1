# 藍 N1 記憶帳 — Tủ đề luyện JLPT N1

App luyện đề N1 chạy hoàn toàn trên trình duyệt (HTML/JS, không cần build, không backend).
Một repo chứa **nhiều đề**, mỗi đề một thư mục. Tiến độ lưu bằng `localStorage`, riêng cho từng người và từng đề.

## Cấu trúc

```
index.html          → Trang chủ tổng: liệt kê các đề (đọc tiến độ để hiện "đã thuộc")
.nojekyll           → Tắt Jekyll cho GitHub Pages
2024-12/            → Đề 2024 tháng 12 (một khóa 9 buổi)
   index.html            → Trang chủ của đề này
   n1-2024-12-mondai-1-2.html   … các buổi …
   n1-2024-12-mondai-12-13.html
   n1-2024-12-ontong.html       → Tổng ôn (bản đồ 66 câu)
2025-07/            → (đề sau) …
```

URL sau khi deploy GitHub Pages:
- Trang tổng: `https://<user>.github.io/<repo>/`
- Một đề:     `https://<user>.github.io/<repo>/2024-12/`

## Vì sao nhiều đề chung một repo vẫn ổn

`localStorage` lưu theo **tên miền** (không theo thư mục), nên mọi đề dùng chung một kho.
Tên file & `key` của mỗi buổi đã gắn ngày thi (vd `n1-2024-12-mondai-5`), nên tiến độ các đề **không đè lên nhau**.

## Thêm một đề mới

1. Tạo thư mục mới theo ngày thi, vd `2025-07/`.
2. Bỏ bộ file của đề đó vào (dùng tên file & `key` có ngày thi của đề mới, vd `n1-2025-07-mondai-1-2`).
3. Thêm một dòng vào mảng `EXAMS[]` trong `index.html` ở gốc:

```js
{ folder:"2025-07", level:"N1", label:"2025 · Tháng 7",
  desc:"66 câu · 8 buổi", status:"ready", total:66,
  keys:["n1-2025-07-mondai-1-2", "n1-2025-07-mondai-3-4", "…"] }
```

4. `git add . && git commit -m "Đề 2025-07" && git push` (hoặc Upload files trên web).

## Deploy GitHub Pages

Settings → Pages → Source: **Deploy from a branch** → `main` / `(root)` → Save.
Mỗi lần push/upload, Pages tự deploy lại.

## Muốn tiến độ chung cho cả nhóm?

Bản này lưu cục bộ trên từng máy. Cần bảng xếp hạng / đồng bộ thì thêm backend nhẹ (Firebase / Supabase).
