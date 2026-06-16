# Luật bảo mật Realtime Database (nên đặt trước sự kiện)

Hiện database đang ở **test mode**: ai cũng đọc/ghi được và **tự hết hạn sau ~30 ngày**.
Cho sự kiện nội bộ ngắn thì dùng được ngay. Để an toàn hơn, dán bộ luật dưới đây vào:

**Firebase Console → Build → Realtime Database → tab _Rules_ → dán → Publish**

```json
{
  "rules": {
    "rooms": {
      "$room": {
        "voters": {
          ".read": true,
          ".write": true,
          "$id": {
            ".validate": "newData.hasChildren(['name','picks','ts']) && newData.child('name').isString() && newData.child('name').val().length <= 60"
          }
        }
      }
    }
  }
}
```

- Cho phép mọi người **đọc** kết quả và **thêm** phiếu mới.
- Bắt buộc mỗi phiếu có `name`, `picks`, `ts`; tên tối đa 60 ký tự.
- Không khoá sửa/xoá ở mức chặt (đủ cho sự kiện nội bộ). Muốn chặt tuyệt đối thì
  đổi `".write": true` ở cấp `voters` thành chỉ cho thêm: bỏ dòng đó và thêm
  `".write": "!data.exists()"` vào trong `$id`.

## Lấy toàn bộ dữ liệu thô
Trên poster: nút **Export results** → tải CSV.
Hoặc Firebase Console → Realtime Database → ⋮ → **Export JSON** tại node `rooms/esports-championship-2026`.
