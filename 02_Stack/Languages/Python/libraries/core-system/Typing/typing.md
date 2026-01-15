```text
- Giúp khai báo kiểu (type hint) để code rõ ràng hơn, dễ debug hơn, IDE tự gợi ý tốt hơn, 
    + Rõ ràng hơn — dễ đọc code
    + IDE thông minh hơn (Hiện gợi ý method đúng kiểu, Báo lỗi trước khi chạy, Giảm bug runtime)
    + Tool tự động kiểm tra (mypy, pylance) (Trong dự án lớn, typing giúp giữ code ổn định)
    + Dùng được với Generic, TypeAlias, Protocol (Typing giúp bạn viết code sạch, an toàn và mở rộng hơn)
- Thư viện này không cần tải. Cần import typing
```
List
from typing import List

def sum_list(numbers: List[int]) -> int:
    return sum(numbers)

print(sum_list([1, 2, 3]))
sum_list(["a", "b", "c"])  # IDE sẽ báo lỗi nếu bạn truyền sai kiểu
Tuple
from typing import Tuple

def get_user() -> Tuple[int, str]:
    return (1, "Thắng")

user = get_user()
print(user)
IDE sẽ hiểu tuple luôn có đúng 2 phần tử: int và str.
Dict 
from typing import Dict

def count_words(words: List[str]) -> Dict[str, int]:
    counts = {}
    for w in words:
        counts[w] = counts.get(w, 0) + 1
    return counts

print(count_words(["a", "b", "a"]))
IDE sẽ gợi ý rằng key là str, value là int.
