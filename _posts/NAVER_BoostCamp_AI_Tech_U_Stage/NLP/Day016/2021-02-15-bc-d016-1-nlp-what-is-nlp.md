---
title: "[부스트캠프 AI Tech / Day16] 자연어처리 What is NLP?"
data: 2021-02-15 20:20:00 +0800
categories: [네이버 부스트캠프 AI Tech, NLP]
tags: [DL, NLP]
use_math: True
---


## **[DAY 16] What is NLP?**

---

### NLP?

- NLP: Natural Language Processing
- 인간의 언어를 이해하고 생산할 수 있도록 한, 딥러닝을 이용한 방법

### NLP의 종류

- Low-level parsing
  - Tokenization: 텍스트를 토큰(모델이 이해할 수 있는 최소한의 단위)으로 분리
  - stemming: 어근추출(품사를 제외하여, 의미가 변하지 않는 단어로 뽑기), 원형추출
- Word and phrase level
  - NER(Named Entity Recognition): 여러 단어로 이루어진 고유명사 찾기
  - POS(Part-of-speech) tagging: 품사 혹은 성분 알아내기
- Sentence level
  - Sengiment analysis: 감정분석
  - Machine translation: 번역
- Multi-sentence and paragraph level
  - Entailment prediction: 두 문장간 논리적 내포/관계를 예측, 모순찾기 가능
  - question answering: 독해기반 질의응답, 질문이 포함된 문서를 검색하고, 독해를 통해 질문에 대한 답을 도출
  - dialog systems: 챗봇
  - summarization

### NLP의 트렌드

- 텍스트 데이터는 단어의 시퀀스라고 볼 수 있다. 그리고 각 단어는 Word2Vec, GloVe라는 기술을 통해 벡터로 표현할 수 있다.  
- RNN-family models(LSTM, GRU)는 입력으로 단어의 벡터들의 시퀀스로 이루어져있는 NLP의 주요 taskd이다.
- Attention module과 Transformer model을 통해서 NLP의 성능을 전반적으로 상승시킬 수 있다. 이들은 RNN을 self-attention으로 대채하였다.
- 최근에 각각 다른 NLP task를 위한 커스텀 모델이 빠르게 증가하였다. <span style="color:firebrick">커스텀하는 방법은 어떤것이 있을까?</span>
- Transformer가 소개된 이후로, 아주 큰 모델이 출시되었다. 이들은 추가적인 레이블링이 필요없는, 방대한 데이터셋을 통해 자가지도학습(Self-supervised training)을 진행한다. 예를들어, BERT, GPT-3가 있다.
- 이후에 모델에 전이학습(transfer learning)이 적용되어 커스텀 모델이 증가했다.
- 최근에 이런 모델들이 NLP에 필수가 되면서, 방대한 데이터를 학습하는 것이 필수가 되었다. 따라서 NLP 연구는 한정된 GPU 자원으로 모델을 학습하기에는 무리가 있다는 단점을 가진다.