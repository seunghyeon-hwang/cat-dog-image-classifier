# 🐶🐱 개 vs 고양이 이미지 분류 AI

TensorFlow를 사용하여 개(dog)와 고양이(cat) 이미지를 분류하는 간단한 CNN 기반 인공지능 모델입니다.
Kaggle의 Dogs vs Cats 데이터를 활용하여 학습합니다.

---

## 📌 프로젝트 개요

이 프로젝트는 이미지 데이터를 입력받아 해당 이미지가 개인지 고양이인지 분류하는 딥러닝 모델을 구현합니다.

* 프레임워크: TensorFlow / Keras
* 데이터셋: Kaggle Dogs vs Cats
* 모델: CNN (합성곱 신경망)

---

## 📂 데이터 준비

Google Colab 환경에서 Kaggle 데이터를 다운로드하여 사용합니다.

1. Kaggle API 키 (`kaggle.json`)를 Google Drive에 업로드
2. Colab에서 Drive 마운트
3. 데이터 다운로드 및 압축 해제

```bash
kaggle competitions download -c dogs-vs-cats-redux-kernels-edition
unzip dogs-vs-cats-redux-kernels-edition.zip
unzip train.zip
```

### 데이터 구조 생성

```plaintext
dataset/
 ├── cat/
 └── dog/
```

이미지를 클래스별로 분류하여 복사합니다.

---

## 🔄 데이터 전처리

TensorFlow의 `image_dataset_from_directory`를 사용하여 데이터셋을 생성합니다.

* 이미지 크기: 64x64
* 배치 크기: 64
* 검증 데이터: 20%

정규화:

```python
image = image / 255.0
```

---

## 🧠 모델 구조

CNN 기반 모델 구성:

* 데이터 증강 (Data Augmentation)

  * RandomFlip
  * RandomRotation
  * RandomZoom
* Conv2D + MaxPooling
* Dropout (과적합 방지)
* Dense Layer

### 모델 구조 요약

```plaintext
Input (64x64x3)
 → Data Augmentation
 → Conv2D (32)
 → MaxPooling
 → Conv2D (64)
 → MaxPooling
 → Dropout
 → Flatten
 → Dense (64)
 → Dense (1, sigmoid)
```

---

## ⚙️ 학습 설정

* Loss: binary_crossentropy
* Optimizer: Adam
* Metric: Accuracy
* Epochs: 5

### 콜백 기능

* TensorBoard: 학습 로그 시각화
* EarlyStopping: 과적합 방지 (val_loss 기준)

---

## 📊 학습 실행

```python
model.fit(
  train_ds,
  validation_data=val_ds,
  epochs=5,
  callbacks=[tensorboard, early_stopping]
)
```

---

## 📈 결과 확인

TensorBoard를 통해 학습 과정을 시각화할 수 있습니다.

```bash
%tensorboard --logdir logs
```

---

## 🚀 실행 환경

* Google Colab
* Python 3.x
* TensorFlow 2.x

---

## 📌 특징 요약

* 간단한 CNN 구조로 빠른 학습 가능
* 데이터 증강으로 일반화 성능 개선
* EarlyStopping으로 과적합 방지
* TensorBoard로 시각적 분석 지원

---

## 🧩 개선 아이디어

* 이미지 해상도 증가 (예: 128x128)
* 더 깊은 CNN 구조 적용
* Transfer Learning (ResNet, MobileNet 등)
* 데이터셋 확장

---

## 📎 참고

* Kaggle Dogs vs Cats Dataset
* TensorFlow 공식 문서

---
