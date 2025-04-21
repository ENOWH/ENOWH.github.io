---
title: "Chapter03 정리"
excerpt: "University"

categories:
  - MachineLearning
tags:
  - [Machine Learning, 머신러닝]

permalink: /categories/MachineLearning/0Chapter03_MachineLearning

toc: true
toc_sticky: true

date: 2025-04-18
last_modified_at: 2025-04-18
---

# 📘 Chapter 3 정리: Kernel Methods & Constrained Optimization

중간고사 범위 중 `slide_ch3.pdf`의 내용을 정리한 포스트입니다.  
총 4개의 세션으로 구성되어 있으며, 각 세션의 핵심 개념과 개념 간 흐름, 포함관계를 정리합니다.

---

## 📚 전체 세션 구성

| 세션 번호 | 세션 이름 | PDF 페이지 (전체 기준) |
|-----------|------------|----------------------|
| 1 | Kernel Methods | 1–26 |
| 2 | Kernel Ridge Regression | 27–44 |
| 3 | Constrained Optimization | 45–124 |
| 4 | Gaussian Processes | 125–173 |

---

## 🧠 전체 흐름

Linear Models (Ch2)
↓ kernel trick
Nonlinear Models with Kernels (세션 1–2)
↓ 최적화 문제 재정의
Constrained Optimization (세션 3)
↓ 확률적 함수 예측
Gaussian Processes (세션 4)

---

## 🔷 세션 1: Kernel Methods

### ✅ 핵심 아이디어
- 선형 모델을 고차원으로 확장하여 **비선형 문제를 선형처럼** 풀기
- `kernel trick`을 이용해 계산 효율성 확보

### ✅ 주요 개념
- **Feature map**: `φ(x)`
- **Kernel function**: `k(x, x') = ⟨φ(x), φ(x')⟩`
- **Mercer’s Theorem**: kernel이 Gram matrix로 표현 가능 + PSD 조건
- **Common kernels**: Linear, Polynomial, RBF

### ✅ 포함관계 및 흐름
- Linear Models ⊂ Kernel Methods
- ERM + kernel → Kernelized Linear Classifier
- Kernelized SVM으로 확장 가능

---

## 🔷 세션 2: Kernel Ridge Regression

### ✅ 핵심 아이디어
- Ridge Regression에 kernel을 도입하여 **비선형 회귀** 구현

### ✅ 수식 비교
- Ridge: min_w || y - Xw ||² + λ||w||²
- Kernel Ridge: min_α || y - Kα ||² + λ αᵀKα


### ✅ 주요 개념
- 해: `α* = (K + λI)^(-1) y`
- 최종 출력: `f(x) = Σ αᵢ k(xᵢ, x)`

### ✅ 포함관계
- Ridge Regression ⊂ Kernel Ridge Regression

---

## 🔷 세션 3: Constrained Optimization

### ✅ 핵심 아이디어
- 제약조건을 갖는 머신러닝 최적화 문제를 수학적으로 해결

### ✅ 주요 개념
- **Lagrangian**: 제약 포함 목적함수
- **KKT 조건**: 최적성 조건 (필요/충분 조건)
- **Duality**: Primal ↔ Dual 전환
- **Slack variable (ξᵢ)**: soft margin 허용

### ✅ 예시
- SVM은 Lagrangian과 KKT 조건으로 설명 가능
- ERM-Hinge ↔ Soft-margin SVM (λ = 1/C)

---

## 🔷 세션 4: Gaussian Processes

### ✅ 핵심 아이디어
- 예측값이 아니라 **함수 전체**를 확률적으로 모델링 (nonparametric)

### ✅ 주요 개념
- **GP prior**: 함수는 무한차원 정규분포에서 추출됨
- **Covariance/kernel**: `k(x, x')`로 함수 간 유사도 측정
- **Posterior**: 관측 데이터 기반 조건부 분포
- **Uncertainty**: 예측 신뢰도 함께 출력됨

### ✅ 포함관계
- kernel method의 확률적 확장
- deterministic 모델(SVM 등)과 대비됨

---

## 🧾 세션별 요약 비교표

| 세션 | 핵심 주제 | 포함/연결 관계 |
|------|-----------|----------------|
| 1. Kernel Methods | 비선형 확장 (Feature Map) | Linear Models ⊂ Kernel Models |
| 2. Kernel Ridge | Ridge + Kernel 확장 | Ridge ⊂ Kernel Ridge |
| 3. Constrained Optimization | 제약조건 포함 최적화 | SVM 포함, ERM과 연결 |
| 4. Gaussian Processes | 함수에 대한 확률적 모델링 | kernel 기반의 비선형 확률 예측 |

---