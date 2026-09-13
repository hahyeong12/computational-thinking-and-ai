# Week 12 - FashionMNIST 분류 실습

이번 주차에서는 FashionMNIST 데이터셋을 이용하여
MLP 기반 이미지 분류 모델을 구현하고 학습했다.

기본 MLP 모델을 학습한 뒤,
모델의 깊이와 뉴런 수, 학습 Epoch를 변경하면서
분류 성능이 어떻게 변화하는지 비교했다.

## 1. FashionMNIST Dataset

FashionMNIST는 `28 × 28` 크기의 이미지를 이용한
이미지 분류 데이터셋이다.

모델 학습을 위해 데이터를 다음과 같이 나누어 사용했다.

- Training Set
- Validation Set
- Test Set

## 2. Data Preprocessing

원본 이미지는 `(28, 28)` 형태이지만,
MLP의 Fully Connected Layer에 입력하기 위해
1차원 Vector 형태로 변환했다.

```python
image = tf.reshape(image, (784,))
```

전체 전처리 과정은 다음과 같다.

1. 이미지 자료형을 `uint8`에서 `float32`로 변환
2. Pixel 값을 `0 ~ 255`에서 `0 ~ 1` 범위로 정규화
3. 이미지 크기를 `(28, 28)`에서 `(784,)`로 변환
4. Label을 One-Hot Vector로 변환

```python
def preprocess(image, label):
    image = tf.cast(image, tf.float32)
    image = image / 255.0
    image = tf.reshape(image, (784,))
    label = tf.one_hot(label, depth=10, dtype=tf.float32)
    return image, label
```

## 3. Basic MLP Model

기본 모델은 하나의 Hidden Layer와
하나의 Output Layer로 구성된 MLP이다.

```python
inputs = Input(shape=(784,), name='input')

x = Dense(
    200,
    activation='relu',
    name='hidden1'
)(inputs)

x = Dense(
    10,
    activation='softmax',
    name='output'
)(x)

model = Model(inputs, x, name='mlp')
```

### Model Parameters

- Input Dimension : 784
- Hidden Neurons : 200
- Output Classes : 10
- Total Parameters : 159,010
- First Hidden Layer Parameters : 157,000

## 4. Loss and Optimizer

분류 문제를 학습하기 위해 다음 설정을 사용했다.

- Loss Function : Categorical Cross Entropy
- Metric : Categorical Accuracy
- Optimizer : SGD
- Momentum : 0.9
- Learning Rate : 0.01
- Learning Rate Schedule : Cosine Decay

```python
metric = CategoricalAccuracy()
loss = CategoricalCrossentropy()

lr_schedule = CosineDecay(
    0.01,
    len(train_dataset) * epochs
)

optimizer = SGD(
    lr_schedule,
    momentum=0.9
)
```

## 5. Basic Model Training

기본 MLP 모델을 30 Epoch 동안 학습했다.

```python
history = model.fit(
    train_dataset,
    epochs=30,
    validation_data=valid_dataset
)
```

### Result

| Dataset | Accuracy |
|---------|---------:|
| Training | 92.07% |
| Validation | 88.94% |
| Test | 88.57% |

Training Accuracy가 가장 높았으며,
Validation과 Test Accuracy는 서로 비슷한 결과를 보였다.

## 6. Training Visualization

학습 과정에서 Training / Validation의
Loss와 Accuracy 변화를 그래프로 확인했다.

```python
losses = pd.DataFrame({
    'train_loss': history.history['loss'],
    'valid_loss': history.history['val_loss'],
})

accuracies = pd.DataFrame({
    'train_acc': history.history['categorical_accuracy'],
    'valid_acc': history.history['val_categorical_accuracy'],
})
```

이를 통해 Epoch가 증가하면서
Loss가 감소하고 Accuracy가 증가하는 과정을 확인했다.

## 7. Output Layer Parameters

기본 FashionMNIST 모델의 Class는 10개이다.

Hidden Layer가 200개의 Neuron으로 구성되어 있으므로
Output Layer의 Parameter는 다음과 같다.

`200 × 10 + 10 = 2,010`

만약 Class가 20개로 증가한다면:

`200 × 20 + 20 = 4,020`

따라서 Output Layer의 Parameter 수도 증가한다.

## 8. Validation Set과 Test Set

Training Set은 실제 Weight Update에 사용되는 데이터이다.

반면 Validation Set은 학습 중 모델의 일반화 성능을 확인하기 위해 사용하며,
직접적인 Weight 학습에는 사용하지 않는다.

따라서 새로운 데이터에 대한 성능을 평가하는 Test Set과
비슷한 조건을 가지며 Accuracy도 비교적 유사하게 나타났다.

---

# Model Improvement

기본 모델의 성능을 개선하기 위해
Network의 크기와 학습 횟수를 증가시켰다.

## 9. Hidden Layer 확장

개선된 모델에서는:

- Hidden Layer 수 : 2개
- 각 Hidden Layer의 Neuron 수 : 2,000개

로 증가시켰다.

### Total Parameters

개선된 모델의 전체 Parameter 수:

`5,612,020`

기본 모델보다 훨씬 많은 Parameter를 이용하여
더 복잡한 패턴을 학습하도록 구성했다.

## 10. Improved Model - 30 Epoch

Hidden Layer와 Neuron 수를 늘린 모델을
30 Epoch 동안 학습했다.

### Result

| Dataset | Accuracy |
|---------|---------:|
| Training | 96.08% |
| Validation | 90.18% |
| Test | 89.93% |

기본 모델의 Test Accuracy인 88.57%보다
향상된 성능을 보였다.

Neuron 수가 증가하면서 더 복잡하고 세밀한 패턴을
학습할 수 있게 되었고,

Hidden Layer가 증가하면서 ReLU와 같은
Non-Linear Activation Function을 여러 번 거치게 되어
더 복잡한 Decision Boundary를 표현할 수 있게 되었다.

## 11. Improved Model - 60 Epoch

같은 모델의 학습 Epoch를
30에서 60으로 증가시켰다.

### Result

| Dataset | Accuracy |
|---------|---------:|
| Training | 99.42% |
| Validation | 90.20% |
| Test | 90.27% |

학습 횟수가 증가하면서
모델이 Training Data의 패턴을 더 많이 학습했고,
Test Accuracy 역시 조금 더 향상되었다.

하지만 Training Accuracy와 Test Accuracy 사이의 차이가 커져
Overfitting 가능성도 확인할 수 있다.

## 12. Model Comparison

| Model | Epoch | Training | Validation | Test |
|------|------:|---------:|-----------:|-----:|
| Basic MLP | 30 | 92.07% | 88.94% | 88.57% |
| Expanded MLP | 30 | 96.08% | 90.18% | 89.93% |
| Expanded MLP | 60 | 99.42% | 90.20% | 90.27% |

Network의 크기와 학습 횟수를 증가시키면서
Test Accuracy가 향상되는 것을 확인했다.

동시에 Training Accuracy가 Test Accuracy보다 크게 높아지면서
모델의 Generalization과 Overfitting도 함께 고려해야 함을 확인했다.

## 13. Further Improvement Ideas

### Dropout

학습 과정에서 일부 Neuron을 임의로 비활성화하여
특정 Feature에 지나치게 의존하는 것을 줄인다.

이를 통해 Overfitting을 완화하고
Generalization 성능을 향상시킬 수 있다.

### Weight Regularization

너무 큰 Weight를 제한하여
모델이 Training Data의 세부적인 Noise까지
학습하는 것을 줄일 수 있다.

### CNN

MLP는 `28 × 28` 이미지를 1차원 Vector로 변환하기 때문에
이미지의 공간적 구조를 충분히 활용하기 어렵다.

CNN을 사용하면 2차원 이미지 구조를 유지하면서
지역적인 Feature를 추출할 수 있다.

### Data Augmentation

기존 Training Image에 다음과 같은 변형을 적용할 수 있다.

- 이동
- 회전
- 반전

이를 이용하여 데이터의 다양성을 증가시키고
모델의 Generalization 성능 향상을 기대할 수 있다.

## 14. Inference

학습된 모델에 새로운 이미지를 입력하여
각 Class에 대한 Prediction을 계산했다.

```python
new_input = test_image[0, :, :]
new_input = tf.cast(new_input, tf.float32) / 255.0
new_input = tf.reshape(new_input, (1, 784))

prediction = model.predict(new_input)
```

이를 통해 학습된 모델이
새로운 FashionMNIST 이미지를 실제로 분류하는 과정까지 실습했다.

## Files

- [FashionMNIST Classification Notebook](./practice/fashion_mnist_classification.ipynb)
- [Baseline MLP Report](./report/fashion_mnist_baseline_report.pdf)
- [Model Improvement Report](./report/fashion_mnist_improvement_report.pdf)