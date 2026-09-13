# Week 04 - 퍼셉트론

## 1차시 - 벡터와 퍼셉트론

### One-Hot Vector

- 원하는 index 하나만 `1`이고 나머지는 모두 `0`인 벡터이다.

### Identity Matrix

- 주대각선의 값은 `1`이고 나머지 값은 모두 `0`인 정방행렬이다.

### Norm

- 벡터의 크기를 구하는 연산이다.
- 예를 들어 `x = (1, 2, 0, 2)`일 때

  `Norm = √(1² + 2² + 0² + 2²) = 3`

- 벡터를 자신의 Norm으로 나누면 Unit Vector를 얻을 수 있다.

## 2. 퍼셉트론

- 퍼셉트론은 초기 인공지능 연산 모델 중 하나이다.
- 단층 퍼셉트론은 직선 하나로 분리할 수 있는 문제를 다룰 수 있다.
- XOR과 같이 하나의 직선으로 분리할 수 없는 문제에서는 한계가 발생한다.
- 다층 퍼셉트론을 이용하면 XOR 연산과 같은 문제를 해결할 수 있다.
- 초기에는 가중치와 편향을 효과적으로 학습시키는 방법이 부족하여 인공신경망 연구가 침체되기도 했다.

## 3. Artificial Neural Network

ANN(Artificial Neural Network)은 인간의 신경망을 모방한 머신러닝 기법이다.

주요 요소:

- Weight
- Weighted Sum
- Output

활용 분야:

- Classification
- Regression
- Grouping

## 4. 고차원 데이터

- 차원이 증가하면 데이터 포인트 사이의 거리가 커질 수 있다.
- 경우에 따라 데이터를 구분하기 쉬워지고 모델 학습에 도움이 될 수 있다.
- 그러나 차원이 지나치게 높아지면 데이터의 복잡도가 증가하고 학습이 어려워진다.

### Curse of Dimensionality

낮은 차원에서도 해결할 수 있는 문제를 불필요하게 높은 차원에서 다루면 데이터와 모델의 복잡도가 증가할 수 있다.

### Manifold Learning

고차원 데이터가 실제로는 더 낮은 차원의 구조를 가지고 있다고 가정하고,
그 숨겨진 구조를 찾아 차원을 줄이는 방법이다.

## 5. Perceptron Learning

딥러닝 및 퍼셉트론 학습에서는 모델의 Weight 값을 반복적으로 수정한다.

기본적인 과정은 다음과 같다.

1. 초기 Weight를 설정한다.
2. 입력 데이터를 이용해 분류 결과를 확인한다.
3. 잘못 분류된 데이터가 있는지 확인한다.
4. 오류가 발생하면 Weight를 업데이트한다.
5. 이 과정을 반복한다.

## 6. Weight Update

퍼셉트론의 가중치 업데이트 식:

`w' = w + (y_k)(x_k)η`

- `w` : 현재 Weight
- `w'` : 업데이트된 Weight
- `y_k` : 정답값
- `x_k` : 입력 데이터
- `η` : Learning Rate

### Learning Rate

- 학습 과정에서 Weight를 얼마나 크게 변경할지를 결정한다.
- Learning Rate가 작을수록 한 번의 업데이트에서 Weight의 변화량도 작아진다.

## 7. Overfitting

- Training Set에 지나치게 맞춰 학습하면 새로운 데이터에서 성능이 떨어질 수 있다.
- 학습 데이터에만 최적화되지 않고 새로운 데이터에도 잘 동작하도록 학습하는 것이 중요하다.

## Assignment

퍼셉트론의 초기 Weight를 이용해 각 데이터를 분류하고,
잘못 분류된 데이터가 발생할 때 Weight를 반복적으로 업데이트하는 과정을 직접 계산했다.

최종적으로 업데이트된 Weight를 이용해 데이터 분류 경계를 그래프로 나타냈다.

- [HW2 Perceptron Solution](./assignment/HW2_perceptron_solution.pdf)