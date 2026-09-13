# Week 05 - 머신러닝

## 1차시 - Machine Learning

### 머신러닝의 개념

- 머신러닝은 경험과 데이터를 이용하여 모델의 성능을 자동으로 향상시키는 방법이다.
- 모델 학습 과정에서는 Weight를 반복적으로 업데이트한다.

### 지도학습과 비지도학습

#### Supervised Learning

- 정답이 포함된 데이터를 이용해 학습한다.
- 학습 과정에서 Weight를 업데이트한다.

#### Unsupervised Learning

- 정답 없이 데이터의 구조나 특징을 찾아낸다.
- Clustering과 같은 방법이 사용된다.

### 머신러닝의 활용

- Classification
- Semantic Segmentation

이미지는 Pixel과 각 Pixel의 RGB 값으로 표현할 수 있다.

RGB 값은 일반적으로 `0 ~ 255` 범위의 값을 가진다.

## 2. Training Data와 Test Data

- 모델을 잘 학습시키기 위해서는 많은 양의 데이터가 필요하다.
- 데이터의 양뿐 아니라 다양한 환경의 데이터를 수집하는 것도 중요하다.
- Training Data를 이용해 모델을 학습한다.
- 학습이 끝난 후에는 새로운 Test Data를 이용해 모델의 성능을 확인한다.
- 이미 학습에 사용한 데이터를 다시 평가에 사용하는 것은 적절하지 않으므로 Training Data와 Test Data를 구분해야 한다.

이미지를 이용한 지도학습에서는 일반적으로 다음과 같은 데이터의 쌍이 필요하다.

- Image
- Label

## 3. Machine Learning과 Deep Learning

### Machine Learning

전통적인 Machine Learning에서는 사람이 먼저 데이터의 특징을 추출한다.

1. 사용할 특징을 정한다.
2. 특징을 추출한다.
3. 특징을 수치화하여 Feature Vector로 만든다.
4. Feature Vector를 모델에 입력하여 학습한다.

즉, 어떤 특징을 사용할지 사람이 결정하는 과정이 필요하다.

### Deep Learning

수업에서는 Deep Learning의 중요한 특징을 **Automatic Feature Extraction**으로 설명했다.

- 데이터를 입력하면 모델이 특징을 자동으로 추출한다.
- 대량의 데이터가 필요하다.
- 많은 연산이 필요하기 때문에 고성능 하드웨어가 중요하다.
- 편향을 줄이기 위해 다양하고 많은 데이터를 확보하는 것이 중요하다.

### 핵심

**Machine Learning과 Deep Learning의 중요한 차이 중 하나는 특징 추출 방식이다.**

- Machine Learning : 사람이 특징을 선택하고 추출
- Deep Learning : 모델이 특징을 자동으로 추출

## 4. Model Learning

모델 학습은 Weight를 반복적으로 업데이트하는 과정이다.

### Feed Forward

입력 데이터를 모델의 앞쪽에서 뒤쪽으로 전달하여 결과를 계산한다.

### Back Propagation

계산된 오류를 이용하여 Weight를 업데이트한다.

전체 과정은 다음과 같이 볼 수 있다.

`Input → Feed Forward → Error Calculation → Back Propagation → Weight Update`

## 5. Deep Neural Network

- Linear Classifier와 같은 단순한 구조를 여러 층으로 쌓아 신경망을 구성할 수 있다.
- 여러 Layer가 깊게 연결된 구조를 Deep Neural Network라고 볼 수 있다.
- Deep Learning의 "Deep"은 많은 Layer를 사용하는 구조와 관련이 있다.

## 6. Dataset 구성

데이터는 일반적으로 다음과 같이 나누어 사용할 수 있다.

### Training Set

모델의 Weight를 학습하는 데 사용한다.

### Validation Set

여러 Hyperparameter 설정을 비교하고 적절한 설정을 선택하는 데 사용한다.

### Test Set

학습이 완료된 모델이 새로운 데이터에서도 잘 작동하는지 평가하는 데 사용한다.

### Hyperparameter

모델 내부에서 학습되는 Weight와 달리,
학습 전에 외부에서 설정하는 값이다.

여러 Hyperparameter 조합을 시도하여 좋은 성능을 내는 설정을 찾는다.

## 7. Tensor

### 3D Tensor

예를 들어 데이터가 3개이고 각각 `5 × 5` 형태라면 다음과 같이 표현할 수 있다.

`(3, 5, 5)`

### 4D Tensor

RGB 이미지처럼 Channel 정보가 추가되면 4차원 Tensor로 표현할 수 있다.

데이터 3개, 각 데이터가 `5 × 5`, RGB 3개 Channel이라면:

`(3, 5, 5, 3)`

## 8. Text Data와 One-Hot Vector

컴퓨터가 문자를 처리하기 위해서는 단어를 숫자로 변환해야 한다.

One-Hot Vector 등을 이용하여 단어를 숫자 형태로 표현할 수 있다.

예를 들어 문장 데이터를 다음과 같은 차원으로 표현할 수 있다.

`(3, 2, 4)`

- 데이터 개수 : 3
- 한 문장을 구성하는 단어 수 : 2
- 각 단어를 표현하는 벡터 크기 : 4

## 9. Overfitting

Overfitting은 모델이 Training Set에 지나치게 맞춰져
새로운 데이터에 대한 성능이 떨어지는 현상이다.

- Training Set에서는 높은 성능
- Test Set에서는 낮은 성능
- 일반화 능력이 낮아짐

신경망의 Layer를 무조건 깊게 만드는 것이 항상 좋은 결과를 만드는 것은 아니다.

## 10. Support Vector Machine

SVM은 **Support Vector Machine**의 약자이다.

두 데이터 그룹을 나누는 좋은 결정 경계를 찾는 Machine Learning 알고리즘이다.

### Margin

- 두 그룹 사이의 결정 경계와 데이터 사이의 거리
- 두 그룹에서 가장 가까운 데이터들과의 거리가 최대가 되는 결정 경계를 찾는다.

## 11. Machine Learning Tools

수업에서 머신러닝을 위한 도구로 다음을 다루었다.

- NumPy
- PyTorch

## 12. 실제 데이터 구축

머신러닝에서는 모델뿐 아니라 데이터의 품질과 관리가 매우 중요하다.

이미지 데이터를 만드는 과정에서는 사람이 직접 객체의 영역을 지정하고 Label을 붙이는 작업이 필요할 수 있다.

예:

- 사진 및 영상에서 객체 영역 지정
- Polygon 형태로 점을 찍어 객체 영역 표시
- 정확한 Labeling

좋은 학습 데이터를 만들기 위해 초기 데이터 구축 과정에 많은 시간과 노력이 필요하다.

또한 실제 문제에서는 Deep Learning뿐 아니라 Machine Learning이나 기존의 전통적인 방법도 상황에 따라 사용될 수 있다.