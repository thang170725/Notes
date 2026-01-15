# input()
**EX**
```bash
a = input("enter: ") # enter: 5
```

## Nhập ma trận (nxm)
```bash
2 3
1 2 3
4 5 6
```
**Ex1**
```python
# Nhập số hàng và số cột
n, m = map(int, input().split())

# Nhập ma trận
a = []
for _ in range(n):
    row = list(map(int, input().split()))
    a.append(row)

for row in a:
    print(*row)
```
**Ex2**
```python
n, m = map(int, input().split())
a = [list(map(int, input().split())) for _ in range(n)]

for row in a:
    print(*row)
```