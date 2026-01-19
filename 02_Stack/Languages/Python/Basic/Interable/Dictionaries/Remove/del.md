# Del
```bash
Để xóa cặp key: value trong dictionary.
```
**Syn**
```bash
del name[key]
```
**Ex**
```python
thisdict =	{
  "brand": "Ford",
  "model": "Mustang",
  "year": 1964
}
del thisdict["model"]
print(thisdict) # {'brand': 'Ford', 'year': 1964}
```