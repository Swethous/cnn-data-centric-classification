# 📌 CNN Data-Centric Image Classification Project
**– Small Data 환경에서 일반화 성능을 높이는 단계적 접근**

---

## 📌 One-Line Summary
**Accuracy 비교에 그치지 않고,  
CNN이 무엇을 학습했고 어디를 보고 판단하는지까지 검증한  
데이터 중심 이미지 분류 프로젝트**

---

## 📊 Final Result at a Glance
> **Best Performance:** Data Augmentation + Transfer Learning

![Final Accuracy](results/notebook5_final/final_accuracy_comparison.png)

---

## 🔍 프로젝트 목표
**적은 데이터 환경에서 CNN의 이미지 분류 성능을 어떻게 효과적으로 향상시킬 수 있을까?**

소량의 이미지 데이터에서는 CNN이 특정 패턴을 암기(overfitting)하여  
**일반화 성능이 떨어지는 문제**가 발생한다.  
본 프로젝트는 **모델을 무작정 복잡하게 만들기 전에**,  
**데이터 중심(Data-centric) 접근**을 통해 이 문제를 해결하는 것을 목표로 한다.

---

## 🧪 실험 환경
- **Dataset**: CIFAR-10 (32×32 RGB)
- **Models**: Custom CNN, MobileNetV2 (Transfer Learning)
- **Framework**: TensorFlow / Keras
- **Evaluation**: Accuracy, Feature Map Visualization, Grad-CAM

---

## 🔄 Project Pipeline
아래 파이프라인은 본 프로젝트의 전체 실험 흐름을 요약한 것이다.

![Pipeline Overview](assets/figures/pipeline_overview.png)

- Data Augmentation을 통한 입력 다양성 확보
- CNN 내부 특징 학습 과정 분석
- Grad-CAM을 활용한 모델 판단 근거 시각화
- 최종 성능 비교 및 의사결정

---

# 🧩 Notebook 구성 및 실험 흐름

## 📘 Notebook 1  
### Baseline CNN vs Data Augmentation 적용 비교

### 🔹 배경
CIFAR-10은 CNN 학습이 가능하지만,  
**클래스 다양성과 데이터 양이 충분하지 않아 과적합이 발생하기 쉬운 데이터셋**이다.

### 🔹 접근
- Baseline CNN 모델 학습
- 동일한 모델에 **Data Augmentation** 적용
  - 회전(Rotation)
  - 이동(Shift)
  - 반전(Flip)

### 🔹 결과 비교
![Accuracy Comparison](results/notebook1_baseline_aug/accuracy_comparison.png)

### 🔹 결과 해석
- **Baseline**
  - 학습 초반 빠른 수렴
  - 높은 초기 accuracy
  - → 쉬운 패턴을 빠르게 암기
  - → 후반부에는 더 이상 배울 특징이 없어 성능 정체

- **Augmentation 적용**
  - 학습 초반은 느림
  - Epoch 증가에 따라 성능 지속 상승
  - → 동일한 객체를 다양한 형태로 관찰
  - → 변하지 않는 **핵심 특징(invariant feature)** 학습

📌 **결론**  
입력은 계속 변하지만 클래스의 본질은 변하지 않기 때문에,  
모델은 점차 일반적인 특징에 집중하게 된다.

---

## 📘 Notebook 2  
### 왜 Augmentation이 일반화를 돕는가? (Feature Map 시각화)

### 🔹 목적
단순한 accuracy 비교를 넘어,  
**CNN 내부에서 어떤 특징이 학습되는지 시각적으로 확인**하는 것이 목표이다.

### 🔹 Conv Layer의 계층적 특징 학습
- **Conv1**
  - 엣지, 색상 대비, 밝기 변화
  - 저수준 특징(Low-level features)

- **Conv2**
  - 엣지 조합
  - 텍스처, 반복 패턴, 부분 형태
  - 고수준 특징(High-level features)

### 🔹 Feature Map 시각화 결과
![Feature Map](results/notebook2_featuremap/feature_maps.png)

📌 **결론**  
Pooling은 augmentation으로 인한 위치 변화(shift)를 자연스럽게 흡수하여  
모델이 위치에 덜 민감한 표현을 학습하도록 돕는다.

---

## 📘 Notebook 3  
### 모델은 어디를 보고 판단하는가? (Grad-CAM)

### 🔹 목적
모델이 “맞췄다”보다 중요한 것은  
**“왜 그렇게 판단했는가”**이다.

### 🔹 Grad-CAM 시각화
![Grad-CAM](results/notebook3_gradcam/gradcam.png)

📌 **결론**  
모델의 판단은 무작위가 아니라,  
시각적으로 의미 있는 근거에 기반하고 있음을 확인하였다.

---

## 📘 Notebook 4  
### 확장: Transfer Learning 적용

### 🔹 접근
- **MobileNetV2**
  - ImageNet으로 사전 학습
  - 경량 구조
  - 정보 손실 최소화 설계

### 🔹 방법
- Feature Extractor 부분 **Freeze**
- Classification Head만 **Fine-tuning**

### 🔹 결과
![Transfer Learning Result](results/notebook4_transfer/transfer_learning.png)

📌 **결론**  
Transfer Learning은 소량 데이터 환경에서 안정적인 성능 향상을 제공한다.

---

## 📘 Notebook 5  
### 최종 비교 및 결과 정리

### 🔹 실험 조합
1. Baseline (No Augmentation)
2. Baseline + Augmentation
3. Transfer Learning (No Augmentation)
4. Transfer Learning + Augmentation

### 🔹 최종 Accuracy 비교
![Final Accuracy](results/notebook5_final/final_accuracy_comparison.png)

📌 **Data Augmentation + Transfer Learning** 조합이  
가장 안정적이고 높은 성능을 기록하였다.

---

# ✅ 최종 결론
- 소량 데이터 환경에서는  
  **모델 복잡도 증가보다 데이터 전략이 더 중요**
- Data Augmentation은 CNN의 일반화 성능을 효과적으로 향상시킨다
- Feature Map과 Grad-CAM을 통해 모델의 학습 근거를 검증하였다
- Transfer Learning은 실무적으로 가장 효과적인 확장 전략이다

---

## 📌 한 줄 요약
**CNN의 성능 향상뿐 아니라,  
모델이 무엇을 학습했고 어떻게 판단하는지까지  
데이터 중심으로 검증한 이미지 분류 프로젝트**
