# Pythonic code

파이썬 특유의 문법을 활용하여 파이썬 스타일로 효율적인 코드 표현 (요즘엔 많은 언어들의 장점 채용)

- **split**
- string type의 값을 '기준값'으로 나눠서 List 형태로 변환
- 예시
name = "Park Young In".split()
name → ["Park", "Young", "In"]
- 언패킹도 가능
- **join**
- string으로 구성된 list를 합쳐 하나의 string으로 변환
- 예시
name = ["Park", "Young", "In"]
result = ''.join(name)   →   "ParkYoungIn"
- **list comprehension**
- 기존의 List를 사용하여 간단히 다른 List를 만드는 기법
- 일반적으로 for + append 보다 속도가 빠름
- 예시

![Pythonic%20code%20b9844617465248579a64f14f3b5b99dc/Untitled.png](Pythonic%20code%20b9844617465248579a64f14f3b5b99dc/Untitled.png)

![Pythonic%20code%20b9844617465248579a64f14f3b5b99dc/Untitled%201.png](Pythonic%20code%20b9844617465248579a64f14f3b5b99dc/Untitled%201.png)

![Pythonic%20code%20b9844617465248579a64f14f3b5b99dc/Untitled%202.png](Pythonic%20code%20b9844617465248579a64f14f3b5b99dc/Untitled%202.png)

![Pythonic%20code%20b9844617465248579a64f14f3b5b99dc/Untitled%203.png](Pythonic%20code%20b9844617465248579a64f14f3b5b99dc/Untitled%203.png)

![Pythonic%20code%20b9844617465248579a64f14f3b5b99dc/Untitled%204.png](Pythonic%20code%20b9844617465248579a64f14f3b5b99dc/Untitled%204.png)

- **Enumerate**
- list의 element를 추출할 때 번호를 붙여서 추출
- 예시
for i, v in enumerate(['one', 'two']):
    print(i, v)   →   0, 'one'   /   1, 'two'
- **Zip**
- 두 개의 list의 값을 병렬적으로 추출
- 예시
alist = ['one', 'two']
blist = ['1', '2']
for a, b in zip(alist, blist):
    print(a, b)   →   'one' '1'   /   'two' '2'
- **Lambda function (권장X)**
- 함수 이름 없이, 함수처럼 쓸 수 있는 익명함수
- Python3 부터는 권장 X (어려운 문법, 테스트 어려움, 문서화 docstring 지원 미비.. 그래도 많이 씀)
- 비교 예시

![Pythonic%20code%20b9844617465248579a64f14f3b5b99dc/Untitled%205.png](Pythonic%20code%20b9844617465248579a64f14f3b5b99dc/Untitled%205.png)

- **Map function**
- 두 개 이상의 list에도 적용 가능함, if filter도 사용 가능
- 예시
result = map(함수이름, 인자)
print(next(result))   →  python3는 iteration을 생성하므로 list를 붙여줘야 list 사용 가능
- **Reduce function (권장X)**
- map function과 달리 list에 똑같은 함수를 적용해서 통합
- 예시
from functools import reduce
print(reduce(lambda x, y: x+y, [1, 2, 3, 4, 5]))
→ 1+2
→ (1+2) + 3
→ ((1+2) + 3) + 4
→ (((1+2) + 3) + 4) + 5
⇒ 15 출력
- **iterable object**
- 시퀀스형 자료형에서 데이터를 순서대로 추출하는 object
- iter(), next() 함수로 iterable 객체를 iterator object로 사용
- 예시
cities = ["Seoul", "Busan", "Jeju"]
iter_obj = iter(cities)   →   cities의 메모리 주소만 가질 뿐 모든 정보 생성X
print(next(iter_obj))   →    Seoul
print(next(iter_obj))   →    Busan
print(next(iter_obj))   →    Jeju
- **Generator (권장!!)**
- iterator object를 특수한 형태로 사용해주는 함수
- element가 사용되는 시점에 값을 메모리에 반환 (yield를 사용해 한번에 하나의 element만 반환)
- 값을 메모리에 올려놓지 않고 주소만 갖고 있다가 print해야하니 값 주세요~ 하면 값을 던져줌 
⇒ 메모리 주소 절약 가능, 데이터가 클 때 더욱 유리
- generator comprehension == generator expression
- [] 대신 ()를 사용하여 표현
- 기존과 비교 예시

![Pythonic%20code%20b9844617465248579a64f14f3b5b99dc/Untitled%206.png](Pythonic%20code%20b9844617465248579a64f14f3b5b99dc/Untitled%206.png)

## Function passing arguments

1) **Keyword arguments** : 함수에 입력되는 parameter의 변수명을 사용하여 arguments 넘김

- 순서 맞추지 않아도 parameter 변수에 들어감

![Pythonic%20code%20b9844617465248579a64f14f3b5b99dc/Untitled%207.png](Pythonic%20code%20b9844617465248579a64f14f3b5b99dc/Untitled%207.png)

2) **Default arguments: parameter**의 기본 값을 사용하여 인자 없을 경우 기본값 출력

- 인자 없으면 default 값인 TEAMLAB 들어감

![Pythonic%20code%20b9844617465248579a64f14f3b5b99dc/Untitled%208.png](Pythonic%20code%20b9844617465248579a64f14f3b5b99dc/Untitled%208.png)

 

3) **Variable-length arguments**

- 개수가 정해지지 않은 변수를 함수의 parameter로 사용하는 법
- Asterisk(*) 기호를 사용하여 함수의 parameter를 표시함
- * 는 가변인자
- **는 키워드 가변인자
- Keyword arguments와 함께, argument 추가가 가능
- 입력된 값은 tuple type으로 사용 가능
- 가변인자는 오진 한개만! 맨 마지막! parameter 위치에 사용 가능

![Pythonic%20code%20b9844617465248579a64f14f3b5b99dc/Untitled%209.png](Pythonic%20code%20b9844617465248579a64f14f3b5b99dc/Untitled%209.png)

![Pythonic%20code%20b9844617465248579a64f14f3b5b99dc/Untitled%2010.png](Pythonic%20code%20b9844617465248579a64f14f3b5b99dc/Untitled%2010.png)

![Pythonic%20code%20b9844617465248579a64f14f3b5b99dc/Untitled%2011.png](Pythonic%20code%20b9844617465248579a64f14f3b5b99dc/Untitled%2011.png)

- **asterisk - unpaking container**
- tuple, dict 등 자료형에 들어가 있는 값을 unpacking

![Pythonic%20code%20b9844617465248579a64f14f3b5b99dc/Untitled%2012.png](Pythonic%20code%20b9844617465248579a64f14f3b5b99dc/Untitled%2012.png)

![Pythonic%20code%20b9844617465248579a64f14f3b5b99dc/Untitled%2013.png](Pythonic%20code%20b9844617465248579a64f14f3b5b99dc/Untitled%2013.png)