# car-parking

🚗 Dự án: Car Parking Platform

📌 Mô tả:
Một nền tảng kết nối chủ bãi đậu xe (người cho thuê) và người đi xe (người thuê) với hệ thống booking theo slot thời gian, thanh toán, xác thực, realtime, v.v.

🧱 Kiến trúc các services (Microservice + Fullstack-ready)
Service	Mô tả chính
auth	Đăng ký, đăng nhập, JWT, RBAC: user, owner, admin
user	Thông tin người dùng, xác thực email, cập nhật profile
parking	CRUD bãi đậu xe, mô tả, vị trí, giá, ảnh
availability	Khai báo thời gian khả dụng theo ngày/giờ của mỗi bãi
booking	Người dùng đặt chỗ, chọn khung giờ, tính toán giá
payment	Stripe/ZaloPay session + webhook + xác thực thanh toán
notification	Gửi email hoặc realtime thông báo về đơn đặt chỗ
realtime	Socket.io cập nhật trạng thái (slot còn trống, đặt thành công,...)
admin	Dashboard quản lý người dùng, booking, bãi xe
gateway	API Gateway dùng cho FE (có Auth + Rate-limit + Logging)

🧰 Công nghệ backend
Thành phần	Mô tả cụ thể
Express.js	Framework chính cho mỗi service
PostgreSQL	Database chính, quản lý giao dịch booking
Redis	Cache slot khả dụng, chống double booking
BullMQ	Queue gửi mail, task delay
Prisma ORM	Mapping DB + Migration
Socket.io	Gửi thông báo realtime khi có thay đổi trạng thái slot
JWT + RBAC	Xác thực + phân quyền cho user/owner/admin
OpenTelemetry + Jaeger	Logging/tracing toàn hệ thống
Docker	Đóng gói, chạy mọi thứ qua docker-compose
GCP (Cloud Run, SQL)	Triển khai miễn phí + dễ mở rộng

🌐 Tính năng phía người dùng
Người dùng (Người thuê)
Tìm kiếm chỗ đậu theo vị trí (geolocation) + thời gian

Đặt trước chỗ đậu → thanh toán → nhận xác nhận

Nhận thông báo realtime khi được chấp nhận/hủy

Chủ bãi (Người cho thuê)
Đăng ký chỗ đậu xe (vị trí, giờ hoạt động, giá)

Cập nhật khả dụng, xem đơn đặt lịch

Xác nhận hoặc từ chối yêu cầu đặt chỗ

