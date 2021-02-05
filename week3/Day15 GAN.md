# Day15 GAN

### Learning a Generative Model

- Implicit model
    - Generation만 됨, Smapling만
- Explicit model
    - Generation
    - Density estimation
        - 어떤 이미지가 들어왔을 때 확률값 하나가 튀어나와서 강가지인지 고양이인지 구분

### Structure Through Independence

- a binary image이면 한 픽셀 표현하는데 2^N → 파라미터 수 너무 많음
- 파라미터 수가 많으면 학습이 어려우니까 n개를 다 쓰지 않고 표현할 방법이 있을까
- 이 distribution을 표현하기 위해서 필요한 숫자는 n개만 있으면 됨

    → 각각의 픽셀에 대해서 파라미터 한개만 있으면 되니까

    → n개의 픽셀이 independent하니까 2^n이 아닌 n개로도 표현할 수 O

### Conditional Independence

- Chain rule: n개의 joint distribution을 n개의 condition distribution으로 바꿈
- Bayes' rule : 조건부 확률
- Conditional independence : chain rule 같은데서 conditional 부분 날려주는 효과 O
    - z라는 random variable이 주어졌을 때, x, y independence함
    - x라는 random variable을 표현하는데 있어서 z가 주어지면 y는 상관 X

![Untitled](https://user-images.githubusercontent.com/73166743/107034192-b9673b00-67f9-11eb-946d-0f2012c9d24d.png)

- x3 만들 때 x1, x2 조합 생각하면 4 나옴
- 그러므로 모든 파라미터 수는 x1을 빼고 2n-1 이 됨
- Auto-regressive models에서 이 conditional independency를 잘 활용함

![Untitled 1](https://user-images.githubusercontent.com/73166743/107034202-bcfac200-67f9-11eb-83c7-87815152b1c8.png)

### Auto-regressive Model

- joint distribution은 chain rule을 통해서 conditional distribution으로 쪼개서 활용
- 하나의 정보가 이전 정보들에 대해 dependent함
- 순서 매기는 것이 중요, V몇개까지 dependent하고 어떻게 순서 매기는 지에 따라 성능 다름

### NADE: Neural Autoregressive Density Estimator

- i번째 픽셀을 1~i-1까지 dependent
- 3번째 픽셀은 1~2까지 NN거쳐서 확률 계산
- NN에 입력 차원이 계속 달라짐 → weight 계속 커짐
- Density Estimator → Explicit하게 확률 계산 O, 1번째 알고 있으면 2번째 알 수 O

![Untitled 2](https://user-images.githubusercontent.com/73166743/107034207-be2bef00-67f9-11eb-95c7-c42ad362df46.png)

### Pixel RNN

- 이미지에 있는 픽셀 만들어내고 싶음
- R을 먼저 만들고 G, B를 순서대로 만들겠다.

![Untitled 3](https://user-images.githubusercontent.com/73166743/107034208-bec48580-67f9-11eb-90b8-cf8acc443192.png)

- Ordering에 따라 2가지로 나뉨
    - 자기 위쪽 정보 전부 활용
    - 자기 이전 정보 전부 활용

![Untitled 4](https://user-images.githubusercontent.com/73166743/107034209-bec48580-67f9-11eb-9df1-ab8c9481b85b.png)

### Variational Auto-encoder

- autoencoder는 generative model 아님
- Posterioir distribution 찾는게 이 모델의 목적
    - 나의 observation이 주어졌을 때 내가 관심있어하는 random variable의 확률 분포
    - 이거 구하기 어려우니가 최적화해서 학습 시킬 수 있게 근사하겠다.

    ![Untitled 5](https://user-images.githubusercontent.com/73166743/107034213-bff5b280-67f9-11eb-875a-cf60e135dde0.png)

    ![Untitled 6](https://user-images.githubusercontent.com/73166743/107034216-bff5b280-67f9-11eb-89fb-d916a92d99cc.png)

    - Reconstruction Term: Reconstruction loss 줄임
    - Prior Fitting Term: latent space에서의 분포와 사전분포가 비슷하게 만들어주는 것을 만족
    - 단점: prior fitting term이 KL Divergence 활용 → 가우시안이 아닌 경우 활용 어려움

### Adversarial Auto-encoder

![Untitled 7](https://user-images.githubusercontent.com/73166743/107034217-c08e4900-67f9-11eb-878c-68b5f1c87424.png)

- Prior fitting term을 GAN으로 바꿔서 latent distribution 맞춰줌

### GAN

![Untitled 8](https://user-images.githubusercontent.com/73166743/107034219-c126df80-67f9-11eb-84df-66f5b9b17c0c.png)

- discriminator가 점차 좋아진다는게 장점

    → generator가 fix된 discriminator로 학습하는게 아니여서 점점 더 잘 생성함

### DCGAN

- MLP로 만듦
- 이미지 도메인으로 함
- generator: D Conv
- discriminator: Conv
- Leaky ReLU

![Untitled 9](https://user-images.githubusercontent.com/73166743/107034220-c126df80-67f9-11eb-9b9f-e43217f08fe9.png)

### Info-GAN

- G에서 단순히 이미지만 만드는게 아니라 클래스라는 C를 매번 G에 집어넣음

    → generation 할 때 GAN이 특정 모드 (one-hot, conditional)에 집중할 수 있게 만듦

![Untitled 10](https://user-images.githubusercontent.com/73166743/107034222-c1bf7600-67f9-11eb-8b49-a5b2cb5e092f.png)

### Text2Image

- 문장이 주어졌을 때 이미지 만듦

### Puzzle-GAN

- subptch들로 원래 이미지 복원

### CycleGAN

- 이미지 사이의 도메인 바꿀 수 O
- 사진 자료만 잔뜩 있으면 됨

### Star-GAN

- 내가 control 할 수 있게 만듦

### Progressive-GAN

- 4x4, 8x8, ... , 1024x1024 까지 픽셀을 키워서 점진적으로 고해상도 이미지로 늘려나가면서 학습