
## 기초문법II

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

<img width="1021" alt="스크린샷 2022-06-28 오후 6 37 01" src="https://user-images.githubusercontent.com/54930076/176151249-49609412-2ebb-47a2-b989-86ea9c15b58d.png">

`Deque` : 스택과 큐를 모두 지원. List에 비해 효율적인 자료저장 방식을 지원
