# Week 11 - MNIST 분류 모델 비교 실습

이번 주차에서는 MNIST 손글씨 숫자 데이터셋을 이용하여
여러 딥러닝 모델을 학습하고 성능을 비교했다.

비교한 모델은 다음과 같다.

- 기본 MLP 모델
- Hidden Layer를 추가한 MLP 모델
- CNN 기반 LeNet 모델

각 모델을 Epoch 30까지 학습한 뒤
정확도와 Loss 변화를 확인했다.

## 1. 기본 MLP 모델

기본적인 MLP(Multi-Layer Perceptron) 모델을 이용하여
MNIST 이미지 분류를 수행했다.

학습 과정에서 다음 결과를 확인했다.

- Epoch : 30
- Accuracy : 약 97.66%
- Training / Validation Accuracy 확인
- Training / Validation Loss 확인

학습이 진행될수록 Accuracy는 증가하고
Loss는 감소하는 모습을 확인했다.

## 2. Hidden Layer 추가

기본 MLP 모델에 Hidden Layer를 추가하여
네트워크의 깊이를 증가시켰다.

결과:

- 기본 MLP : 약 97.66%
- Hidden Layer 추가 : 약 98.06%
- Accuracy 약 0.4%p 향상

Hidden Layer가 추가되면서
모델이 더 복잡한 특징을 학습할 수 있게 되었다.

각 Hidden Layer에서는 `tanh`와 같은
Non-Linear Activation Function을 사용하여
단순한 선형 관계보다 복잡한 패턴을 표현할 수 있다.

따라서 Network가 깊어지면서
비선형적인 Decision Boundary를 보다 효과적으로 학습할 수 있었다.

## 3. CNN - LeNet

CNN(Convolutional Neural Network) 구조인
LeNet 모델을 이용해서도 MNIST 분류를 수행했다.

결과:

- 기본 MLP : 약 97.66%
- LeNet : 약 99.32%
- Accuracy 약 1.66%p 향상

세 모델 중 LeNet이 가장 높은 정확도를 보였다.

## 4. MLP와 CNN의 차이

### MLP

MLP는 `28 × 28` 형태의 이미지 데이터를
1차원 Vector로 펼쳐 입력한다.

이 과정에서는 원래 이미지가 가지고 있던
2차원 공간 구조에 대한 정보가 줄어들 수 있다.

### CNN

CNN은 이미지의 2차원 구조를 유지한 상태에서
Convolution Layer를 이용한다.

Kernel(Filter)이 이미지 영역을 이동하면서
지역적인 특징을 추출한다.

이를 통해 다음과 같은 이미지 특징을 효과적으로 학습할 수 있다.

- Edge
- Shape
- Local Pattern

## 5. Weight Sharing

CNN에서는 하나의 Filter가 이미지 전체를 이동하면서
동일한 Weight를 공유한다.

따라서 모든 위치에 각각 다른 Weight를 사용하는 것보다
필요한 Parameter 수를 줄일 수 있다.

장점:

- 학습 효율 향상
- Parameter 수 감소
- Overfitting 위험 감소

## 6. Pooling

Pooling Layer는 Feature Map의 크기를 줄인다.

이를 통해 이미지의 위치가 조금 바뀌거나
일부 변형이 발생하더라도 비슷한 Feature로 인식할 수 있도록 한다.

즉, 위치 변화에 대한 민감도를 줄이고
일정 수준의 불변성을 확보할 수 있다.

## 7. Model Comparison

| Model | Accuracy |
|------|---------:|
| Basic MLP | 97.66% |
| MLP + Hidden Layer | 98.06% |
| LeNet (CNN) | 99.32% |

실습 결과 Network의 구조를 변경하면서
MNIST 분류 성능이 향상되는 것을 확인했다.

특히 이미지 데이터에서는
2차원 구조와 지역적인 특징을 활용할 수 있는 CNN이
기본 MLP보다 더 높은 성능을 보였다.

## Report

- [MNIST Model Comparison Report](./report/mnist_model_comparison_report.docx)