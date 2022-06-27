
# 인공지능 기초 다지기 - 파이썬 기초
네이버커넥트재단 Boostcourse
## 기초문법I

### **Function and Console IO**

**Parameter vs Argument**

- `parameter` : 함수의 입력 값 인터페이스
- `argument` : 실제 parameter에 대입된 값

파이썬은 쉘에서 함수결과를 자동으로 프린트해줌. return 값의 유무를 조심할 것!

<img width="1061" alt="스크린샷 2022-06-27 오후 1 05 57" src="https://user-images.githubusercontent.com/54930076/175894765-4b928ee1-2ae7-429e-af01-e554e94ba717.png">

```python
def f_x(x):
    return 2*x + 7

def g_x(x):
    return x**2

def h_x(x) :
    f = f_x(x)
    print("f(x) = ", f)
    g = g_x(x)
    print("g(x) = ", g)
    fg = f_x(g)
    print("f(g(x)) = ", fg)
    gf = g_x(f)
    print("g(f(x)) = ", gf)
    return f + g + fg + gf

print("답은 ", h_x(2), "입니다.")
```

**Console IO**

출력(`print()`)과 입력(`input()`)이 있음.

input()은 str만 가능하므로 형변환을 해주면 됨

Print Formatting

1) %-format

`padding` : %type 앞에 숫자를 사용하면 숫자만큼의 칸 수를 사용하겠다는 뜻

ex )`%5.3f` → 5칸을 사용하고 소수점 아래 3자리를 출력하겠다

`naming` : dict를 쓸 때 표시할 내용을 변수로 표시하여 입력함

2) format 함수

3) fstring (이게 많이 쓰임)

예시코드

```python
print('%s %s'%('one', 'two'))
print('{} {}'.format('one', 'two'))
print('%d %d'%(1, 2))
print('{} {}'.format(1, 2))

print("***********%-format***********")
print("I have %d apples"%3)
print("You have %s apples"%"five")
number = 3
day = "three"
print("I ate %d apples. I was sic for %s days"%(number, day))
print("Product : %8s, Price per Unit : %10.6f"%("Apple", 5.243445))
#naming - dict type
print("Product : %(name)s, Price per Unit : %(price)5.3f"%{"name":"Apple", "price":5.234})

print("***********str.format()***********")
age = 23
name = "Boin Jeong"
print("I'm {0} years old".format(age))
print("My name is {0} and {1} years old".format(name, age))
print("Product : {0}, Price per Unit : {1:5.3f}".format("Apple", 4.243))

print("***********f-string***********")
print(f"Hello, {name}. You are {age} years old.")
print(f'{name:20}') #왼쪽 정렬 20칸 패딩
print(f'{name:>20}') #오른쪽 정렬 20칸 패딩
print(f'{name:*<20}') #왼쪽 정렬 20칸 패딩 + 빈칸은 *로 채움
print(f'{name:*>20}') #오른쪽 정렬 20칸 패딩 + 빈칸은 *로 채움
print(f'{name:*^20}') #중간 정렬 20칸 패딩 + 빈칸은 *로 채움
pi = 3.141502653589
print("pi is", f'{pi:.2f}') #floating point print
```

Lab과제

```python
def ctof(x):
    return 9/5*x+32

print("본 프로그램은 섭씨를 화씨로 변환해주는 프로그램입니다")
print("변환하고 싶은 섭씨 온도를 입력해주세요 : ")
cel = float(input())
print(f'섭씨온도 : {cel}')
print(f'화씨온도 : {ctof(cel):.2f}')
```

### Conditionals and Loops

**Condition - 조건문**

비교 연산자 `is`

`x is y` 는 메모리의 주소를 비교함

단 -5~256은 옛날 파이썬 사용 환경 때문에 정적 메모리에 숫자를 저장해서 사용하므로 is 연산에서 true가 나오지만 이 바운드를 벗어나면 false가 됨! - ~~근데 내 컴퓨터에선 바운드 벗어나도 True 나옴…~~

```python
a = 100
b = 100
print(a is b) #false

a = 300
b = 300
print(a is b) #false
```

숫자형의 경우 존재하면 참 없으면 거짓 → 0은 `false`, 나머지는 `true`

문자형의 경우 “”은 `false` 나머지는 `true`

**리스트에서 all, any 조건 사용**

```python
boolean_list = [True, False, True, False, True]
all(boolean_list) #False. And조건과 같음
any(boolean_list) #True. Or와 같음
```

**삼항 연산자(Ternary Operators)**

python에서는 잘 안썼는데 강사님이 알아두면 좋다고 함.

```python
value = 12
is_even = True if value%2==0 else False 
print(is_even) #True
#조건문에 괄호 넣어도 됨
```

연습문제

```python
#[연습] 무슨 학교 다니세요?
from datetime import datetime

print("당신이 태어난 년도를 입력하세요")
year = int(input())
age = datetime.today().year - year + 1
result = ""

if(20<=age & age<=26):
    result = "대학생"

elif(17<=age & age<20):
    result = "고등학생"

elif(14<=age & age<17):
    result = "중학생"

elif(8<=age & age<14):
    result = "초등학생"

else:
    result = "학생이 아닙니다"

print(f'{result}')
```

**Loop - 반복문**

반복문 상식

- 변수명 : i,j,k
- 0부터 시작 : 2진수가 0부터 시작하기 때문에 권장함
- 무한loop : CPU 메모리 등 리소스 많이 쓰기 때문에 권장하지 않음

For 문

```python
#시퀀스형 자료형
for i in "abcdefg":
    print(f'{i}')

#리스트 처리
for i in ["happy", "angry", "excited", "sad"]:
    print(f'{i}')

#간격 range
for i in range(0, 10, 2):
    print(f'{i}')

#역순으로 10부터 1까지 출력
for i in range(10, 0, -1):
    print(f'{i}')
```

While문

반복문 제어 - break, continue

```python
for i in range(10):
    print(f'{i}')

else:
    print("EOP")

i = 0
while i<10:
    print(f'{i}')
    i+=1
else: #break로 종료된 반복문은 else block을 수행하지 않음
    print("EOP") 

#출력결과
#0
#1
#2
#3
#4
#5
#6
#7
#8
#9
#EOP
```

연습문제 - 구구단 계산기

```python
#[연습] 구구단 계산기
print("구구단 몇 단을 계산할까요?")
num = int(input())
print(f"구구단 {num}단을 계산합니다.")

for i in range(1, 10):
    print(f"{num} X {i} = {num*i}")
```

```python
sentence = "i love you"
reverse_s = ""

for char in sentence:
    reverse_s = char + reverse_s
    print(reverse_s)
```

```python
#2진수 계산기 답이랑 이상한 문장들이 같이 출력돼ㅠㅠ 이게모야
decimal = 1024
result = ''

while(decimal > 0):
    remainder = decimal%2
    decimal = decimal // 2
    result = str(remainder) + result

print(result)
```

```python
#[연습] 숫자 찾기 게임 1~100 임의의 숫자를 맞춰라
import random

number = random.randint(1, 100)
answer = 0
print(f"숫자를 맞춰보세요(1~100)")

while(number != answer):
    answer = int(input())
    if(answer > number):
        print("숫자가 너무 큽니다.")

    elif(answer < number):
        print("숫자가 너무 작습니다.")

print(f"정답입니다. 입력한 숫자는 {answer} 입니다.")
```

```python
#[연습] 연속적인 구구단 입력
num = 1

while(True):
    print("구구단 몇 단을 계산할까요?(1~9)")
    num = int(input())

    if(num == 0):
        print("구구단 게임을 종료합니다.")
        break
    
    elif(num<1 or num>9):
        continue

    print(f"구구단 {num}단을 계산합니다.")
    
    for i in range(1, 10):
        print(f"{num} X {i} = {num*i}")
```

```python
#[연습] 사람별 점수 평균을 구해라
kor_score = [49, 79, 20, 100, 80]
math_score = [43, 59, 85, 30, 90]
eng_score = [49, 79, 48, 60, 100]
midterm_score = [kor_score, math_score, eng_score]
aver_score = []

print("사람 별로 평균을 구해라")

for i in range(0, len(midterm_score[0])):
    sum = 0
    sum = midterm_score[0][i] + midterm_score[1][i] + midterm_score[2][i]
    aver_score.append(sum/3)

print(aver_score)
```

### String & Advanced Function Concept

**String**

문자열 : 시퀀스 자료형. 문자형data를 메모리에 저장함. 영문 1글자는 1byte

문자열 특징

- 인덱싱 - 개별 오프셋을 가짐
    
    a[-1], a[-5] → a 변수의 오른쪽에서 0번째, 4번째 주소의 값
    
- 슬라이싱
    
    범위를 넘어서면 최대범위를 지정함.
    

```python
#[연습] Yesterday 노래엔 Yesterday가 몇 번 나올까?
#대소문자를 구분하여 “Yesterday”와 “yesterday”는 각각 몇 번 나올까?
f = open('Yesterday.txt', 'r')
all_count = 0
u_count = 0
l_count = 0

while True:
    line = f.readline()
    if not (line):
        break

    u_count += line.count("Yesterday")
    l_count += line.count("yesterday")
    all_count += line.upper().count("YESTERDAY")

print(f"Yesterday 라는 단어는 {all_count}번 나온다.")
print(f"대문자로 시작하는 Yesterday 는 {u_count}번 나온다.")
print(f"소문자로 시작하는 yesterday 는 {l_count}번 나온다.")

f.close()
```

### Function

**call by object reference**

전달된 객체를 참조하여 변경했을 때 영향을 주지만 함수 내에서 같은 이름으로 새로운 객체를 선언하면 기존 연결을 끊고 새로 만들어냄. (약간 move constructor 랑 비슷한 느낌…?)

```python
def spam(eggs):
    eggs.append(1)
    eggs.append(5)
    eggs = [3,4]
    print(eggs)

ham = [0]
spam(ham)
print(ham)

###출력결과
#[3, 4]
#[0, 1, 5]
```

```python
def swap_value(x, y):
    temp = x
    x = y
    y = temp

def swap_offset(offset_x, offset_y):
    temp = list[offset_x]
    list[offset_x] = list[offset_y]
    list[offset_y] = temp

def swap_ref(list, offset_x, offset_y):
    temp = list[offset_x]
    list[offset_x] = list[offset_y]
    list[offset_y] = temp

list = [1,2,3,4,5]
swap_value(list[0], list[4])
print(list)

swap_offset(0, 4)
print(list)

swap_ref(list, 0, 4)
print(list)

# 출력 결과
# [1, 2, 3, 4, 5]
# [5, 2, 3, 4, 1]
# [1, 2, 3, 4, 5]
# 단, ref에서는 원본값을 수정할 가능성이 있으므로 복사해서 사용하는 게 좋음
```

**Scoping Rule**

함수 내에서 전역변수를 사용하고자 할 때에는 global 예약어 사용

```python
def f():
    global s
    s = "l love NCTDREAM"
    print(s)

s = "I like NCTDREAM"
f()
print(s)

# 출력결과
# l love NCTDREAM
# l love NCTDREAM
```

**Recursive Function**

```python
# 일반 loop 팩토리얼 코드
num = 10
fact = 1

for i in range(1, 11):
    fact = fact*i

print(fact) #3628800

#재귀함수 코드
def factorial(n):
    if n == 1:
        return 1

    else :
        return n * factorial(n-1)

print(factorial(num)) #3628800
```

**Function Type Hints**

dynamic typing 이기 때문에 처음 함수를 쓰는 사람은 잘 모를 수 있음.

→ 3.5 이후로는 Type Hints 기능을 제공함!

문서화할 때 정보를 쉽게 파악할 수 있고 시스템의 전체적인 안정성을 확보할 수 있음.

```python
def function(var_name : var_type) -> return type:
	#...

#예시
def hint(name:str) -> str:
	return f"hello, {name}"
```

**Function Docstring**

함수를 만들 때 어떤 기능을 하는지, param, return은 무엇인지 ‘’’(내용)’’’ 적어주는 것 - vscode에 *“Python Docstring Generator”* 가 있음.

**Function Guideline + Python Coding Convention**

- 최대한 간결하게, 이름은 특징이 드러나게
- 함수 하나에는 유사한 역할을 하는 코드만 포함할 것
- 인자로 받은 값을 바꾸지 말 것. 임시변수를 선언해서 사용할 것
- 한 줄은 최대 79자까지!
- 연산자는 1칸 이상 띄우면 안됨.
- 주석은 항상 갱신, 불필요한 주석은 삭제
- 코드의 마지막에는 항상 한 줄 추가
- 소문자 l, 대문자 I, 대문자 O 사용 자제
- flake8 모듈을 사용하여 체크 가능함
