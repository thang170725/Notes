# .nunique()
```bash
- Để đếm tổng số lượng các giá trị khác nhau trong một cột nào đó.
```
**Ex**
```python
df = pd.DataFrame({
    "Color": ["Red", "Blue", "Red", "Green", "Blue", "Yellow", "Red"]
})

print(df["Color"].nunique()) # 4
```