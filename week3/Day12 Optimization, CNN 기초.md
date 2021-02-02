# Day12 Optimization, CNN 기초

## Optimization

### Gradient Descent

- 1차 미분한 값만 사용하여 반복적으로 최적화를 이루어 local minimum 찾음

### Optimization

- Generalization
    - 트레이닝 에러와 테스트 에러를 최소화
- Underfitting VS Overfitting
    - Underfitting: 학습X
    - Overfitting: 학습O, 테스트X
- Cross-validation (= K-fold validation)
    - 최적의 하이퍼파라미터 찾음 (단순히 학습만 하면 감 잡기 어려워서 사용)
    - 테스트 데이터는 절대 쓰면 X
    - 예) 학습 데이터 10만개, 5 fold validation
        - 2만개씩 partitioning, 8만개로 학습하고 나머지 2만개로 validation
        - 1, 2, 3, 4 / 5 → 1, 2, 4, 5 / 3 이런식으로
- Bias and Variance
    - Low variance: 출력이 일관적
    - Low Bias: 평균적으로 true target에 맞음
    - Bias를 많이 줄이면 Variance가 커질 수도 있고 혹은 그 반대로 될수도

![Untitled](https://user-images.githubusercontent.com/73166743/106597496-d8679200-6599-11eb-8e2a-780cc176d02f.png)

![Untitled 1](https://user-images.githubusercontent.com/73166743/106597558-f0d7ac80-6599-11eb-8fa1-034c85592083.png)

- Bootstrapping
    - 학습데이터에서 subsampling 해서 여러 모델을 만들고 무언가를 하겠다.
- Bagging VS Boosting
    - Bagging (Bootstrapping aggregating)
        - 학습데이터에서 subsampling해 여러 모델을 만들고 output으로 평균을 내겠다. (앙상블)
    - Boosting
        - 데이터가 100개면 80개로 간단한 모델 하나 만들고, 20개로 잘 안되는 데이터로만 모델 만듦
        - weak learner들을 sequential하게 합펴서 하나의 strong learner 만듦

### Gradient Descent Methods

- Stochastic gradient descent
    
    - 하나의 샘플에 대해서만 gradient 구해서 업데이트
- Mini-batch gradient descent
    
    - 데이터의 서브셋으로 gradient 구해서 업데이트
- Batch gradient descent
    
    - 한번에 다 사용, 예를 들면 10만개의 gradient 평균을 가지고 업데이트
- Batch-size Matters
    - large batch → sharp minimizers
    - small batch → flat minimizers
        - flat minimizers하면 트레이닝 function에서 조금 멀어져도 테스팅 function에서도 적당히 낮은 값 나옴 → generalization

    ![Untitled 2](https://user-images.githubusercontent.com/73166743/106597567-f33a0680-6599-11eb-801b-acbab461916a.png)

- Gradient Descent

    ![Untitled 3](https://user-images.githubusercontent.com/73166743/106597573-f503ca00-6599-11eb-9a60-ff83740c3ff9.png)

- Momentum
    - mini-batch로 이전 방향과 비슷하게 이어가게 만듦
    - 왜 미니배치 트레이닝 할 때 momentum이 좋을까?
        - SGD 쓰면 많은 iteratir 사용해야 데이터 convergence 가능인데

            모멘텀은 이전에 받은 정보를 현재도 어느 정도 반영해서 데이터를 한번에 많이 보는 효과 생김

    ![Untitled 4](https://user-images.githubusercontent.com/73166743/106597576-f59c6080-6599-11eb-99c7-749c6df19e0c.png)

- Nesterov Accelerated Gradient (NAG)
    - Lookahead Gradient
        
        - 현재 정보가 있으면 그 방향으로 가보고, 간 곳에서 gradeint 계산한 걸 가지고 accumulation
- momentum만 있으면 관성 때문에 계속 왔다갔다 하니까 local minimum convergence 못함
    
    NAG는 지나서 gradient 구하니까 반대 방향으로 갈 수 O → 빠르게 local minimum 도달
    
![Untitled 5](https://user-images.githubusercontent.com/73166743/106597578-f59c6080-6599-11eb-8777-cea5dbbff2a7.png)
    
- Adagrad
    - NN의 파라미터가 얼만큼 지금까지 많이 변해, 안변해 왔는지 봄 (안변했으면 변하게, 혹은 그 반대로)
    - 입실론은 0으로 나눠주기 위함
    - Gt: 변화(각 step의 모든 gradient)를 제곱해서 더함
        - 분모에 넣어서 현재 상황에 따라 조절
    - 문제: 뒤로 갈수록 숫자가 커지니까 학습이 멈추는 현상 발생

    ![Untitled 6](https://user-images.githubusercontent.com/73166743/106597580-f634f700-6599-11eb-9fc8-51ff33861599.png)

- Adadelta
    - Gt: 윈도우 사이즈 만큼의 gradinet제곱의 변화를 보겠다.
    - gt: 윈도우 사이즈* 파라미터 개수만큼 들고 있어야 함
    - ΔWt: 실제로 업데이트 하려는 weight의 변화값 (learning rate 없이도 어느정도 되게 만들겠다.)

    ![Untitled 7](https://user-images.githubusercontent.com/73166743/106597581-f634f700-6599-11eb-9ae4-f7c47d4e5e7e.png)

- RMSprop
    - 지수 이동 평균 이용
    - Adagrad의 Gt 값이 무한이 커지는 것을 방지

    ![Untitled 8](https://user-images.githubusercontent.com/73166743/106597584-f6cd8d80-6599-11eb-88c1-381e12eaa6ab.png)

- Adam
    - 가장 잘됨
    - Momentum + RMSprop
    - 1-Bt : 바이어스 보정, 초기값이 0이여서 편향될 추정값 방지

    ![Untitled 9](https://user-images.githubusercontent.com/73166743/106597586-f7662400-6599-11eb-9c1c-c9e1e9f4746a.png)

### Regularization

- Early Stopping
    - loss 가 커지기 시작하면 stop

    ![Untitled 10](https://user-images.githubusercontent.com/73166743/106597588-f7662400-6599-11eb-9d80-6e8a163eb9fd.png)

- Parameter Norm Penalty (= weight decay)
    - 파라메터 너무 커지지 않게 (크기 관점에서)
    - NN이 만들어내는 function space 속에서 함수를 최대한 부드러운 함수로 보자

        (= generaliztion 성능 좋음)

- Data Augmentation
    - 이미지 라벨이 변하지 않는 한도 내에서 조정

    ![Untitled 11](https://user-images.githubusercontent.com/73166743/106597592-f7feba80-6599-11eb-816f-c68ca8ad49bd.png)

- Noise Robustness
    - Random noise를 인풋이나 웨이트에 줌

    ![Untitled 12](https://user-images.githubusercontent.com/73166743/106597594-f8975100-6599-11eb-8c5c-ff4dfeef1461.png)

- Label Smoothing
    - 학습데이터 2개를 뽑아서 섞음 → decision boundary를 부드럽게

    ![Untitled 13](https://user-images.githubusercontent.com/73166743/106597595-f8975100-6599-11eb-8d27-8d47f4cb869f.png)

- Dropout
    - 각각의 뉴런들이 조금 더 robust한 피쳐가 나올 수 있도록함
    - 랜덤하게 뉴런을 0으로 설정
- Batch Normalization
    - 각각의 레어어의 평균과 분산을 구해서 정규화 함
    - 깊은 네트워크도 더 빠르고 안정적으로 학습시킬수 있고 네트워크의 generalization 성능도 좋아짐
    - Group Norm
        - batch 크기 작아지면 성능 떨어짐 → 그룹으로 나누어 Norm

        ![Untitled 14](https://user-images.githubusercontent.com/73166743/106597597-f92fe780-6599-11eb-9dbf-1c413fe569e5.png)

## CNN 기초

### Convolution 연산 이해

- Kernel 이라는 고정된 가중치 행렬 사용
- 커널을 입력벡터 상에서 움직여 가면서 선형모델과 합성함수 적용
- 커널을 이용해 국소적으로 증폭, 감소시켜 정보 추출, 필터링
- 커널은 정의역 내에서 움직여도 변하지 않고 주어진 신호에 local하게 적용

![Untitled 15](https://user-images.githubusercontent.com/73166743/106597600-f9c87e00-6599-11eb-93c8-54a31b71d385.png)

![Untitled 16](https://user-images.githubusercontent.com/73166743/106597602-f9c87e00-6599-11eb-873d-b68964d2d7e5.png)

- 다양한 차원에서 계산 가능

![Untitled 17](https://user-images.githubusercontent.com/73166743/106597603-fa611480-6599-11eb-923c-86f3ca06da8b.png)

- 입력 크기를 (H,W), 커널 크기를 (Kh, Kw), 출력 크기를 (Oh, Ow) 일 때 출력 크기 계산

    ![Untitled 18](https://user-images.githubusercontent.com/73166743/106597605-faf9ab00-6599-11eb-87b4-7a55da6eaf94.png)

- 3차원 Convolution은 2차원 Convolution을 3번 적용한다고 생각

![Untitled 19](https://user-images.githubusercontent.com/73166743/106597607-fb924180-6599-11eb-9ef0-6ba60423d828.png)

### Convolution의 역전파

- Convolution 연산은 커널이 모든 입력데이터에 공통으로 적용되기 때문에 역전파를 계산할 때도 convolution 연산이 나오게 됨

![Untitled 20](https://user-images.githubusercontent.com/73166743/106597609-fc2ad800-6599-11eb-91ec-a4e29a8fccff.png)

![Untitled 21](https://user-images.githubusercontent.com/73166743/106597528-e6b5ae00-6599-11eb-839d-67c210fcd22a.png)

![Untitled 22](https://user-images.githubusercontent.com/73166743/106597529-e74e4480-6599-11eb-9293-39ca8495e181.png)

