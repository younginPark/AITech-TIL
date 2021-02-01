# Day10 matplotlib, 통계학 맛보기

## matplotlib

- 파이썬의 대표적인 시각화 도구
- pyplot 객체를 사용하여 데이터를 표시 (그림 판떼기)
- pyploy 객체에 그래프들을 쌓은 다음 flush (plt.show() 하면 flush됨)
- graph는 figuere 객체에 생성됨
- axes → figure → pyplot 객체

```python
# 하나의 figure 안에 여러개의 pyplot 가능
ax_1 = fig.add_subplot(1, 2, 1) # 두개의 plot 중에 하나 생성
ax_2 = fig.add_subplot(1, 2, 2) # 두개의 plot 중에 하나 생성

ax_1.plot(x_1, y_1, c = "b")
ax_2.plot(x_2, y_2, c = "g")
```

- color: 색깔 속성
- ls, linestyle: 선의 스타일
- title: pyplot의 이름 정할 수 있고 figure의 subplot 별로 입력도 가능, latex 타입의 표현도 가능
- legend: 범례 표시, 위치 지정 가능
- grid: 보조선을 긋는 grid

### matplotlib graph

- scatter
    - marker: 모양 지정 가능
    - s: 데이터의 크기 지정
- bar chart
    
    - 옆으로 쌓을 수도, 위로 쌓을 수도 O
- histogram
- boxplot

    ![Untitled](https://user-images.githubusercontent.com/73166743/106468881-d93ced00-64e1-11eb-8848-22f166a101d8.png)

### seaborn

- 기존 matplotlib에 기본 설정 추가
- basic plots

    ```python
    sns.lineplot(x="timepoint", y="signal", data=fmri) # fmri는 데이터 알아서 정렬
    # 선으로 먼저 그려주고 그 선의 주변에 음영을 주어 분포 알려줌

    sns.lineplot(x="timepoint", y="signal", hue="event", data=fmri)
    # x, y에는 numeric 데이터 넣고 hue에는 카테고리컬 데이터 넣어 한 그래프에 카테고리 별로 그래프 그림
    ```

- Vilointplot: boxplot에 distribution을 함께 표현
- Stripplot: scatter와 category 정보를 함께 표현
- Swarmplot: 분포와 함께 scatter를 함께 표현
- Pointplot: category 별로 numeric의 평균, 신뢰구간 표시
- regplot: scatter + 선형함수를 함께 표시
- replot: Numeric 데이터 중심의 분포/선형 표시
- catplot: category 데이터 중심의 표시
- FacetGrid: 특정 조건에 다른 다양한 Plot을 grid로 표시
- pairplot: 데이터 간의 상관관계 표시
- Implot: regression 모델과 category 데이터를 함께 표시

## 통계학 맛보기

### 통계적 모델링

- 적절한 가정 위에서 확률분포를 추정(inference)하는 것이 목표
- 기계학습과 통계학이 공통적으로 추구하는 목표

### 유한한 개수의 데이터만 관찰해서는 모집단의 분포 정확하게 알아낼 수 X

- 모수적(parametric) 방법론

    데이터가 특정 확률분포를 따른다고 선험적으로(a priori) 가정한 후 그 분포 를 결정하는 모수(parameter)를 추정하는 방법

    ex) 정규분포: 평균, 분산 이라는 모수를 가지고 있음

- 비모수(nonparametric) 방법론

    특정 확률분포를 가정하지 않고 데이터에 따라 모델의 구조 및 모수의 개수 가 유연하게 바뀔 때의 방법

    (모수가 없는게 비모수인 것은 X, 모수가 무한하거나 개수 바뀔 때임)

### 확률분포 가정 방법

- 데이터가 2개의 값(0 또는 1)만 가지는 경우 → 베르누이분포
- 데이터가 n개의 이산적인 값을 가지는 경우 → 카테고리분포
- 데이터가 [0,1] 사이에서 값을 가지는 경우 → 베타분포
- 데이터가 0 이상의 값을 가지는 경우 → 감마분포, 로그정규분포 등
- 데이터가 R 전체에서 값을 가지는 경우 → 정규분포, 라플라스분포 등
- !!!! 하지만 기계적으로 확률분포 가정 X !!!! 데이터를 생성하는 원리를 먼저 고려해야 함

### 최대가능도 추정법

- 이론적으로 가장 가능성이 높은 모수 추정 방법

    ![Untitled 1](https://user-images.githubusercontent.com/73166743/106468893-dc37dd80-64e1-11eb-8c7d-0461cdc3b229.png)

- 데이터 집합 X가 독립적으로 추출되었으면 로그가능도를 최적화
    - 로그가능도의 경우 maximum을 찾아주므로 음의 로그가능도 사용 (최소화하는 목적식으로 바꿔주기 위해서)
    - 우리에게 주어진 데이터를 가지고 현재 수식과 같이 가능도 함수를 최적화하는 theta 찾는 것이 목표

    ![Untitled 2](https://user-images.githubusercontent.com/73166743/106468899-de01a100-64e1-11eb-933b-100e3562298b.png)

    ![Untitled 3](https://user-images.githubusercontent.com/73166743/106468903-df32ce00-64e1-11eb-9e8d-b96cb76ffd23.png)

    ![Untitled 4](https://user-images.githubusercontent.com/73166743/106468907-e063fb00-64e1-11eb-86d8-b1f56ab144ee.png)