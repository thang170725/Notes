# Kế thừa
Là lớp con. Nó sẽ kế thừa lại các thuộc tính của lớp cha.
**Cú pháp**
```bash
class Car(object):
	Def __init__(self, make, model, year):
	--snip—
class ElectricCar(Car):
	def __init__(self, make, model, year):
		super(ElectricCar, self).__init__(make, model,  year)
	--snip—
```
**Ex**
```python
class Person:
  def __init__(self, fname, lname):
    self.firstname = fname
    self.lastname = lname
  def printname(self):
    print(self.firstname, self.lastname)
class Student(Person):
  pass
x = Student("Mike", "Olsen")
x.printname() # Mike Olsen
```