---
title: "[부스트캠프 AI Tech / Day16] 자연어처리 Naive Bayes Classifier - 문서 분류"
data: 2021-02-15 20:20:00 +0800
categories: [네이버 부스트캠프 AI Tech, NLP]
tags: [DL, NLP]
use_math: True
---


## **[DAY 16] Naive Bayes Classifier - Document Classification*

---

### Naive Bayes Classification?

- 특성들 사이의 독립을 가정하는 베이즈 정리를 적용한 확률 분류기
- 나이브 베이즈 분류기에서 모든 특성 값은 서로 독립임을 가정한다.
- MLE(Maximum Likelihood Estimation, 최대우도방법)을 사용
- 지도학습에서 효율적이며, 파라미터 추정을 위한 학습데이터의 양이 적어도 가능하다.
- 간단한 디자인에도 불구하고 복잡한 실제상황에서도 꽤 잘 동작한다.