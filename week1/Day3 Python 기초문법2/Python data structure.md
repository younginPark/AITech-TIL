# Python data structure

- **Stack**
- 나중에 넣은 데이터를 먼저 반환하도록 설계된 메모리 구조
- LIFO (Last In First Out)
- 데이터 입력은 push, 출력은 pop
- 리스트를 사용하여 스택 구현 가능 (push: append(), pop: pop())
- **Queue**
- 먼저 넣은 데이터를 먼저 반환하도록 설계된 메모리 구조
- FIFO (First In First Out)
- 리스트 활용하여 큐 구현 가능 (push: append(), pop:pop(0))
- **Tuple**
- 값의 변경이 불가능한 리스트
- 선언 시 "[]" 가 아닌 "()"를 사용
- 리스트의 연산, 인덱싱, 슬라이싱 등을 동일하게 사용
- 값이 변경되지 않음
- 함수의 반환 값 등에 사용되며 사용자의 실수에 의한 에러 사전 방지 가능
- 선언 시   t = (1, )   쉼표 붙여야 함 t = (1)로 하게 되면 일반 정수로 인식
- **Set**
- 집합으로 값을 순서 없이 저장, 중복 불허
- 수학에서 활용하는 다양한 집합연산 가능 (합집합: union |, 교집합: intersection &, 차집합: difference -)
- **Dict (Hash Table)**
- Key, Value를 활용하여 데이터를 저장할 때 구분 지을 수 있게 함
- Key와 Value를 매칭하여 Key로 Value를 검색
- 함수
데이터 출력: dict_ex.items()  → tuple 형태로 읽기만 가능
key 값만 출력: dict_ex.keys()
value 값만 출력: dict_ex.values()
- for k, v in country_code.items():  → k, v로 언패킹 가능
- **Collections**
- List, Tuple, Dict에 대한 Python Built-in 확장 자료 구조(모듈)
- 편의성, 실행 효율 등을 사용자에게 제공
- Deque, OrderDict, defaultdict, Counter,namedtuple
- **Deque**
- from collections import deque
- Stack과 Queue를 지원하는 모듈
- List에 비해 빠르게 자료 저장 방식을 지원하여 효율적 → 처리 속도 향상
- rotate, reverse 등 Linked List의 특성을 지원 (실제로 양방향 링크드 리스트로 구현되어 있음)
- 메모리가 차례대로 이어지는 구조가 아니라 하나가 다음 데이터가 있는 메모리 공간을 가리킴
- 함수
deque_list.rotate(2)  →  회전
deque_list.extend([5, 6, 7])  → 뒤에 이어 붙음
deque_list.extendleft([5, 6, 7])  → 앞에 7, 6, 5 순으로 붙음
- **OrderDict**
- from collections import OrderDict
- Dict와 달리, 데이터를 입력한 순서대로 dict를 반환 (3.6부터는 Dict가 입력 순서 보장해서 안씀)
- **Defaultdict**
- from collections import defaultdict
- Dict type의 값에 기본 값을 지정, 신규값 생성시 사용하는 방법
- 예시
d = defaultdict(object)
d = defaultdict(lambda: 0) → default 값을 0을 설정
print(d["first"]) → Key 값이 없어도 에러 대신 default 값을 출력
- 하나의 지문에 각 단어들이 몇개나 있는지 세고 싶을 때 유용
- **Counter**
-  from collections import Counter
- 시퀀스 타입의 데이터 요소들의 갯수를 dict 형태로 반환
- 예시
c = Counter('abcc')
c → Counter({'a': 1, 'b': 1, 'c': 2})
- 리스트 형태로 반환도 해줌
c = Counter(cats = 2, dogs = 1)
print(list(c.elements()))  →  ['cats', 'cats', 'dogs']
- Set의 연산들 지원 (합집합: union |, 교집합: intersection &, 차집합: difference -)
- **Namedtuple**
-  from collections import namedTuple
- Tuple 형태로 Data 구조체 저장: 데이터의 기본적인 체계를 하나로 묶어주는 장점 O
- 예시
Point = namedtuple('Point', ['x', 'y'])
p = Point(x = 11, y = 22)
print(p[0] + p[1])  →  33
x, y = p  →  언패킹 가능