---
title: "Chapter05"
excerpt: "MachineLearning_Chap05"

categories:
  - MachineLearning
tags:
  - [Machine Learning, 머신러닝]

permalink: /categories/MachineLearning/Chapter05_MachineLearning

toc: true
toc_sticky: true

date: 2025-05-27
last_modified_at: 2025-05-27
---

# 📘 Chapter 5: Multilayer Perceptrons & Reinforcement Learning

## Part 1. Multilayer Perceptrons (MLPs)
1. Feedforward Neural Networks
2. Structure of MLP
3. Forward Pass and Algorithm
4. Activation Functions (Sigmoid, tanh, ReLU)
5. Mathematical Formulation
6. MLPs for Regression and Classification
7. Softmax and Prediction
8. Empirical Risk Minimization
9. Backpropagation Algorithm
10. Practical Considerations
11. Summary

---

## Part 2. Reinforcement Learning (RL)
1. Introduction and Framework
2. Policies (Stochastic vs Deterministic)
3. Returns (Episodic vs Continuing)
4. Value Functions: Vπ and Qπ
5. Multi-Armed Bandit Problem
6. Action Selection (ε-Greedy, Exploration vs Exploitation)
7. MDPs and Bellman Equations
8. Solving Bellman Equations
9. Policy Iteration vs Value Iteration
10. Learning via Interaction (Model-Free RL)
    - Monte Carlo Methods
    - Temporal Difference (TD) Learning
    - SARSA
    - Q-Learning
11. Policy Gradient Methods
    - REINFORCE
    - Baseline and Advantage Function
    - Gradient Derivation

---

# Part 1. Multilayer Perceptrons (MLPs)

## ✅ 주요 개념 흐름
Multilayer Perceptron (MLP)은 Feedforward Neural Network(FNN)의 대표적인 형태로,  
입력 → 은닉층 → 출력층 구조를 가지며, 각 층은 **선형변환 + 비선형 활성화 함수**로 구성됨.  
학습은 손실 함수를 최소화하도록 **역전파(backpropagation)**를 통해 수행된다.

---

## ✅ 개념과 수식 정리

### 🎯 Forward Pass

입력 $$ \mathbf{x} $$에 대해 출력 $$ f(\mathbf{x}) $$를 계산하는 과정:

- 초기값:
$$ z^{(0)} = \mathbf{x} $$

- 각 층 ℓ (1 ≤ ℓ ≤ L):
$$
a^{(\ell)} = W^{(\ell)} z^{(\ell-1)} \\
z^{(\ell)} = \sigma(a^{(\ell)})
$$

- 출력층 (활성화 X):
$$ f(\mathbf{x}) = a^{(L)} $$

---

### 🎯 활성화 함수 (Activation Functions)

- **Sigmoid**:
$$ \sigma(t) = \frac{1}{1 + e^{-t}} $$
→ 범위: (0, 1), gradient vanishing 문제 존재

- **Tanh**:
$$ \sigma(t) = \tanh(t) = \frac{e^t - e^{-t}}{e^t + e^{-t}} $$
→ 범위: (−1, 1), zero-centered

- **ReLU**:
$$ \sigma(t) = \max(0, t) $$
→ 범위: [0, ∞), 연산 빠르고 gradient vanishing 문제 완화

---

### 🎯 MLP의 목적 함수

#### ▪️ Regression (Mean Squared Error):
- Scalar output:
$$ R(\theta) = \sum_{n=1}^N (y_n - f(x_n))^2 $$
- Vector output:
$$ R(\theta) = \sum_{n=1}^N \| y_n - f(x_n) \|^2 $$

#### ▪️ Classification (Cross Entropy):
$$ R(\theta) = - \sum_{n=1}^N \sum_{k=1}^K y_{nk} \log \psi_k(f(x_n)) $$

- Softmax:
$$ \psi_k(\mathbf{v}) = \frac{e^{v_k}}{\sum_{j=1}^K e^{v_j}} $$

---

### 🎯 Backpropagation 핵심 수식

- 에러 시그널:
$$ \delta_{ni}^{(\ell)} = \frac{\partial R_n}{\partial a_{ni}^{(\ell)}} $$

- weight gradient:
$$ \frac{\partial R_n}{\partial w_{ij}^{(\ell)}} = \delta_{ni}^{(\ell)} z_{nj}^{(\ell-1)} $$

- 역전파 (은닉층):
$$ \delta_{ni}^{(\ell)} = \sigma'(a_{ni}^{(\ell)}) \sum_k w_{ki}^{(\ell+1)} \delta_{nk}^{(\ell+1)} $$

---

### 🎯 출력층 에러 (예: Regression)
$$ \delta_{n1}^{(L)} = \frac{\partial R_n}{\partial a_{n1}^{(L)}} = -2(y_n - a_{n1}^{(L)}) $$

---

## ✅ Practical Tips

1. **ReLU 사용** → 빠르고 gradient 문제 완화  
2. **데이터 표준화** (sigmoid 사용 시 특히 중요)  
3. **가중치 초기화**: 작은 랜덤값 (0으로 초기화하면 학습 불가)

---

## ✅ 정리 포인트

- MLP는 층별로 $$ a^{(\ell)} = W^{(\ell)} z^{(\ell-1)} $$ 계산 후 비선형 $$ \sigma $$ 적용
- 출력층은 활성화 없이 $$ f(x) = a^{(L)} $$
- 목적 함수는 Regression → MSE, Classification → Cross Entropy
- Backpropagation을 통해 각 weight의 gradient 계산
- 실전에서는 **ReLU + 정규화 + 초기화**가 중요

---

# Part 2. Reinforcement Learning (RL)

## ✅ 주요 개념 흐름
Reinforcement Learning(RL)은 에이전트가 **환경과 상호작용**하며 **보상 누적 최대화**를 학습하는 프레임워크다.  
환경은 보상을 통해 목표를 전달하고, 에이전트는 상태에 따라 행동을 선택하는 **정책(policy)**을 학습한다.  
MDP 모델을 기반으로, 다양한 방식으로 최적 정책을 찾는다 (Value-based, Policy-based 등).

---

## ✅ 개념과 수식 정리

### 🎯 MDP (Markov Decision Process)

- 상태: $$ s \in \mathcal{S} $$
- 행동: $$ a \in \mathcal{A} $$
- 보상: $$ r \in \mathbb{R} $$
- 전이확률: $$ P(s' \mid s, a) $$
- 감가율: $$ \gamma \in [0, 1) $$

---

### 🎯 정책 (Policy)

- 확률적 정책:
$$ \pi(a \mid s) = P(a_t = a \mid s_t = s) $$

- 결정적 정책:
$$ a = \pi(s) $$

---

### 🎯 Return (누적 보상)

- **Episodic**:
$$ R_t = r_{t+1} + r_{t+2} + \dots + r_T $$

- **Continuing**:
$$ R_t = \sum_{k=0}^\infty \gamma^k r_{t+k+1} $$

---

### 🎯 Value Functions

- **State Value**:
$$ V^\pi(s) = \mathbb{E}_\pi[R_t \mid s_t = s] $$

- **Action Value**:
$$ Q^\pi(s, a) = \mathbb{E}_\pi[R_t \mid s_t = s, a_t = a] $$

- **Advantage Function**:
$$ A^\pi(s, a) = Q^\pi(s, a) - V^\pi(s) $$

---

### 🎯 Bellman Equations

- **Expectation Equation (V)**:
$$
V^\pi(s) = \sum_a \pi(a \mid s) \sum_{s'} P(s' \mid s, a) [R(s, a, s') + \gamma V^\pi(s')]
$$

- **Expectation Equation (Q)**:
$$
Q^\pi(s, a) = \sum_{s'} P(s' \mid s, a) [R(s, a, s') + \gamma \sum_{a'} \pi(a' \mid s') Q^\pi(s', a')]
$$

---

### 🎯 Optimality Equations

- **Optimal V\* (nonlinear)**:
$$
V^*(s) = \max_a \sum_{s'} P(s' \mid s, a)[R(s, a, s') + \gamma V^*(s')]
$$

- **Optimal Q\* (nonlinear)**:
$$
Q^*(s, a) = \sum_{s'} P(s' \mid s, a)[R(s, a, s') + \gamma \max_{a'} Q^*(s', a')]
$$

---

### 🎯 Policy Iteration

1. Policy Evaluation: $$ V^\pi $$ 계산  
2. Policy Improvement: $$ \pi(s) \leftarrow \arg\max_a Q^\pi(s, a) $$  
→ 반복하여 $$ \pi \to \pi^* $$

---

### 🎯 Value Iteration

$$
V_{k+1}(s) = \max_a \sum_{s'} P(s' \mid s, a)[R(s, a, s') + \gamma V_k(s')]
$$

→ 반복 후 $$ V^* $$ 수렴

---

### 🎯 Model-Free Learning (환경 모델 없이 학습)

#### ▪️ Monte Carlo (MC):
$$ V(s) \leftarrow \text{average of returns } R_t $$  
→ 에피소드 종료 후 업데이트

#### ▪️ TD(0):
$$ V(s_t) \leftarrow V(s_t) + \eta [r_{t+1} + \gamma V(s_{t+1}) - V(s_t)] $$  
→ 온라인/부트스트랩 방식

---

### 🎯 Control 알고리즘

#### ▪️ SARSA (On-policy):
$$ Q(s_t, a_t) \leftarrow Q(s_t, a_t) + \eta [r_{t+1} + \gamma Q(s_{t+1}, a_{t+1}) - Q(s_t, a_t)] $$

#### ▪️ Q-Learning (Off-policy):
$$ Q(s_t, a_t) \leftarrow Q(s_t, a_t) + \eta [r_{t+1} + \gamma \max_{a'} Q(s_{t+1}, a') - Q(s_t, a_t)] $$

---

### 🎯 Policy Gradient

- 목표 함수:
$$ J(\theta) = \mathbb{E}_{\pi_\theta} [R(\tau)] $$

- 기본 gradient:
$$
\nabla_\theta J(\theta) = \mathbb{E}_{\pi_\theta} \left[ \sum_t \nabla_\theta \log \pi_\theta(a_t \mid s_t) R_t \right]
$$

- Baseline 적용:
$$
\nabla_\theta J(\theta) = \mathbb{E} \left[ \sum_t \nabla_\theta \log \pi_\theta(a_t \mid s_t)(R_t - b(s_t)) \right]
$$

- Advantage 기반:
$$
\nabla_\theta J(\theta) \approx \mathbb{E} [\nabla_\theta \log \pi_\theta(a_t \mid s_t) A^\pi(s_t, a_t)]
$$

---

## ✅ 정리 포인트

- RL은 상태-행동-보상 순환 구조로, 누적 보상을 최대화하는 정책을 학습함
- Bellman 식은 가치 함수를 재귀적으로 정의
- Value Iteration / Policy Iteration → 모델 기반 방식
- MC, TD, SARSA, Q-Learning → 모델 없이 학습하는 방식
- Policy Gradient는 파라미터화된 정책을 직접 최적화