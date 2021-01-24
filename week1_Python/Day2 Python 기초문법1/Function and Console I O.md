# Function and Console I/O

## Function

- 어떤 일을 수행하는 코드의 덩어리
- 메모리에 올라감 (그래서 코드 상단에 적어줘야 함)
- 반복적인 수행을 1회만 작성 후 호출
- 코드를 논리적인 단위로 분리
- 캡슐화: 인터페이스만 알면 타인의 코드 사용
- Parameter VS Argument
- Parameter: 함수의 입력 값 인터페이스 
   def f(**x**):
        ~~~~
- Argument: 실제 Parameter에 대입된 값
   print(f(**2**))
- Parameter 유무, 반환 값 유무에 따라 함수의 형태가 다름
sorted(list_ex)는 list_ex가 sorting 된 값을 return 하는거지 list_ex가 sort되는거 X
sort 하고 싶으면 list_ex.sort()

## Console I/O

- 입력: input()
- 출력: print()
- print formatting
- f-string:
   name = "Youngin"
   age = 5
   print(f"Hello, {name}. You are {age}.")
   print(f"{name:20}")  #왼쪽 정렬이 기본
   print(f"{name:>20}") #오른쪽으로 붙어 있음
- %-format
   print("%8.2f " % 59.058)) #소수점을 포함하여 8자리로 표현하고 소수점은 2자리까지 표시해라
   .....59.06