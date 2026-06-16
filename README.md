# Esports Championship 2026 — Voting Poster (gói hoàn chỉnh)

✅ **Đã cấu hình sẵn Firebase** (project `egs-esports`) — vote online realtime đa thiết bị đã sẵn sàng,
đã test ghi/đọc thành công và đã xoá dữ liệu test về 0.

## Dùng ngay
- **Online realtime (khuyên dùng cho sự kiện):** đưa **toàn bộ thư mục này** lên hosting
  (Netlify / Vercel / Firebase Hosting / server nội bộ), giữ nguyên cấu trúc — file
  `Esports Championship Poster.dc.html`, `support.js`, và thư mục `ds/` phải nằm cạnh nhau.
  Mở link trên nhiều điện thoại/máy → phiếu + Live Feed cập nhật realtime giữa mọi thiết bị.
- **1 file gọn:** `Esports Championship Poster (single-file).html` đã nhúng sẵn mọi asset.
  Mở trực tiếp là chạy; khi có mạng nó cũng đồng bộ realtime với cùng database.

## Trước sự kiện — đặt luật bảo mật
Xem **`DATABASE-RULES.md`**: dán bộ luật vào Firebase Console (test mode hiện tại sẽ hết hạn ~30 ngày).

## Lấy dữ liệu về máy
- Nút **Export results** trên poster → tải CSV (tổng phiếu theo game + danh sách người vote).
- Hoặc Firebase Console → Realtime Database → Export JSON tại `rooms/esports-championship-2026`.

## Nội dung thư mục
- `Esports Championship Poster.dc.html` — bản nguồn (đã gắn config, sửa nội dung tại đây).
- `Esports Championship Poster (single-file).html` — bản 1 file nhúng sẵn asset.
- `support.js` — runtime cần khi host bản `.dc.html`.
- `ds/` — font Montserrat, logo, CSS thương hiệu Eastgate.
- `FIREBASE-SETUP.md` — hướng dẫn Firebase (đã làm xong, để tham khảo).
- `DATABASE-RULES.md` — luật bảo mật nên đặt + cách export dữ liệu.

## Tuỳ chỉnh nhanh (đầu phần logic trong file .dc.html)
- `roomId` — đổi nếu chạy nhiều sự kiện trên cùng database (mỗi phòng đếm riêng).
- props `subhead`, `closeDate` — dòng mô tả & hạn bỏ phiếu hiển thị trên poster.
