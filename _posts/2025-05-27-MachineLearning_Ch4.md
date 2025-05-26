---
title: "Chapter04_Part1"
excerpt: "MachineLearning_Chap04_Part1"

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

# 📘 Chapter 4: Unsupervised Learning & Dimensionality Reduction

## Part 1. Principal Component Analysis (PCA)
1. Introduction to Dimensionality Reduction
2. Feature Selection vs. Feature Extraction
3. Linear Algebra Review for PCA
4. Principal Component Analysis (PCA)
   - Formulation 1: Linear Approximation
   - Formulation 2: Maximum Variance
   - Equivalence of Two Formulations
   - Eigen-decomposition and Eckart–Young Theorem
5. Choosing the Number of Components
6. Preprocessing and Limitations

---

## Part 2. Model Selection
1. Introduction to Model Selection
2. Tuning Parameters
3. Risk Estimation and Training Error
4. Holdout Method
5. Cross-Validation (K-fold, Stratified)
6. Bootstrap Method
7. Final Model Fitting
8. Beyond Grid Search (Random Search, Bayesian Optimization)

---

## Part 3. k-Means Clustering
1. Introduction to Clustering
2. k-Means Criterion and Algorithm
3. Optimization and Convergence
4. Initialization (Random, k-Means++)
5. Geometric Interpretation
6. Choosing the Number of Clusters

---

## Part 4. Gaussian Mixture Models (GMMs)
1. Limitations of k-Means
2. Gaussian Mixture Model Definition
3. Maximum Likelihood Estimation
4. Expectation-Maximization (EM) Algorithm for GMMs
5. E-Step and M-Step Derivations
6. GMM vs. k-Means

---

## Part 5. Expectation-Maximization Algorithm (General)
1. General EM Framework
2. ELBO (Evidence Lower Bound)
3. KL Divergence Interpretation
4. EM in General Notation
5. Summary and Applications

---

# Part 1. Principal Component Analysis (PCA)

## ✅ 주요 개념 흐름
PCA는 고차원 데이터를 저차원으로 축소하면서도 **정보 손실을 최소화**하는 대표적인 비지도 학습 방법이다.  
두 가지 관점에서 설명 가능:
1. **Linear Approximation 관점**: 데이터에 가장 잘 맞는 k차원 선형 부분공간을 찾음
2. **Maximum Variance 관점**: 분산을 가장 많이 보존하는 방향으로 투영

---

## ✅ 개념과 수식 정리

### 🎯 Dimensionality Reduction 목적
고차원 데이터 $$ x_1, \ldots, x_n \in \mathbb{R}^d $$를  
저차원 표현 $$ \theta \in \mathbb{R}^k \quad (k < d) $$로 변환

---

### 🎯 Feature Selection vs. Feature Extraction
- Feature Selection: 기존 특성에서 일부만 선택
- Feature Extraction: 기존 특성의 **선형/비선형 결합**으로 새로운 특성 생성

---

### 🎯 PCA 설정: Linear Approximation 관점

각 데이터에 대해 다음과 같이 근사:
$$ x_i \approx \mu + A\theta_i $$

- $$ \mu \in \mathbb{R}^d $$: 평균 벡터
- $$ A \in \mathbb{R}^{d \times k}, \quad A^\top A = I_k $$: 정규 직교 기저 (orthonormal)
- $$ \theta_i \in \mathbb{R}^k $$: 투영 좌표

---

### 🎯 PCA 최적화 문제 (Least Squares Formulation)

$$
\min_{\mu, A, \{\theta_i\}} \sum_{i=1}^n \left\| x_i - \mu - A \theta_i \right\|^2
$$

---

### 🎯 해 (Solution)

- 평균:  
  $$ \mu = \bar{x} = \frac{1}{n} \sum_{i=1}^n x_i $$
- 투영 좌표:  
  $$ \theta_i = A^\top (x_i - \bar{x}) $$
- 투영 기저:  
  $$ A = [u_1, \ldots, u_k] $$  
  → 공분산 행렬 $$ S $$의 상위 k개 고유벡터

---

### 🎯 PCA = 최소 제곱 근사 (Eckart–Young Theorem)

SVD 분해:  
$$ X = U\Sigma V^\top $$  
상위 k개 성분만 유지한 근사 행렬:  
$$ \hat{X} = U_k \Sigma_k V_k^\top $$  
→ 가장 낮은 오류의 rank-k 근사

---

### 🎯 PCA = 분산 극대화 문제

목표: 투영된 데이터의 총 분산 최대화  
$$
\max_{A \in \mathbb{R}^{d \times k}, A^\top A = I_k} \operatorname{tr}(A^\top S A)
$$

- $$ S $$: 공분산 행렬  
  $$ S = \frac{1}{n} \sum_{i=1}^n (x_i - \bar{x})(x_i - \bar{x})^\top $$

- 해:  
  $$ A = [u_1, \ldots, u_k] $$ (S의 상위 k개 고유벡터)

- 분산 총합:  
  $$ \sum_{j=1}^k \lambda_j $$

---

### 🎯 PCA의 두 관점의 등가성

- Reconstruction error 최소화  
  $$ \| X - AA^\top X \|_F^2 \longleftrightarrow \min $$
- 투영 분산 최대화  
  $$ \operatorname{tr}(A^\top S A) \longleftrightarrow \max $$

→ 동일한 A (top-k eigenvectors) 얻음

---

### 🎯 Component 수 k 선택 기준

전체 분산 중 비율:  
$$
\frac{\lambda_1 + \cdots + \lambda_k}{\lambda_1 + \cdots + \lambda_d} \geq 0.95
$$

→ 95% 이상 분산을 설명하는 최소 k 선택

---

### 🎯 PCA 전처리

- **Centering** (평균 제거):  
  $$ x_i \leftarrow x_i - \bar{x} $$
- **Scaling** (표준화):  
  $$ x_i \leftarrow \frac{x_i}{\sigma} $$

→ feature 간 scale 차이 제거

---

### 🎯 PCA의 한계와 확장

- 선형성만 모델링 가능 → 원형, 곡선형 구조 설명 불가
- 확장: **Kernel PCA**, **Nonlinear PCA**

---

## ✅ 정리 포인트
- PCA는 고차원 데이터를 저차원 선형 공간으로 투영하여 정보를 최대한 보존
- 두 관점: **재구성 오류 최소화 vs. 분산 최대화** → 동일한 해
- 공분산 행렬의 고유값 분해를 통해 주성분 방향 추출
- 데이터 정규화 및 고유값 누적 비율로 k 선택

---

# Part 2. Model Selection

## ✅ 주요 개념 흐름
Model Selection은 주어진 데이터에서 가장 일반화 성능이 좋은 모델 또는 하이퍼파라미터를 선택하는 과정이다.  
Training Error만으로 판단하면 Overfitting 위험이 있으므로, **추정된 일반화 오류(Risk)** 기반의 평가가 중요하다.  
이 때 사용할 수 있는 주요 방법은 Holdout, Cross-Validation, Bootstrap 등이다.

---

## ✅ 개념과 수식 정리

### 🎯 모델 선택이란?
- 여러 후보 모델 중 **가장 적절한 모델**을 선택하는 것
- Overfitting과 Underfitting 간의 trade-off 조절

---

### 🎯 튜닝 파라미터란?

- 학습 알고리즘이 직접 학습하지 않는 외부 설정값
- 예시:
  - $$ \lambda $$ (regularization in ridge)
  - $$ \sigma $$ (kernel width)
  - $$ k $$ (in k-NN)

---

### 🎯 Risk 정의

- **True Risk (expected risk)**:
$$
R(\hat{f}_\theta) = \mathbb{E}_{X,Y} \left[ L(Y, \hat{f}_\theta(X)) \right]
$$

- 문제: 실제 분포를 모르므로 $$ R(\hat{f}_\theta) $$는 계산 불가

---

### 🎯 대안: Empirical Risk (훈련 오차)

- **Training Error**:
$$
\hat{R}_{\text{train}}(\hat{f}_\theta) = \frac{1}{n} \sum_{i=1}^n L(y_i, \hat{f}_\theta(x_i))
$$

- 문제점: 학습 데이터에 대한 과적합 발생 가능

---

### 🎯 Holdout Validation

1. 데이터 $$ D $$를 train / validation으로 분할: $$ D = D_{\text{train}} \cup D_{\text{val}} $$
2. $$ \hat{f}_\theta $$ 학습 → validation set에서 성능 측정

- **Holdout Risk Estimate**:
$$
\hat{R}_{\text{holdout}}(\hat{f}_\theta) = \frac{1}{|D_{\text{val}}|} \sum_{(x_i, y_i) \in D_{\text{val}}} L(y_i, \hat{f}_\theta(x_i))
$$

- 장점: 구현 간단
- 단점: 데이터 낭비, 분할에 따라 편향 큼

---

### 🎯 K-Fold Cross-Validation

1. 데이터를 K개 블록으로 나눔
2. 각 fold를 validation으로 사용하며 나머지로 학습
3. 평균 오차 계산

- **K-Fold Estimate**:
$$
\hat{R}_{\text{CV}}(\hat{f}_\theta) = \frac{1}{K} \sum_{j=1}^K \hat{R}^{(j)}(\hat{f}_\theta^{(j)})
$$

- 일반적으로 $$ K=5 $$ 또는 $$ 10 $$ 사용
- **Stratified CV**: 클래스 비율 유지 → 분류 문제에서 중요

---

### 🎯 Bootstrap Method

1. 데이터에서 B번 복원 추출로 학습 데이터 생성
2. OOB(Out-Of-Bag) 데이터로 평가
3. 평균하여 최종 위험 추정

- **Bootstrap Risk**:
$$
\hat{R}_{\text{BS}}(\hat{f}_\theta) = \frac{1}{B} \sum_{b=1}^B \hat{R}^{(b)}_{\text{OOB}}(\hat{f}_\theta^{(b)})
$$

- 장점: 데이터 활용 효율 ↑
- 단점: 계산량 많고 오차 과추정 경향

---

### 🎯 최종 모델 학습

- 튜닝 파라미터 선택 후 → **전체 데이터로 재학습**  
→ 일반화 성능 향상 기대

---

### 🎯 Beyond Grid Search

- **Grid Search**: 전부 탐색 → 비효율
- **Random Search**: 랜덤 샘플링 → 효율적
- **Bayesian Optimization**: 이전 평가 결과 기반 탐색
- **Hyperband**: Random + Early Stopping

---

## ✅ 정리 포인트

- 모델 선택은 **일반화 오류 최소화**가 핵심
- Validation set 또는 Cross-Validation으로 **true risk 추정**
- Grid Search 대신 **Random / Bayesian / Hyperband** 추천
- 최종 모델은 **전체 데이터로 재학습**

---

# Part 3. k-Means Clustering

## ✅ 주요 개념 흐름
k-Means는 대표적인 **비지도 학습 클러스터링 알고리즘**으로, 각 데이터를 k개의 군집으로 분할하는 것이 목표다.  
"군집 내 거리 제곱합 최소화"를 통해 유사한 데이터끼리 묶는다.  
간단하지만 빠르고 직관적이며, 벡터 양자화, 전처리 등에 널리 활용된다.

---

## ✅ 개념과 수식 정리

### 🎯 Clustering이란?

- 입력: $$ \mathbf{x}_1, \dots, \mathbf{x}_n \in \mathbb{R}^d $$
- 출력: 군집 함수 $$ C: \{1, \dots, n\} \to \{1, \dots, k\} $$

목표: 같은 클러스터 내에서는 유사도 ↑, 서로 다른 클러스터는 유사도 ↓

---

### 🎯 k-Means Objective (Within-Cluster Sum of Squares)

$$
W(C) = \sum_{\ell=1}^k \sum_{i: C(i)=\ell} \left\| \mathbf{x}_i - \bar{\mathbf{x}}_\ell \right\|^2
$$

- $$ \bar{\mathbf{x}}_\ell $$: 클러스터 $$ \ell $$의 중심 (centroid)  
$$ \bar{\mathbf{x}}_\ell = \frac{1}{n_\ell} \sum_{j: C(j)=\ell} \mathbf{x}_j $$

---

### 🎯 k-Means 알고리즘 (Lloyd’s Algorithm)

1. 초기 클러스터 중심 $$ \{m_1, \dots, m_k\} $$ 설정
2. **Assignment step**: 각 $$ \mathbf{x}_i $$를 가장 가까운 중심에 할당
   $$ C(i) = \arg\min_\ell \| \mathbf{x}_i - m_\ell \| $$
3. **Update step**: 중심 재계산
   $$ m_\ell = \frac{1}{n_\ell} \sum_{i: C(i)=\ell} \mathbf{x}_i $$
4. 수렴할 때까지 반복

---

### 🎯 알고리즘의 수렴 보장

- 매 반복마다 $$ W(C) $$는 감소 or 유지
- 국소 최솟값(local minimum)에 수렴
- 전체 최적 해 보장은 없음 (초기화에 따라 달라짐)

---

### 🎯 Assignment Step의 수학적 정당성

- 각 데이터 $$ \mathbf{x}_i $$는 가장 가까운 중심에 할당됨:
$$
\left\| \mathbf{x}_i - m_{C(i)} \right\|^2 \leq \left\| \mathbf{x}_i - m_\ell \right\|^2 \quad \forall \ell
$$

→ 각 스텝에서 $$ W(C) $$는 감소

---

### 🎯 Update Step의 수학적 정당성

- 고정된 할당 $$ C(i) $$ 하에서 최적 중심 $$ m_\ell $$는 평균값:
$$
m_\ell = \arg\min_m \sum_{i: C(i)=\ell} \| \mathbf{x}_i - m \|^2 = \bar{\mathbf{x}}_\ell
$$

---

### 🎯 k-Means++ 초기화

- 첫 중심은 랜덤으로 선택
- 이후 각 데이터 $$ \mathbf{x} $$는 기존 중심과의 거리 $$ D(\mathbf{x})^2 $$에 비례하여 선택

→ 잘 퍼진 초기 중심 확보 → 성능 향상

---

### 🎯 클러스터 기하학적 성질

- 클러스터는 선형 분리 (Voronoi Partition)
- 모든 클러스터는 **볼록집합(convex set)**

---

### 🎯 클러스터 수 k 선택

- 정해진 k에 따라 결과 달라짐
- **Elbow Method**:  
  - $$ W(C) $$ vs. k 그래프 그려서 꺾이는 점(elbow) 찾기

---

### 🎯 k-Means의 한계점

- 클러스터가 구형(spherical), 등 크기라고 가정
- 초기화 민감도 높음
- k 필요
- 이상치(outlier)에 민감

---

## ✅ 정리 포인트

- k-Means는 **Within-cluster variance** 최소화
- Lloyd 알고리즘은 Assignment + Update 반복
- k-Means++로 초기화 성능 향상
- 클러스터 수 선택은 Elbow Method 등 활용
- GMM을 통해 soft assignment와 비정규 형태 확장 가능

---

# Part 4. Gaussian Mixture Models (GMMs)

## ✅ 주요 개념 흐름
k-Means는 단순하고 효율적이지만, 클러스터가 **구형이며 같은 크기**라는 제한을 가짐.  
GMM은 데이터를 **여러 개의 가우시안 분포로 모델링**하여, 비정형/비대칭/중첩된 군집도 처리 가능.  
GMM은 soft assignment(확률 기반 클러스터링)를 제공하며, **EM 알고리즘**으로 학습된다.

---

## ✅ 개념과 수식 정리

### 🎯 Multivariate Gaussian Distribution

$$
\phi(\mathbf{x}; \mu, \Sigma) = \frac{1}{(2\pi)^{d/2} |\Sigma|^{1/2}} \exp\left(-\frac{1}{2} (\mathbf{x} - \mu)^\top \Sigma^{-1} (\mathbf{x} - \mu) \right)
$$

- $$ \mu \in \mathbb{R}^d $$: 평균 벡터
- $$ \Sigma \in \mathbb{R}^{d \times d} $$: 공분산 행렬

---

### 🎯 Gaussian Mixture Model (GMM)

$$
f(\mathbf{x}) = \sum_{k=1}^K w_k \cdot \phi(\mathbf{x}; \mu_k, \Sigma_k)
$$

- $$ w_k \geq 0,\ \sum w_k = 1 $$
- $$ \mu_k, \Sigma_k $$: 각 component의 평균과 공분산

---

### 🎯 Soft Assignment (Responsibilities)

데이터 $$ \mathbf{x}_i $$가 클러스터 $$ k $$에 속할 확률:

$$
\gamma_{i,k} = \frac{w_k \cdot \phi(\mathbf{x}_i; \mu_k, \Sigma_k)}{\sum_{l=1}^K w_l \cdot \phi(\mathbf{x}_i; \mu_l, \Sigma_l)}
$$

---

### 🎯 Log-Likelihood

$$
\ell(\theta;\mathcal{X}) = \sum_{i=1}^n \log \left( \sum_{k=1}^K w_k \cdot \phi(\mathbf{x}_i; \mu_k, \Sigma_k) \right)
$$

→ 직접 최적화 불가 → EM 알고리즘 사용

---

### 🎯 EM 알고리즘 개요 (GMM 학습)

1. **E-step**: Soft assignment 계산
   $$
   \gamma_{i,k}^{(t)} = \frac{w_k^{(t)} \cdot \phi(\mathbf{x}_i; \mu_k^{(t)}, \Sigma_k^{(t)})}{\sum_{\ell=1}^K w_\ell^{(t)} \cdot \phi(\mathbf{x}_i; \mu_\ell^{(t)}, \Sigma_\ell^{(t)})}
   $$

2. **M-step**: 파라미터 업데이트
   - Mixing coefficient:
     $$
     w_k^{(t+1)} = \frac{1}{n} \sum_{i=1}^n \gamma_{i,k}^{(t)}
     $$
   - Mean:
     $$
     \mu_k^{(t+1)} = \frac{\sum_{i=1}^n \gamma_{i,k}^{(t)} \mathbf{x}_i}{\sum_{i=1}^n \gamma_{i,k}^{(t)}}
     $$
   - Covariance:
     $$
     \Sigma_k^{(t+1)} = \frac{\sum_{i=1}^n \gamma_{i,k}^{(t)} (\mathbf{x}_i - \mu_k^{(t+1)})(\mathbf{x}_i - \mu_k^{(t+1)})^\top}{\sum_{i=1}^n \gamma_{i,k}^{(t)}}
     $$

3. 반복 until 수렴 (log-likelihood 증가량 < ε)

---

### 🎯 GMM vs. k-Means

| 항목 | k-Means | GMM |
|------|---------|-----|
| 할당 방식 | Hard (1 or 0) | Soft (확률) |
| 클러스터 형태 | 구형(spherical) | 타원형(general Gaussian) |
| 모델링 | 거리 기반 | 확률 모델 기반 |
| 목적함수 | Within-cluster SSE | Log-likelihood 최대화 |
| 알고리즘 | Lloyd’s Algorithm | EM Algorithm |

---

### 🎯 GMM이 k-Means를 일반화하는 경우

- $$ \Sigma_k = \sigma^2 I,\ \sigma^2 \to 0 $$ 이면,
$$
\gamma_{i,k} \to \begin{cases}
1, & k = \arg\min_\ell \| \mathbf{x}_i - \mu_\ell \| \\
0, & \text{otherwise}
\end{cases}
$$

→ EM 알고리즘이 k-Means 알고리즘으로 수렴

---

## ✅ 정리 포인트

- GMM은 다양한 모양/크기의 군집을 모델링할 수 있는 **확률적 클러스터링 모델**
- EM 알고리즘은 **E-step (soft assignment)**과 **M-step (parameter update)**를 반복
- GMM은 k-Means보다 유연하며, 실제 데이터 분포에 대한 확률 모델링 가능
- k-Means는 GMM의 특수한 경우로 해석 가능

---

# Part 5. Expectation-Maximization (EM) Algorithm

## ✅ 주요 개념 흐름
EM 알고리즘은 **잠재변수(latent variable)**가 존재하는 확률 모델에서  
**최대우도추정(Maximum Likelihood Estimation)**을 효율적으로 수행하기 위한 반복적 최적화 알고리즘이다.  
GMM을 포함한 다양한 모델에 적용되며, 매 반복마다 **log-likelihood가 증가**하는 성질을 가진다.

---

## ✅ 개념과 수식 정리

### 🎯 문제 세팅

- 관측 데이터: $$ \{x_i\}_{i=1}^n $$
- 잠재 변수 (숨겨진 변수): $$ z $$
- 모델 파라미터: $$ \theta $$
- 목표: 최대화  
$$ \ell(\theta; x) = \log p(x; \theta) = \log \int p(x, z; \theta) dz $$

→ 직접 계산 어려움 (적분 안 됨)

---

### 🎯 Evidence Lower Bound (ELBO)

분해:
$$
\log p(x;\theta) = \log \int q(z) \frac{p(x, z; \theta)}{q(z)} dz
= \log \mathbb{E}_{q(z)} \left[ \frac{p(x, z; \theta)}{q(z)} \right]
$$

→ Jensen's Inequality 적용:
$$
\log p(x;\theta) \geq \mathbb{E}_{q(z)} \left[ \log \frac{p(x, z; \theta)}{q(z)} \right] =: \text{ELBO}(q, \theta)
$$

---

### 🎯 KL Divergence로 표현

$$
\log p(x;\theta) = \text{ELBO}(q, \theta) + \text{KL}(q(z) \| p(z \mid x; \theta))
$$

→ ELBO가 클수록 log-likelihood에 가까워짐  
→ E-step에서 KL을 최소화, M-step에서 ELBO를 최대화

---

### 🎯 EM Algorithm 과정

1. **E-step (잠재변수 분포 추정)**  
   현재 파라미터 $$ \theta^{(t)} $$에서 posterior 계산:  
   $$
   q^{(t)}(z) = p(z \mid x; \theta^{(t)})
   $$

2. **M-step (파라미터 최적화)**  
   E-step에서 얻은 $$ q^{(t)}(z) $$ 고정 후, 파라미터 업데이트:  
   $$
   \theta^{(t+1)} = \arg\max_\theta \mathbb{E}_{q^{(t)}(z)}[\log p(x, z; \theta)]
   $$

---

### 🎯 EM 알고리즘의 수렴 보장 (Ascent Property)

- 각 단계에서 log-likelihood는 감소하지 않음:
$$
\log p(x; \theta^{(t+1)}) \geq \log p(x; \theta^{(t)})
$$

→ 국소 최댓값으로 수렴 보장

---

### 🎯 여러 데이터의 경우 (iid 데이터)

- 관측: $$ \{x_i\}_{i=1}^n $$
- 잠재변수: $$ \{z_i\}_{i=1}^n $$
- 전체 log-likelihood:
$$
\ell(\theta) = \sum_{i=1}^n \log p(x_i; \theta)
$$

- ELBO:
$$
\sum_{i=1}^n \mathbb{E}_{q_i(z_i)} \left[ \log p(x_i, z_i; \theta) - \log q_i(z_i) \right]
$$

---

### 🎯 EM과 KL Divergence 관계

- 아래 항등식 항상 성립:
$$
\log p(x; \theta) = \text{ELBO}(q, \theta) + \text{KL}(q(z) \| p(z \mid x; \theta))
$$

→ E-step은 KL을 0으로 만들고,  
→ M-step은 ELBO를 최적화함

---

## ✅ 정리 포인트

- EM은 잠재변수를 포함한 확률모형에서 최대우도 추정을 위한 최적화 기법
- E-step: posterior 계산 → q 업데이트
- M-step: q 고정 후 θ 업데이트
- 매 반복마다 log-likelihood 증가 → 수렴 보장
- GMM, HMM, 결측값 보정 등 다양한 모델에 활용 가능

---

# Part 5. Expectation-Maximization (EM) Algorithm

## ✅ 주요 개념 흐름
EM 알고리즘은 **잠재변수(latent variable)**가 존재하는 확률 모델에서  
**최대우도추정(Maximum Likelihood Estimation)**을 효율적으로 수행하기 위한 반복적 최적화 알고리즘이다.  
GMM을 포함한 다양한 모델에 적용되며, 매 반복마다 **log-likelihood가 증가**하는 성질을 가진다.

---

## ✅ 개념과 수식 정리

### 🎯 문제 세팅

- 관측 데이터: $$ \{x_i\}_{i=1}^n $$
- 잠재 변수 (숨겨진 변수): $$ z $$
- 모델 파라미터: $$ \theta $$
- 목표: 최대화  
$$ \ell(\theta; x) = \log p(x; \theta) = \log \int p(x, z; \theta) dz $$

→ 직접 계산 어려움 (적분 안 됨)

---

### 🎯 Evidence Lower Bound (ELBO)

분해:
$$
\log p(x;\theta) = \log \int q(z) \frac{p(x, z; \theta)}{q(z)} dz
= \log \mathbb{E}_{q(z)} \left[ \frac{p(x, z; \theta)}{q(z)} \right]
$$

→ Jensen's Inequality 적용:
$$
\log p(x;\theta) \geq \mathbb{E}_{q(z)} \left[ \log \frac{p(x, z; \theta)}{q(z)} \right] =: \text{ELBO}(q, \theta)
$$

---

### 🎯 KL Divergence로 표현

$$
\log p(x;\theta) = \text{ELBO}(q, \theta) + \text{KL}(q(z) \| p(z \mid x; \theta))
$$

→ ELBO가 클수록 log-likelihood에 가까워짐  
→ E-step에서 KL을 최소화, M-step에서 ELBO를 최대화

---

### 🎯 EM Algorithm 과정

1. **E-step (잠재변수 분포 추정)**  
   현재 파라미터 $$ \theta^{(t)} $$에서 posterior 계산:  
   $$
   q^{(t)}(z) = p(z \mid x; \theta^{(t)})
   $$

2. **M-step (파라미터 최적화)**  
   E-step에서 얻은 $$ q^{(t)}(z) $$ 고정 후, 파라미터 업데이트:  
   $$
   \theta^{(t+1)} = \arg\max_\theta \mathbb{E}_{q^{(t)}(z)}[\log p(x, z; \theta)]
   $$

---

### 🎯 EM 알고리즘의 수렴 보장 (Ascent Property)

- 각 단계에서 log-likelihood는 감소하지 않음:
$$
\log p(x; \theta^{(t+1)}) \geq \log p(x; \theta^{(t)})
$$

→ 국소 최댓값으로 수렴 보장

---

### 🎯 여러 데이터의 경우 (iid 데이터)

- 관측: $$ \{x_i\}_{i=1}^n $$
- 잠재변수: $$ \{z_i\}_{i=1}^n $$
- 전체 log-likelihood:
$$
\ell(\theta) = \sum_{i=1}^n \log p(x_i; \theta)
$$

- ELBO:
$$
\sum_{i=1}^n \mathbb{E}_{q_i(z_i)} \left[ \log p(x_i, z_i; \theta) - \log q_i(z_i) \right]
$$

---

### 🎯 EM과 KL Divergence 관계

- 아래 항등식 항상 성립:
$$
\log p(x; \theta) = \text{ELBO}(q, \theta) + \text{KL}(q(z) \| p(z \mid x; \theta))
$$

→ E-step은 KL을 0으로 만들고,  
→ M-step은 ELBO를 최적화함

---

## ✅ 정리 포인트

- EM은 잠재변수를 포함한 확률모형에서 최대우도 추정을 위한 최적화 기법
- E-step: posterior 계산 → q 업데이트
- M-step: q 고정 후 θ 업데이트
- 매 반복마다 log-likelihood 증가 → 수렴 보장
- GMM, HMM, 결측값 보정 등 다양한 모델에 활용 가능