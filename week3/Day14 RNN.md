# Day14 RNN

## RNN

### Sequence data

- 소리, 문자열, 주가 등의 데이터가 시퀀스 데이터
- 순서 바꾸면 과거 정보 손실 → 데이터 확률 분포 바뀜
- 데이터의 확률 분포
    - S = 1 인 초기시점부터 바로 직전인 S-1까지의 정보를 사용해서,

        현재 시점은 Xs를 모델링

    - 시퀀스 데이터를 분석할 때 모든 과거 정보들이 필요한 것은 X

    ![Untitled](https://user-images.githubusercontent.com/73166743/106902654-6b403200-673c-11eb-939b-6f4801b9e34d.png)

- 길이가 가변적인 데이터를 다룰 수 있는 모델 필요
    - 모델링 하기 전에 사전에 결정
    - 하나의 모델 안에서 t 계속 바꿀 수 있음
    - 이전 정보를 제외한 나머지 정보들을 Ht 라는 잠재변수로 인코딩

        2가지 데이터 ⇒ 가변적이지 않고 고정된 길이의 데이터가 됨

![Untitled 1](https://user-images.githubusercontent.com/73166743/106902690-75623080-673c-11eb-8854-232bfbb8fa6c.png)

### RNN 식

- W들은 t에 따라서 변하지 않는 가중치 행렬
- Ht는 현재 시점의 잠재 변수
- Ht-1 는 이전 벡터로부터 정보 전달
- 빨간색 선이 Gradient로 2개가 들어가게 됨

![Untitled 2](https://user-images.githubusercontent.com/73166743/106902704-77c48a80-673c-11eb-8349-7ce6f65dd912.png)

### BPTT

- 시퀀스 길이가 길어질 수록 빨간 박스 항이 불안정해지기 쉬운 이유는?

    이 값이 1보다 커지게 되면 엄청 커지기 때문, 1보다 작게 되면 굉장히 작은 값이 됨

    → 길이를 끊는 것이 필요 (기울기 소실되면 과거 정보 유실 될 수 O)

- truncated BPTT
    - 미래의 정보 중에서 몇개는 gradient 끊고, 과거의 정보에 해당하는 몇개의 블럭을 나눠

        Back prop 계산

![Untitled 3](https://user-images.githubusercontent.com/73166743/106902707-785d2100-673c-11eb-94fd-dc65eef899e8.png)

## Sequential Models

### Autoregressive model

- 과거의 몇개만 보자

![Untitled 4](https://user-images.githubusercontent.com/73166743/106902711-78f5b780-673c-11eb-9845-7dc0b8e363be.png)

### Markov model

- 현재는 바로 직전 과거에만 dependent 함 (많은 정보 버리는 단점 갖고 있음)

![Untitled 5](https://user-images.githubusercontent.com/73166743/106902714-798e4e00-673c-11eb-83a9-17218a87db60.png)

### Latent autoregressive model

- Hidden state : 과거의 정보를 요약하고 있음

![Untitled 6](https://user-images.githubusercontent.com/73166743/106902718-798e4e00-673c-11eb-8e93-e886a402da6d.png)

### RNN

- ht는 Xt에만 dependent한게 아니라 이전 t-1에서 얻어진 cell state에 dependent
- 시간상으로 이렇게 풀면 입력이 아주 많은 fully connected layer로 표현됨
- Short-term dependencies
    - 내가 과거에 얻어지는 정보들이 다 취합돼서 미래에서 고려해야 하는데,

        과거의 정보가 미래까지 살아남기 어려움

- Long-term dependencies
    - X0의 정보가 ht+1까지 유지됨
    - 하지만 이는 sigmoid → Vanishing, ReLU → Exploding Gradient 문제가 있음

![Untitled 7](https://user-images.githubusercontent.com/73166743/106902720-7a26e480-673c-11eb-837d-08141979afec.png)

### Long Short Term Memory

- Core idea : 어떤 정보가 유용한지 조작
- Previous cell state

    LSTM 밖으로 나가지 X, 지금까지 들어온 정보를 다 취합, 요약

- Forget Gate

    sigmoid로 0~1 값만 가짐, 어떤 정보를 버릴지 결정

- Input Gate
    - it : 어떤 정보를 cell state에 추가할지
    - Ct(C tilda) : 현재 정보와 이전 출력값을 가지고 만드는 cell state 예비군
- Update cell

    지금까지 time sequence를 요약하는 cell state를 업데이트 함

- Output Gate

    어떤 값을 밖으로 내보낼지 해당하는 output gate 만들고 그만큼 곱해서 Next Ht로 흘러가게 만듦

- 결론

    이전까지 들어온 정보를 현재 입력 바탕으로 지울지 혹은 새롭게 쓸지 이 두 정보를 취합하는게 update cell,

    이 취합된 cell state를 한번 더 조작해서 어떤 값을 밖으로 빼낼지 정함

![Untitled 8](https://user-images.githubusercontent.com/73166743/106902722-7abf7b00-673c-11eb-99da-999622e2a84f.png)

### GRU (Gated Recurrent Unit)

- Reset Gate : 가장 왼쪽 X
- Update Gate: 두번째 sigmoid 통과해서 두갈래로 나옴
- cell state 없고 hidden state 있음 (이게 곧 output)

![Untitled 9](https://user-images.githubusercontent.com/73166743/106902723-7b581180-673c-11eb-8659-14d2184c2234.png)

## Transformer

- 재귀가 아니라 한번에 다 받아들임
- 이미지 분류에도 사용
- sequnce to sequence
- 입력 seq와 출력 seq 수가 다를 수 있음
- 입력 seq 도메인과 출력 seq 도메인 다를 수 O
- 모델은 하나

### Encoder

![Untitled 10](https://user-images.githubusercontent.com/73166743/106902725-7b581180-673c-11eb-8e99-aa17ea0089da.png)

- 3개의 단어가 들어가든 100개의 단어가 들어가든 한번에 encoding 가능

    generation 할 때는 한 단어씩 autoregressive 함

- 동일한 구조를 가지고 있지만 네트워크 파라미터가 다르게 학습됨
- Feed Forward NN
    - MLP와 비슷
    - dependency 없이 그냥 각각에 대해 조정하여 통과시킴
- Self attention!!!!
    
    - X1 → Z1으로 갈 때 단순히 X1의 정보만 활용하는 것이 아니라 X2, X3의 정보 모두 활용

![Untitled 11](https://user-images.githubusercontent.com/73166743/106902726-7bf0a800-673c-11eb-9596-5355b884f4f7.png)

- 각각 임베딩된 단어에서 Query, Key, Value 벡터 계산
- score : i번째 단어가 나머지 단어와 얼마나 유사도가 있는지, 관계가 있는지 봄 (학습)
- 이후 해당 값을 Key vector의 dim으로 나누어 Normalize
- 이후 softmax를 통해 합이 1이 되게 만듦, Value vector와 weighted sum
- Queris, Keys는 항상 차원이 같아야 함
- Value는 위와 차원 달라도 됨, 그렇지만 thinking이라는 단어의 인코딩된 차원은 같아야함
- Positional Encoding

    순서대로 넣는다고 순서의 의미를 파악하지는 못함

### Computation Cost = N^2

- N개의 단어를 한번에 처리함
- 단점

    메모리 많이 먹고 계산에 한계 존재

- 장점

    MLP, CNN은 Input이 고정되어 있으면 Output도 같이 고정되어 있음 (w, filter 고정이여서)

    하지만 Transformer는 Input이 고정되어 있더라도 내가 이 encoding 하려는 단어와 

    그 옆에 있는 단어들에 따라서 인코딩된 값이 달라짐! → Flexible !!

### Multi-Headed Attention

- 앞에서 했던 attention 여러번
- 하나의 임베딩된 벡터에 대해 Q, K, V 여러개 만듦

### Decoders

![Untitled 12](https://user-images.githubusercontent.com/73166743/106902727-7bf0a800-673c-11eb-84cd-9d877bcdc58a.png)

- 생성
- Key, Value 전달
- autoregressive 방식으로 하나의 단어씩 만들게 됨
- 학습할 때 마스킹 : 이전 단어들만 dependent하고, 뒤는 independent, 미래에 있는 정보 활용X
- Encoder-Decoder Attention

    지금까지 generation된 단어들을 가지고 query 만들고 K, V는 Input raw sequence에서 나오는 ecode벡터로 활용

- 마지막 층에서는 단어들의 분포를 만들어서 그 중에 단어 하나를 매번 샘플링 함