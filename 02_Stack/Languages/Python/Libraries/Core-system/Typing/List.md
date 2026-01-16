# List
```python
from typing import List

def sum_list(numbers: List[int]) -> List[int]:
    return numbers

print(sum_list([1, 2, 3]))          # truyền đúng -> không lỗi
print(sum_list(["a", "b", "c"]))    # truyền sai -> không lỗi

# Chỉ dùng để gợi ý cho IDE không gây lỗi runtime dù có truyền sai
```