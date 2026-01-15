[*row](./*row.md)
- [\[:\]](#)
  - [.apend() \& + \& .extend()](#apend----extend)
  - [.insert()](#insert)
  - [.count()](#count)
  - [.index()](#index)
  - [.reverse()](#reverse)
  - [.pop()](#pop)
- [Bài tập](#bài-tập)
  - [Tìm cặp có tổng bằng target](#tìm-cặp-có-tổng-bằng-target)

---





# [:]
Lấy phần tử trong mảng
a = ["VietNam", "America", "Island", "Porland", "Canada"]
print(a[2:4])
['Island', 'Porland']

## .apend() & + & .extend()
Thêm phần tử vào trong mảng hoặc nối 2 mảng

## .insert()
Để thêm phần tử vào một vị trí nào đó trong mảng.
**Ex**
```python
arr.insert(1, “orange”) # thêm orange vào vị trí index 1 trong mảng arr
fruits = ['apple', 'banana', 'cherry']
fruits.insert(1, "orange")
print(fruits)
['apple', 'orange', 'banana', 'cherry']
```

## .count()
Trả về số lượng phần tử có giá trị được chỉ định.
**Ex**
```python
fruits = ["apple", "banana", "cherry"]
x = fruits.count("cherry")
print(x) # 1
```

## .index()
Trả về vị trí đầu tiên xuất hiện của giá trị được chỉ định.
```python
fruits = ['apple', 'banana', 'cherry']
x = fruits.index("cherry")
print(x)
```

## .reverse()
Để đảo ngược một mảng.
**Ex**
```python
a = [1,2,3,4]
a.reverse()
print(a)
```


## .pop()
Lấy phần tử  ra khỏi mảng. trong các ngôn ngữ khác nó được sử dụng với nhiệm vụ là stack.

# Bài tập
## Tìm cặp có tổng bằng target
```python
def sum(target, li):
    li.sort()
    l, r = 0, len(li)-1
    while l < r:
            total = li[l] + li[r]
            if total == target:
                return li[l], li[r]
            elif total < target:
                l += 1
            else:
                r -= 1
    return 0, 0
```
**Result**
```text
n1, n2 = sum(12, [3,2,5,7,8,1,9])
print(n1, n2)
Example 1: 
Input: nums = [3,9,7], k = 5
Output: 4
Explanation:
    Perform 4 operations on nums[1] = 9. Now, nums = [3, 5, 7].
    The sum is 15, which is divisible by 5.
```
