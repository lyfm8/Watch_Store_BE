# ⌚ WatchStore (Project-CNPM)

## 1. 📌 Giới thiệu dự án

**WatchStore** là hệ thống thương mại điện tử chuyên bán đồng hồ, gồm website khách hàng và dashboard quản trị (Owner/Staff) với đầy đủ nghiệp vụ mua bán, quản lý kho, đơn hàng và chăm sóc khách hàng. Backend viết bằng Spring Boot, frontend dùng React + Vite.

**Mục đích hệ thống**
- Cung cấp kênh mua sắm đồng hồ trực tuyến cho khách hàng.
- Hỗ trợ nhân viên/owner quản trị danh mục, sản phẩm, đơn hàng, bảo hành và báo cáo.
- Tích hợp AI tư vấn sản phẩm dựa trên dữ liệu hệ thống.

**Chức năng chính**
- Đăng ký/đăng nhập, xác thực JWT và OTP qua email.
- Quản lý sản phẩm, danh mục, nhà cung cấp, tồn kho, phiếu nhập.
- Giỏ hàng, đặt hàng, theo dõi trạng thái đơn.
- Đánh giá sản phẩm, bảo hành sau mua.
- Báo cáo doanh thu và thống kê dashboard.
- Upload ảnh sản phẩm lên Cloudinary.
- Tư vấn/chat AI (Google GenAI + Qdrant).

## 2. 🧰 Công nghệ sử dụng

**Frontend**
- React 18, TypeScript, Vite
- Tailwind CSS, Radix UI, Framer Motion
- React Router, React Query, Zustand
- React Hook Form + Zod
- Recharts (biểu đồ)
- Axios (gọi API)
- Vitest + Testing Library (test)

**Backend**
- Java 17, Spring Boot 3.5.x
- Spring Web, Spring Data JPA
- Spring Security + JWT (jjwt)
- Spring Validation
- Spring Mail
- Lombok
- Spring AI (Google GenAI) + Vector Store (Qdrant)
- Tomcat (packaging WAR)

**Database**
- MySQL (script mẫu: `Project-CNPM/demo/docs/data_v2.sql`)

**Dịch vụ bên thứ ba**
- Cloudinary (upload ảnh sản phẩm)
- Google GenAI (AI chat/embedding)
- Qdrant (vector search)
- Email SMTP (gửi OTP)

## 3. 🏗️ Kiến trúc và cấu trúc thư mục

```
WatchStore/
├── Project-CNPM/
│   └── demo/
│       ├── pom.xml
│       ├── docs/
│       ├── API_FLOW.md
│       └── src/main/java/com/example/demo/
│           ├── config/          # Cấu hình security, JWT, CORS, AI, Jackson
│           ├── controllers/     # REST controllers theo từng nghiệp vụ
│           ├── dtos/            # DTO request/response + mapper
│           ├── entities/        # Entity JPA
│           ├── exceptions/      # Xử lý lỗi và exception
│           ├── repositories/    # Spring Data JPA repositories
│           ├── services/        # Business logic, tích hợp Cloudinary/AI/Email
│           └── ProjectCnpmApplication.java
├── Project-CNPM-UI/
│   └── frontend/
│       ├── package.json
│       ├── docs/
│       ├── src/
│       │   ├── app/            # Layouts, router, providers
│       │   ├── assets/         # Style, ảnh, icons
│       │   ├── entities/       # Types/domain models theo module
│       │   ├── features/       # Module nghiệp vụ (auth, staff, orders,...)
│       │   ├── services/       # HTTP clients và service gọi API
│       │   ├── shared/         # UI components, hooks, utils, types dùng chung
│       │   └── main.tsx
└── README.md
```

## 4. 📋 Các chức năng của hệ thống

| Chức năng | Mô tả |
| --- | --- |
| Đăng ký | Đăng ký tài khoản, gửi OTP xác thực email |
| Đăng nhập | Xác thực bằng JWT, phân quyền theo vai trò |
| Quản lý người dùng | CRUD user/staff/owner |
| Quản lý danh mục | CRUD danh mục sản phẩm |
| Quản lý sản phẩm | CRUD sản phẩm, upload ảnh Cloudinary |
| Tìm kiếm sản phẩm | Lọc theo nhiều tiêu chí + phân trang |
| Giỏ hàng | Thêm/sửa/xóa item, xóa toàn bộ giỏ |
| Đặt hàng | Tạo đơn hàng và theo dõi trạng thái |
| Đánh giá | Đánh giá sản phẩm và tính điểm trung bình |
| Voucher | Quản lý và áp dụng mã giảm giá |
| Nhà cung cấp | Quản lý supplier và kiểm tra ràng buộc |
| Phiếu nhập | Nhập hàng, cập nhật tồn kho |
| Bảo hành | Tạo yêu cầu bảo hành và xử lý trạng thái |
| Báo cáo | Thống kê doanh thu, đơn hàng, top sản phẩm |
| Thông báo | Hệ thống notification nội bộ |
| AI Chat | Tư vấn sản phẩm bằng GenAI + Qdrant |

## 5. ⚙️ Hướng dẫn cài đặt

### 5.1 Clone project

```bash
git clone <repo-url>
```

### 5.2 Cài đặt package

**Frontend**

```bash
cd Project-CNPM-UI/frontend
npm install
```

**Backend**

```bash
cd Project-CNPM/demo
mvn -v
```

### 5.3 Cấu hình file .env / application properties

**Frontend (`.env`)**

```bash
VITE_API_BASE_URL=http://localhost:8080/api
```

**Backend (Spring Boot properties hoặc biến môi trường)**

```bash
# Database
spring.datasource.url=jdbc:mysql://localhost:3306/watchstore
spring.datasource.username=<db_user>
spring.datasource.password=<db_password>

# JWT
jwt.secret=<your-secret-key>
jwt.expiration-ms=86400000

# Mail OTP
spring.mail.username=<smtp_user>
spring.mail.password=<smtp_password>
spring.mail.host=<smtp_host>
spring.mail.port=<smtp_port>
app.mail.from=<optional-from-email>

# Cloudinary
cloudinary.url=<cloudinary-url>
cloudinary.folder=project-cnpm/products

# AI + Vector search
app.ai.qdrant.search-top-k=5
```

### 5.4 Chạy dự án

**Backend**

```bash
cd Project-CNPM/demo
mvn spring-boot:run
```

**Frontend**

```bash
cd Project-CNPM-UI/frontend
npm run dev
```

## 6. 🧭 API chính (trích yếu)

> Xem đầy đủ trong `Project-CNPM/demo/API_FLOW.md`

**Auth**
- `POST /api/auth/register` - Gửi OTP đăng ký
- `POST /api/auth/verify-email` - Xác thực OTP và tạo tài khoản
- `POST /api/auth/login` - Đăng nhập
- `POST /api/auth/forgot-password` - Gửi OTP reset mật khẩu
- `POST /api/auth/reset-password` - Đặt lại mật khẩu

**Users**
- `GET /api/users` - Danh sách user
- `GET /api/users/{id}` - Lấy user theo id
- `POST /api/users` - Tạo user nội bộ

**Products / Categories**
- `GET /api/products` - Danh sách sản phẩm
- `GET /api/products/search` - Tìm kiếm có filter + phân trang
- `POST /api/products` - Tạo sản phẩm
- `POST /api/products/{id}/images` - Upload ảnh
- `GET /api/categories` - Danh sách danh mục

**Cart / Orders**
- `GET /api/cart/{customerId}` - Lấy hoặc tạo giỏ hàng
- `POST /api/cart/{customerId}/items` - Thêm item
- `POST /api/orders` - Tạo đơn hàng
- `PATCH /api/orders/{id}/status` - Cập nhật trạng thái

**Reviews / Vouchers / Warranty**
- `POST /api/reviews` - Tạo đánh giá
- `GET /api/vouchers/active` - Voucher còn hiệu lực
- `POST /api/vouchers/apply/{code}` - Áp dụng voucher
- `POST /api/warranties` - Tạo yêu cầu bảo hành

**Reports**
- `GET /api/reports/summary` - Báo cáo tổng hợp

## 7. 🔄 Quy trình hoạt động của hệ thống

1. Người dùng thao tác trên frontend (React) và gọi API qua Axios.
2. Backend nhận request, xác thực JWT, phân quyền và xử lý nghiệp vụ.
3. Dữ liệu được lưu/truy vấn từ MySQL thông qua JPA.
4. Các dịch vụ bên thứ ba được gọi khi cần:
   - Cloudinary để upload ảnh.
   - SMTP để gửi OTP.
   - Google GenAI + Qdrant để trả lời tư vấn AI.

## 8. ✨ Các tính năng nổi bật

- Xác thực JWT + phân quyền theo role (OWNER/STAFF/ADMIN).
- OTP qua email cho đăng ký và quên mật khẩu.
- Upload ảnh sản phẩm lên Cloudinary.
- AI tư vấn sản phẩm theo dữ liệu thật (GenAI + Qdrant).
- Dashboard quản trị theo module nghiệp vụ.
- Báo cáo doanh thu và thống kê bán hàng.

## 9. 🚀 Hướng phát triển trong tương lai

- Tích hợp cổng thanh toán (VNPAY, Momo, ...).
- Thêm real-time notification (WebSocket).
- Hoàn thiện CRUD các module frontend còn placeholder.
- Bổ sung CI/CD và kiểm thử tự động end-to-end.

## 10. 👥 Thông tin nhóm phát triển

### Thành viên thực hiện

| STT | Họ tên              | Vai trò   |
| --- |---------------------|-----------|
| 1 | Lê Nguyễn Đăng Khoa | Fullstack |
| 2 | Trịnh Đại Nghĩa     | Fullstack  |
| 3 | Nguyễn Sư Thành Đạt | Fullstack   |
| 3 | Hà Trường Giang     | Fullstack   |
