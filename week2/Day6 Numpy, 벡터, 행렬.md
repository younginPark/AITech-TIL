# Day6 Numpy, 벡터, 행렬

## Numpy

- Numerical Python
- Matrix, Vector와 같은 Array 연산의 표준
- 일반 List에 비해 빠르고, 메모리 효율적
- 반복문 없이 데이터 배열에 대한 처리 지원

- ndarray
    - test_array = np.array([1, 4, 5, 8], float)
    - type(test_array[3])  → numpy.float64
    - numpysms np.array 함수를 활용하여 배열 생성 (ndarray)
    - numpy는 하나의 데이터 type만 배열에 넣을 수 있음 (dynamic typing not supported)
- array creation
    - shape: numpy array의 dimension 구성, 크기 반환
    - dtype: numpy array의 데이터 type을 반환
    - ndim: number of dimensions
    - size: data의 개수 예) (4, 3, 4) ⇒ 48

    ```python
    test_array = np.array([1,4,5,"8], flaot) # String Type의 데이터를 입력해도 float
    print(test_array[3]) # float 타입으로 자동 형변환
    print(test_array[3].dtype) # 배열 전체의 데이터 타입 반환 float64 (하나의 데이터공간 64)
    print(test_array[3].shape) # (4, ) 
    ```

    ```python
    matrix = [[1, 2, 5, 8], [1, 2, 5, 8], [1, 2, 5 ,8]]
    np.array(matrix, int).shape  # (3, 4) 차원이 늘어나면 밀리면서 앞에 새로운 차원 들어옴
    ```

    - nbytes: ndarray object의 메모리 크기 반환

    ```python
    np.array([[1, 2, 3], [4.5, "5", "6"]], dtype=np.float32).nbytes
    # 24    32bits = 4bytes => 6 * 4bytes = 24bytes
    ```

- Hadling shape
    - reshape: Array의 shape의 크기를 변경, element의 갯수는 동일 (2,4) → (8, )
        - -1이면 size를 기반으로 알아서 지정

    ```python
    test_matrix = [[1, 2, 3, 4], [1, 2, 5, 8]]
    np.array(test_matrix).shape
    # (2, 4)

    np.array(test_matrix).reshape(4, 2)
    # array([[[1, 2],
            [3, 4]],
           [[1, 2],
            [5, 8]]])
    ```

    - flatten: 다차원 array를 1차원 array로 변환 (2, 2, 4) → (16,)
- Indexing & Slicing
    - indexing for numpy array
        - list와 달리 이차원 배열에서 [0, 0] 표기법을 제공
        - matrix일 경우 (row, col) 의미
    - slicing for numpy array
        - list와 달리 행과 열 부분 슬라이싱 가능

        ```python
        test_exmaple = np.array([[1, 2, 3, 4, 5], [6, 7, 8, 9, 10]], int)
        test_exmaple[1:3]  # 1Row ~ 2Row 전체
        ```

- creation function
    - arange: array의 범위를 지정하여, 값의 list를 생성하는 명령어

    ```python
    a = np.arange(100).reshape(10, 10)
    # array([[ 0,  1,  2,  3,  4,  5,  6,  7,  8,  9],
           [10, 11, 12, 13, 14, 15, 16, 17, 18, 19],
           [20, 21, 22, 23, 24, 25, 26, 27, 28, 29],
           [30, 31, 32, 33, 34, 35, 36, 37, 38, 39],
           [40, 41, 42, 43, 44, 45, 46, 47, 48, 49],
           [50, 51, 52, 53, 54, 55, 56, 57, 58, 59],
           [60, 61, 62, 63, 64, 65, 66, 67, 68, 69],
           [70, 71, 72, 73, 74, 75, 76, 77, 78, 79],
           [80, 81, 82, 83, 84, 85, 86, 87, 88, 89],
           [90, 91, 92, 93, 94, 95, 96, 97, 98, 99]])
    ```

    - zeros: 0으로 가득찬 ndarray 생성

    ```python
    np.zeros(shape, dtype, order)

    np.zeros((2, 5))
    # array([[0., 0., 0., 0., 0.],
           [0., 0., 0., 0., 0.]])
    ```

    - ones: 1로 가득찬 ndarray 생성
    - empty: shape만 주어지고 비어있는 ndarray 생성
        
        - memory initilization X ⇒ 빈 공간만 잡아줘서 이전에 쓰던 공간이면 값이 남아있을 수도 O
    - something_like
    - 기존 ndarray의 shape 크기 만큼 1, 0 또는 empty array 반환
    
        ```python
        np.zeros_like(test_matrix, dtype=np.float32) 
        # test_matix와 똑같이 생긴 0으로 가득찬 ndarray 생성
        # array([[0., 0., 0., 0., 0., 0., 0., 0., 0., 0., 0., 0., 0., 0., 0., 0.,
                0., 0., 0., 0.],
               [0., 0., 0., 0., 0., 0., 0., 0., 0., 0., 0., 0., 0., 0., 0., 0.,
                0., 0., 0., 0.],
               [0., 0., 0., 0., 0., 0., 0., 0., 0., 0., 0., 0., 0., 0., 0., 0.,
                0., 0., 0., 0.],
               [0., 0., 0., 0., 0., 0., 0., 0., 0., 0., 0., 0., 0., 0., 0., 0.,
                0., 0., 0., 0.],
               [0., 0., 0., 0., 0., 0., 0., 0., 0., 0., 0., 0., 0., 0., 0., 0.,
                0., 0., 0., 0.]], dtype=float32)
    ```
    
    - identity: 대각 행렬 (i 행렬)을 생성함
- eye: 대각선이 1인 행렬, k 값의 시작 index의 변경 가능
    
    ```python
    np.eye(3) # 일반 대각 행렬
    np.eye(3, 5, k = 2)
    # array([[0., 0., 1., 0., 0.],
           [0., 0., 0., 1., 0.],
           [0., 0., 0., 0., 1.]])
```
    
- diag: 대각 행렬의 값을 추출함
    
    ```python
    matrix는 [[0, 1 ,2],
    					[3, 4, 5],
    					[6, 7, 8]]
    np.diag(matrix, k=1) # k는 start index
    # array([1, 5])
```
    
    - random sampling: 데이터 분포에 따른 sampling으로 array를 생성
        - np.random.uniform(0, 1, 10).reshape(2, 5) # (균등분포  시작, 끝, 데이터사이즈)
        - np.random.normal(0, 1, 10).reshape(2, 5) # 정규분포
- operation functions
    - sum: ndarray의 element들 간의 합을 구함, list의 sum 기능과 동일
    - axis: 모든 operation function을 실행할 때 기준이 되는 dimension 축
        - (3, 4) # axis = 0, axis = 1

        ```python
        test_array.sum(axis=1), test_array.sum(axis=0)
        # (array([10, 26, 42]), array([15, 18, 21, 24]))
        ```

    - mean, std: ndarray의 element들 간의 평균 또는 표준 편차를 반환
    - 그 외에도 다양한 수학 연산자 제공..
    - concatenate: numpy array를 합치는 함수
        - vstack: vertical
        - hstack: horizontal
        - concatenate, axis = 0
    - array operations
        - numpy는 array간의 기본적인 사칙 연산을 지원감
        - element wise operations: Array 간 shape이 같을 때 일어나는 연산
        - dot product: Matrix의 기본 연산, dot 함수 사용 # test_a.dot(test_b)
        - tranpose: tranpose 또는 T attribute 사용
        - broadcasting: shape이 다른 배열 간 연산을 지원 (scalar * vector, vector * matrix)
- Comparisons
    - All & Any : Array의 데이터 전부 (and → all) 또는 일부 (or → any)가 조건에 만족 여부 반환

    ```python
    np.logical_and(a > 0, a < 3)  # and 조건의 condition
    ```

    - np.where: Index 값을 반환

    ```python
    # array([0, 1, 2, 3, 4, 5, 6, 7, 8, 9])
    np.where(a > 5)
    # (array([6, 7, 8, 9], dtype=int64),)
    ```

    - argmax & argmin: array 내 최대값 또는 최소값의 index를 반환
    - boolean
        - 특정 조건에 따른 값을 배열 형태로 추출
        - comparison operation 함수들도 모두 사용 가능

        ```python
        test_array = np.array([1, 4, 0, 2, 3, 8, 9, 7], float)
        test_array > 3
        # array([False, True, False, False, False, True, True, True])
        ```

    - fancy  index
        - numpy는 array를 index value로 사용해서 값 추출

        ```python
        a = np.array([2, 4, 6, 8], float)
        cond = np.array([0, 0, 1, 3], int)
        # array([2., 2., 4., 8., ])
        ```

- numpy data I/O
    - loadtxt & savetxt

    ```python
    # 파일 호출
    a = np.loadtxt("./populations.txt", delimiter="\t")

    # int_data.csv 로 저장
    np.savetxt("int_data.csv", a_int, fmt="%.2e", delimiter=",")
    ```

## 벡터 1

- 벡터란?
    - 벡터는 숫자를 원소로 가지는 리스트 또는 배열 (세로: 열벡터, 가로: 행벡터)
    - 공간에서 한 점을 나타냄
    - 원점으로부터 상대적 위치 표현
    - 숫자를 곱해주면 길이만 변함
- 벡터 특징
    - 벡터끼리 같은 모양을 가지면 덧셈, 뺄셈 계산 가능
    - 같은 모양을 가지면 성분곱 가능 (성분끼리 곱)
- 벡터 덧셈, 뺄셈
    
    - 두 벡터의 덧셈은 다른 벡터로부터 상대적 위치 이동 표현
- norm
    - 원점에서부터의 거리
    - || || → 는 norm의 기호
    - 임의의 차원 d에 대해 성립함 (구성성분의 개수와 상관없이)
    - L1-norm: 각 성분의 변화량의 절대값 모두 더함
    - L2-norm: 피타고라스 정리를 이용해 유클리드 거리를 계산

    ![Untitled 1](https://user-images.githubusercontent.com/73166743/105712107-bd26d200-5f5c-11eb-892f-377764061c7d.png)

    - 두 벡터 간의 각도 계산

    ![Untitled 2](https://user-images.githubusercontent.com/73166743/105712115-be57ff00-5f5c-11eb-8d20-1a479e562dfb.png)

- 내적: 정사영된 벡터의 길이와 관련

![Untitled 3](https://user-images.githubusercontent.com/73166743/105712118-bef09580-5f5c-11eb-89fb-b1dd2ca7fb4d.png)

## 행렬 1

- 행렬은 벡터를 원소로 가지는 2차원 배열
- 행과 열을 인덱스로 가짐
- 행렬의 특정 행(열)을 고정하면 행(열) 벡터라고 부름
- 벡터의 덧셈, 뺄셈

- ![Untitled 4](https://user-images.githubusercontent.com/73166743/105712121-bf892c00-5f5c-11eb-85fb-09f7cc1ddc03.png)성분곱

![Untitled 5](https://user-images.githubusercontent.com/73166743/105712123-c021c280-5f5c-11eb-985b-cee347926a82.png)

- 스칼라곱

![Untitled 6](https://user-images.githubusercontent.com/73166743/105712126-c021c280-5f5c-11eb-99f6-1f6d30d063cb.png)

- 행렬 곱셈: i번째 행벡터와 j번째 열벡터 사이의 내적을 성분으로 가지는 행렬 계산

![Untitled 7](https://user-images.githubusercontent.com/73166743/105712128-c0ba5900-5f5c-11eb-841d-413172f48410.png)


- 행렬 내적: numpy에서 np.inner (수학에서 말하는 내적과 다름)

![Untitled 8](https://user-images.githubusercontent.com/73166743/105712131-c152ef80-5f5c-11eb-873b-8731294ec8e0.png)

- 역행렬
    - 역행렬은 행과 열의 숫자가 같아야 하고 행렬식이 0인 경우에만 계산 가능
    - 순서 상관 X

![Untitled 9](https://user-images.githubusercontent.com/73166743/105712135-c152ef80-5f5c-11eb-929a-32a4bf6494f6.png)

- 유사 역행렬
    - n: 행개수, m: 열개수
    - 행과 열의 값이 달라도 가능

![Untitled](https://user-images.githubusercontent.com/73166743/105712137-c1eb8600-5f5c-11eb-8dd0-0ff7a21b01fc.png)

