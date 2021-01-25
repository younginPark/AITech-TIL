# Day4 Python OOP와 모듈

## Python Object-Oriented Programming

### OOP란?

- 객체: 실생활에서 일종의 물건의 속성(Attribute)와 행동(Action)을 가짐
- 속성은 변수(variable), 행동은 함수(method)로 표현됨
- OOP는 이러한 객체 개념을 프로그램으로 표현
- 파이썬은 객체 지향 프로그램 언어
- OOP는 설계도에 해당하는 클래스 (class)와 실제 구현체인 인스턴스 (instance) 로 나눔
- class 선언, object는 python3에서 자동 상속
    - __ 는 특수한 예약 함수나 변수 그리고 함수명 변경(맨글링)으로 사용
    - 예) "__main__", "__add__", "__str__". "__eq__"

    ![Day4%20Python%20OOP%E1%84%8B%E1%85%AA%20%E1%84%86%E1%85%A9%E1%84%83%E1%85%B2%E1%86%AF%20832766e9f9a14dd6a3dd3794e2514eab/Untitled.png](Day4%20Python%20OOP%E1%84%8B%E1%85%AA%20%E1%84%86%E1%85%A9%E1%84%83%E1%85%B2%E1%86%AF%20832766e9f9a14dd6a3dd3794e2514eab/Untitled.png)

- method(Action) 추가는 기존 함수와 같으나, 반드시 self를 추가해야만 class 함수로 인정됨

    (self는 생성된 인스턴스 자신)

![Day4%20Python%20OOP%E1%84%8B%E1%85%AA%20%E1%84%86%E1%85%A9%E1%84%83%E1%85%B2%E1%86%AF%20832766e9f9a14dd6a3dd3794e2514eab/Untitled%201.png](Day4%20Python%20OOP%E1%84%8B%E1%85%AA%20%E1%84%86%E1%85%A9%E1%84%83%E1%85%B2%E1%86%AF%20832766e9f9a14dd6a3dd3794e2514eab/Untitled%201.png)

### OOP에서 필요한 것들

- Inheritance 상속
    - 부모클래스로부터 속성과 Method를 물려받은 자식 클래스로 생성하는 것

    ![Day4%20Python%20OOP%E1%84%8B%E1%85%AA%20%E1%84%86%E1%85%A9%E1%84%83%E1%85%B2%E1%86%AF%20832766e9f9a14dd6a3dd3794e2514eab/Untitled%202.png](Day4%20Python%20OOP%E1%84%8B%E1%85%AA%20%E1%84%86%E1%85%A9%E1%84%83%E1%85%B2%E1%86%AF%20832766e9f9a14dd6a3dd3794e2514eab/Untitled%202.png)

    - super()는 부모의 함수과 똑같은 자식의 함수가 오버라이딩된 상황에서 부모의 함수를 호출하고 싶을 때 사용된다.

    ![Day4%20Python%20OOP%E1%84%8B%E1%85%AA%20%E1%84%86%E1%85%A9%E1%84%83%E1%85%B2%E1%86%AF%20832766e9f9a14dd6a3dd3794e2514eab/Untitled%203.png](Day4%20Python%20OOP%E1%84%8B%E1%85%AA%20%E1%84%86%E1%85%A9%E1%84%83%E1%85%B2%E1%86%AF%20832766e9f9a14dd6a3dd3794e2514eab/Untitled%203.png)

- Polymorphism 다형성
    - 같은 이름 메소드의 내부 로직을 다르게 작성

    → 개념적으로는 같은데 세부적으로 다른 일을 할 때 사용함

    ![Day4%20Python%20OOP%E1%84%8B%E1%85%AA%20%E1%84%86%E1%85%A9%E1%84%83%E1%85%B2%E1%86%AF%20832766e9f9a14dd6a3dd3794e2514eab/Untitled%204.png](Day4%20Python%20OOP%E1%84%8B%E1%85%AA%20%E1%84%86%E1%85%A9%E1%84%83%E1%85%B2%E1%86%AF%20832766e9f9a14dd6a3dd3794e2514eab/Untitled%204.png)

- Visibility 가시성
    - 객체의 정보를 볼 수 있는 레벨 조절
    - 누구나 객체 안에 모든 변수를 볼 필요가 없음
    - __를 사용하여 private변수로 선언

        ![Day4%20Python%20OOP%E1%84%8B%E1%85%AA%20%E1%84%86%E1%85%A9%E1%84%83%E1%85%B2%E1%86%AF%20832766e9f9a14dd6a3dd3794e2514eab/Untitled%205.png](Day4%20Python%20OOP%E1%84%8B%E1%85%AA%20%E1%84%86%E1%85%A9%E1%84%83%E1%85%B2%E1%86%AF%20832766e9f9a14dd6a3dd3794e2514eab/Untitled%205.png)

    - Private이지만 접근해야 할 때

        → 외부에서는 __items 접근 안되지만 내부에서 접근해서 반환하는 방식으로 구현

        ![Day4%20Python%20OOP%E1%84%8B%E1%85%AA%20%E1%84%86%E1%85%A9%E1%84%83%E1%85%B2%E1%86%AF%20832766e9f9a14dd6a3dd3794e2514eab/Untitled%206.png](Day4%20Python%20OOP%E1%84%8B%E1%85%AA%20%E1%84%86%E1%85%A9%E1%84%83%E1%85%B2%E1%86%AF%20832766e9f9a14dd6a3dd3794e2514eab/Untitled%206.png)

### Decorate

- First-class objects
    - 일등함수 또는 일급 객체
    - 변수나 데이터 구조에 할당이 가능한 객체
    - 파라메터로 전달이 가능 + 리턴 값으로 사용 ex) map(f, ex)
    - 파이썬의 함수는 일급함수

![Day4%20Python%20OOP%E1%84%8B%E1%85%AA%20%E1%84%86%E1%85%A9%E1%84%83%E1%85%B2%E1%86%AF%20832766e9f9a14dd6a3dd3794e2514eab/Untitled%207.png](Day4%20Python%20OOP%E1%84%8B%E1%85%AA%20%E1%84%86%E1%85%A9%E1%84%83%E1%85%B2%E1%86%AF%20832766e9f9a14dd6a3dd3794e2514eab/Untitled%207.png)

- Inner function 함수 내에 또 다른 함수 존재

![Day4%20Python%20OOP%E1%84%8B%E1%85%AA%20%E1%84%86%E1%85%A9%E1%84%83%E1%85%B2%E1%86%AF%20832766e9f9a14dd6a3dd3794e2514eab/Untitled%208.png](Day4%20Python%20OOP%E1%84%8B%E1%85%AA%20%E1%84%86%E1%85%A9%E1%84%83%E1%85%B2%E1%86%AF%20832766e9f9a14dd6a3dd3794e2514eab/Untitled%208.png)

- closures : inner function을 return 값으로 반환

![Day4%20Python%20OOP%E1%84%8B%E1%85%AA%20%E1%84%86%E1%85%A9%E1%84%83%E1%85%B2%E1%86%AF%20832766e9f9a14dd6a3dd3794e2514eab/Untitled%209.png](Day4%20Python%20OOP%E1%84%8B%E1%85%AA%20%E1%84%86%E1%85%A9%E1%84%83%E1%85%B2%E1%86%AF%20832766e9f9a14dd6a3dd3794e2514eab/Untitled%209.png)

- decorator function
    - 복잡한 클로져 함수를 간단하게

    ![Day4%20Python%20OOP%E1%84%8B%E1%85%AA%20%E1%84%86%E1%85%A9%E1%84%83%E1%85%B2%E1%86%AF%20832766e9f9a14dd6a3dd3794e2514eab/Untitled%2010.png](Day4%20Python%20OOP%E1%84%8B%E1%85%AA%20%E1%84%86%E1%85%A9%E1%84%83%E1%85%B2%E1%86%AF%20832766e9f9a14dd6a3dd3794e2514eab/Untitled%2010.png)

    ---

    ## Module and Project

    - 객체 < 모듈 < 패키지
    - 모듈
        - 프로그램에서 작은 프로그램 조각들
        - 모듈들을 모아서 하나의 큰 프로그램 개발
        - Module == py파일
        - import 문을 사용해서 module 호출

            ![Day4%20Python%20OOP%E1%84%8B%E1%85%AA%20%E1%84%86%E1%85%A9%E1%84%83%E1%85%B2%E1%86%AF%20832766e9f9a14dd6a3dd3794e2514eab/Untitled%2011.png](Day4%20Python%20OOP%E1%84%8B%E1%85%AA%20%E1%84%86%E1%85%A9%E1%84%83%E1%85%B2%E1%86%AF%20832766e9f9a14dd6a3dd3794e2514eab/Untitled%2011.png)

    - 패키지
        - 모듈을 모아놓은 단위, 하나의 프로그램
        - 다양한 모듈들의 합, 폴더로 연결됨
        - "__init__", "__main__" 등 키워드 파일명이 사용됨

        ![Day4%20Python%20OOP%E1%84%8B%E1%85%AA%20%E1%84%86%E1%85%A9%E1%84%83%E1%85%B2%E1%86%AF%20832766e9f9a14dd6a3dd3794e2514eab/Untitled%2012.png](Day4%20Python%20OOP%E1%84%8B%E1%85%AA%20%E1%84%86%E1%85%A9%E1%84%83%E1%85%B2%E1%86%AF%20832766e9f9a14dd6a3dd3794e2514eab/Untitled%2012.png)

    - 네임스페이스
        - 모듈을 호출할 때 범위 정하는 방법
        - 모듈 안에는 함수와 클래스 등이 존재 가능
        - 필요한 내용만 골라서 호출 할 수 있음
        - from과 import 키워드 사용

        ![Day4%20Python%20OOP%E1%84%8B%E1%85%AA%20%E1%84%86%E1%85%A9%E1%84%83%E1%85%B2%E1%86%AF%20832766e9f9a14dd6a3dd3794e2514eab/Untitled%2013.png](Day4%20Python%20OOP%E1%84%8B%E1%85%AA%20%E1%84%86%E1%85%A9%E1%84%83%E1%85%B2%E1%86%AF%20832766e9f9a14dd6a3dd3794e2514eab/Untitled%2013.png)

## 가상환경 설정하기

- conda 사용하여 프로젝트 진행 시 필요한 패키지만 설치하여 관리