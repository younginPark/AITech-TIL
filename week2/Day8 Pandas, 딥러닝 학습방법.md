# Day8 Pandas, 딥러닝 학습방법

## Pandas

- 구조화된 데이터의 처리를 지원하는 Python 라이브러리
- Panel data → pandas
- 테이블형 tabular
- 데이터 처리 및 통계 분석을 위해 사용

![Untitled](https://user-images.githubusercontent.com/73166743/105998867-66ea9800-60f0-11eb-8e01-a8aa3704a7f4.png)

```python
# data_url = 'https://archive.ics.uci.edu/ml/machine-learning-databases/housing/housing.data' #Data URL
data_url = "./housing.data"  # Data URL
df_data = pd.read_csv(
    data_url, sep="\s+", header=None
)  # csv 타입 데이터 로드, separate는 빈공간으로 지정하고, Column은 없음
```

- series: DataFrame 중 하나의 Column에 해당하는 데이터의 모음 Object
    - 리스트와 다른 특징은 0, 1, 2, / A, B, C와 같은 Index 값이 붙어나옴
    - .values: 값 리스트만
    - .index: Index 리스트만

    ```python
    dict_data = {"a": 1, "b": 2, "c": 3, "d": 4, "e": 5}
    example_obj = Series(dict_data, dtype=np.float32, name="example_data")
    # a    3
    	b    2
    	c    3
    	d    4
    	e    5
    	dtype: int64
    ```

- DataFrame: Data Table 전체를 포함하는 Object
    - column 별로 dtype이 다를 수도 O
    - Series를 모아서 만든게 Data Table (기본 2차원)

    ![Untitled 1](https://user-images.githubusercontent.com/73166743/105998832-5fc38a00-60f0-11eb-8faa-93b16e4f9995.png)

    - loc - index location : 인덱스를 부르는 이름으로 사용
    - iloc - index position : 인덱스 기준으로 생각함
- 참고) astype: 타입 바꾸는거

    ```python
    example_obj = example_obj.astype(int) -> dtype: int64
    ```

- Dataframe handling
    - tranpose df.T
    - 값 출력 : df.values
    - CSV 변환 : df.to_csv()
    - del : column 삭제 (메모리 주소 자체 삭제)  : del df["debt"]
    - drop : 출력이 안되는거지 메모리 상에는 여전히 존재

        : df.drop([0, 1, 2, 3]), df.drop("city", axis = 1) # column 중에 "city" 삭제

- Selection with column names

    ```python
    df[["account", "street", "state"]].head() # 한개 이상의 column을 선택, head 기본 5줄 
    ```

    ```python
    df["name"][:3] # column이름과 함께 row index 사용시, 해당 column만
    							 # 만약 index가 0, 1, 2가 아니라 a, b, c면 안뽑힘
    ```

- reset_index 하면 index 앞에 index 하나 더 추가
- inplace = True 하면 자기 자신 자체의 테이블이 변하는걸 허용
- series operation
    - add, sub, div, mul
    - s1.add(s2) == s1 + s2
        - index를 기준으로 연산 수행
        - 겹치는 indexrk 없을 경우 NaN 값으로 반환
        - series 에서 인덱스 중복 허용
    - df1 + df2 == df1.add(df2, fill_value=0)
        - df는 column과 index를 모두 고려
        - add operation을 쓰면 NaN값 0으로 변환
    - df + s2 == df.add(s2, axis = 0)
        - axis를 기준으로 row 브로드캐스팅 일어남
- map for series
    - 인덱스에 맞춰서 값을 적용해줌
    - dict type으로 데이터 교체
    - 없는 값은 NaN

    ```python
    z = {1: "A", 2: "B", 3: "C"}
    s1.map(z)
    # 0    NaN
    	1      A
    	2      B
    	3      C
    	4    NaN
    	5    NaN
    	6    NaN
    	7    NaN
    	8    NaN
    	9    NaN
    	dtype: object
    ```

- apply for dataframe
    - map과 달리, series 전체에 해당 함수 적용
    - 각 column 별로 결과값 반환 (컬럼 별로 적용)

    ```python
    def f(x):
        return Series(
            [x.min(), x.max(), x.mean(), sum(x.isnull())],
            index=["min", "max", "mean", "null"],
        )

    df_info.apply(f)
    ```

    ![Untitled 2](https://user-images.githubusercontent.com/73166743/105998843-6225e400-60f0-11eb-8370-a7ea7986b5df.png)

- applymap for dataframe
    - seires 단위가 아닌 element 단위로 함수를 적용 (모든 값에 적용)
    - series 단위에 apply를 적용시킬 때와 같은 함수

    ```python
    f = lambda x: x // 2
    df_info.applymap(f).head(5)
    ```

    ![Untitled 3](https://user-images.githubusercontent.com/73166743/105998848-62be7a80-60f0-11eb-9c8a-1f0b0ece3242.png)

- pandas built-in functions
    - describe
        - Numeric type 데이터의 요약 정보를 보여줌

        ![Untitled 4](https://user-images.githubusercontent.com/73166743/105998850-63571100-60f0-11eb-9ea5-91b2f1ab8f78.png)

    - unique
        - series data의 유일한 값을 list로 반환

        ```python
        df.sex.unique()
        # array(['male', 'female'], dtype=object)
        ```

    - isnull
        - column 또는 row 값의 NaN(null) 값의 index를 반환
        - df.isnumm()
    - sort_values
        - column 값을 기준으로 데이터를 sorting

        ```python
        df.sort_values("age", ascending=False).head(10)
        ```

        ![Untitled 5](https://user-images.githubusercontent.com/73166743/105998854-63efa780-60f0-11eb-8164-ab7ec3cbbcc0.png)

    - Correlation & Covariance
        - 상관계수와 공분산을 구하는 함수
        - corr, cov, corrwith (이 값과 나머지 전체값 간의 correlation)

## 딥러닝 학습방법 이해하기

- 신경망 = 비선형 모델 = 선형 모델 + 비선형 함수(활성 함수)
- 벡터를 input으로 받지 않고 하나의 실수 값만 받게 됨
- 소프트맥스
    - 모델의 출력을 확률로 해석할 수 있게 변환해주는 함수
    - 특정 벡터가 어떤 클래스에 속해 있는지 알 수 O

    ![Untitled 6](https://user-images.githubusercontent.com/73166743/105998859-64883e00-60f0-11eb-9c01-0ca368d3d73a.png)

    - np.max 사용하여 너무 큰 벡터가 들어올 상황에서의 오버플로우를 방지
    - 추론만 할 때는 one-hot 벡터로 최대값을 가진 주소만 1로 출력하고 softmax 사용 안함, 학습용임
- 활성함수
    - 비선형 함수
    - 활성함수를 사용하지 않으면 딥러닝에서 선형모형과 차이X
    - 시그모이드, tanh, ReLU 가 있는데 ReLU 많이 씀

    ![Untitled 7](https://user-images.githubusercontent.com/73166743/105998861-6520d480-60f0-11eb-8a11-06fbd4d2fc91.png)

    - 활성함수는 각 벡터에 개별적으로 적용
- 층을 여러개 쌓는 이유
    - 목적함수를 근사하는데 필요한 뉴런(노드)의 숫자가 훨씬 빨리 줄어들어 좀 더 효율적 학습 가능
    - 층이 깊다고 수월한 것은 X
- 역적파
    - 딥러닝은 역전파 알고리즘을 이용하여 각 층에 사용된 파라미터인 W, b를 학습
    - 각 층 파라미터의 그레디언트 벡터는 윗층부터 역순으로 계산
    - 연쇄법칙으로 합성함수 미분

    ![Untitled 8](https://user-images.githubusercontent.com/73166743/105998863-65b96b00-60f0-11eb-9254-62c1e3c80181.png)

    ![Untitled 9](https://user-images.githubusercontent.com/73166743/105998864-66520180-60f0-11eb-9668-efa8debf105e.png)