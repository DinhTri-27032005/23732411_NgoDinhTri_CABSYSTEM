# CAB System - API Specification

## 1. Giới thiệu

API Specification là tài liệu đặc tả các API của hệ thống **CAB System**.

Tài liệu được xây dựng dựa trên:

- Software Requirements Specification (SRS).
- Các Functional Requirements (FR).
- Business Rules (BRL).
- Use Cases (UC).
- Acceptance Criteria (AC).
- Các yêu cầu phi chức năng (NFR).

API được mô tả bằng định dạng **OpenAPI 3.0.0 (YAML)**.

Mục đích của API Specification:

- Mô tả các API của hệ thống.
- Xác định HTTP Method và Endpoint.
- Xác định Request và Response.
- Xác định HTTP Status Code.
- Mô tả các trường dữ liệu.
- Mô tả lỗi có thể xảy ra.
- Traceability giữa API và yêu cầu trong SRS.
- Hỗ trợ kiểm tra API bằng Swagger Editor hoặc Postman.

---

# 2. Cấu trúc thư mục

API được chia thành nhiều nhóm chức năng để dễ quản lý:

```text
API-Specification/
│
├── README.md
│
├── authentication/
│   └── authentication.yaml
│
├── booking/
│   └── booking.yaml
│
├── driver-matching/
│   └── driver-matching.yaml
│
├── trip-request/
│   └── trip-request.yaml
│
├── trip/
│   └── trip.yaml
│
├── driver-location/
│   └── driver-location.yaml
│
├── fare/
│   └── fare.yaml
│
├── payment/
│   └── payment.yaml
│
├── notification/
│   └── notification.yaml
│
├── trip-history/
│   └── trip-history.yaml
│
├── rating/
│   └── rating.yaml
│
├── operation/
│   └── operation.yaml
│
└── report/
    └── report.yaml
```
## 3. Danh sách nhóm API

| STT | Nhóm API | File | Chức năng chính |
|:---:|---|---|---|
| 1 | Authentication | `authentication/authentication.yaml` | Đăng ký, đăng nhập và quản lý thông tin tài khoản |
| 2 | Booking | `booking/booking.yaml` | Tạo và quản lý yêu cầu đặt xe |
| 3 | Driver Matching | `driver-matching/driver-matching.yaml` | Tìm kiếm và phân công tài xế |
| 4 | Trip Request | `trip-request/trip-request.yaml` | Xử lý yêu cầu chuyến đi của tài xế |
| 5 | Trip | `trip/trip.yaml` | Quản lý trạng thái và thông tin chuyến đi |
| 6 | Driver Location | `driver-location/driver-location.yaml` | Cập nhật và truy vấn vị trí tài xế |
| 7 | Fare | `fare/fare.yaml` | Tính và truy vấn cước chuyến đi |
| 8 | Payment | `payment/payment.yaml` | Xử lý và quản lý thanh toán |
| 9 | Notification | `notification/notification.yaml` | Gửi và quản lý thông báo |
| 10 | Trip History | `trip-history/trip-history.yaml` | Tra cứu lịch sử chuyến đi |
| 11 | Rating | `rating/rating.yaml` | Đánh giá tài xế |
| 12 | Operation | `operation/operation.yaml` | Quản lý và tra cứu dữ liệu vận hành |
| 13 | Report | `report/report.yaml` | Xem và quản lý báo cáo hoạt động hệ thống |

