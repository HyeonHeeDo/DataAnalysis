# BERT
* 구글이 공개한 인공지능 언어모델
* 큰 텍스트 이해 → 언어 이해 모델 훈련 → 모델을 통한 실제 자연어 처리 (질문, 응답 등)에 적용
* 보통의 텍스트 corpus만 이용해 훈련
* 문맥에 의존하는 특징적인 표현 반영

***
### __BERT 입력 임베딩 = Token + Segment + Position__  
__1. Token Embeddings__
* Word Piece 임베딩 방식을 사용
  - 자주 등장하면서 가장 긴 길이의 sub-word를 하나의 단위로 만든다  
  (자주 등장하는 sub-word 자체가 하나의 단위가 됨)
  - 자주 등장하지 않는 단어는 sub-word로 쪼개어진다.
  - Out-Of-Vocabulary (처음 접하는 단어)에 대한 학습 및 처리에 효과적
  
__2. Sentence Embeddings__
* 두 개의 문장을 문장 구분자와 함께 합쳐서 넣음

__3. Position Embeddings__
* Self-Attention 모델 사용
* Positon encoding 통해 토큰 순서대로 인코딩 진행

***
### __BERT 프로세스__

__1. Pre-training__ 언어 모델링
* 거대 encoder가 입력 문장들을 임베딩하는 언어 모델링
* 스스로 라벨을 만들고 수행하는 준지도학습
* Transformer 구조 기반 encoder-decoder 모델  
* 1. __MLM__ Masked Language Model
    - 입력 문장에서 임의로 토큰 masking 후, 해당 토큰 맞추는 방식으로 학습 (예)문장의 빈칸 채우기 문제 학습
    - 다음에 올 단어를 예측하는 것이 아니라, random 단어를 마스킹한 후 해당 단어를 예측
    - 한국어의 경우 : 형태소 단위로 쪼개서 masking하는 방법이 효과적  
* 2. __NSP__ Next Sentence Prediction
    - 두 문장이 주어졌을 때, 두 번째 문장이 첫 번째 문장의 바로 다음에 오는 문장인지 여부를 예측  
      (연속 문장인지 아닌지만 판단)

__2. Fine-Tuning__ 전이학습 (Transfer Learning)
* 자연어 처리 task 수행
* 라벨이 주어지는 지도학습
* BERT의 언어 모델 출력에 추가적인 모델을 쌓는 과정  
* 사용 예시  
  * 두 문장간의 관계 구하기
  * 한 문장 입력 후 문장 종류 분류류
  * 문장/문단 내에서 원하는 정답의 시작, 끝 위치 찾기
  * 입력 문장 토큰들의 개체명/품사 구하기 (입력된 모든 토큰들에 대한 결과 구함)
