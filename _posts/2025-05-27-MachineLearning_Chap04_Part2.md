---
title: "Chapter04_Part2"
excerpt: "MachineLearning_Chap04_Part2"

categories:
  - MachineLearning
tags:
  - [Machine Learning, 머신러닝]

permalink: /categories/MachineLearning/Chapter04_Part2_MachineLearning

toc: true
toc_sticky: true

date: 2025-05-27
last_modified_at: 2025-05-27
---

# 📘 Chapter 4 Part 2: Advanced Unsupervised Learning

## Part 1. Kernel Density Estimation (KDE)
1. Introduction to Density Estimation
2. Applications: Classification, Clustering, Anomaly Detection
3. Kernel Density Estimation
   - Kernel Functions and Properties
   - Effect of Bandwidth (σ)
4. Model Selection in KDE
   - Integrated Squared Error (ISE)
   - Leave-One-Out Cross Validation (LOOCV)
   - LS-LOOCV Criterion

---

## Part 2. Kernel Principal Component Analysis (Kernel PCA)
1. Motivation and Limitations of Linear PCA
2. Kernel Trick and Nonlinear Feature Mapping
3. KPCA Algorithm
   - Eigenvalue Problem in Feature Space
   - Computing α using Kernel Matrix
   - Projection of New Data Points
4. Summary and Implementation Details

---

## Part 3. Spectral Clustering
1. Motivation and Introduction
2. Similarity Graphs and Laplacian
3. Spectral Clustering Algorithm
   - Eigenvectors of Graph Laplacian
   - Embedding and Clustering via k-means
4. Graph Cut Perspective (RatioCut & Ncut)
5. Perturbation Theory and Generalization
6. Nonlinear Dimensionality Reduction Interpretation
7. Model Selection: Number of Clusters

---

# Part 1. Kernel Density Estimation (KDE)

## ✅ 주요 개념 흐름
Kernel Density Estimation은 비모수적 방식으로 확률 밀도 함수를 추정하는 방법이다.  
클래스 분류, 클러스터링, 이상탐지 등 다양한 비지도 학습 응용에서 사용된다.  
데이터에 커널 함수를 얹어서 부드러운 확률 밀도 곡선을 만든다.

---

## ✅ 개념과 수식 정리

### 🎯 밀도 추정 (Density Estimation)
- 목표: 데이터 $$ \{X_1, \dots, X_n\} $$로부터 분포 $$ f(x) $$ 추정

---

### 🎯 KDE 기본 수식

$$
\hat{f}_\sigma(x) = \frac{1}{n} \sum_{i=1}^n k_\sigma(x - X_i)
$$

- $$ k_\sigma(y) = \frac{1}{\sigma^d} k\left(\frac{y}{\sigma}\right) $$
- $$ \sigma $$: Bandwidth (핵심 조절 파라미터)

---

### 🎯 커널 함수의 조건

- 정규화: $$ \int k(y)\,dy = 1 $$
- 비음성: $$ k(y) \geq 0 $$
- 대칭: $$ k(y) = \psi(\|y\|) $$ (radial kernel)

---

### 🎯 커널 함수 예시

- **Gaussian**:
$$
k(y) = \frac{1}{(2\pi)^{d/2}} \exp\left(-\frac{1}{2} \|y\|^2 \right)
$$

- **Uniform**:
$$
k(y) = \frac{1}{C} \cdot \mathbf{1}_{\|y\| \leq 1}
$$

- 기타: Epanechnikov, Triangular, Quartic

---

### 🎯 KDE의 직관

- 각 데이터 포인트에 커널을 하나씩 얹어 더한 형태
- 데이터 밀도가 높은 구간에 더 높은 $$ \hat{f}(x) $$ 값

---

### 🎯 Bandwidth (σ)의 역할

- **작은 σ** → 뾰족한 추정 (high variance)
- **큰 σ** → 부드러운 추정 (high bias)

→ Bias-Variance 트레이드오프 존재

---

### 🎯 KDE vs Histogram

| 항목 | KDE | Histogram |
|------|-----|-----------|
| 형태 | 연속적 | 이산적 |
| 민감도 | σ | bin width / location |
| 부드러움 | 높음 | 낮음 |

---

## ✅ KDE 기반 응용

### 🔹 분류 (Classification)
- Bayes classifier:
$$
x \rightarrow \arg\max_k \pi_k g_k(x)
$$

- 추정된 밀도 사용 (Plug-in classifier):
$$
x \rightarrow \arg\max_k \hat{\pi}_k \hat{g}_k(x)
$$

---

### 🔹 클러스터링 (Density-based)
- 모드 기반 클러스터링: 높은 밀도 영역 중심으로 군집 형성
- Mean-Shift 알고리즘 활용 가능

---

### 🔹 이상 탐지 (Anomaly Detection)
- 규칙:
$$
x \text{ is anomaly if } \hat{f}(x) < \gamma
$$

- $$ \gamma $$: threshold 값

---

## ✅ 모델 선택 (Bandwidth 선택)

### 🎯 성능 기준: ISE (Integrated Squared Error)

$$
ISE(\sigma) = \int \left(\hat{f}_\sigma(x) - f(x) \right)^2 dx
$$

→ $$ \sigma $$를 ISE 최소화하도록 선택

---

### 🎯 ISE 전개

$$
ISE(\sigma) = \int \hat{f}_\sigma(x)^2 dx - 2 \int \hat{f}_\sigma(x) f(x) dx + \int f(x)^2 dx
$$

→ 마지막 항은 $$ \sigma $$와 무관 → 무시

---

### 🎯 첫 번째 항 추정

(Gaussian 커널일 경우)

$$
\int \hat{f}_\sigma(x)^2 dx = \frac{1}{n^2} \sum_{i=1}^n \sum_{j=1}^n k_{\sqrt{2}\sigma}(X_i - X_j)
$$

---

### 🎯 두 번째 항 추정 (LOOCV 사용)

$$
\int \hat{f}_\sigma(x) f(x)\,dx \approx \frac{1}{n} \sum_{i=1}^n \hat{f}_{\sigma}^{(-i)}(X_i)
$$

- Leave-one-out KDE:
$$
\hat{f}_{\sigma}^{(-i)}(x) = \frac{1}{n-1} \sum_{j \ne i} k_\sigma(x - X_j)
$$

---

### 🎯 최종 성능 평가 함수: LS-LOOCV

$$
LS\text{-}LOOCV(\sigma) = \frac{1}{n^2} \sum_{i=1}^n \sum_{j=1}^n k_{\sqrt{2}\sigma}(X_i - X_j) - \frac{2}{n(n - 1)} \sum_{i=1}^n \sum_{j \ne i} k_\sigma(X_i - X_j)
$$

→ $$ \sigma $$를 최소화하는 값 선택

---

## ✅ 정리 포인트

- KDE는 데이터로부터 부드러운 밀도 추정을 제공하는 비모수 기법
- 핵심 하이퍼파라미터는 **Bandwidth σ**
- **분류, 클러스터링, 이상탐지**에 활용됨
- 적절한 σ 선택은 **Cross-Validation 기반 ISE 최소화**로 수행

---

# Part 2. Kernel PCA (KPCA)

## ✅ 주요 개념 흐름
PCA는 선형 구조를 가정하므로 비선형 데이터에 한계가 있음.  
KPCA는 데이터를 **비선형 고차원 공간**으로 매핑한 뒤, 그 공간에서 **선형 PCA**를 수행함.  
이 때 **커널 트릭(kernel trick)**을 통해 고차원 매핑 없이도 내적 계산만으로 PCA를 구현할 수 있음.

---

## ✅ 개념과 수식 정리

### 🎯 PCA 요약 (선형 PCA)

- 공분산 행렬:
$$
S = \frac{1}{n} \sum_{i=1}^n \mathbf{x}_i \mathbf{x}_i^\top
$$

- 고유값 분해:
$$
S = U \Lambda U^\top
$$

→ $$ u_1, u_2, \dots $$: 주성분 방향  
→ $$ \mathbf{x}_i $$를 $$ u_j $$에 투영하여 차원 축소

---

### 🎯 KPCA 핵심 아이디어

1. 데이터 $$ \mathbf{x}_i \in \mathbb{R}^d $$를 고차원 공간으로 매핑:  
   $$ \Phi(\mathbf{x}_i) \in \mathcal{H} $$

2. 공분산 행렬:
$$
\bar{S} = \frac{1}{n} \sum_{i=1}^n \Phi(\mathbf{x}_i) \Phi(\mathbf{x}_i)^\top
$$

3. 주성분 방향 $$ u_j $$는 다음을 만족:
$$
\bar{S} u_j = \lambda_j u_j
$$

→ 단, $$ u_j \in \text{span}\{\Phi(x_1), \dots, \Phi(x_n)\} $$ 이므로:
$$
u_j = \sum_{i=1}^n \alpha_{ji} \Phi(x_i)
$$

---

### 🎯 고유값 문제 변환 (커널 기반)

- 커널 행렬 정의:
$$
K_{ij} = k(x_i, x_j) = \langle \Phi(x_i), \Phi(x_j) \rangle
$$

- 최종 고유값 문제:
$$
K \alpha_j = n \lambda_j \alpha_j
$$

→ $$ \alpha_j $$: 커널 공간에서의 고유벡터

---

### 🎯 정규화 조건

- 고차원 공간에서의 정규화:
$$
\|u_j\|^2 = \alpha_j^\top K \alpha_j = 1
$$

- 고유벡터 norm:
$$
\|\alpha_j\|^2 = \frac{1}{n \lambda_j}
$$

---

### 🎯 새로운 데이터의 투영

- 새로운 데이터 $$ x $$를 j번째 성분으로 투영:
$$
y_j = u_j^\top \Phi(x) = \sum_{i=1}^n \alpha_{ji} k(x_i, x)
$$

→ 고차원 공간 계산 없이 **커널만으로 투영값 계산 가능**

---

### 🎯 KPCA 요약 알고리즘

1. 커널 행렬 K 계산 (Gaussian, Polynomial 등)
2. 필요시 중심화:
$$
K_{\text{centered}} = K - \frac{1}{n}K\mathbf{1} - \frac{1}{n}\mathbf{1}K + \frac{1}{n^2}\mathbf{1}K\mathbf{1}
$$

3. 고유값 분해:  
   $$ K = A \Lambda A^\top $$
4. 고유벡터 정규화:
   $$ \alpha_j = \frac{1}{\sqrt{n \lambda_j}} \tilde{\alpha}_j $$
5. 새로운 샘플 $$ x $$ 투영:
   $$ y_j = \sum_{i=1}^n \alpha_{ji} k(x_i, x) $$

---

## ✅ 정리 포인트

- KPCA는 **선형 PCA의 커널 확장**
- 고차원 매핑 없이 내적 계산만으로 **비선형 구조 반영 가능**
- 커널 행렬의 고유값 분해를 통해 주성분 획득
- 새로운 데이터 투영도 커널 함수만으로 계산 가능

---

# Part 3. Spectral Clustering

## ✅ 주요 개념 흐름
Spectral Clustering은 **그래프 기반의 클러스터링 알고리즘**으로,  
복잡하고 비선형적인 데이터 구조에서도 효과적으로 군집화할 수 있다.  
핵심 아이디어는 **유사도 그래프 → 라플라시안 행렬 → 고유벡터**를 이용하여  
데이터를 임베딩한 후 **k-means**로 군집화하는 것이다.

---

## ✅ 개념과 수식 정리

### 🎯 입력 데이터

$$
X = \{x_1, x_2, \dots, x_n\} \subset \mathbb{R}^d
$$

---

### 🎯 유사도 그래프 & 커널 함수

- 커널 (예: Gaussian)
$$
w_{ij} = \exp\left( -\frac{\|x_i - x_j\|^2}{2\sigma^2} \right)
$$

- 유사도 행렬 W (대칭)
- degree matrix:
$$
D_{ii} = \sum_{j} w_{ij}
$$

---

### 🎯 Graph Laplacian

- **Unnormalized Laplacian**:
$$
L = D - W
$$

- **Properties**:
  - $$ L $$은 symmetric, PSD
  - $$ \lambda_1 = 0, \quad u_1 = \mathbf{1} $$
  - $$ f^\top L f = \frac{1}{2} \sum_{i,j} w_{ij} (f_i - f_j)^2 $$

---

### 🎯 Spectral Clustering 알고리즘

1. **유사도 행렬 W** 생성
2. **그래프 라플라시안 L** 계산
3. L의 **작은 고유값 K개**에 대응하는 **고유벡터 u₁,…,u_K** 추출
4. 행렬 $$ Y = [u_1,\dots,u_K] \in \mathbb{R}^{n \times K} $$
5. $$ Y $$의 행 벡터들에 대해 **k-means** 수행
6. 최종 군집 결과 반환

---

### 🎯 Graph Cut 관점

- **RatioCut**:
$$
\text{RatioCut}(A_1,\dots,A_K) = \frac{1}{2} \sum_{k=1}^K \frac{W(A_k, \bar{A}_k)}{|A_k|}
$$

- **Ncut (Normalized Cut)**:
$$
\text{Ncut}(A_1,\dots,A_K) = \frac{1}{2} \sum_{k=1}^K \frac{W(A_k, \bar{A}_k)}{\text{vol}(A_k)}
$$

→ Spectral Clustering은 이러한 cut 문제를 **완화(relaxation)**한 형태로 해결

---

### 🎯 RatioCut 2-way 분할 해석

- 벡터 $$ f_A $$ 정의:
$$
f_{Ai} =
\begin{cases}
+ \sqrt{\frac{|\bar{A}|}{|A|}}, & i \in A \\
- \sqrt{\frac{|A|}{|\bar{A}|}}, & i \in \bar{A}
\end{cases}
$$

- 이 때:
$$
f_A^\top L f_A = n \cdot \text{RatioCut}(A, \bar{A})
$$

---

### 🎯 최적화 문제 완화 (Relaxation)

- 원래는 NP-hard → 연속 최적화로 완화:
$$
\min_{f \in \mathbb{R}^n,\ f \perp \mathbf{1},\ \|f\|^2 = n} \frac{f^\top L f}{f^\top f}
$$

- 해:
$$
f^* = u_2
$$

→ 두 번째 고유벡터로 분할 가능

---

### 🎯 Perturbation 관점

- 이상적인 경우: L은 block diagonal → null space 차원 = K
- 현실에서는 block 구조에 잡음이 존재함
- 그래도 고유벡터 $$ u_1,\dots,u_K $$는 여전히 각 클러스터 정보를 담고 있음
- 행 $$ y_i = [u_1(i), u_2(i), ..., u_K(i)] $$를 k-means로 분류

---

### 🎯 Spectral Clustering = 비선형 차원 축소 + k-means

- 유사도 커널 → 비선형 구조 반영
- Laplacian의 고유벡터 → 비선형 임베딩
- 이후 k-means 적용

---

## ✅ 정리 포인트

- Spectral Clustering은 그래프 기반 클러스터링 알고리즘
- Laplacian 고유벡터를 이용해 데이터 임베딩 후 k-means 적용
- RatioCut, Ncut 등 그래프 컷을 완화하여 고유값 문제로 해결
- Laplacian의 고유벡터는 클러스터 구조를 내포함
- GMM/k-means가 잘 못하는 복잡 구조도 잘 분리 가능

---

