# Bật vote online realtime (Firebase) — 5 phút

File `Esports Championship Poster.dc.html` đã được nối sẵn Firebase Realtime Database.
Khi chưa điền config → chạy local (mỗi máy đếm riêng). Điền config → mọi máy/điện thoại
vote chung một bộ dữ liệu, bảng % và Live Feed cập nhật **realtime**.

## Các bước

1. Vào https://console.firebase.google.com → **Add project** (đặt tên bất kỳ, có thể tắt Analytics).
2. Bên trái chọn **Build → Realtime Database → Create Database**.
   - Chọn location gần (Singapore `asia-southeast1` cho VN).
   - Chọn **Start in test mode** (cho sự kiện ngắn — xem mục Bảo mật bên dưới).
3. Bấm biểu tượng web `</>` ở **Project settings → Your apps → Web app** để tạo app,
   rồi copy đoạn `firebaseConfig` (apiKey, authDomain, **databaseURL**, projectId, appId).
4. Mở file, tìm khối `firebaseConfig = { ... }` ở đầu phần logic và dán giá trị vào.
   Bắt buộc có **apiKey** và **databaseURL**. Ví dụ:

   ```js
   firebaseConfig = {
     apiKey: "AIza....",
     authDomain: "my-event.firebaseapp.com",
     databaseURL: "https://my-event-default-rtdb.asia-southeast1.firebasedatabase.app",
     projectId: "my-event",
     appId: "1:1234567890:web:abcdef"
   };
   roomId = "esports-championship-2026"; // đổi tên phòng nếu chạy nhiều sự kiện
   ```

5. Xong. Mở trang trên nhiều thiết bị để kiểm tra — vote ở máy này hiện ngay ở máy khác.

## Đưa lên mạng (hosting)

- Cách nhanh nhất: dùng **Firebase Hosting** (`firebase deploy`) hoặc kéo–thả thư mục lên
  **Netlify / Vercel**. Nhớ kèm cả thư mục `ds/` (font + logo + CSS) cạnh file HTML.
- Hoặc xuất bản 1 file standalone đã nhúng sẵn assets rồi host file đó (assets đã gói trong file).

## Lấy dữ liệu về máy

- Nút **Export results** trên poster tải file CSV (tổng phiếu theo game + danh sách người vote).
- Dữ liệu gốc cũng nằm trong Realtime Database tại `rooms/<roomId>/voters` — có thể export JSON
  từ Firebase Console bất cứ lúc nào.

## Bảo mật (quan trọng)

Test mode mở read/write cho mọi người và **tự hết hạn sau ~30 ngày**. Cho sự kiện nội bộ ngắn thì ổn.
Để chặt hơn, vào **Realtime Database → Rules** và dùng luật chỉ-thêm (không cho sửa/xoá phiếu cũ):

```json
{
  "rules": {
    "rooms": {
      "$room": {
        "voters": {
          ".read": true,
          "$id": {
            ".write": "!data.exists()",
            ".validate": "newData.hasChildren(['name','picks','ts'])"
          }
        }
      }
    }
  }
}
```
