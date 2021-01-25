# Day5 Python으로 데이터 다루기

## Exception

- Exception Handling
    - 예외가 발생할 경우 후속 조치 등 대체 필요
    - try ~ except 문법

        ```python
        try:
        	예외 발생 가능 코드
        except <Exception Type>:
        	예외 발생시 대응하는 코드
        else:
        	예외가 발생하지 않을 때 동작하는 코드 # 추천X
        ```

        (if 문은 예외가 아닌 로직적인 문제를 다룰 때 처리)

    - 0으로 숫자를 나눌 때 예외처리 하기

        ```python
        for i in range(10):
        	try:
        		print(10 / i)
        	except ZeroDivisionError: # 빌트 인 에러
        		print("Not divided by 0")
        	except exception as e: # 다른 사용자가 어디서 에러났는지 정확히 파악하기 어려움
        		print(e) # 어떤 에러인지 찍어줌
        ```

    - Build-in Exception: 기본적으로 제공하는 예외
        - IndexError: List의 Index 범위를 넘어갈 때
        - NameError: 존재하지 않은 변수를 호출 할 때
        - ZeroDivisionError: 0으로 숫자를 나눌 때
        - ValueError: 변환할 수 없는 문자/숫자를 변환할 때
        - FileNotFoundError: 존재하지 않는 파일을 호출할 때
    - try~except~finally

        ```python
        try:
        	예외 발생 가능 코드
        except <Exception Type>:
        	예외 발생시 대응하는 코드
        finally:
        	예외 발생 여부와 상관없이 실행됨
        ```

    - raise 구문
        - 필요에 따라 강제로 Exception을 발생
        - raise <Exception Type>(예외정보)  # 코드 중간에 멈출 수 있음
    - assert 구문
        - 특정 조건에 만족하지 않을 경우 예외 발생
        - assert 예외조건 # True or False 로 나와서 False면 코드 멈춤

    ## File Handling

    - File system, 파일 시스템
        - os에서 파일을 저장하는 트리구조 저장 체계
        - 파일의 종류는 Bianry 파일, Text 파일

            ![Day5%20Python%E1%84%8B%E1%85%B3%E1%84%85%E1%85%A9%20%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%84%90%E1%85%A5%20%E1%84%83%E1%85%A1%E1%84%85%E1%85%AE%E1%84%80%E1%85%B5%2082e033bc0301436f8ca4351f4884a5df/Untitled.png](Day5%20Python%E1%84%8B%E1%85%B3%E1%84%85%E1%85%A9%20%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%84%90%E1%85%A5%20%E1%84%83%E1%85%A1%E1%84%85%E1%85%AE%E1%84%80%E1%85%B5%2082e033bc0301436f8ca4351f4884a5df/Untitled.png)

    - File I/O

        파이썬은 파일 처리를 위해 "open" 키워드 사용

        ```python
        f = open("<파일이름>", "접근 모드") # r:읽기모드, w:쓰기모드, a:추가모드
        f.close()
        ```

    - File Read

        ```python
        # read() txt 파일 안에 있는 내용을 문자열로 반환
        f = open("i_hava_a_dream.txt", "r") # r을 하면 파일ㅇ르 읽어올 수 있도록 주소전환
        contents = f.read()
        print(contents)
        f.close

        # with 구문과 함께 사용하기 read
        with open("i_have_a_dream.txt", "r") as my_file:
        	content = my_file.read() # 인덴테이션 일어나는 순간에 적용됨 => 별도의 close 필요X
        	print(type(contents), contents)

        # with 구문과 함께 사용하기 readlines
        with open("i_have_a_dream.txt", "r") as my_file:
        	content_list = my_file.readlines() # 한줄씩 읽어서 list에 저장
        	print(type(content_list))
        	print(content_list)
        ```

    - File Write

        파일을 새로 만들어서 적음

        ```python
        f = open("count_log.txt", 'w', encoding="utf8") #컴퓨터에 문자 저장할 때 어떤 형식으로 할지
        for i in range(1, 11):
        	data = "%d번째 줄입니다.\n" % i
        	f.write(data) 
        f.close()
        ```

    - File append

        추가

        ```python
        with open("count_log.txt", 'a', encoding="utf8") as f:
        	for i in range(1, 11):
        		data = "%d번째 줄입니다.\n" % i 
        		f.write(data)
        ```

    - directory 다루기

        ```python
        import os
        os.mkdir("log") # 폴더 만듦

        if not os.path.isdir("log"): # 디렉토리가 있는지 확인 (exists도 사용 가능)
        	os.mkdir("log")
        ```

        ```python
        import shutill

        source = "i_hava_a_dream.txt"
        dest = os.path.join("abc", "sungchul.txt")
        shutill.copy(source, dest) # 파일 복사 함수
        ```

        ```python
        >>> import pathlib
        >>>
        >>> cwd = pathlib.Path.cwd() # Current Working Directory
        >>> cwd
        WindowsPath('D:/workspace') 
        >>> cwd.parent # 뒤에 빠짐 (상위 디렉토리만 남음)
        WindowsPath('D:/')
        >>> list(cwd.parents)
        [WindowsPath('D:/')]
        >>> list(cwd.glob("*"))
        [WindowsPath('D:/workspace/ai-pnpp'), WindowsPath('D:/workspace/cs50_auto_grader'), WindowsPath('D:/workspace/data-academy'), WindowsPath('D:/workspace/DSME-AI-Smart- Yard'), WindowsPath('D:/workspace/introduction_to_python_TEAMLAB_MOOC'),
        ```

    - Pickle
        - 파이썬의 객체를 영속화하는 built-in 객체

            객체는 메모리에 존재하고 Python Interpreter가 끝나면 메모리 종료되면서 객체도 사라짐

        - 데이터, object 등 실행 중 정보를 저장 → 불러와서 사용
        - 저장해야하는 정보, 계산 결과(모델)등 활용이 많음

        ```python
        import pickle

        f = open("list.pickle", "wb") # wb의 b는 binary
        test = [1, 2, 3, 4, 5] 
        pickle.dump(test, f) # test라는 객체를 f에 저장해라
        f.close() # 만약 del test해도 list.pickle에 이미 저장됨

        f = open("list.pickle", "rb") 
        test_pickle = pickle.load(f) # 저장해둔 f 불러옴
        print(test_pickle)
        f.close()
        ```

## Logging Handling

- Logging
    - 프로그램이 실행되는 동안 일어나는 정보를 기록
    - 유저의 접근, 프로그램의 Exception, 특정 함수의 사용
    - Console 화면에 출력, 파일에 남기기, DB에 남기기
    - 기록된 로그를 분석하여 의미있는 결과를 도출 할 수 있음
    - 실행시점에 남겨야 하는 기록 (유저 분석), 개발시점에 남겨야하는 기록 (에러 사전에 잡기 위해)
- Logging 모듈
    - 프로그램 진행 상황에 따라 다른 Level의 Log를 출력함
    - 파이썬의 기본 로깅 레벨은 warning 부터

    ```python
    import logging

    logging.debug("틀렸잖아!") # 개발 시점 
    logging.info("확인해") # 운영자 시점
    logging.warning("조심해!") # 운영자 시점
    logging.error("에러났어!!!") # 사용자 시점
    logging.critical ("망했다...") # 사용자 시점
    ```

    ```python
    import logging

    logger = logging.getLogger("main") # Logger 선언
    stream_hander = logging.StreamHandler() # Logger의 output 방법 선언
    logger.addHandler(stream_hander) # Logger의 output 등록

    logging.basicconfig(level=logging.DEBUG)
    logger.setLevel(logging.DEBUG) # 레벨 정하기
    logger.debug("틀렸잖아!") 
    logger.info("확인해") 
    logger.warning("조심해!") 
    logger.error("에러났어!!!") 
    logger.critical("망했다...")
    ```

## Configparser, Argparser

- configparser
    - 프로그램의 실행 설정을 file에 저장
    - Section, Key, Value 값의 형태로 설정된 설정 파일을 사용
    - 설정파일을 Dict Type으로 호출 후 사용

    [Section name]

    Status: Single (속성-Key: Value)

- argparser
    - Console 창에서 프로그램 실행 시 setting 정보를 저장함
    - Command-Line Option 이라고 부름

    ![Day5%20Python%E1%84%8B%E1%85%B3%E1%84%85%E1%85%A9%20%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%84%90%E1%85%A5%20%E1%84%83%E1%85%A1%E1%84%85%E1%85%AE%E1%84%80%E1%85%B5%2082e033bc0301436f8ca4351f4884a5df/Untitled%201.png](Day5%20Python%E1%84%8B%E1%85%B3%E1%84%85%E1%85%A9%20%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%84%90%E1%85%A5%20%E1%84%83%E1%85%A1%E1%84%85%E1%85%AE%E1%84%80%E1%85%B5%2082e033bc0301436f8ca4351f4884a5df/Untitled%201.png)

- Logging formatter
    - Log의 결과값의 format을 지정해 줄 수 있음

        formatter = logging.Formatter('%(asctime)s %(levelname)s %(process)d %(message)s')

                                                              날짜                   레벨                   PId

## CSV

- 필드를 쉼표 , 로 구분한 텍스트 파일 (탭, 빈칸도 가능)
- 엑셀 양식의 데이터를 프로그램에 상관없이 쓰기 위한 데이터 형식
- Text 파일 형태로 데이터 처리시 문장 내에 있는 , 에 대해 전처리 과정 필요
- 파이썬으로 CSV 파일 읽기/쓰기
    - 일반적으로 textfile을 처리하듯 파일을 읽어온 후, 한 줄 한 줄씩 데이터를 처리함

    ```python
    line_counter = 0 # 파일의 총 줄수를 세는 변수 
    data_header = [] # data의 필드값을 저장하는 
    list customer_list = [] # cutomer 개별 List를 저장하는 List

    with open ("customers.csv") as customer_data: #customer.csv 파일을 customer_data 객체에 저장
    	
    	while True:
    		data = customer_data.readline() # customer.csv에 한줄씩 data 변수에 저장 
    		if not data: break # 데이터가 없을 때, Loop 종료
    		if line_counter==0: # 첫번째 데이터는 데이터의 필드
    			data_header = data.split(",") # 데이터의 필드는 data_header List에 저장, 데이터 저장시 “,”로 분리 
    		else:
    			customer_list.append(data.split(",")) # 일반 데이터는 customer_list 객체에 저장, 데이터 저장시 “,”로 분리 
    		line_counter += 1

    print("Header :\t", data_header) # 데이터 필드 값 출력 
    for i in range(0,10): # 데이터 출력 (샘플 10개만)
    	print ("Data",i,":\t\t",customer_list[i])
    print (len(customer_list)) # 전체 데이터 크기 출력
    ```

    - CSV 객체 활용

    ```python
    import csv
    reader = csv.reader(f,
    										delimiter=',', 
    										quotechar='"', # " 로 되어있으면 하나의 캐릭터로 보기  ,로 나누지X
    										quoting=csv.QUOTE_ALL)
    ```

## Web

- World Wide Web
- HTML 페이지 생성에 규칙이 있어서 규칙을 분석하여 데이터의 추출 가능
- 정규식 (regular expression)
    - 복잡한 문자열 패턴을 정의하는 문자 표현 공식
    - 인터넷에 필요할 때마다 찾아서 공부
    - 010-0000-0000 ^\d{3}\-\d{4}\-\d{4}$
    - 203.252.101.40 ^\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3}$
- re 모듈
    - 함수
        - search - 한 개만 찾기
        - findall - 전체 찾기
    - 추출된 패턴은 tuple로 반환
    - ID 패턴: [영문대소문자|숫자] 여러 개, 별표로 끝남

        "([A-Za-z0-9]+\*\*\*)“ 정규식

    ```python
    import re
    import urllib.request
    url = "https://bit.ly/3rxQFS4"

    html = urllib.request.urlopen(url)
    html_contents = str(html.read())
    id_results = re.findall(r"([A-Za-z0-9]+\*\*\*)", html_contents) 
    #findall 전체 찾기, 패턴대로 데이터 찾기

    for result in id_results: 
    	print (result) 
    ```

## XML

- 데이터의 구조와 의미를 설명 (스키마, DTD)
- TAG와 TAG 사이에 값이 표시되고, 구조적인 정보를 표현할 수 있음
- 정규표현식으로 Parsing 가능
- 유명 parser: beautifulsoup

    ```python
    # 모듈 호출
    from bs4 import BeautifulSoup

    # 객체 생성
    soup = BeautifulSoup(books_xml, "lxml")

    # Tag 찾는 함수 find_all 생성
    soup.find_all("author")
    ```

    - find_all : 정규식과 마찬가지로 해당 패턴을 모두 반환
    - get_text(): 반환된 패턴의 값 반환 (태그와 태그 사이)

## JSON

- JavaScript Object Notation
- JavaScript의 데이터 객체 표현 방식
- 간결, 데이터 용량 적고 code로의 전환이 쉬움
- dict 타입으로 상호 호환 가능
- json 파일의 구조를 확인 → 로드 → Dict Type 처럼 처리

    ```python
    {"employees":
    	[{"firstName":"John", "lastName":"Doe"}, 
    	{"firstName":"Anna", "lastName":"Smith"}, 
    	{"firstName":"Peter", "lastName":"Jones"}
    ]}

    import json

    with open("json_example.json", "r", encoding="utf8") as f: 
    	contents = f.read()
    	json_data = json.loads(contents) 
    	print(json_data["employees"])
    ```

- Dict Type으로 저장 → json 모듈로 Write

    ```python
    import json

    dict_data = {'Name': 'Zara', 'Age': 7, 'Class': 'First'}

    with open("data.json", "w") as f: 
    	json.dump(dict_data, f)
    ```