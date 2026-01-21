# Hiển thị list of dict ra dạng bảng đẹp
**Ex1**
**Resource**
```python
data = [
    {"name": "An", "age": 20, "score": 8.5},
    {"name": "Bình", "age": 21, "score": 9.25},
    {"name": "Chi", "age": 19, "score": 7},
]
```
**Output**
```python
name | age | score
-----+-----+------
An   | 20  | 8.5  
Bình | 21  | 9.25 
Chi  | 19  | 7 
```
```python
def print_table(data: list) -> None:
    headers = list(data[0].keys())

    # Tính độ rộng mỗi cột
    col_widths = {
        h: max(len(str(h)), max(len(str(row[h])) for row in data))
        for h in headers
    }

    # In header
    header_line = " | ".join(f"{h:<{col_widths[h]}}" for h in headers)
    separator = "-+-".join("-" * col_widths[h] for h in headers)

    print(header_line)
    print(separator)

    # In dữ liệu
    for row in data:
        print(" | ".join(f"{str(row[h]):<{col_widths[h]}}" for h in headers))

data = [
    {"name": "An", "age": 20, "score": 8.5},
    {"name": "Bình", "age": 21, "score": 9.25},
    {"name": "Chi", "age": 19, "score": 7},
]

print_table(data)
```
**Ex2**
**Resource**
```python
data = {
    'names': ['Thang', "Minh", "Nghia", "Quy"],
    'ages': [18, 20, 23, 16],
    'scores': [10, 9, 6, 7]
}
```
**Output**
```python
names | ages | scores
------+------+-------
Thang | 18   | 10    
Minh  | 20   | 9     
Nghia | 23   | 6     
Quy   | 16   | 7 
```
**Answer**
```python
def convert_to_list_of_dict(data: dict):
    return [ 
        dict(zip(data.keys(), values))
        for values in zip(*data.values())
    ]

def print_table(data: list):
    headers = list(data[0].keys())
    
    col_widths = {
        h: max(len(h), max(len(str(row[h])) for row in data) )
        for h in headers
    }

    headers_line = ' | '.join(f'{h:<{col_widths[h]}}' for h in headers)
    separator = '-+-'.join('-'*col_widths[h] for h in headers)

    print(headers_line)
    print(separator)

    for row in data:
        print(" | ".join(f'{row[h]:<{col_widths[h]}}' for h in headers))
data = {
    'names': ['Thang', "Minh", "Nghia", "Quy"],
    'ages': [18, 20, 23, 16],
    'scores': [10, 9, 6, 7]
}

data = convert_to_list_of_dict(data)

print_table(data)
```

# Hiển thị list of list ra dạng bảng đẹp
**Resource**
```python
data = [
    ["Name", "Age", "Score"],
    ["An", 20, 8.5],
    ["Bình", 21, 9.25],
    ["Chi", 19, 7],
]
```
**Answer**
```python
def print_table_list(data):
    col_count = len(data[0])

    col_widths = [
        max(len(str(row[i])) for row in data)
        for i in range(col_count)
    ]

    for idx, row in enumerate(data):
        line = " | ".join(f"{str(cell):<{col_widths[i]}}" for i, cell in enumerate(row))
        print(line)

        if idx == 0:
            print("-+-".join("-" * w for w in col_widths))
```