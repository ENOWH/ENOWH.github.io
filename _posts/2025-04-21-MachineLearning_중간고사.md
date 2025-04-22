---
title: "머신러닝 중간고사 Chap01, 02, 03"
excerpt: "머신러닝 01, 02, 03 전체 흐름"

categories:
  - MachineLearning
tags:
  - [Machine Learning, 머신러닝]

permalink: /categories/MachineLearning/MachineLearning_중간고사

toc: true
toc_sticky: true

date: 2025-04-21
last_modified_at: 2025-04-21
---

# 🧠 Machine Learning Concepts: 총정리 (Chapters 1~3)

---

## 🌐 1. 머신러닝 전체 구조

```
Supervised Learning
├── Regression
│   ├── Linear Regression
│   └── Ridge Regression (Regularized)
├── Classification
│   ├── Generative Models
│   │   ├── Bayes Classifier (이론적 최적 분류기)
│   │   ├── Linear Discriminant Analysis (LDA)
│   │   └── Naïve Bayes
│   ├── Discriminative Models
│   │   ├── Logistic Regression
│   │   └── Support Vector Machine (SVM)
│   └── Nonparametric
│       └── k-Nearest Neighbor (k-NN)
└── Unified Framework
    └── Empirical Risk Minimization (ERM)
```

---

## 📦 2. 각 개념 설명 & 연결

---

### 🔹 Linear Regression

- **목적**: 연속값 예측
- **수식**: $f(\mathbf{x}) = \boldsymbol{\theta}^\top \mathbf{x}$
- **손실**: MSE (평균 제곱 오차)
- **해법**: Least Squares / Closed-form / Gradient Descent
- **확장**:
  - **Ridge Regression**: 정규화 추가
  - **ERM 프레임워크에 포함됨**

✅ 분류가 아니라 회귀임

---

### 🔹 Logistic Regression

- **목적**: 확률적 이진 분류 ($y \in \{0,1\}$)
- **수식**:  
  $$
  \Pr(Y = 1 \mid \mathbf{x}) = \frac{1}{1 + \exp(-\boldsymbol{\theta}^\top \mathbf{x})}
  $$
- **손실 함수**: Logistic Loss (Convex surrogate of 0-1 loss)
- **ERM에 포함됨** + **Discriminative Model**

✅ Linear Regression과는 출력값과 목적이 다르다  
✅ 그러나 구조는 거의 동일하고, loss function만 다름 → **형제 모델**

---

### 🔹 Bayes Classifier (이론)

- **정의**:  
  $$
  f^*(\mathbf{x}) = \arg\max_y \Pr(Y = y \mid \mathbf{x})
  $$
- **목표**: 가장 낮은 오류 확률 달성 (Bayes Optimal Classifier)
- **문제점**: 실제로는 $\Pr(Y \mid \mathbf{x})$ 를 알 수 없음
- **Plug-in 방식으로 근사**: → LDA, Naïve Bayes 등

✅ 모든 분류기의 이론적 기준점

---

### 🔹 LDA (Linear Discriminant Analysis)

- **Bayes Classifier 근사 방법**
- **가정**: 클래스별 Gaussian + 공통 공분산 $\Sigma$
- **결과**: 선형 결정 경계
- **모델 구조**: generative

✅ Logistic Regression과 결정 경계는 비슷하지만,  
✅ 확률 모델 방식이 다르다 → **LDA는 likelihood 기반 (Generative)**

---

### 🔹 Naïve Bayes

- **Bayes Classifier 근사**
- **가정**: 클래스 조건부 독립성  
  $$
  \Pr(\mathbf{x} \mid y) = \prod_j \Pr(x_j \mid y)
  $$
- **특징**: 계산 빠름, 차원 수 커도 적용 가능
- **모델 구조**: Generative

✅ LDA와 마찬가지로 Bayes를 근사하는 **Generative 모델**

---

### 🔹 Support Vector Machine (SVM)

- **기하학적 분류기**
- **Margin을 최대화하는 결정 경계 학습**:
  $$
  \min \frac{1}{2} \|\mathbf{w}\|^2 + C \sum \xi_i
  $$
- **손실 함수**: Hinge Loss (Convex surrogate)
- **ERM 프레임워크에 포함**

✅ Logistic Regression과 목적 유사  
✅ 둘 다 Discriminative이고 margin 기반

---

### 🔹 k-Nearest Neighbor (k-NN)

- **특징**: 학습 없음, 저장만 함 (Nonparametric)
- **결정**: 입력 $\mathbf{x}$와 가장 가까운 $k$개 이웃의 다수결

✅ 다른 모델과 달리 **parametric form 없음**  
✅ 직관적이고 baseline으로 자주 사용

---

### 🔹 Empirical Risk Minimization (ERM)

- **공통 프레임워크**:
  $$
  \min_{f \in \mathcal{F}} \frac{1}{n} \sum_{i=1}^n L(y_i, f(x_i)) + \lambda \cdot \Omega(f)
  $$

- Linear Regression, Logistic Regression, SVM, Ridge 등  
  전부 **ERM에 포함됨**

---

## 🔄 3. 관계 요약 표

| 모델 | 목적 | 분류/회귀 | Generative? | ERM? | 손실 함수 |
|------|------|------------|-------------|------|-----------|
| **Linear Regression** | 연속값 예측 | 회귀 | ✖️ | ✅ | MSE |
| **Ridge Regression** | 정규화된 회귀 | 회귀 | ✖️ | ✅ | MSE + 정규화 |
| **Logistic Regression** | 확률적 분류 | 분류 | ✖️ | ✅ | Logistic Loss |
| **Bayes Classifier** | 이론적 최적 분류 | 분류 | ✅ | ✖️ | 0-1 Loss |
| **LDA** | Bayes 근사 | 분류 | ✅ | ✖️ | Likelihood 기반 |
| **Naïve Bayes** | Bayes 근사 | 분류 | ✅ | ✖️ | Likelihood 기반 |
| **SVM** | Margin 최대화 | 분류 | ✖️ | ✅ | Hinge Loss |
| **k-NN** | 이웃 기반 분류 | 분류 | ✖️ | ✖️ | 없음 |
| **ERM** | 모든 학습 기반 | 분류/회귀 | - | ✅ | General $L(y,f(x))$ |

---

## ✅ 결론 요약

- **Linear vs Logistic Regression**:  
  → 구조는 같지만 목적과 손실 함수가 다름 (회귀 vs 분류)

- **Generative vs Discriminative**:  
  → LDA/Naïve Bayes는 **데이터 생성 모델**  
  → Logistic/SVM은 **결정 경계 모델**

- **모든 학습 모델은 ERM으로 통합 가능** (단, k-NN, Bayes Classifier 제외)

- **ERM은 머신러닝의 중심 축**,  
  모든 현대적 알고리즘은 거의 다 이 틀에서 해석 가능하다