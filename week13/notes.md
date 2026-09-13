# Week 13 - Generative AI

이번 주차에서는 기존 인공신경망 내용을 복습하고,
순환 신경망(RNN), LSTM, GRU, Transformer,
토큰화와 임베딩, Large Language Model까지 학습했다.

---

# 1차시

## 1. Artificial Neural Network Review

인공신경망은 인간의 신경망 구조를 모방한 모델이다.

기본적인 구조:

- Input Layer
- Hidden Layer
- Output Layer

신경망에서는 입력값을 받아 중간 계산을 수행하고,
그 결과를 다음 Neuron으로 전달한다.

학습의 목적은 원하는 결과를 얻기 위한
적절한 Weight를 찾는 것이다.

Weight는 여러 Iteration 또는 Epoch 동안 반복적으로 업데이트한다.

### Backpropagation

신경망 학습에서는 Loss Function을 이용해 Error를 계산하고,
미분을 통해 Gradient를 구한다.

그 Gradient를 역방향으로 전달하여
각 Weight를 업데이트한다.

전체적인 흐름:

`Input → Prediction → Loss → Gradient → Backpropagation → Weight Update`

## 2. Perceptron Review

Perceptron은 인공신경망의 초기 수학적 모델이다.

### Single-Layer Perceptron

- 하나의 Layer로 구성
- 단순한 선형 분리 문제를 처리
- XOR과 같은 문제는 해결하기 어려움

### Multi-Layer Perceptron

여러 Perceptron을 여러 Layer로 쌓은 구조이다.

Hidden Layer를 추가함으로써
더 복잡한 문제를 처리할 수 있다.

### Activation Function

신경망의 각 Layer에서는
Activation Function을 이용하여 출력값을 결정한다.

어떤 Activation Function을 사용할지에 따라
모델의 특성과 학습 결과가 달라질 수 있다.

## 3. Deep Neural Network

DNN은 **Deep Neural Network**의 약자이다.

여러 개의 Layer를 깊게 쌓아 만든 신경망으로,
대량의 데이터를 이용하여 복잡한 패턴을 학습한다.

신경망이 깊어질수록
앞쪽 Layer까지 Gradient가 제대로 전달되지 않는 문제도 발생할 수 있다.

---

# 4. Recurrent Neural Network

RNN은 **Recurrent Neural Network**의 약자이다.

순차적인 데이터의 관계를 처리하기 위한 신경망 구조이다.

RNN에서는 현재의 Output이
단순히 출력으로만 사용되는 것이 아니라
다음 계산의 Hidden State에도 영향을 준다.

따라서 이전 Sequence의 정보를 이용하여
현재 값을 판단할 수 있다.

예:

- 문장
- 단어 Sequence
- 시간에 따라 변화하는 데이터

언어 모델에서는 입력과 출력의 단위를
Token으로 나누고,
Embedding을 거쳐 Vector 형태로 사용한다.

## 5. Deep RNN

RNN을 여러 Layer로 쌓아
더 깊은 구조로 만들 수 있다.

하지만 Sequence가 길어지면
초기의 정보를 점점 잃어버리는 문제가 발생한다.

이를 **Long-Term Dependency Problem**으로 볼 수 있다.

긴 문장에서는 초반의 중요한 내용을
뒤쪽 계산까지 유지하기 어려울 수 있다.

## 6. LSTM

LSTM은 **Long Short-Term Memory**의 약자이다.

기존 RNN의 장기 의존성 문제를 개선하기 위한 구조이다.

기억해야 할 정보와
버려야 할 정보를 조절하기 위한 Gate를 사용한다.

### Forget Gate

- 불필요한 정보를 제거
- 어떤 정보를 유지하고 어떤 정보를 잊을지 결정

이를 통해 긴 Sequence에서도
중요한 정보를 더 오래 유지하려고 한다.

## 7. GRU

GRU는 **Gated Recurrent Unit**의 약자이다.

LSTM과 마찬가지로
Sequence 정보를 효과적으로 유지하기 위한 구조이다.

LSTM의 여러 Gate를 보다 단순화하여 다음을 사용한다.

- Reset Gate
- Update Gate

필요한 정보를 갱신하면서
Sequence를 처리한다.

---

# 8. Transformer와 자연어 처리

수업에서는 Transformer를
번역과 자연어 처리 맥락에서 다루었다.

자연어를 모델에 입력하기 전에는
여러 전처리 과정이 필요하다.

예:

- 데이터 정제
- 정규화
- 불용어 처리
- Tokenization
- Embedding

## 9. Stopword Processing

불용어 처리는
분석에 큰 의미가 없는 단어를 제거하는 과정이다.

불필요한 Token을 줄여
데이터 처리의 효율을 높일 수 있다.

## 10. Tokenization

Tokenization은 문장을
컴퓨터가 분석할 수 있는 작은 단위인 Token으로 나누는 과정이다.

모델이 인식하는 가장 작은 단위를
Token이라고 볼 수 있다.

### Word Tokenization

공백이나 구두점 등을 기준으로
문장을 단어 단위로 분리한다.

장점:

- 간단함
- 직관적임

단점:

- 희귀 단어 학습이 어려울 수 있음
- Vocabulary가 커질 수 있음
- Memory와 계산 비용이 증가할 수 있음

### Sentence Tokenization

텍스트를 문장 단위로 나눈다.

예:

- `.`
- `!`
- `?`

등의 문장 구분 기호를 이용할 수 있다.

번역이나 요약과 같은
문장 단위 작업에 활용할 수 있다.

언어별 문장 구분 방식의 차이 때문에
처리가 복잡해질 수 있다.

### Character Tokenization

텍스트를 개별 문자 단위로 나눈다.

장점:

- Vocabulary 크기가 작음
- Memory 효율성이 높음
- 다국어 처리에 유리할 수 있음

단점:

- Sequence가 매우 길어질 수 있음
- Model Complexity 증가
- 의미 정보가 줄어들 수 있음

### Subword Tokenization

단어보다 작은 단위로 나누는 방식이다.

모르는 단어를 모두 하나의
OOV(Out Of Vocabulary)로 처리하는 대신,
단어를 여러 Subword로 나누어 표현할 수 있다.

장점:

- 모르는 단어 처리 가능
- 단어의 일부 정보를 이용할 수 있음
- 효율성과 표현 능력을 함께 고려 가능

GPT와 같은 Transformer 기반 모델에서도
Subword 기반 Tokenization을 사용한다.

---

# 11. Embedding

Tokenization이 끝난 텍스트는
모델에서 계산할 수 있도록 숫자 형태로 변환해야 한다.

Embedding은 텍스트 데이터를
실수 Vector 공간으로 변환하는 방법이다.

## 12. One-Hot Encoding

One-Hot Encoding은
각 단어를 서로 독립적인 Vector로 표현한다.

장점:

- 구현이 단순함
- 별도의 학습이 필요하지 않음
- 직관적임

단점:

- 단어 사이의 의미적 유사성을 표현하기 어려움

## 13. Word Embedding

Word Embedding은
단어를 Vector 형태로 표현하면서
단어 사이의 관계를 반영할 수 있도록 한다.

의미가 비슷한 단어는
Vector 공간에서도 어느 정도 가까운 관계를 가질 수 있다.

## 14. Contextual Embedding

Contextual Embedding은
같은 단어라도 문맥에 따라 다른 의미를 표현할 수 있도록 한다.

다의어처럼 하나의 단어가 여러 의미를 가지는 경우에도
문맥을 이용해 의미를 구분할 수 있다.

수업에서 언급한 예:

- BERT
- ELMo

---

# 15. Transformer

Transformer는 Sequence를
순차적으로 하나씩 처리하는 방식 대신
병렬적인 구조를 활용한다.

기본적으로 Encoder와 Decoder 구조를 가진다.

## Encoder

입력 문장을 Vector 형태로 변환하고,
문장에서 중요한 정보를 추출한다.

## Decoder

Encoder에서 만들어진 정보를 이용하여
다시 Text 형태의 출력을 생성한다.

전체 흐름:

`Tokenization → Embedding → Encoder → Vector Representation → Decoder → Output`

## 16. Positional Encoding

Transformer는 여러 Token을 병렬로 처리하기 때문에
Token의 순서를 직접 알기 어렵다.

Positional Encoding을 이용하여
각 Token의 위치와 순서 정보를 추가한다.

이를 통해 모델이 문장의 순서를 고려할 수 있도록 한다.

## 17. Attention Mechanism

Attention은 Transformer의 핵심 개념 중 하나이다.

문장을 처리할 때 모든 단어를 똑같이 보는 것이 아니라,
현재 문제를 해결하는 데 중요한 부분에 더 높은 Weight를 준다.

- 중요한 정보에 높은 Attention
- 중요하지 않은 정보는 상대적으로 낮게 반영

주변 단어와 문맥 정보를 함께 활용하여
각 Token의 의미를 해석한다.

---

# 2차시

## 18. Transformer Structure

Transformer는 Encoder와 Decoder,
Attention Mechanism 등을 이용하여
Sequence 데이터를 처리한다.

여러 Token을 병렬적으로 처리하면서도
Positional Encoding과 Attention을 이용하여
문장 내 관계와 순서를 고려한다.

## 19. Large Language Model

LLM은 **Large Language Model**의 약자이다.

수업에서는 Transformer를 기반으로 하는
대규모 언어 모델을 다루었다.

대량의 데이터와 큰 규모의 모델을 이용하여
언어의 패턴을 학습한다.

## 20. GPT

GPT 계열 역시 Transformer를 기반으로 한다.

수업에서는 GPT-3.5가
일반 사용자들이 실제로 사용할 수 있을 정도의 성능을 보여주면서
ChatGPT 등장으로 이어진 흐름을 다루었다.

## 21. Multimodal AI

생성형 AI는 Text뿐 아니라
여러 형태의 데이터를 함께 처리하는 방향으로 발전하고 있다.

예:

- Text
- Image
- Video

이처럼 여러 종류의 데이터를 함께 다루는 방식을
Multimodal이라고 한다.

## 22. Generative AI의 문제점

수업에서 다룬 대표적인 문제:

- Bias
- Hallucination
- Ethical Issues

### Bias

학습 데이터나 모델의 특성에 따라
특정 방향으로 편향된 결과가 나타날 수 있다.

### Hallucination

모델이 실제 사실과 다른 내용을
그럴듯하게 생성할 수 있다.

### Ethical Issues

생성형 AI의 사용 과정에서는
여러 사회적·윤리적 문제가 발생할 수 있다.

## 23. 해결을 위한 접근

수업에서 다음과 같은 대응 방법을 다루었다.

### Prompt Engineering

모델이 원하는 방향으로 답할 수 있도록
입력 Prompt를 보다 효과적으로 구성하는 방법이다.

### Retrieval Augmented Generation

외부 정보를 검색하거나 가져와
모델의 생성 과정에 함께 사용하는 방식이다.

모델이 추가적인 정보를 참고하도록 하여
더 적절한 답변을 생성하도록 돕는다.

### Policy

기술적인 방법뿐 아니라
AI 사용을 위한 정책과 법적 보호도 필요하다.

---

# 핵심 정리

- 인공신경망은 Weight를 반복적으로 업데이트하며 학습한다.
- Perceptron을 여러 Layer로 쌓으면 더 복잡한 문제를 처리할 수 있다.
- RNN은 이전 Sequence의 정보를 다음 계산에 활용한다.
- 긴 Sequence에서는 장기 의존성 문제가 발생할 수 있다.
- LSTM과 GRU는 이러한 문제를 개선하기 위한 구조이다.
- 자연어 처리를 위해 Tokenization과 Embedding이 필요하다.
- Transformer는 병렬 처리 구조를 사용한다.
- Positional Encoding은 Token의 순서 정보를 제공한다.
- Attention은 문맥상 중요한 정보에 더 높은 가중치를 준다.
- LLM은 Transformer를 기반으로 대규모 언어 데이터를 학습한다.
- 생성형 AI에서는 Bias, Hallucination, 윤리 문제 등을 함께 고려해야 한다.