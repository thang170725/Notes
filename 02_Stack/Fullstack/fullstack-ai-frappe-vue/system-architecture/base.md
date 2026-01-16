- [Vì sao ERP dùng Frappe?](#vì-sao-erp-dùng-frappe)

---

```bash
- Frappe là một “hệ thống làm app quản lý” dựng sẵn gần như mọi thứ
- Nếu ví von:
    + Django / Spring = bộ khung + gạch + xi măng → bạn tự xây nhà
    + Microservice = cả khu đô thị → cần đội xây dựng chuyên nghiệp
    + Frappe = nhà lắp ghép cao cấp → chọn phòng, chọn cửa là ở được
- Frappe thực chất là 1 gói “ALL-IN-ONE”
    + Khi bạn dùng Frappe, bạn đã có sẵn:
        + Database
        + Backend (API)
        + Frontend (giao diện)
        + Login / User
- Phân quyền
    + CRUD
    + Form
    + Report
    + Workflow (duyệt, từ chối…)
    + Log, audit
- Bạn không phải hỏi: “Giờ làm giao diện kiểu gì, API ở đâu, auth sao đây?”
- Ví dụ đời thường (rất quan trọng): Bạn muốn làm app quản lý nhà đất
    + Không dùng Frappe:
        + Thiết kế DB
        + Viết model
        + Viết API
        + Viết form nhập
        + Viết trang list
        + Viết phân quyền
        + Viết report
- Dùng Frappe: Khai báo: Nhà đất có các cột: giá, diện tích, quận -> BẤM LƯU
    + Có luôn:
        + Bảng DB
        + Màn hình nhập
        + Màn hình xem
        + API
        + Quyền user
```

# Vì sao ERP dùng Frappe?
```bash
- ERP thực chất là:
    + Nhập dữ liệu
    + Sửa dữ liệu
    + Xem dữ liệu
    + Phân quyền
    + Duyệt
    + Báo cáo
-> Frappe sinh ra chỉ để làm mấy việc này cho nhanh và chuẩn
```