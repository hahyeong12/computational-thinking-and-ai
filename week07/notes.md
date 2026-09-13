# Week 07 - Learning Techniques

## 1차시 - Regularization & Optimization

## 1. 학습 데이터 분할

모델 학습을 위해 데이터를 다음과 같이 나누어 사용할 수 있다.

- Training Set
- Validation Set
- Test Set

예시 비율:

- `6 : 2 : 2`
- `8 : 1 : 1`

각 데이터를 분리하여 모델 학습과 평가에 사용한다.

## 2. Underfitting과 Overfitting

모델의 Capacity가 너무 낮거나 너무 높으면 문제가 발생할 수 있다.

목표는 모델을 적절한 Capacity에 가깝게 만드는 것이다.

### Underfitting

모델이 충분히 학습되지 않은 상태이다.

- Training Loss가 아직 충분히 낮아지지 않음
- Validation/Test Loss 역시 높은 상태
- 모델이 데이터의 패턴을 충분히 학습하지 못함

### Overfitting

모델이 Training Set에 지나치게 맞춰진 상태이다.

- Training Loss는 낮아짐
- Validation/Test Loss는 다시 높아질 수 있음
- 새로운 데이터에 대한 일반화 능력이 떨어짐

## 3. Regularization

Regularization은 모델의 Capacity를 제한하여
Training Data에 지나치게 적합되는 것을 방지하는 방법이다.

목표는 모델을 적절한 Capacity 근처로 유도하여
Generalization Error를 낮추는 것이다.

### L1 Regularization

- 일부 Weight를 두드러지게 만든다.
- 소수의 특징에 집중하는 성격을 가진다.

### L2 Regularization

- Weight를 비교적 균등하게 사용한다.
- 여러 특징을 골고루 고려하는 성격을 가진다.

## 4. Lambda

`λ`는 Regularization의 강도를 조절하는 값이다.

### λ가 큰 경우

- Regularization 효과가 강해진다.
- 모델이 지나치게 단순해질 수 있다.

### λ가 작은 경우

- Regularization 효과가 약해진다.
- Loss를 줄이는 데 지나치게 집중하면서 Overfitting이 발생할 수 있다.

즉,

`λ = Regularization Strength`

---

# Optimization

## 5. Gradient Descent

Gradient Descent는 함수의 기울기를 이용해
함수값이 작아지는 방향으로 이동하는 Optimization Algorithm이다.

목표:

`Loss Function의 최소값 찾기`

현재 위치의 Gradient를 계산하고,
가장 빠르게 함수값이 감소하는 방향으로 이동한다.

가장 빠른 감소 방향은 현재 Gradient의 반대 방향이다.

## 6. Learning Rate

한 번에 얼마나 이동할지를 Learning Rate로 결정한다.

### Learning Rate가 너무 작은 경우

- 이동 속도가 느림
- 학습 시간이 오래 걸림

### Learning Rate가 너무 큰 경우

- 최적 지점을 지나칠 수 있음
- 학습이 불안정해질 수 있음
- 발산할 수도 있음

## 7. Local / Global Optimum

함수에는 여러 개의 최소점과 최대점이 존재할 수 있다.

- Local Minimum
- Local Maximum
- Global Minimum
- Global Maximum

특히 Non-Convex Function은 여러 개의 봉우리와 골짜기를 가질 수 있어
Global Optimum을 찾기 어렵다.

## 8. Gradient Descent와 SGD

### Gradient Descent

전체 Training Dataset을 이용해 Gradient를 계산하고
Parameter를 업데이트한다.

데이터가 많아질수록 계산 비용과 시간이 커질 수 있다.

### SGD

SGD는 **Stochastic Gradient Descent**의 약자이다.

전체 데이터를 한 번에 사용하는 대신,
하나의 Sample 또는 작은 Sample 묶음을 이용해 Gradient를 계산한다.

장점:

- 계산 속도가 빠름
- Memory 효율성이 좋음

단점:

- Gradient에 Noise가 많음
- Parameter의 이동 경로가 불안정할 수 있음
- 지그재그 형태로 이동할 수 있음
- 수렴에 시간이 걸릴 수 있음

## 9. SGD with Momentum

Momentum은 이전 단계에서 이동했던 방향을 기억한다.

현재 Gradient의 방향이 이전 이동 방향과 비슷하면
더 빠르게 이동할 수 있다.

반대로 방향이 자주 바뀌는 곳에서는 움직임을 줄인다.

효과:

- 지그재그 움직임 완화
- 평탄한 구간에서도 빠른 이동 가능
- Local Point를 관성으로 지나갈 가능성
- 더 나은 Optimum을 찾는 데 도움

---

# 2차시 - Learning Rate & Model Learning

## 10. Learning Rate Scheduling

학습 초반에는 큰 Learning Rate를 이용해 빠르게 이동하고,
목표 지점에 가까워지면 Learning Rate를 줄여
더 세밀하게 접근할 수 있다.

따라서 Training 과정에 따라 Learning Rate를 조절하는 것이 중요하다.

## 11. Epoch

Training Set 전체를 한 번 학습하는 것을 한 번의 Epoch라고 한다.

예:

`1 Epoch = Training Set 전체를 한 번 학습`

## 12. Hyperparameter

Hyperparameter는 모델 학습 과정에서
사람이 외부에서 설정하는 값이다.

예:

- Learning Rate
- Epoch
- Layer 수
- 기타 학습 설정

이러한 값은 학습 전에 사람이 정한다.

## 13. Learning 상태

### Underfitting

Training Set과 Validation/Test Set의 Loss가
아직 충분히 감소하지 않은 상태이다.

모델 학습이 더 필요한 상태이다.

### Overfitting

Training Loss는 계속 좋아지지만,
Validation/Test Loss는 다시 나빠지는 상태이다.

Training Data에 지나치게 맞춰진 결과
새로운 데이터에 대한 일반화 능력이 떨어진다.

## 14. 잘못된 Data Split

Training Set에 포함된 데이터가 Test Set에도 포함되면
올바른 평가를 할 수 없다.

이미 학습한 데이터를 이용하여 다시 Test를 수행하면
실제 일반화 능력을 제대로 확인할 수 없기 때문이다.

## 15. Hyperparameter Tuning

모델 성능은 Hyperparameter 설정에 따라 크게 달라질 수 있다.

설정할 수 있는 요소의 예:

- Learning Rate
- Layer 수
- Weight 관련 설정
- Epoch
- 기타 모델 구조

### Manual Tuning

연구자나 개발자가 경험과 직관,
기존 실험 결과를 바탕으로 직접 값을 선택한다.

장점:

- 경험을 활용할 수 있음
- 불필요한 탐색 범위를 줄일 수 있음

단점:

- 주관적일 수 있음
- 새로운 문제에서는 적절한 값을 찾기 어려울 수 있음

### Grid Search

1. Hyperparameter의 범위를 정한다.
2. 여러 개의 후보 값을 선택한다.
3. 가능한 조합을 반복적으로 테스트한다.
4. 가장 좋은 성능을 보이는 조합을 찾는다.

## 16. 모델 깊이와 데이터

모델이 깊어질수록 더 복잡한 패턴을 표현할 수 있지만,
Overfitting 가능성도 고려해야 한다.

따라서 다양한 패턴을 가진 충분한 데이터를 확보하는 것이 중요하다.

## 핵심 정리

- Underfitting과 Overfitting 사이의 적절한 Capacity를 찾는 것이 중요하다.
- Regularization을 이용해 Overfitting을 줄일 수 있다.
- `λ`는 Regularization의 강도를 결정한다.
- Gradient Descent는 Gradient의 반대 방향으로 이동한다.
- Learning Rate는 이동하는 보폭을 결정한다.
- SGD는 일부 데이터를 이용해 빠르게 Gradient를 계산한다.
- Momentum은 이전 이동 방향을 활용한다.
- Hyperparameter는 사람이 설정하며 적절한 Tuning이 필요하다.