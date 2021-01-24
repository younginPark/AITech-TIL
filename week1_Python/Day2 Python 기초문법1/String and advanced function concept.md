# String and advanced function concept

## String

- 시퀀즈 자료형으로 문자형 data를 메모리에 저장
- 영문자 한 글자는 1byte 메모리 공간을 사용
- 1 byte = 8 bit = 2^8 = 256 = 0~255
- 컴퓨터는 문자를 직접적으로 인식 X → 모든 데이터는 2진수로 인식
- 이를 위해 2진수를 문자로 변환하는 표준 규칙(한글은 UTF-8)을 정함
- 인덱싱 가능
- 문자열의 각 문자는 개별 주소(offset)를 가짐
- 함수
- [https://www.w3schools.com/python/python_ref_string.asp](https://www.w3schools.com/python/python_ref_string.asp)

## Function2

- Call by Value
- 함수에 인자를 넘길 때 값만 넘김
- 함수 내에 인자 값 변경 시, 호출자에게 영향을 주지 않음
- Call by Reference
- 함수에 인자를 넘길 때 메모리 주소를 넘김(포인터)
- 함수 내에 인자 값 변겨 시, 호출자의 값도 변경됨
- Call by Object Reference (파이썬!!!)
- 객체의 주소가 함수로 전달되는 방식
- 전달된 객체를 참조하여 변경 시 호출자에게 영향을 주나, 
  새로운 객체를 만들 경우 호출자에게 영향 주지 X

![String%20and%20advanced%20function%20concept%20eec165cbb988435c8211b63c87be31ae/Untitled.png](String%20and%20advanced%20function%20concept%20eec165cbb988435c8211b63c87be31ae/Untitled.png)

- 변수의 범위
- 지역 변수: 함수내에서만 사용
- 전역 변수: 프로그램 전체에서 사용
- 전역 변수는 함수내에서 사용가능하지만 함수 내에 전역 변수와 같은 이름의 변수를 선언하면 새로운 지역 변수 생김
- 함수 내에서 전역변수 사용 시 global 키워드 사용
- 재귀함수
- 자기 자신을 호출하는 함수
- 재귀 종료 조건 존재, 종료 조건까지 함수 호출 반복
- function type hints
- 파이썬의 가장 큰 특징인 dynamic typing
→ 처음 함수를 사용하는 사용자들은 interface 알기 어렵다는 단점 존재
그래서 type hints 제공
ex) def type_hint_example(name: str) → str: 
- 함수의 문서화시 parameter에 대한 정보를 명확히 알 수 있음
- docstring
- 파이썬 함수에 대한 상세 스펙을 사전에 작성 → 함수 사용자의 이행도 UP
- 세개의 따옴표로 docstring 영역 표시
- vscode의 경우 플러그인 설치하여 편하게 사용 가능
- 함수 가이드 라인
- 가능하면 짧게 작성
- 이름에 함수의 역할, 의도 명확하게
- 유사한 역할을 하는 코드만 포함
- 인자로 받은 값 자체를 바꾸지 말고 복사 형태 사용
- 복잡한 수식, 복잡한 조건 → 식별 가능한 이름의 함수로 변환

## Python coding convention

- 일관성
- 들여쓰기는 Tab or 4 Space (혼합 금지)
- 연산자는 1칸 이상 안띄움
- 주석 항상 개신, 불필요한 주석은 삭제
- 코드의 마지막에는 항상 한 줄 추가
- 소문자 l, 대문자 O, 대문자 I 금지
- 함수명은 소문자로 구성, 필요하면 밑줄로 나눔
- flake8 모듈로 체크하고 black으로 수정 가능