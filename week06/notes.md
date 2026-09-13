\# Week 06 - 딥러닝과 인공신경망



\## 1차시 - Artificial Neural Network



\## 1. Linear Score Function



인공신경망에서는 입력 데이터 `x`와 Weight `W`를 이용해 값을 계산한다.



`f(x, W)`



\- Weight를 많이 사용하면 데이터를 더 다양하게 표현할 수 있다.

\- 하지만 Weight만 추가한다고 해서 선형성 자체가 사라지는 것은 아니다.

\- 선형 구조만으로는 복잡한 문제를 표현하는 데 한계가 있다.



\## 2. Non-Linearity



복잡한 문제를 해결하기 위해서는 신경망에 비선형성(Non-Linearity)이 필요하다.



이를 위해 Activation Function을 사용한다.



대표적인 Activation Function:



\- Sigmoid

\- tanh

\- ReLU



여러 Layer를 쌓고 비선형성을 추가함으로써 더 복잡한 문제를 표현할 수 있다.



\## 3. 여러 Perceptron과 Feature Space



서로 다른 Perceptron을 결합하면 새로운 Feature Space를 만들 수 있다.



기존 공간에서는 여러 개의 선이 필요했던 문제도,

새로운 Feature Space로 변환하면 하나의 선으로 분리할 수 있는 경우가 있다.



여러 Layer를 사용하는 경우:



\- 앞쪽 Layer : 새로운 Feature Space를 생성

\- 뒤쪽 Layer : 생성된 Feature를 이용해 데이터를 분류



이러한 구조가 여러 층으로 확장되면서 인공신경망이 구성된다.



\## 4. Artificial Neural Network Structure



인공신경망은 크게 다음 Layer들로 구성된다.



\### Input Layer



\- 입력할 데이터와 데이터의 종류를 결정한다.

\- 입력 데이터가 네트워크로 들어오는 부분이다.



\### Hidden Layer



\- 실제 계산이 이루어지는 부분이다.

\- 여러 개의 Node와 Weight를 사용할 수 있다.

\- Layer와 Node의 수는 모델 구조에 따라 조정할 수 있다.



\### Output Layer



\- 최종 결과를 출력한다.

\- Classification 문제에서는 각 Class에 대응하는 출력 Node를 구성할 수 있다.



\## 5. Perceptron



단층 Perceptron에서는 입력 `x`와 Weight `w`의 곱을 합산한다.



그 결과를 Threshold와 비교하여 `0` 또는 `1`을 판단하고 데이터를 분류한다.



개념적으로 다음과 같은 연산을 수행한다.



`Σ(x × w)`



\### Bias



Threshold를 직접 사용하는 대신 Bias를 추가하여

결정 기준을 조정할 수도 있다.



\## 6. Activation Function



Activation Function은 뉴런의 계산 결과를 조절하고

신경망에 Non-Linearity를 추가하는 역할을 한다.



최종 출력뿐 아니라 Hidden Layer의 중간 결과에도 사용된다.



\### Sigmoid



출력 범위:



`0 \~ 1`



\### tanh



출력 범위:



`-1 \~ 1`



\### ReLU



음수 영역은 `0`으로 만들고 양수 영역은 입력값을 그대로 사용한다.



신경망 내부에 비선형성을 추가하는 대표적인 Activation Function이다.



\## 7. Feedforward



Feedforward는 입력 데이터를 시작으로

각 Layer의 계산 결과를 다음 Layer로 순차적으로 전달하는 과정이다.



`Input → Hidden Layer → Output`



즉, Layer들이 Chain 형태로 연결되어 결과값을 앞으로 전달한다.



\## 8. Biological Neuron과 Artificial Neuron



인공신경망은 인간의 신경망 구조를 모방한 개념이다.



| Biological Neuron | Artificial Neural Network |

|-------------------|---------------------------|

| Soma | Neuron |

| Dendrite | Input |

| Axon | Output |

| Synapse | Weight |



\## 9. Weight Learning



신경망 학습에서 중요한 목표 중 하나는 적절한 Weight를 찾는 것이다.



모델의 예측 결과와 정답 사이의 Error를 이용하여

Weight를 반복적으로 업데이트한다.



이 과정에서 기울기(Gradient)를 이용한다.



\## 10. Loss Function



Weight를 얼마나 수정해야 하는지 판단하기 위해 Loss를 계산한다.



목표는 정답과 예측값 사이의 Error를 줄이는 것이다.



수업에서 다룬 Loss Function:



\- L1 Loss

\- MSE Loss

\- Cross Entropy Loss



Loss가 작아지는 방향으로 Weight를 업데이트한다.



\---



\# 2차시 - Backpropagation과 Weight Update



\## 11. 미분과 Weight



예를 들어 다음 식이 있다고 하자.



`y = wx + b`



\- `x` : Input

\- `w` : Weight

\- `b` : Bias



미분을 이용하면 각 요소가 결과에 얼마나 영향을 주는지 확인할 수 있다.



이러한 기울기 정보는 Weight를 업데이트하는 데 활용된다.



\## 12. Backpropagation



Backpropagation은 출력에서 발생한 Error를 이용하여

앞쪽 Layer 방향으로 기울기를 전달하는 과정이다.



각 Weight가 Error에 얼마나 영향을 주었는지 계산하고,

그 결과를 이용해 Weight를 업데이트한다.



\### 연산에 따른 미분



덧셈 연산에서는 편미분 이후 다른 변수의 영향이 사라질 수 있다.



곱셈 연산에서는 편미분 이후 다른 변수의 값이 남아

Gradient 계산에 영향을 준다.



이러한 연산들이 연결되어 전체 신경망의 Gradient를 계산한다.



\## 13. 전체 학습 흐름



신경망 학습은 다음과 같은 과정으로 볼 수 있다.



1\. Input Data 입력

2\. Feedforward

3\. Prediction 계산

4\. Loss Function으로 Error 계산

5\. Backpropagation

6\. Gradient 계산

7\. Weight Update

8\. 반복



\## 14. Learning Rate



Weight를 업데이트할 때는 Learning Rate도 중요하다.



\- 너무 큰 값은 학습을 불안정하게 만들 수 있다.

\- 작은 값을 사용하면 비교적 안정적인 업데이트가 가능하다.

\- 모델 구조와 Learning Rate를 함께 실험하며 적절한 값을 찾을 필요가 있다.



\## 핵심 정리



\- Weight만 여러 개 추가한다고 Non-Linearity가 생기는 것은 아니다.

\- Activation Function을 이용하여 Non-Linearity를 추가한다.

\- 여러 Layer를 사용하여 더 복잡한 Feature를 표현할 수 있다.

\- Feedforward를 통해 결과를 계산한다.

\- Loss Function으로 Error를 계산한다.

\- Backpropagation과 미분을 이용해 Gradient를 구한다.

\- Gradient를 이용해 Weight를 업데이트한다.

