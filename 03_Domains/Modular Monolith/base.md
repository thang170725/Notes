- [Thành phần cốt lõi của Modular Monolith](#thành-phần-cốt-lõi-của-modular-monolith)

---

```bash
- Modular Monolith = Monolith + ranh giới module rõ ràng
- Monolith:
    → 1 codebase
    → 1 ứng dụng chạy
    → 1 lần deploy
- Modular:
    → Chia hệ thống thành các module theo domain
    → Mỗi module có trách nhiệm rõ ràng
    → Module không xâm phạm logic của nhau
- Nó KHÔNG phải microservice, và cũng KHÔNG phải “monolith lộn xộn”.
```
**Hình dung nhanh (rất quan trọng)**
**Monolith “truyền thống” (spaghetti)**
```bash
Controller
  ↕
Service
  ↕
Service khác
  ↕
Repository
```

Logic xuyên domain

Debug đau đầu

Không thể tách ra sau này

✅ Modular Monolith (đúng nghĩa)
┌───────────┐   ┌───────────┐   ┌───────────┐
│  User     │   │ Listing   │   │  Payment  │
│  Module   │   │  Module   │   │  Module   │
└─────▲─────┘   └─────▲─────┘   └─────▲─────┘
      │               │               │
      └──────────┬────┴───────┬───────┘
                  Shared Kernel


Mỗi module như “mini-system”

Chạy chung process, nhưng suy nghĩ như tách biệt

3️⃣ Modular Monolith KHÔNG phải là gì?
Hiểu sai	Sự thật
Là microservice chạy chung	❌ Không
Là chia folder cho đẹp	❌ Không
Dùng cho hệ lớn	❌ Không
Giải pháp tạm	❌ Không

👉 Nó là kiến trúc hoàn chỉnh, không phải “bước đệm rẻ tiền”.

# Thành phần cốt lõi của Modular Monolith
**Module theo Domain, không theo kỹ thuật**
**Sai**
```bash
controller/
service/
repository/
```
**Đúng**
```bash
user/
listing/
property/
payment/
ai/

- Mỗi module có đầy đủ layer riêng
listing/
 ├── api/
 ├── application/
 ├── domain/
 ├── infrastructure/
- api: controller / endpoint
- application: use-case
- domain: business rules
- infra: DB, cache
```