# Dict 
```python
from typing import Dict

def count_words(words: List[str]) -> Dict[str, int]:
    counts = {}
    for w in words:
        counts[w] = counts.get(w, 0) + 1
    return counts

print(count_words(["a", "b", "a"]))

# IDE sẽ gợi ý rằng key là str, value là int.
```