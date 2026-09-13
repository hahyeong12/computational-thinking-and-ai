# Week 08 - Learning Techniques 2

## 1차시 - Activation Functions

## 1. Activation Function

각 Neuron은 입력을 받은 후
Weighted Sum을 계산하고 Activation Function을 거쳐
출력을 다음 Layer로 전달한다.

전체 흐름:

`Input → Weighted Sum → Activation Function → Output`

Activation Function의 중요한 역할은
신경망에 Non-Linearity를 추가하는 것이다.

이를 통해 신경망이 더 복잡한 패턴을 학습할 수 있다.

## 2. Sigmoid Activation

Sigmoid Function은 출력값을 `0 ~ 1` 사이로 만든다.

특징:

- 모든 지점에서 미분 가능
- Gradient 계산 가능
- 출력값을 `0 ~ 1` 범위로 압축
- 출력값을 확률과 비슷하게 해석할 수 있음

하지만 여러 단점도 존재한다.

## 3. Vanishing Gradient

Sigmoid 그래프의 양 끝에서는 기울기가 거의 `0`에 가까워진다.

입력값이 특정 범위를 벗어나면
Gradient가 매우 작아지게 된다.

이 상태가 여러 Layer에 걸쳐 반복되면
Backpropagation 과정에서 앞쪽 Layer로 전달되는 Gradient가 점점 작아진다.

결과적으로 학습이 제대로 진행되지 않을 수 있다.

이를 Vanishing Gradient라고 한다.

## 4. Not Zero-Centered

Sigmoid의 출력은 항상 양수이다.

따라서 다음 Layer로 전달되는 값 역시 양수가 된다.

이 경우 Weight Gradient의 방향이 제한될 수 있고,
최적의 Weight를 찾는 과정에서 지그재그 형태의 비효율적인 이동이 발생할 수 있다.

실제 Weight Update에서는

- 어떤 Weight는 증가
- 다른 Weight는 감소

하는 식으로 서로 다른 방향의 업데이트가 필요할 수 있다.

## 5. Saturated Neuron

Activation Function의 출력값이 극단적인 영역에 도달하여
Gradient가 거의 `0`이 된 Neuron을 Saturated Neuron이라고 한다.

이 경우 해당 Neuron의 학습이 매우 느려지거나 멈출 수 있다.

## 6. tanh

tanh는 출력 범위가 다음과 같다.

`-1 ~ 1`

Sigmoid와 달리 Zero-Centered라는 특징이 있다.

하지만 그래프 양 끝에서는 Gradient가 작아지는 문제가 있기 때문에
Vanishing Gradient 문제를 완전히 해결하지는 못한다.

## 7. ReLU

ReLU는 양수 입력에서는 입력값을 그대로 사용하고,
음수 입력에서는 `0`을 출력한다.

특징:

- 양수 영역에서는 Saturation 문제가 적음
- 비교적 크고 일정한 Gradient 제공
- 빠른 수렴에 도움
- Deep Learning 발전에 크게 사용됨

## 8. Dead ReLU

ReLU의 입력값이 계속 음수라면
출력값은 계속 `0`이 된다.

음수 영역에서는 Gradient도 `0`이기 때문에,
해당 Neuron은 더 이상 학습에 참여하지 못할 수 있다.

이를 Dead ReLU라고 한다.

## 9. Dead ReLU 해결 방법

### Positive Bias Initialization

Bias를 약간의 양수 값으로 초기화하여
Neuron이 활성 상태에 머물 가능성을 높인다.

### Leaky ReLU

음수 입력을 완전히 `0`으로 만들지 않고
작은 Gradient를 허용한다.

예:

`0.01x`

이렇게 하면 음수 영역에서도 Gradient가 존재하여
Neuron이 완전히 죽는 것을 방지할 수 있다.

### Parametric ReLU

PReLU에서는 음수 영역의 작은 기울기를
고정된 값으로 사용하는 대신 Parameter `α`로 표현한다.

이 `α` 자체도 학습할 수 있다.

---

# 2차시 - Weight Initialization

## 10. Weight Initialization

초기 Weight를 어떻게 설정하는지에 따라
학습 결과가 크게 달라질 수 있다.

잘못된 초기값은 Optimum에 도달하는 것을 어렵게 만들 수 있다.

## 11. 모든 Weight를 0으로 초기화하는 문제

모든 Weight를 `0`으로 설정하면
Hidden Layer의 모든 Neuron이 동일한 계산을 수행하게 된다.

결과적으로:

- 모든 Neuron의 출력이 같아짐
- 동일한 Gradient를 가짐
- Neuron들이 서로 다른 Feature를 학습하지 못함

신경망에서는 이러한 대칭성을 깨는 것이 중요하다.

따라서 일반적으로 Weight를 모두 `0`으로 초기화하지 않고
무작위 값으로 초기화한다.

## 12. 너무 작은 Weight

매우 작은 값으로 Weight를 초기화하면
Layer를 통과할수록 출력 신호가 점점 작아질 수 있다.

여러 Layer를 통과하면서 값이 `0` 근처로 몰리면
Backpropagation에서도 Gradient가 작아질 수 있다.

결과:

- Signal 감소
- Gradient 감소
- Vanishing Gradient 가능성

## 13. 너무 큰 Weight

Weight가 너무 크면 각 Neuron에 들어가는 입력의 합이 커진다.

tanh와 같은 Activation Function에서는
출력값이 `+1` 또는 `-1`과 같은 극단적인 영역으로 몰릴 수 있다.

이 영역에서는 Gradient가 작아져
역시 학습이 어려워질 수 있다.

## 14. Xavier Initialization

Xavier Initialization은
Forward와 Backward 과정에서 Signal의 분산을
Layer를 지나면서 가능한 일정하게 유지하는 것을 목표로 한다.

입력 Neuron 수를 고려하여 Weight의 분산을 조정한다.

- 입력 Neuron 수가 많으면 Weight를 작게
- 입력 Neuron 수가 적으면 Weight를 크게

목표:

- Forward 과정에서 출력 분산 유지
- Backpropagation에서 Gradient 분산 유지
- Activation Function의 유효한 영역에서 작동하도록 도움

수업에서는 tanh와 함께 사용할 수 있는 초기화 방법으로 다루었다.

예시:

`1 / n`

## 15. Kaiming Initialization

Xavier Initialization을 ReLU와 함께 사용할 경우
ReLU가 음수 입력을 `0`으로 만들면서
신호의 일부가 사라질 수 있다.

그 결과 Layer를 통과할수록 분산이 감소할 수 있다.

Kaiming Initialization은
ReLU에 맞게 이 감소를 보정하는 방법이다.

예시:

`2 / n`

ReLU 계열 Activation Function을 사용할 때
Signal의 분산을 유지하는 것을 목표로 한다.

## 16. Network Depth와 Width

신경망 구조를 볼 때 다음 두 가지를 구분할 수 있다.

### Depth

Layer가 몇 층으로 구성되어 있는가.

### Width

각 Layer에 몇 개의 Neuron이 있는가.

Neuron은 다음 과정을 수행한다.

1. Input을 받는다.
2. Weight를 곱한다.
3. Weighted Sum을 계산한다.
4. Activation Function을 통과한다.
5. Output Signal을 만든다.

## 17. Backpropagation 복습

Backpropagation은 Loss Function으로 계산한 Error를
Network의 출력 쪽에서 입력 쪽으로 역방향으로 전달하는 과정이다.

목적:

각 Weight가 Loss에 얼마나 영향을 미치는지 Gradient를 계산하고,
Weight를 어느 방향으로 얼마나 업데이트해야 하는지 판단한다.

가중치에 대한 Gradient는 다음 요소들과 관계된다.

- 바로 앞 Layer의 Output
- 현재 Layer Activation Function의 Gradient
- 다음 Layer에서 전달된 Gradient

## 18. Optimization

Weight Update 과정에서는 여러 Optimization Algorithm을 사용할 수 있다.

수업에서 다룬 예:

- SGD
- SGD with Momentum

Momentum은 이전 이동 방향을 이용해
더 안정적이고 빠른 학습을 시도하는 방법이다.

## 19. 깊은 Network의 한계

단순히 Layer의 수만 계속 늘리는 것이 항상 좋은 방법은 아니다.

구조에 대한 고려 없이 깊이만 늘리면:

- Optimization이 어려워질 수 있음
- 성능이 정체될 수 있음
- 오히려 성능이 떨어질 수 있음

더 좋은 성능을 위해서는 단순히 Layer를 늘리는 것뿐 아니라
문제에 맞는 새로운 Network Structure가 필요하다.

수업에서 언급한 구조:

- CNN
- RNN
- Transformer

## 핵심 정리

- Activation Function은 Network에 Non-Linearity를 추가한다.
- Sigmoid는 Vanishing Gradient와 Not Zero-Centered 문제가 있다.
- tanh는 Zero-Centered이지만 Vanishing Gradient 문제는 남는다.
- ReLU는 학습이 빠르지만 Dead ReLU 문제가 발생할 수 있다.
- Leaky ReLU와 PReLU는 Dead ReLU 문제를 완화하기 위한 방법이다.
- Weight를 모두 0으로 초기화하면 Neuron 간 대칭성을 깨지 못한다.
- 너무 작거나 큰 Weight 역시 학습 문제를 발생시킬 수 있다.
- Xavier Initialization은 Signal의 분산 유지를 목표로 한다.
- Kaiming Initialization은 ReLU 특성을 고려한 초기화 방법이다.
- Deep Network에서는 Activation Function, Weight Initialization, Optimization과 Network Structure를 함께 고려해야 한다.