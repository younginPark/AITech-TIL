# Day11 베이즈 통계학, Historical Review

## 베이즈 통계학

### 조건부 확률

![Untitled](https://user-images.githubusercontent.com/73166743/106469227-61bb8d80-64e2-11eb-8475-7d31a5868949.png)

### 베이즈 정리

- 베이즈 정리는 조건부 확률을 통해 정보를 갱신하는 법을 알려줌
- 사전 확률에서 사후 확률로 업데이트 가능

![Untitled 1](https://user-images.githubusercontent.com/73166743/106469240-66804180-64e2-11eb-8b14-67e0f0452913.png)

- 예 1) COVID-99의 발병률이 10%로 알려져있다. COVID-99에 실제로 걸렸을 때 검진될 확률은 99%, 실제로 걸리지 않았을 때 오검진될 확률이 1%라고 한다.

    어떤 사람이 질병에 걸렸다고 검진결과가 나왔을 때 정말로 COVID-99에 감염되었을 확률은?

    ![Untitled 2](https://user-images.githubusercontent.com/73166743/106469243-6718d800-64e2-11eb-91db-480ef28672d5.png)

    P(Θ) = 0.1  → 사전확률, 실제 데이터 관측하기 이전에 알 수 O

    P(D|Θ) = 0.99 → 가능도, 실제로 걸렸을 대 검진될 확률

    P(D|ㄱΘ) = 0.01 → 가능도, Θ가 부정되었을 때의 D, 실제로 걸리지 않았는데 오검진 될 확률

예 2) COVID-99의 발병률이 10%로 알려져있다. COVID-99에 실제로 걸렸을 때 검진될 확률은 99%, 실제로 걸리지 않았을 때 오검진될 확률이 10%라고 한다. 

어떤 사람이 질병에 걸렸다고 검진결과가 나왔을 때 정말로 COVID-99에 감염되었을 확률은?

![Untitled 3](https://user-images.githubusercontent.com/73166743/106469246-67b16e80-64e2-11eb-8623-2d58c65611f1.png)

## 베이즈 정리를 통한 정보 갱신

- 베이즈 정리를 통해 새로운 데이터가 들어왔을 때 이전에 계산한 사후확률을 사전확률로 사용하여 사후확률 갱신 할 수 있음
- 데이터 새로 들어올 때마다 모델의 파라미터인 Θ를 점점 업데이트

![Untitled 4](https://user-images.githubusercontent.com/73166743/106469248-684a0500-64e2-11eb-9658-3704c13185e6.png)

![Untitled 5](https://user-images.githubusercontent.com/73166743/106469250-684a0500-64e2-11eb-80b2-4563d254b705.png)

### 조건부 확률과 인과관계

- 데이터가 많아져도 조건부 확률만 가지고 인과관계 추론할 수는 없음
- 인과관계를 통해 데이터 분포의 변화에 강건한 예측 모형 만들 수 있음
    - 예) 조건부확률 기반 예측모형: 실제 테스트에서는 정확도가 높은데 데이터 변화면 정확성 떨어짐
    - 예) 인과관계 기반 예측모형: 여러 시나리오에도 예측 정확도 크게 변하지 X
- 단, 인관관계를 알아내기 위해서는 중첩요인의 효과를 제거
    - 예1) 키 → 지능의 인과관계를 볼 때 '나이'를 제거
    - 예2) 치료법 → 완치의 경우는 신장 결석 크기를 제거

## NN_MLP

- Beyond Linear Neural Networks
    - "Hidden Layer가 1개만 있는 NN의 표현력은 우리가 일반적으로 생각할 수 있는 Continuous func를 다 포함"XXXXX →  "그냥 다양한 함수를 표현할 만큼의 표현력을 갖고 있다는 것을 의미" 
    (근데 어떻게 찾는지는 모름)

## Historical_Review

![Untitled 6](https://user-images.githubusercontent.com/73166743/106469251-68e29b80-64e2-11eb-818b-eedbafd07468.png)

- 딥러닝의 주요 구성
    - 데이터를 통해 모델이 학습
    - 데이터 변환 방법 모델
    - 손실 함수를 통해 모델의 잘못된 점 수량화
    - 알고리즘을 통해 손실을 최소화 하도록 파라미터 조정
- Loss

    Loss func이 어떤 성질을 가지고 있고, 이게 왜 내가 원하는 결과를 얻어낼 수 있는지 이해하는게 중요!

    - Regression: 제곱을 평균 내서 줄임
    - Classification
        - 크로스엔트로피 로스 최소화, 분류만 하는 것이 목적이라면 log를 써서 정답에 해당하는 값만 높이겠다.
    - Probabilistic: 출력이 단순한 값이 아니라 그 값에 대한 평균과 분산, 가우시안으로 모델링

![Untitled 7](https://user-images.githubusercontent.com/73166743/106469253-68e29b80-64e2-11eb-8e40-e7e57ae017b9.png)

- Hisotrical Review
    - 2012 - AlexNet
    - 2013 - DQN
    - 2014 - Encoder/Decoder
    - 2014 - Adam Optimizer
    - 2015 - GAN
    - 2016 - Residual Networks
    - 2017 - Transformer
    - 2018 - BERT
    - 2019 - BIG Language Models
    - 2020 - Self Supervised Learning

    ## 데이터셋 다루기

    - 파이썬 코드 구성할 때 OOP 개념 써서 만들기
        - config : argparser
        - main: 파이썬 실행 파일
        - network: 모델만 담아둠, 나중에 모델만 바꿔치기 하게(메인에서 부르면 됨)