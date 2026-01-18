# .value_counts()
```bash
Đếm số lượng giá trị trong một cột.
```
**Syn**
```python
c = self.df[column].value_counts()
df = pd.DataFrame({
    "Color": ["Red", "Blue", "Red", "Green", "Blue", "Yellow", "Red"]
})

# Đếm số lần xuất hiện mỗi giá trị
# print(df["Color"].value_counts())
# Red       3
# Blue      2
# Green     1
# Yellow    1
```