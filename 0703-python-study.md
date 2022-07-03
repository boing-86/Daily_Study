# 인공지능 기초다지기 - 파이썬 기초문법II

속성: 2022

# 기초문법II

### Python Data Structure

---

`Stack` : Last In First Out

push는 입력, pop은 출력

list 구조를 사용하여 `append()`, `pop()` 으로 구현 가능

`Queue` : First In First Out

list에서 `append()`, `pop(0)` 으로 구현 가능

`Tuple` : 값 변경이 불가능한 리스트. 선언할 때 `()` 사용

리스트의 연산, 인덱싱, 슬라이싱은 동일하게 사용

튜플의 값이 1개인 경우 반드시 “,”를 붙여주어야 함.

```python
t = (1) #일반 정수 입력으로 인식
t = (1,) #이렇게 선언!
```

`Set` : 값을 순서없이 저장. 중복은 불허함

set 객체 선언을 이용하여 객체를 생성함

`remove()`, `discard()`로 특정값 삭제. `update()`로 추가. `clear()`로 전부삭제

수학에서 활용하는 집합 연산 가능 → `union()`, `intersection()`, `difference()` 등

`Dictionary` : 구분지을 수 있는 값과 함께 저장함. 고유값을 Identifier 또는 Key라고 함. Key를 활용하여 Value를 관리함.

- Key로 Value를 검색함
- {Key1:Value1, Key2:Value2, Key3:Value3 …} 형태

**Collection 모듈**

아래 모듈을 모두 지원함

![스크린샷 2022-06-28 오후 6.37.01.png](%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%80%E1%85%A9%E1%86%BC%E1%84%8C%E1%85%B5%E1%84%82%E1%85%B3%E1%86%BC%20%E1%84%80%E1%85%B5%E1%84%8E%E1%85%A9%E1%84%83%E1%85%A1%E1%84%8C%E1%85%B5%E1%84%80%E1%85%B5%20-%20%E1%84%91%E1%85%A1%E1%84%8B%E1%85%B5%E1%84%8A%E1%85%A5%E1%86%AB%20%E1%84%80%E1%85%B5%E1%84%8E%E1%85%A9%E1%84%86%E1%85%AE%E1%86%AB%E1%84%87%E1%85%A5%E1%86%B8II%20a7da4053249748e0897a71bb4e638dda/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2022-06-28_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_6.37.01.png)

`Deque` : 스택과 큐를 모두 지원. List에 비해 효율적인 자료저장 방식을 지원

## Pythonic Code

---

사용하는 이유

- 코드 이해도를 높인다 : 많은 개발자들이 python 스타일로 코딩한다.
- 효율 : for loop append보다 list가 빠르고 짧다

### `split` & `join`

`split` 함수 : string type의 값을 기준값으로 나누어서 List 형태로 반환함

```python
string.split("기준값")
```

join 함수 : string으로 구성된 list를 합쳐서 하나의 string 으로 변환

```python
'연결 사이에 들어갈 내용'.join(list)
'-'.join(['red', 'green', 'blue']#red-green-blue
```

### List Comprehension

기존 리스트로 다른 리스트를 만드는 기법. 일반적으로 for-loop-append 보다 빠름

```python
result = [i for i in range(10) if(i%2 == 0)]
print(result) #[0, 2, 4, 6, 8]

word_1 = "Hello"
word_2 = "World"
result = [i+j for i in word_1 for j in word_2]
#for i in word_1:
#   for j in word_2: 와 동일
print(result)
#출력결과
#['HW', 'Ho', 'Hr', 'Hl', 'Hd', 
#'eW', 'eo', 'er', 'el', 'ed', 
#'lW', 'lo', 'lr', 'll', 'ld', 
#'lW', 'lo', 'lr', 'll', 'ld', 
#'oW', 'oo', 'or', 'ol', 'od']

case_1 = ["A", "B", "C"]
case_2 = ["D", "E", "A"]
result = [i+j for i in case_1 for j in case_2 if not(i==j)]
print(result)
#출력결과
#['AD', 'AE', 'BD', 'BE', 'BA', 'CD', 'CE', 'CA']

word = 'The quick brown fox jumps over the lazy dog'.split()
print(word)
stuff = [[w.upper(), w.lower(), len(w)] for w in word]
print(stuff)

case_1 = ["a", "b", "c"]
case_2 = ["d", "e", "a"]
result = [[i + j for i in case_1] for j in case_2]
#for j in word_2:
#   for i in word_1: 와 동일
print(result)
```

`enumerate` : 리스트의 element를 추출할 때 번호를 붙여서 추출함

```python
for i, v in enumerate(['tic', 'tac', 'toe']):
    print(i, v)
#0 tic
#1 tac
#2 toe

my_list = ['a', 'b', 'c', 'd']
print(list(enumerate(my_list)))
#[(0, 'a'), (1, 'b'), (2, 'c'), (3, 'd')]

print({i:j for i, j in enumerate('Artificial intelligence (AI), is intelligence demonstrated by machine, unlike the natural intelligence displayed by humans and animals'.split())})
```

`zip` : n개의 list의 값을 병렬적으로 가져옴

```python
alist = ['a1', 'a2', 'a3']
blist = ['b1', 'b2', 'b3']
for a,b in zip(alist, blist):
    print(a, b)
#a1 b1
#a2 b2
#a3 b3

a,b,c = zip((1,2,3), (10, 20, 30), (100, 200, 300))
print(a,b,c)
#(1, 10, 100) (2, 20, 200) (3, 30, 300)

print([sum(x) for x in zip((1,2,3), (10, 20, 30), (100, 200, 300))])
#[111, 222, 333]

alist = ['a1', 'a2', 'a3']
blist = ['b1', 'b2', 'b3']
for i, (a, b) in enumerate(zip(alist, blist)):
    print(i, a, b)
#0 a1 b1
#1 a2 b2
#2 a3 b3
```

### lambda, map, reduce

**lambda function**

함수 이름 없이, 함수처럼 쓸 수 있는 익명 함수. python3 부터는 권장하지 않으나 여전히 많이 쓰이고 있음.

```python
#예시코드
f = lambda x, y:x+y
g = lambda x: x**2
h = lambda x: x/2
print(f(1,4)) #5
print(g(3)) #9
print(h(3)) #1.5
print((lambda x: x+1)(5)) #6
```

하지만 PEP8에서는 사용을 권장하지 않음 : 문법 어려움, 테스트 어려움, 문서화 docstring 지원이 미흡, 해석 어려움, 이름없는 함수 출현 등 문제

**map function**

실행시점의 값을 생성하고 메모리를 효율적으로 사용할 수 있음.

그러나 이해하기 어려우므로 사용을 권장하지 않음.

```python
ex = [1,2,3,4,5]
f = lambda x, y : x+y
print(list(map(f, ex, ex)))
#[2, 4, 6, 8, 10]
```

**reduce function**

여러개의 데이터를 누적집계하기 위해서 사용함. 

reduce (집계함수, 순회데이터)

```python
from functools import reduce #많이 안씀
print(reduce(lambda x, y : x+y, [1,2,3,4,5])) #15
```

![스크린샷 2022-07-01 오후 5.04.09.png](%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%80%E1%85%A9%E1%86%BC%E1%84%8C%E1%85%B5%E1%84%82%E1%85%B3%E1%86%BC%20%E1%84%80%E1%85%B5%E1%84%8E%E1%85%A9%E1%84%83%E1%85%A1%E1%84%8C%E1%85%B5%E1%84%80%E1%85%B5%20-%20%E1%84%91%E1%85%A1%E1%84%8B%E1%85%B5%E1%84%8A%E1%85%A5%E1%86%AB%20%E1%84%80%E1%85%B5%E1%84%8E%E1%85%A9%E1%84%86%E1%85%AE%E1%86%AB%E1%84%87%E1%85%A5%E1%86%B8II%20a7da4053249748e0897a71bb4e638dda/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2022-07-01_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_5.04.09.png)

→ 단, lambda, map, reduce 모두 권장하지 않음. legacy library나 머신러닝 코드에서 사용중이므로 알고 있어야 함!

### Iterable Object

Sequence형 자료형에서 데이터를 순서대로 추출하는 오브젝트

리스트, 튜플, string 등

내부적 구현으로 _ _iter_ _와 _ _ next_ _ 가 사용됨

iter(), next()함수로 iterable 객체를 iterator object로 사용함!

```python
cities = ["Seoul", "Busan", "Jeju"]
iter_obj = iter(cities) #memory address를 가져옴

print(next(iter_obj)) #Seoul
print(next(iter_obj)) #Busan
print(next(iter_obj)) #Jeju
#next(iter_obj) - StopIteration Error!
```

### Generator

element가 사용되는 시점에 값을 메모리에 반환한다.

```python
def general_list(value):
    result = []
    for i in range(value):
        result.append(i)
    return result

def generator_list(value):
    result = []
    for i in range(value):
        yield i

print(general_list(5)) #[0, 1, 2, 3, 4]

for a in generator_list(5):
    print(a)
#호출시점에 값을 던져줌. 
#덩어리를 가지고 불러오는 것보다 메모리 주소를 절약할 수 있다.
#0
#1
#2
#3
#4
```

Generator Comprehension

list comprehension과 비슷한 형태. generator형태의 리스트를 생성함.

[ ] 대신 ( )를 사용함! 

```python
import sys
gen_ex = (n*n for n in range(500))
print(type(gen_ex)) #<class 'generator'>
print(sys.getsizeof(gen_ex)) #112 메모리를 조금 쓴다!
print(sys.getsizeof(list(gen_ex))) #4216
list_ex = [n*n for n in range(500)]
print(sys.getsizeof(list_ex)) #4216
```

list 타입의 데이터를 반환해주는 함수는 generator로 만든다 → 읽기 쉬움, 중간에서 loop이 중단될 수 있을 때 사용하면 좋음

큰 데이터를 처리할 때에는 generator expression을 고려하라 → 큰 데이터 처리에 좋음!

### Function Passing Arguments

**Keyword arguments**

함수에 입력되는 param의 변수명을 사용해서 arguments를 넘김. 순서대로 넣지 않아도 됨!

```python
def print_some(my_name, your_name):
    print("Hello {0}, I'm {1}".format(your_name, my_name))

print_some("Psy", "JYP") #Hello JYP, I'm Psy
print_some(your_name="JYP", my_name="Psy") #Hello JYP, I'm Psy
```

**Default arguments**

param에 기본값을 설정해놓고 입력하지 않을 경우에는 기본값을 씀

```python
def print_some(my_name, your_name="JYP"):
    print("Hello {0}, I'm {1}".format(your_name, my_name))

print_some("Psy", "JYP") #Hello JYP, I'm Psy
print_some("Psy") #Hello JYP, I'm Psy
```

**Variable-length arguments - 가변인자**

함수의 param이 정해지지 않음. 

Asterisk(*)로 param을 표시하고 입력된 값은 **tuple type**으로 사용할 수 있다. 

가변인자는 오직 한 개만 맨 마지막 parameter 위치에 사용가능하다

```python
def variable_length_ex(a, b, *args):
    print('a = {0}, b = {1}, args = {2}'.format(a, b, args))
    return a+b+sum(args)

print(variable_length_ex(1,2,3,4,5))

#a = 1, b = 2, args = (3, 4, 5)
#15
```

**Keyword variable-length - 키워드 가변인자**

param 이름을 따로 지정하지 않고 입력하는 방법

Asterisk 2개 (**)로 인자를 표시하며 입력된 값은 **dict type**으로 사용한다

가변인자는 오직 한 개만 기존 가변인자 다음에 사용한다.

```python
def kwargs_test_1(**kwargs):
    print(kwargs)

def kwargs_test_2(**kwargs):
    print(kwargs)
    print("First value is {first}".format(**kwargs))
    print("First value is {second}".format(**kwargs))
    print("First value is {third}".format(**kwargs))

def kwargs_test_3(one, two, *args, **kwargs):
    print('one = {0}, two = {1}, args = {2}'.format(one, two, args))
    print('sum = {}'.format(one+two+sum(args)))
    print(kwargs)

kwargs_test_1(first = 1, second = 2, third = 3)
kwargs_test_2(first = 10, second = 20, third = 30)
kwargs_test_3(3,4,5,6,7,8,9,first = 3, second = 4, third = 5)

# 출력 결과
# {'first': 1, 'second': 2, 'third': 3}
# {'first': 10, 'second': 20, 'third': 30}
# First value is 10
# First value is 20
# First value is 30
# one = 3, two = 4, args = (5, 6, 7, 8, 9)
# sum = 42
# {'first': 3, 'second': 4, 'third': 5}
```

### Asterisk *

단순 곱셈, 제곱, 가변인자 등 다양하게 활용됨

unpacking a container : tuple, dict 등 자료형에 들어가있는 값을 unpacking 해준다. 함수의 입력값, zip 등 다양하게 사용가능함

```python
def as_test(a, *args):
    print(a, args)
    print(a, *args)
    print(type(args))

as_test(1, *(2,3,4,5,6))
as_test(1, (2,3,4,5,6))
```
