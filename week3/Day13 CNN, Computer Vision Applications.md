# Day13 CNN, Computer Vision Applications

## CNN

![Untitled](https://user-images.githubusercontent.com/73166743/106901655-6333c280-673b-11eb-8f23-1bbaf1fa3982.png)

- RGB Image Convolution

![Untitled 1](https://user-images.githubusercontent.com/73166743/106901688-6af36700-673b-11eb-9350-9f91ea5f1f28.png)

### CNN

- deep하게, parameter 수는 적게
- conv, pooling layers : feature extraction
- fully connected layer: decision making
- 내가 학습해야하는 파라미터의 숫자가 늘어날 수록 학습이 어렵고, generalization performance 떨어짐 (Test 데이터에 대한 동작)
- 어떤 NN을 볼 때 네트워크의 레이어 별로 몇개의 파라미터로 이루어져 있고, 전체 파라미터의 개수가 몇개인지 바로 알아야 함
- Stride: 건너 뛰는 칸 수
- Padding: 가장자리 conv operating 되게 인풋 테두리 늘림
- 각각의 커널의 채널 크기는 Input과 dim과 똑같음

![Untitled 2](https://user-images.githubusercontent.com/73166743/106901706-6e86ee00-673b-11eb-84c3-57d8f4a46a85.png)

### Exercise

![Untitled 3](https://user-images.githubusercontent.com/73166743/106901713-7050b180-673b-11eb-9aff-c6f1005dc654.png)

- 48*2 → 96으로 해야했는데 GPU 2개 쓸 때 안에 개수 다르므로 *2 해줌

![Untitled 4](https://user-images.githubusercontent.com/73166743/106901718-721a7500-673b-11eb-9f65-1b7c5a1a3a73.png)

- dense layer : MLP, fully connected
- 13 * 13 * 128 * 2 ⇒ Input의 뉴런의 개수 (13은 채널의 값, 128은 채널 숫자)
- 2048 * 2 ⇒ Output의 뉴런 개수
- conv과 FC 간의 파라미터 수가 차이가 나는 이유는?
    - conv의 kernel은 shared parameter 이므로!!

### 1x1 Convolution

- Dimension(채널) 줄임
- conv layer를 깊게 쌓으면서 parameter 줄일 수 O

### 트렌드

- NN의 성능을 올리기 위해서 parameter를 줄이는게 중요하기 때문에

    뒷단에 있는 FC를 최대한 줄이고 앞단의 conv layer를 깊게 쌓는게 트렌드

## Modern CNN

### ILSVRC

- ImageNet Large-Scale Visual Recognition Challenge

### AlexNet

![Untitled 5](https://user-images.githubusercontent.com/73166743/106901729-73e43880-673b-11eb-8fa2-00913c37d51c.png)

- ReLU → Non-Linear, gradient Vanishing 줄임
- 2 GPUs
- Local response normalization(어떤 입력공간에서 response가 많이 나오면 몇개 죽임)
- Data augmentation
- Dropout

### VGGNet

![Untitled 6](https://user-images.githubusercontent.com/73166743/106901743-76469280-673b-11eb-8ea8-63f06b92fba6.png)

- 3x3 커널 사용
    - Receptive field: 내가 하나의 conv 피쳐맵 값을 얻기 위해서 고려할 수 있는 입력의 spatial dim
    - 커널의 크기가 커짐으로써 가지는 이점: 하나의 conv 필터를 찍었을 때 고려되는 Input의 크기가 커짐
- fully connected에서 1x1
    - 1x1 conv는 채널(tensor의 depth 방향) reduction 효과 O → parameter 숫자 줄일 수 O
- Dropout
- VGG16, VGG19

### GoogLeNet

![Untitled 7](https://user-images.githubusercontent.com/73166743/106901745-7777bf80-673b-11eb-94cc-d9a8e74da548.png)

![Untitled 8](https://user-images.githubusercontent.com/73166743/106901749-78105600-673b-11eb-8854-5bfaa55933de.png)

- Network In Network 구조
- Inception block
    - 1x1 (파라미터 수 30%까지 줄임)
    - 하나의 입력에 대해서 여러 개의 receptive field를 가지는 것을 거치고 이걸 통해서 여러 개의 response들을 합치는 효과도 있지만 가장 큰 효과는 파라미터 줄임!!!
    - 채널 방향으로 dim을 줄이는 효과 O

### ResNet

![Untitled 9](https://user-images.githubusercontent.com/73166743/106901753-78a8ec80-673b-11eb-881e-afe06521a9ed.png)

- f(x): NN의 출력값 or conv 레이어
- NN 깊게 쌓을 수 있음

![Untitled 10](https://user-images.githubusercontent.com/73166743/106901755-78a8ec80-673b-11eb-9735-e3f4c77c225b.png)

- 1x1 하는 이유: 차원이 다를까봐 맞춰주기 위해서

![Untitled 11](https://user-images.githubusercontent.com/73166743/106901759-79418300-673b-11eb-9846-e755d9790dda.png)

- 1x1, 256 : 채널 늘림
- 1x1, 64 : 채널 줄임

### DenseNet

![Untitled 12](https://user-images.githubusercontent.com/73166743/106901761-79418300-673b-11eb-9580-e6c056ce8a88.png)

- 더하기 대신에 concatenation 함
    - 피쳐맵 더하는 대신에 쌓으면서 좋은 성능 냄
- 문제 발생: 채널 증가 → 파라미터 수 증가 → 그럼 중간에 하나씩 줄이자!!
    - Transition Block (dim 감소)
        - BatchNorm → 1x1 Conv → 2x2 AvgPooling

## Computer Vision Applications

### Fully Convolutional Network

- dense Layer 없애고 싶음!
- conv로 하는데 flatten+dense랑 파라미터 개수 같음
- Input 이미지와 상관없이 네트워크가 돌아갈 수 O
    
    - Input의 Spatial dim에 Independent 함
- Output이 커지면 그것과 비례해서 뒷단의 네트워크가 커짐

    (conv가 가지는 shared parameter 특징 때문)

![Untitled 13](https://user-images.githubusercontent.com/73166743/106901766-79da1980-673b-11eb-925a-d7467aacca0d.png)

### Deconvolution (conv transpose)

- 엄밀한 역은 아니지만 출력의 느낌은 비슷

![Untitled 14](https://user-images.githubusercontent.com/73166743/106901770-7a72b000-673b-11eb-9295-c241c0f932f3.png)

### Detection

- R-CNN

    1) Input img에서 2000개의 바운딩 박스 뽑음

    2) 똑같은 크기로 맞춤

    3) CNN에 다 통과시킴

    4) SVM으로 분류

    - 문제: 이미지 안에서 하나의 바운딩 박스를 2000개 치면 2000개를 다 CNN에 통과시켜야 함

![Untitled 15](https://user-images.githubusercontent.com/73166743/106901775-7a72b000-673b-11eb-9ff3-27ab30ab1dae.png)

- SPPNet
    - 이미지 안에서 CNN 한번만 돌리자!

    1) 이미지 안에서 바운딩 박스 뽑음

    2) 이미지 전체에 대해서 conv 피쳐 맵을 만듦

    3) 뽑힌 바운딩 박스에 해당하는 conv 피쳐맵의 텐서만 뜯어온다.

    ![Untitled 16](https://user-images.githubusercontent.com/73166743/106901780-7b0b4680-673b-11eb-8bc5-1b94c37924eb.png)

- Fasc R-CNN
    - ROL pooling으로 고정길이 피쳐 뽑음
    - bbox regressor : 바운딩 박스를 어떻게 움직여야 좋을지 라벨 찾음
    - 바운딩 박스를 뽑아내는 것도 학습을 하자! (물체가 있는지, 의미가 있는지)

![Untitled 17](https://user-images.githubusercontent.com/73166743/106901784-7ba3dd00-673b-11eb-9bf1-b97d221610e5.png)

- Region Proposal Network
    - k anchor boxes : 미리 정해놓은 Bounding box 크기 k개

    ![Untitled 18](https://user-images.githubusercontent.com/73166743/106901788-7c3c7380-673b-11eb-82e5-dc99c05a2168.png)

    ![Untitled 19](https://user-images.githubusercontent.com/73166743/106901792-7c3c7380-673b-11eb-87f8-5de7ce1c9b83.png)

    - fully conv: conv feature map의 모든 영역을 돌아가면서 찍음

        → 해당하는 영역에 있는 이미지에 물체가 있는지 들고 있게 됨

    - 9: 3개의 다른 사이즈를 3개의 다른 비율로 영역 정함 (128, 256, 512), (1:1, 1:2, 2:1)
    - 4: 바운딩 박스를 얼마나 키우고 줄일지 (W, H, X, Y)
    - 2: 해당 바운딩 박스가 쓸모가 있는지 (box classification)
- YOLO
    - 바운딩 박스 치는거랑 클래스 찾는 것을 동시에 함
    - 이미지 안에 내가 찾고 싶은 물체의 중앙이 해당 grid 안에 들어가면

        그 그리드 셀이 해당 바운딩 박스에 있는 물체와 그 해당 물체가 무엇인지 같이 예측 필요

        ![Untitled 20](https://user-images.githubusercontent.com/73166743/106901795-7cd50a00-673b-11eb-8ada-36595e5b35c3.png)