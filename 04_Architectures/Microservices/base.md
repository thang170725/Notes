```bash
- Microservice là kiến trúc, không phải chân lý.
- Nó rất mạnh khi:
    + Hệ thống rất lớn
    + Nhiều team làm song song
    + Mỗi phần scale độc lập
    + Có DevOps + CI/CD xịn
- Nhưng đổi lại:
    + Debug mệt
    + Triển khai phức tạp
    + Network latency
    + Over-engineering nếu dự án nhỏ / vừa
    -> 90% dự án ban đầu KHÔNG cần microservice
```