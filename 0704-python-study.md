# 인공지능 기초 다지기 - 파이썬 기초 문법III

속성: 2022

### 객체지향 프로그래밍

Object-Oriented Programming, OPP

- 객체 : 속성과 행동을 가짐. 속성은 변수, 행동은 함수로 표현됨
- 클래스와 실제 구현체인 인스턴스(instance)로 나뉜다

**Objects in Python**

- Python naming Rule (알아두면 좋은 상식)
    - snack_case : 띄워쓰기 부분에 “_” 추가. 뱀처럼 늘여씀. 파이썬 함수/변수명에서 사용하는 방식
    - CamelCase : 띄워쓰기 부분이 대문자. 파이썬 클래스명에 사용함
- __ 의 의미 : 특수한 예약 함수/변수 또는 함수명 변경(맨글링)에서 사용
    
    ex : __ main __ , __ add __ , __ str __ , __eq __ 등 - **매직메소드** 라고 함
    

```python
class SoccerPlayer(object):
    def __init__(self, name:str, position:str, back_number:int):
        self.name = name
        self.position = position
        self.back_number = back_number

    def change_back_number(self, new_number):
        print("선수의 등번호를 변경합니다. from {0} to {1}".format(self.back_number, new_number))
        self.back_number = new_number

    def __str__(self):
        return "Hello My name is {0}. My BackNumber is {1}".format(self.name, self.back_number)

    def __add__(self, other):
        return self.name + other.name

park = SoccerPlayer("Jiseong", "Mid", 21)
print(park)
park.change_back_number(23)
print(park)

son = SoccerPlayer("Heungmin", "FW", 25)
print(park+son)

# 출력 결과
# Hello My name is Jiseong. My BackNumber is 21
# 선수의 등번호를 변경합니다. from 21 to 23
# Hello My name is Jiseong. My BackNumber is 23
# JiseongHeungmin
```

### OPP Implementation Example

**노트북 만들기**

- Note를 정리하는 프로그램. 사용자는 노트에 뭔가를 적을 수 있음.
- Content가 있고 내용을 제거할 수 있으며 두 노트북을 합쳐서 하나로 만들 수 있음
- Note는 Notebook에 삽입되며 삽입될 때마다 페이지를 생성하고 최대 300페이지까지 생성이 가능하다.

```python
class Note(object):
    def __init__(self, content = None):
        self.content = content

    def write_content(self, content):
        self.content = content

    def remove_content(self, content):
        self.content = None

    def __add__(self, other):
        return self.content + other.content

    def __str__(self):
        return self.content

class NoteBook():
    def __init__(self, title):
        self.title = title
        self.page_number = 0
        self.notes = {}

    def add_note(self, note, page = 0):
        if(self.page_number > 300):
            print("꽉 찼습니다.")

        else:
            if page == 0:
                self.notes[self.page_number] = note
                self.page_number += 1
            
            else:
                self.notes = {page : note}
                self.page_number += 1

    def remove_note(self, page_number):
        if(page_number in self.notes.keys()):
            return self.notes.pop(page_number)
        
        else:
            print("페이지가 존재하지 않음")
        
    def get_number_of_page(self):
        return len(self.notes.keys())

book1 = NoteBook("1_notebook")
new_note = Note(input())

book1.add_note(new_note)
print(book1.get_number_of_page())
print(book1.notes[0])
```

### 객체지향 프로그래밍의 특징

inheritance : 상속, polymorphism : 다형성, visibility : 가시성

**Inheritance : 상속**

부모클래스로부터 속성과 메소드를 물려받은 자식 클래스를 생성하는 것

클래스를 선언할 때 상속받을 클래스를 () 안에 써줌.

```python
class Person(object):
    ...

class Korean(Person): #부모클래스 Person 을 상속받음
    ...
```

부모 클래스의 객체를 사용하고 싶다면 super()를 사용

부모 클래스 함수를 overriding 가능함.

**Polymorphism : 다형성**

같은 이름의 메소드의 내부 로직을 다르게 작성함.

Dynamic Typing의 특성으로 인해 파이썬에서는 같은 부모클래스의 상속에서 주로 발생함.

중요한 OOP의 개념이지만 파이썬에서 깊이 알 필요는 없다. 함수 재정의로 구현함.

**Visibility : 가시성**

객체의 정보에 접근할 수 있는 레벨을 조절하는 것. 누구나 객체의 모든 변수를 볼 필요는 없음. - 캡슐화(Encapsulation)

private 변수 선언 방법 : 앞에 “__” 를 붙인다.

property decorator : 숨겨진 변수를 반환해준다. @property 라고 씀

주로 deep copy로 반환해줌

### Decorator

first-class objects, inner function, decorator

**First-Class Objects : 일등함수/일급객체**

변수나 데이터구조에 할당이 가능한 객체, 파라미터로 전달이 가능하거나 리턴값으로 사용함. 파이썬 함수는 일급함수임. 다음이 성립함.

```python
def square(x):
    return x*x

f = square
print(f(5)) #25
```

**Inner Function**

함수 내에 또다른 함수가 존재할 수 있음.

```python
def print_msg(msg):
    def printer():
        print(msg)
    printer()

print_msg("i love you") #i love you
```

```python
def print_msg(msg):
    def printer():
        print(msg)
    return printer

message = print_msg("i love you") 
message() # i love you
```

**Decorator Function**

클로저, warpper를 씀

```python
def star(func): #func에 printer()가 들어감
    def inner(*args, **kwargs):
        print(args[1]*30)
        func(*args, **kwargs)
        print(args[1]*30)
    return inner

@star
def printer(msg, mark): 
    print(msg)

printer("hello", "*")
```

## Module & Project

모듈 : 프로그램에서 사용하는 작은 프로그램 조각들. 모듈을 모아서 하나의 큰 프로그램을 개발함. 모듈화하면 다른 프로그램에 갖다쓰기 편함

### Module

파이썬의 모듈 = .py

같은 폴더에 모듈.py와 돌리고자 하는 파일을 저장한 후 import를 통해서 모듈을 호출한다.

build-in module 이 있음.
