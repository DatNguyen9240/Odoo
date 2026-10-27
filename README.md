# Hướng dẫn chạy Odoo 18 với Docker Compose

Dự án cài đặt và vận hành Odoo 18 Community cùng cơ sở dữ liệu PostgreSQL 16 bằng Docker Compose.

---

## 1. Cấu trúc thư mục

```text
D:\Dat\Odoo\
│
├── addons/               # Thư mục chứa các module/addon tùy chỉnh của bạn
├── config/
│   └── odoo.conf         # File cấu hình Odoo
├── .env                  # Cấu hình biến môi trường (port, database user/password,...)
├── docker-compose.yml    # Định nghĩa dịch vụ Odoo và PostgreSQL
└── README.md             # Hướng dẫn sử dụng
```

---

## 2. Các lệnh quản lý cơ bản

Mở PowerShell tại thư mục `d:\Dat\Odoo` và thực thi:

### Khởi động Odoo (chạy ngầm - background)
```powershell
docker compose up -d
```

### Xem log theo thời gian thực
```powershell
docker compose logs -f
```
*(Hoặc xem riêng log của Odoo: `docker compose logs -f web`)*

### Dừng dịch vụ
```powershell
docker compose stop
```

### Khởi động lại
```powershell
docker compose restart
```

### Dừng và xóa container (Dữ liệu database và filestore vẫn được giữ an toàn trong volumes)
```powershell
docker compose down
```

---

## 3. Truy cập Odoo

- Địa chỉ web: [http://localhost:8069](http://localhost:8069)
- **Master Password**: `admin` (Dùng để tạo mới database, sao lưu hoặc khôi phục dữ liệu)
- Lần đầu tiên truy cập, Odoo sẽ hiển thị màn hình **Database Manager**. Bạn điền:
  - **Database Name**: Tên database muốn tạo (vd: `odoo_db`)
  - **Email**: Tài khoản đăng nhập quản trị viên (vd: `admin@example.com`)
  - **Password**: Mật khẩu đăng nhập cho tài khoản admin
  - **Phone number**, **Language**, **Country**
  - Tích chọn **Demo data** nếu muốn có dữ liệu mẫu để thử nghiệm.

---

## 4. Cài đặt Custom Addons

Khi tải hoặc phát triển module mới:
1. Đặt thư mục module vào thư mục `addons/`.
2. Khởi động lại container Odoo:
   ```powershell
   docker compose restart web
   ```
3. Truy cập Odoo -> Kích hoạt chế độ **Developer Mode** -> vào menu **Apps** -> bấm **Update Apps List** -> tìm và cài đặt module.
