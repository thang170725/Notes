```bash
- Đây là nơi chứa các hàm, phương thức để xử lý list trong Python
```
**Index**
<section style="background: #ee9; color: ">

1. [Add-to-List](./Add-to-List/) - Nơi chứa các hàm nhằm mục đích thêm phần tử vào danh sách
2. 
</section>

àm sao để nhập một mảng kiểu gì cũng được ví dụ tôi nhập cùng dòng,enter sau mỗi dòng hoặc thậm chí nhập kiểu [1,2,3], list(1,2,3) nó vẫn hiểu là list thì làm thế nào

Câu hỏi này rất hay 👍
Tóm gọn mục tiêu của bạn là:

Cho phép người dùng nhập “mảng” dưới NHIỀU kiểu khác nhau
– nhập từng dòng
– nhập cùng dòng, cách nhau bằng dấu phẩy
– nhập [1,2,3]
– nhập list(1,2,3)
→ cuối cùng chương trình vẫn hiểu là list

Mình chia làm 3 mức độ (từ đơn giản → chuyên nghiệp → dùng Pydantic).

1️⃣ Cách THỰC TẾ, phổ biến nhất (khuyên dùng)

👉 Nhận input là string → parse → convert thành list

import ast

def parse_list_input(user_input: str):
    user_input = user_input.strip()

    # Trường hợp người dùng nhập từng dòng
    if "\n" in user_input:
        return [line.strip() for line in user_input.splitlines() if line.strip()]

    # Trường hợp nhập dạng [1,2,3], ('a','b'), list(...)
    try:
        value = ast.literal_eval(user_input)
        if isinstance(value, (list, tuple, set)):
            return list(value)
    except:
        pass

    # Trường hợp: 1,2,3 hoặc a,b,c
    if "," in user_input:
        return [x.strip() for x in user_input.split(",")]

    # fallback: 1 phần tử
    return [user_input]

🔹 Ví dụ sử dụng
inputs = [
    "1,2,3",
    "[1,2,3]",
    "('a','b')",
    "list(range(3))",  # ❌ sẽ không chạy vì literal_eval an toàn
    "a\nb\nc"
]

for i in inputs:
    print(parse_list_input(i))

2️⃣ Muốn hỗ trợ cả list(1,2,3) → dùng regex + xử lý thủ công

⚠️ KHÔNG dùng eval() trực tiếp (rất nguy hiểm)

import ast
import re

def parse_any_list(s: str):
    s = s.strip()

    # list(1,2,3)
    if s.startswith("list(") and s.endswith(")"):
        inside = s[5:-1]
        return parse_any_list(f"[{inside}]")

    # nhiều dòng
    if "\n" in s:
        return [x.strip() for x in s.splitlines() if x.strip()]

    try:
        val = ast.literal_eval(s)
        if isinstance(val, (list, tuple, set)):
            return list(val)
    except:
        pass

    if "," in s:
        return [x.strip() for x in s.split(",")]

    return [s]


✔ An toàn
✔ Linh hoạt
❌ Không chạy code tùy ý

3️⃣ Cách CHUYÊN NGHIỆP: Dùng Pydantic custom validator
🎯 Dùng khi:

Input đến từ API / FastAPI

Muốn validate + normalize dữ liệu

from pydantic import BaseModel, field_validator
import ast

class InputModel(BaseModel):
    items: list

    @field_validator("items", mode="before")
    @classmethod
    def parse_items(cls, v):
        if isinstance(v, list):
            return v

        if isinstance(v, str):
            v = v.strip()

            if "\n" in v:
                return [x.strip() for x in v.splitlines() if x.strip()]

            if v.startswith("list(") and v.endswith(")"):
                v = f"[{v[5:-1]}]"

            try:
                parsed = ast.literal_eval(v)
                if isinstance(parsed, (list, tuple, set)):
                    return list(parsed)
            except:
                pass

            if "," in v:
                return [x.strip() for x in v.split(",")]

        raise ValueError("Không thể parse thành list")

🔹 Test
InputModel(items="1,2,3").items
InputModel(items="[1,2,3]").items
InputModel(items="a\nb\nc").items
InputModel(items="list(1,2,3)").items

4️⃣ Cách NHANH nếu nhập từ terminal
print("Nhập các phần tử (Enter trống để kết thúc):")
arr = []

while True:
    x = input()
    if not x:
        break
    arr.append(x)

print(arr)


✔ Dễ hiểu
✔ Thân thiện người dùng

5️⃣ KHÔNG nên làm
eval(user_input)  # ❌ cực kỳ nguy hiểm


Ví dụ người dùng nhập:

__import__('os').system('rm -rf /')


💀

6️⃣ Tổng kết
Cách	Linh hoạt	An toàn	Dùng khi
String parse thủ công	⭐⭐⭐⭐	⭐⭐⭐⭐	CLI
ast.literal_eval	⭐⭐⭐	⭐⭐⭐⭐⭐	Chuẩn Python
Pydantic validator	⭐⭐⭐⭐⭐	⭐⭐⭐⭐⭐	API
eval()	⭐⭐⭐⭐⭐	❌	KHÔNG BAO GIỜ

Nếu bạn muốn:

Tự động ép kiểu int/float/str

Nhập nested list

Nhập JSON + Python list

Dùng cho FastAPIs