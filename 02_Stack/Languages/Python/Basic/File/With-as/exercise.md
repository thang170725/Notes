# Đọc ghi file
**Resources**
**input.txt**
```bash
Hello world
File handling is important
Hello file
I love programming
```
**Topic**
```bash
- Đọc toàn bộ nội dung từ file input.txt.
- Thực hiện các xử lý sau:
    + Đếm số dòng trong file.
    + Đếm tổng số từ trong file.
    + Đếm số lần xuất hiện của từ "hello" (không phân biệt hoa/thường).
    + Ghi kết quả ra file output.txt theo định dạng:
- output.txt
Number of lines: X
Number of words: Y
Occurrences of 'hello': Z
```
**Answer**
```python
import os

input_file = 'input.txt'
output_file = 'output.txt'

if not os.path.exists(input_file):
    print("Input file does not exist")
else:
    with open(input_file, 'r') as inp, open(output_file, 'w') as out:
        lines = [line.strip() for line in inp]

        num_lines = len(lines)
        words = [word.lower() for line in lines for word in line.split()]
        num_words = len(words)
        hello_count = words.count('hello')

        print('Number of lines:', num_lines)
        print('Number of words:', num_words)
        print("Occurrences of 'hello':", hello_count)

        out.write(f"Number of lines: {num_lines}\n")
        out.write(f"Number of words: {num_words}\n")
        out.write(f"Occurrences of 'hello': {hello_count}\n")
        out.write('-' * 30 + '\n')
```