# Day9 Pandas2, 딥러닝에서의 확률론

## Pandas2

### Groupby1

- SQl groupby 명령어와 같음
- split → apply → combine 과정을 거쳐 연산

```python
df.groupby("Team")["Points"].sum()
			# 묶음의 기준  #적용받는 컬럼 #적용받는 연산

df.groupby(["Team", "Year"])["Points"].sum()
		       # 1단계,   2단계    
```

- Hierachical Index
    - Groupby 명령의 결과물도 결국은 dataframe
    - 두 개의 column으로 groupby를 할 경우, index가 두개 생성
    - unstack()
        - Group으로 묶여진 데이터를 matrix 형태로 전환

        ![Untitled](https://user-images.githubusercontent.com/73166743/106118436-74a72880-6197-11eb-983f-cc13f15be2d8.png)

    - swaplevel()
        - Index level을 변경할 수 있음

        ![Untitled 1](https://user-images.githubusercontent.com/73166743/106118457-7a047300-6197-11eb-9787-73256d191aae.png)

        - Index level을 기준으로 기본 연산 수행 가능

            ```python
            h_index.sum(level = 0)
            ```

    ### Groupby2

    - grouped
        - groupby에 의해 split된 상태를 추출 가능
        - Tuple 형태로 그룹의 key 값 value 값이 추출됨

        ```python
        grouped = df.groupby("Team")
        for name, group in grouped:
        	print(name)
        	print(group)

        # 특정 key 값을 가진 그룹의 정보만 추출 가능
        grouped.get_group("Devils")

        # Aggregation: 요약된 통계정보를 추출
        grouped.agg(sum)
        grouped.agg(max) # 각 컬럼 별로 젤 큰값을 알려주는거지 한 줄을 주는 것X
        grouped['Points'].agg([np.sum, np.mean, np.std])

        # Transformation: 해당 정보를 변환해줌, 개별 데이터 변환 지원 ex) 람다 함수
        score = lambda x: (x.max())
        grouped.transform(score) # 그룹 별로 각 column에 대해 최대값을 보여줌

        # Filtration: 특정 정보를 제거하여 보여주는 필터링 기능
        # filter 안에는 boolean 조건이 존재
        # len(x)는 grouped된 dataframe 개수
        df.groupby('Team').filter(lambda x: len(x) >= 3) # 팀 별로 3개 이상의 데이터가 존재하는 팀만 출력
        ```

    ### Case study

    ```python
    # 시간과 데이터 종류가 정리된 통화량 데이터 연습
    df_phone = pd.read_csv("./data/phone_data.csv")
    df_phone.head()
    ```

    ![Untitled 2](https://user-images.githubusercontent.com/73166743/106118459-7a9d0980-6197-11eb-8545-3d6ca88b3a68.png)

    ```python
    df_phone.groupby('month')['duration'].sum() # 달 별 통화시간

    df_phone[df_phone['item'] == 'call'].groupby('month')['duration'].sum() # item이 call인 것만

    df_phone.groupby(['month', 'item'])['duration'].sum() # month, item으로 묶고 date들 count

    df_phone.groupby(['month', 'item'])['date'].count().unstack() # 위의 것들을 표로

    df_phone.groupby('month', as_index=False).agg({"duration": "sum"}) # month를 index로 안함, duration에 sum 적용

    df_phone.groupby(['month', 'item']).agg({'duration':sum,      # 각 그룹의 duration 별 sum
                                         'network_type': "count", # network_type별로 count
                                         'date': 'first'})    # 그룹 별로 첫번째 값 보여줌

    grouped.rename(columns={"min": "min_duration", "max": "max_duration", "mean": "mean_duration"}) # column이름을 rename

    grouped.add_prefix("duration_") # column 이름 앞에 항상 붙어 나옴
    ```

### Pivot Table Crosstab

- Pivot Table
    - Index 축은 groupby와 동일
    - column에 추가로 labeling 값을 추가하여 Value에 numeric type 값을 aggregation

    ```python
    df_phone.pivot_table(["duration"],
                         index=[df_phone.month,df_phone.item], 
                         columns=df_phone.network, aggfunc="sum", fill_value=0)

    ==

    df_phone.goupby(["month", "item", "network"])["duration"].sum().unstack()
    ```

    ![Untitled 3](https://user-images.githubusercontent.com/73166743/106118462-7b35a000-6197-11eb-8b7d-4f9640a22b80.png)

- Crosstab
    - 두 Column의 교차 빈도, 비율, 덧셈 등을 구할 때 사용
    - Pivot table의 특수한 형태

    ```python
    pd.crosstab(index=df_movie.critic,columns=df_movie.title,values=df_movie.rating,
                aggfunc="first").fillna(0)

    == 

    df_movie.groupby(["critic","title"]).agg({"rating":"first"}).unstack().fillna(0)
    ```

    ![Untitled 4](https://user-images.githubusercontent.com/73166743/106118466-7b35a000-6197-11eb-9c49-b1e75d682992.png)

### Merge & Concat

- Merge
    - SQL에서 많이 사용하는 join과 같은 기능

    ```python
    # on은 양쪽에 다 같은 column 있어야 함
    pd.merge(df_a, df_b, on='subject_id')

    # 두 dataframe의 column 이름이 다를 때
    pd.merge(df_a, df_b, left_on='subject_id', right_on='subject_id')
    ```

    - join method
        - Inner join: 양쪽다 있는 것만  ex) subject_id에 같은 값이 있을 때
        - Full join(outer): 같은건 붙이고 아닌건 각각
        - Left join: 왼쪽 기준으로 합쳐주고 왼쪽X, 오른쪽O이면 nan 값 처리
        - Right join: 오른쪽 기준으로 합쳐주고 왼쪽O, 오른쪽X이면 nan 값 처리

![Untitled 5](https://user-images.githubusercontent.com/73166743/106118468-7bce3680-6197-11eb-9d00-91ff7a96b57f.png)

```python
# 사용 예시
pd.merge(df_a, df_b, on='subject_id', how='left')
pd.merge(df_a, df_b, on='subject_id', how='right')
pd.merge(df_a, df_b, on='subject_id', how='outer')
pd.merge(df_a, df_b, on='subject_id', how='inner')
```

- index based join

```python
# 인덱스 값 기준으로 붙이므로 
pd.merge(df_a, df_b, right_index=True, left_index=True)
```

![Untitled 6](https://user-images.githubusercontent.com/73166743/106118472-7c66cd00-6197-11eb-95e3-aaf3044c5f72.png)

- concat
    - 같은 형태의 데이터를 붙이는 연산 작업

    ```python
    # concat, append의 전재가 a,b의 데이터들이 같은 column을 가지고O
    df_new = pd.concat([df_a, df_b]) # 리스트 형태로 값을 붙임
    df_a.append(df_b) # 밑으로 붙임
    ```

## Persistence

- Data loading시 DB connection 기능 제공

```python
import sqlite3 #pymysql <- 설치

conn = sqlite3.connect("./data/flights.db") # db 연결 코드
cur = conn.cursor()
cur.execute("select * from airlines limit 5;")
results = cur.fetchall()

df_airplines = pd.read_sql_query("select * from airlines;", conn) # db 연결 conn을 사용하여 dataframe 생성
```

- XLS persistence
    - Dataframe의 엑셀 코드 추출
    - Xls 엔진으로 openpyxls 또는 XlsxWrite 사용

    ```python
    writer = pd.ExcelWriter('./data/df_routes.xlsx', engine='xlsxwriter')
    df_routes.to_excel(writer, sheet_name='Sheet1')
    ```

- Pickle persistence
    - 가장 일반적인 python 파일 persistence

    ```python
    df_routes_pickle = pd.read_pickle("./data/df_routes.pickle")
    df_routes_pickle.head()
    ```

## 딥러닝에서의 확률론

- 딥러닝은 확률론 기반의 기계학습 이론에 바탕을 둠
- 기계학습에서 사용되는 손실함수들의 작동 원리는 데이터 공간을 통계적으로 해석해서 유도함
- 회귀 분석에서는 손실함수로 사용되는 L2 Norm을 예측오차의 분산을 가장 최소화 하는 방향으로 학습 유도
- 분류 문제에서 사용되는 교차엔트로피는 모델 예측의 불확실성을 최소화 하는 방향으로 학습 유도

- 확률분포는 데이터의 초상화
    - 데이터 공간: X x Y
    - 확률 분포(데이터 공간에서 데이터를 추출하는 분포): D
    - 데이터 확률 변수: (x, y) ~ D
    - 파란점은 연속, 빨간점은 이산 → 모델링 방법에 따라 연속, 이산 결정

    ![Untitled 7](https://user-images.githubusercontent.com/73166743/106118475-7cff6380-6197-11eb-8723-611b9d310575.png)

- 이산확률변수 VS 연속확률변수
    - 확률변수는 확률분포 D에 따라 이산형, 연속형으로 확률 변수 구분
    - 이산형 확률변수
        - 확률변수가 가질 수 있는 경우의 수를 모두 고려하여 확률을 더해서 모델링

        ![Untitled 8](https://user-images.githubusercontent.com/73166743/106118478-7d97fa00-6197-11eb-8661-858ab1ebe064.png)

    - 연속형 확률변수
        - 데이터 공간에 정의된 확률변수의 밀도(density) 위에서의 적분을 통해 모델링

        ![Untitled 9](https://user-images.githubusercontent.com/73166743/106118479-7e309080-6197-11eb-8585-f20ccd6431e3.png)

- 조건부확률과 기계학습
    - 조건부확률 P(y | X) 는 입력변수 X에 대해 정답이 y일 확률을 의미
    - 로지스틱 회귀에서 사용했던 선형모델과 소프트맥스 함수의 결합은 데이터에서 추출된 패턴을 기반으로 확률을 해석
    - 분류문제에서 softmax(WΦ + b)은 데이터 x로부터 추출된 특징패턴 Φ(x)과 가중치행렬 W을 통해 조건부확률 P(y|x)을 계산

- 기대값
    - 기대값은 데이터를 대표하는 통계량으로 고등학생 때 평균으로 배움
    - 기대값을 이용해 분산, 첨도, 공분산 등 여러 통계량 계산 가능
    - 연속
        - f(x): 주어진 함수
        - P(x): 확률 밀도 함수
        - dx: 적분
    - 이산
        - f(x): 주어진 함수
        - P(x): 확률질량함수

    ![Untitled 10](https://user-images.githubusercontent.com/73166743/106118481-7e309080-6197-11eb-9a91-fc288cb773f4.png)

- 몬테카를로 샘플링
    - 확률분포를 모를 때 데이터를 이용하여 기대값을 계산하려면 몬테카를로 샘플링 방법 사용
    - 샘플링: 샘플링하는 방법을 알면 적분이나 시그마 대신 samplin을 통해 기대값을 대신 계산 가능
    - 몬테카를로 샘플링은 분포에서 독립추출만 보장된다면 대수의 법칙에 의해 수렴성 보장

    ![Untitled 11](https://user-images.githubusercontent.com/73166743/106118483-7ec92700-6197-11eb-9388-a0858b29e46e.png)

    - 예제: 적분 계산하기

        함수 f(x) = e^-2x의 [-1, 1] 상에서 적분값을 어떻게 구할까?

        ![Untitled 12](https://user-images.githubusercontent.com/73166743/106118485-7ec92700-6197-11eb-93cc-df580af01a13.png)

        ```python
        import numpy as np

        def mc_int(fun, low, high, sample_size = 100, repeat = 10):
        	int_len = np.abs(high - low)
        	stat = []
        	for _ in range(repeat):
        		x = np.random.uniform(low = low, high = high, size = sample_size)
        		fun_x = fun(x)
        		int_val = int_len * np.mean(fun_x)
        		stat.append(int_val)
        	return np.mean(stat), np.std(stat)

        def f_x(x):
        	return np.exp(-x**2)

        print(mc_int(f_x, low = -1, high = 1, sample_size = 10000, repeat = 100)
        # (1.4938754306231912, 0.00391398451303653) 으로 오차 범위 안에 참값 존재
        ```