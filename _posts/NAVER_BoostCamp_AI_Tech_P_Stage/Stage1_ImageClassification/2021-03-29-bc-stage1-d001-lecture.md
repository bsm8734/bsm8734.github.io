---
title: "[부스트캠프 AI Tech / P Stage1] Lecture1 - competition?"
data: 2021-03-29 20:30:00 +0800
categories: [네이버 부스트캠프 AI Tech (P stage), (P stage 1) Image Classification]
tags: [CV, ImageClassification]
---


## **[P Stage 1 - 이미지 분류] Competition, EDA**

---

- U stage
  - 데이터 사이언스 기본지식 학습
  - 머신러닝, 딥러닝 이론 학습
  - 파이썬 및 딥러닝 프레임워크 기초
- P stage
  - 경진대회를 통한 프로젝트 실습
  - 실습 위주의 practical skills 학습
  - 전처리, 학습, 추론까지의 전체적인 과정

---

### P stage Goal

- U stage에서 경험한 이론을 바탕으로 실제 데이터와 코드 베이스를 통한 이해
- competition 형태의 실습을 통해 점진적인 모델 성능 향상을 경험
- 머신러닝 파이프라인의 한 부분을 경험

### Competition이란?

- 주어진 데이터를 통해 원하는 결과를 얻기 위해 여러 사람들이 공모하는 것
- 문제를 제기한 이유를 통해 방향성을 찾아놓으면, 추후 의사결정 시에 도움이 됨
  - "발생 이유, 어떤 문제가 있는지, 왜 안되는지" 잘 확인할 것!

### 문제 정의(Problem Definition)

- 내가 지금 풀어야하는 문제가 무엇인가?
- 이 문제의 input과 output은 무엇인가?
- 이 솔루션은 어디서 어떻게 사용되는가?

#### Data Description

- field의 의미를 알면, 빠르게 목적에 맞게 수렴 가능
- 데이터 스펙 요약본!
- 의료데이터 같은 경우, 배경지식이 필요하므로, description 읽는 것은 필수!

#### Discussion

- competition는 여러 사람이 공모하여, 원하는 결과를 얻기 위함이다.
- 따라서 경험을 공유하고 지식을 공유하는 등의 discussion은 매우 가치있는 일이다.

### 머신러닝 파이프라인

1. Domain Understanding ✔️
2. Data Mining
3. Data Analysis ✔️
4. Data Processing ✔️
5. Modeling ✔️
6. Training ✔️
7. Deploy

> Competition Scope: ✔️ 해놓은 과정을 모두 경험할 수 있음

---

## EDA(Exploratory Data Analysis)

- 데이터 자체로는 의미를 알기 어려움
- 데이터의 특징을 알고, 왜 주어졌는지 알아야 문제 해결가능
- 따라서 EDA는 데이터를 이해하기 위한 노력이다!
- 같은 데이터이더라도, 주제/output이 다르므로 다르게 해석해야한다.
- 이 데이터를 왜 줬는지 생각해보기!

### EDA의 목적

- EDA가 어려운 이유
  - 너무 어렵게 생각해서!
  - 정답이 있는지, 맞을지, 틀리면 어떡하지... 이런 고민들을 하곤 함
- EDA의 진짜 목적은 궁금한 것을 알아보기 위해 탐색하는 것!
- EDA는 데이터를 확인/이해하는데 사용되는 도구일 뿐
- 결국 거창한 분석결과보다는 나의 궁금증을 해결하는 것에 초점을 두면 된다.
- 데이터를 보고 궁금한 것을 해결하고, 내 방식대로 데이터를 해석해본다!

---

### Baseline

1. Domain Understanding
2. Data Mining
3. Data Analysis ✔️
   - EDA
4. Data Processing ✔️
   - dataset
   - pre-processing
   - generator
   - augmentation
5. Modeling ✔️
   - torch model
   - prerained model
   - loss, opt, metric
6. Training ✔️
   - training process
   - ensemble
7. Deploy
