Mypy/
    ├── basic_types.md
    ├── functional_types.md
    ├── complex_protocols.md
    └── config.mdfrom typing import Protocol


# 1. Định nghĩa "interface" bằng Protocol
class Speaker(Protocol):
    def speak(self) -> str:
        ...


# 2. Các class KHÔNG cần kế thừa Speaker
class Dog:
    def speak(self) -> str:
        return "Gâu gâu"


class Human:
    def speak(self) -> str:
        return "Hello"


class Robot:
    def speak(self) -> str:
        return "Beep beep"


# 3. Class KHÔNG đúng interface
class Cat:
    def meow(self) -> str:
        return "Meo meo"


# 4. Hàm dùng duck typing
def make_sound(x: Speaker) -> None:
    print(x.speak())


if __name__ == "__main__":
    make_sound(Dog())
    make_sound(Human())
    make_sound(Robot())

    make_sound(Cat())
