---
title: "[부스트캠프 AI Tech / Day14] 딥러닝 기초 RNN"
data: 2021-02-04 20:20:00 +0800
categories: [네이버 부스트캠프 AI Tech, DeepLearning_Basic]
tags: [DL, ML]
use_math: True
---


## **[DAY 14] RNN**

---

- 이전까지는 이미지/벡터에 관한것이었음
- MLP: 벡터 ➡ 벡터를 바꾸는 것
- CNN: 이미지를 원하는 형태로 만들어줌
  - classification: 이미지 ➡ 원핫벡터, 클래스
  - detection: NN의 출력값이, 각 영역의 bounding box를 찾음
  - sementic segmentation: 픽셀별로 어떤 클래스에 속하는지 알려줌
- RNN: 입력자체가 sequential data

### **Sequential Model**

- sequential data를 처리하는데 있어서 가장 큰 어려움
  - 얻고싶은 것: 하나의 라벨, 어떤 하나의 정보
  - 그러나 sequential data는 데이터 특성상, 길이가 언제 끝날지 모름
  - ➡ 받아들여야하는 차원의 개수를 알기 어려움
  - 그래서 이전의 네트워크를 사용하기 어려움
  - ➡ 몇 개의 입력이 들어오는지에 상관없이 잘 동작해야한다는 문제점이 있음

#### Naive sequence model

![3](/assets/img/sources/2021-02-04-12-40-05.png)

- 입력이 들어왔을 때, 다음번 입력을 예측하는 것
- 이전의 입력값들을 고려하여 출력값을 도출
- 고려해야하는 과거의 정보들이 점점 늘어남

#### Auto regressive model

![4](/assets/img/sources/2021-02-04-12-40-17.png)

- 가장 쉽게할 수 있는 방법: 내가 확인할 과거의 개수(범위)를 정함
- 현재로 부터 과거 몇개(time span)만을 고려하기

#### Markov model (first-order auto regressive model)

![5](/assets/img/sources/2021-02-04-12-41-33.png)

- Markov assumption을 가짐
- MDP(Markov Decision Process) in 강화학습 ➡ 이와 같음
- Markovian Property의 가장 큰 특징: 내가 가정을 하기에, 나의 현재는 (바로 직전) 과거에만 dependent
  - 옳지않음 예제) 수능점수는 수능전날에 결정됨
- 따라서, 이 모델은 과거의 정보를 다수 버리게 됨
- joint distribution이 굉장히 쉬워짐
- 문제: 사실, 과거에 일어났던 어느정도의 사건들이 현재에 계속 영향을 미치는데, 마코브 모델은, 이를 반영하지 못함

#### Latent auto regressive model

![6](/assets/img/sources/2021-02-04-12-41-57.png)

- 과거의 정보를 고려하기 위함
- 중간에 hidden state가 들어가있음
- 이 **hidden state가 과거의 정보를 요약**하고 있음
- 다음 time step은 이 hidden state 하나에만 dependent
- output model만 봤을 때는 하나의 과거 정보에만 dependent 함
- 그러나 하나의 과거와, 과거 이전의 정보들을 요약하는 hidden state라고 생각하는 것 (latent state)
- latent space를 어떻게 만드느냐에 따른 차이가 있을 것

---

### Recurrent Neural Network

![9](/assets/img/sources/2021-02-04-12-42-27.png)

- MLP와 다 똑같은데, 자기 자신으로 돌아오는 구조가 하나 더 있는 것
- 나의 $H_t$ (Hidden state에서의 time step $t$ 시간에서의 hidden state)는 $x_t$에만 dependent한 것이 아니라, 이전 $t-1$ 에서 얻어진 어떤 cell state에 dependent하게 됨
- 오른쪽 구조) 시간순으로 풀어서 그린 것
- 내가 현재 $t$ 시간에 있다고 하면, 내가 보고 있는 값들 중 하나는 $t-1$ 시간대에서 넘어온 정보 ➡ 이걸 그냥 시간순으로 풀어서 작성한 것
- ✔ 중요: recurrent 구조를 사실상 시간순으로 풀면, 입력이 굉장히 많은 Fully Connected Layer로 표현 가능
- 이렇게 푸는게 학습하는 것과 같음 -?

> time span을 fix하고, 시간순으로 풀게 되면, 결국에는 각 네트워크가 파라미터를 쉐어하는 굉장히 큰 네트워크가 됨

#### Short-term dependencies

![10](/assets/img/sources/2021-02-04-12-43-00.png)

- 과거에 얻어진 어떤 정보들이 다 취합되어, 미래에서 그것을 고려해야함
- RNN은 고정된 규칙으로 이 정보들을 계속 취합하므로, 과거의 정보가 미래까지 살아남기가 어려움
- step 직전의 정보는 잘 전달이 되는데, 더 이전의 정보는 전달이 안되는 문제
- RNN에서 Short term를 찾아볼 수 있지만 Long term은 잘 찾아볼 수 없음

#### Long-term dependencies

![11](/assets/img/sources/2021-02-04-12-43-29.png)

위의 문제(과거의 정보손실)를 해결하기 위해서 LSTM 같은 것들이 나타남

#### RNN의 식

![12](/assets/img/sources/2021-02-04-12-44-02.png)

시간에 대해서 식을 풀게 되면(one row? unrow?)


---

### Long Short Term Memory

#### RNN

![14](/assets/img/sources/2021-02-04-12-44-34.png)

#### Long Short Term Memory

![15](/assets/img/sources/2021-02-04-12-44-57.png)

![16](/assets/img/sources/2021-02-04-12-45-26.png)

#### Core idea

![17](/assets/img/sources/2021-02-04-12-46-06.png)

![18](/assets/img/sources/2021-02-04-12-46-31.png)

![19](/assets/img/sources/2021-02-04-12-46-52.png)

#### 요약

![20](/assets/img/sources/2021-02-04-12-47-16.png)

---

### Gated Recurrent Unit

![21](/assets/img/sources/2021-02-04-12-47-45.png)

Simpler architecture with two gates (reset gate and update gate)
No cell state, just hidden state