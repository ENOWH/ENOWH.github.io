---
title: "Chapter02_MicroElectronics"
excerpt: "전자회로 Chap02 전체 흐름"

categories:
  - MicroElectronics
tags:
  - [MicroElectronics]

permalink: /categories/MicroElectronics/Chapter02_MicroElectronics

toc: true
toc_sticky: true

date: 2025-04-23
last_modified_at: 2025-04-23
---


# ⚛️ Chapter 2: Basic Physics of Semiconductors

## 📑 전체 구성

### 🟦 2.1 Semiconductor Materials and Their Properties (pp. 3–21)
- 반도체 물질의 종류, 도핑, 전하 운반자, 이동 메커니즘 (drift/diffusion)
- 고유 반도체 vs. 도핑된 반도체
- 전류 흐름, 이동도, 확산, Einstein’s Relation

### 🟦 2.2 pn Junction (pp. 22–39)
- pn 접합 형성 원리: 확산 vs. 드리프트
- 균형 상태, forward bias, reverse bias에서의 전류 흐름
- 고유 전위(built-in potential), 소수 캐리어 분포

### 🟦 2.3 Reverse Breakdown (pp. 43–44)
- 정전압 역방향 항복(Zener) vs. Avalanche breakdown
- 도핑 농도에 따른 breakdown 메커니즘 차이

### 🟦 2.4 Chapter Summary (p. 45)
- np = ni², 전하 수송, pn 접합의 3가지 모드 요약
- forward bias 시 지수 함수 형태의 전류 발생


---

# ⚛️ 2.1 Semiconductor Materials and Their Properties

## 🌱 개념 흐름 요약

- 반도체는 **마이크로전자공학의 핵심 재료**로 사용
- pn 접합을 이해하려면:
  1. 전하 운반자의 거동
  2. 캐리어 밀도 제어 방법
  3. 전류 흐름 메커니즘 (drift, diffusion)
- 반도체 재료는 실리콘(Si)을 중심으로 다룸

---

## 🔑 개념별 정리 (개념 ↔ 수식 연결 중심)

---

### ✅ 원자 구조와 공유 결합

- 실리콘(Si)은 **4개의 원자가 전자**를 가짐 → 이웃 원자들과 공유 결합 형성
- 온도가 올라가면 결합이 깨지고 자유전자 생성

📌 중요한 현상:  
- 자유전자 생성
- **구멍(hole)** 생성 (전자 이동의 결과)

---

### ✅ 전자-정공 쌍 (Electron-Hole Pair)

- 전자가 결합을 깨고 자유전자가 되면, 남은 자리에 **정공(hole)**이 생김
- 자유전자와 정공은 전하 운반자로 작용

---

### ✅ 자유전자 농도 (Intrinsic Semiconductor)

- 밴드갭 에너지 ($E_g$)를 넘는 에너지가 필요
- 자유전자 밀도는 온도 $T$와 $E_g$에 따라 지수적으로 변동

📐 자유전자 농도:
$$
n_i \propto \exp\left( -\frac{E_g}{2kT} \right)
$$

- $k$: Boltzmann 상수
- $E_g$: 밴드갭 에너지 (실리콘: 1.12 eV)
- $T$: 절대 온도 (K)

---

### ✅ 도핑 (Doping)

- 순수 Si에 불순물 원소를 추가하여 전기적 특성 조정
- **n형 도핑**: (ex. 인(P), 15족 원소) → 자유전자 증가
- **p형 도핑**: (ex. 붕소(B), 13족 원소) → 정공 증가

📌 핵심 관계:
$$
np = n_i^2
$$

- $n$: 자유전자 밀도
- $p$: 정공 밀도
- $n_i$: 고유 반도체의 자유전자 밀도

---

### ✅ 전하 운반자의 이동 (Charge Transport)

#### (1) Drift (전기장에 의한 이동)

- 전기장 $E$에 의해 전자가 이동
- 속도:
  $$
  v = \mu E
  $$
- 전류 밀도:
  $$
  J_n = qn\mu_n E, \quad J_p = qp\mu_p E
  $$

| 항목 | 값 (Si 기준) |
|------|--------------|
| 전자 이동도 $\mu_n$ | $1350\ \mathrm{cm^2/V\cdot s}$ |
| 정공 이동도 $\mu_p$ | $480\ \mathrm{cm^2/V\cdot s}$ |

---

#### (2) Diffusion (농도 구배에 의한 이동)

- 고농도 → 저농도 방향으로 전자 이동
- 전류 밀도:
  $$
  J_n = qD_n \frac{dn}{dx}, \quad J_p = -qD_p \frac{dp}{dx}
  $$
- $D_n$, $D_p$: 전자/정공 확산 계수

---

### ✅ Einstein Relation (아인슈타인 관계식)

- drift와 diffusion을 연결하는 관계

📐 수식:
$$
\frac{D_n}{\mu_n} = \frac{D_p}{\mu_p} = V_T
$$

- $V_T$: thermal voltage  
  $$
  V_T = \frac{kT}{q} \approx 26\ \text{mV} \quad \text{(at 300K)}
  $$

---

## ✅ 핵심 요약

| 항목 | 개념 요약 |
|------|-----------|
| 자유전자 생성 | 온도 상승 → 공유결합 파괴 |
| 전자-정공 쌍 | 하나의 자유전자 + 하나의 정공 |
| 도핑 | n형: 전자 증가 / p형: 정공 증가 |
| 전류 흐름 | Drift (전기장), Diffusion (농도 구배) |
| 핵심 식 | $np = n_i^2$, $V_T = \frac{kT}{q}$, $D/\mu = V_T$ |

🧠 이 개념들은 pn 접합의 전류 흐름, 전위 형성, 다이오드 동작을 이해하는 기반이 된다!

---

# 🔋 2.2 pn Junction

## 🌱 개념 흐름 요약

- **pn 접합**은 n형과 p형 반도체가 만날 때 형성됨
- 전하 운반자의 확산과 드리프트가 동시에 일어남
- 접합부에는 고정된 이온이 남아 "공핍층 (Depletion Region)" 형성
- 이 공핍층 내 전기장이 **전류 흐름을 제어**
- pn 접합은 전류를 한 방향으로만 흐르게 하는 **다이오드의 기초**

---

## 🔑 개념별 정리 (개념 ↔ 수식 연결 중심)

---

### ✅ pn 접합 형성

- **n형 영역**: 전자 다수
- **p형 영역**: 정공 다수

📌 형성 직후 → 전자가 p형으로 확산, 정공이 n형으로 확산  
→ 각 영역에 **고정된 이온들**이 남아 공핍 영역 생성

---

### ✅ Depletion Region (공핍 영역)

- 이동 가능한 전하 운반자는 없어짐
- 대신 고정된 **도너/억셉터 이온**만 존재 → 전기장 생성
- 이 전기장이 **정반대 방향의 drift current** 유발

---

### ✅ 전류 구성 요소: 확산 vs. 드리프트

| 메커니즘 | 원인 | 방향 | 설명 |
|----------|------|------|------|
| **확산 (Diffusion)** | 농도 구배 | n → p | 다수 캐리어 이동 |
| **드리프트 (Drift)** | 전기장 | p → n | 소수 캐리어 이동 |

📐 평형 상태 (equilibrium)일 때:
$$
I_{\text{drift}} = I_{\text{diffusion}} \Rightarrow I_{\text{total}} = 0
$$

---

### ✅ Built-in Potential (내장 전위장벽)

- 확산에 의해 생성된 전기장이 다시 확산을 억제
- 결과적으로 **내장 전위(V₀)** 생성:
  $$
  V_0 = \frac{kT}{q} \ln\left( \frac{N_A N_D}{n_i^2} \right)
  $$

- $N_A$, $N_D$: p/n형의 도핑 농도  
- $n_i$: intrinsic carrier 농도

---

### ✅ 동작 모드

#### ① 평형 상태 (Equilibrium)

- **총 전류 = 0** (확산 ↔ 드리프트 균형)
- Built-in potential만 존재

#### ② Reverse Bias (역방향 바이어스)

- 외부 전압이 **내장 전위보다 반대 방향**
- 공핍 영역이 **넓어짐**
- 전류 거의 없음 (이론상 역포화 전류 $I_S$만 흐름)

#### ③ Forward Bias (순방향 바이어스)

- 외부 전압이 내장 전위와 **동일 방향**
- 공핍층 **얇아짐**, 전기장 약해짐 → 확산 우세
- **지수 함수 형태의 전류 발생**:

📐 전류-전압 관계 (다이오드 방정식):
$$
I = I_S \left( e^{\frac{V}{V_T}} - 1 \right)
$$

---

## ✅ 핵심 요약

| 항목 | 내용 |
|------|------|
| pn 접합 | p형 + n형 → 확산 + 드리프트 + 공핍층 |
| 전류 메커니즘 | 확산 (다수 캐리어), 드리프트 (소수 캐리어) |
| 내장 전위 | $V_0 = \frac{kT}{q} \ln\left( \frac{N_A N_D}{n_i^2} \right)$ |
| 동작 모드 | 평형, 순방향, 역방향 바이어스 |
| 순방향 전류 | $I = I_S (e^{V/V_T} - 1)$ |

🧠 이 개념은 다이오드 회로, 정류기, 트랜지스터 해석의 핵심 기반이 된다!

---


# 💥 2.3 Reverse Breakdown

## 🌱 개념 흐름 요약

- 다이오드에 역방향 전압을 계속 높이면,  
  **특정 임계 전압 이상에서 갑자기 큰 전류가 흐름**
- 이 현상을 **Breakdown (항복)**이라고 부르며,  
  다이오드는 이 지점부터 **전류를 제한 없이 흘리게 됨**
- 항복 현상은 크게 **Zener Breakdown**과 **Avalanche Breakdown** 두 가지로 나뉨

---

## 🔑 개념별 정리 (개념 ↔ 수식 연결 중심)

---

### ✅ Breakdown 조건

- 다이오드에 **Reverse Bias** 전압을 인가
- 일정 전압 이상에서 **전류가 급격히 증가**

📐 다이오드 전류 방정식의 연장:
$$
I = -I_S \quad \text{(for small reverse bias)}
$$
→ 이 범위를 넘어서면 Breakdown 발생 → **모델 변경 필요**

---

### ✅ ① Zener Breakdown

- **고농도 도핑된 pn 접합**에서 발생
- 공핍층이 **매우 얇고**, 내부 전기장이 매우 큼  
→ **전기장에 의해 전자가 직접 결합에서 이탈 (양자 터널링)**

| 조건 | 특징 |
|------|------|
| 고농도 도핑 | 매우 얇은 공핍층 |
| 낮은 breakdown voltage | $\approx$ 몇 V 이하 |
| 작동 메커니즘 | 전기장에 의한 전자-정공 분리 |

✅ **Zener 다이오드**는 이 원리를 이용하여 **정전압 레퍼런스**로 사용됨

---

### ✅ ② Avalanche Breakdown

- **저농도 도핑된 pn 접합**에서 발생
- 전자나 정공이 가속되어 **고정 이온과 충돌 → 새로운 전하 생성**
- 일종의 **전하 증폭 반응** (Avalanche: 눈사태처럼 커짐)

| 조건 | 특징 |
|------|------|
| 낮은 도핑 농도 | 두꺼운 공핍층 |
| 높은 breakdown voltage | 수십 V 이상 |
| 작동 메커니즘 | 입자 충돌에 의한 이온화 (impact ionization) |

---

### ✅ Breakdown 비교 정리

| 항목 | Zener | Avalanche |
|------|-------|-----------|
| 도핑 농도 | 높음 | 낮음 |
| 공핍층 폭 | 얇음 | 두꺼움 |
| 발생 전압 | 낮음 ($< 5$ V) | 높음 ($> 5$ V) |
| 메커니즘 | 터널링 | 이온화 충돌 |
| 용도 | 전압 기준 | 고전압 회로 보호 등 |

---

## ✅ 핵심 요약

| 항목 | 내용 |
|------|------|
| Reverse Breakdown | 다이오드에 역전압 인가 시 큰 전류 발생 현상 |
| Zener Breakdown | 전기장에 의한 터널링 (고도핑) |
| Avalanche Breakdown | 충돌 이온화에 의한 전하 증폭 (저도핑) |
| 회로적 활용 | Zener 다이오드 → 전압 기준, 안정화 회로 등 |

🧠 항복은 손상 아닌 정상 동작일 수 있다!  
Zener 다이오드는 일부러 항복시켜 쓰는 다이오드임 😎

---

# 📘 2.4 Chapter Summary

## 🌱 전체 흐름 요약

- 반도체 소자, 특히 **pn 접합 다이오드**의 동작 원리를 이해하기 위한  
  물리적 기초 개념들을 다룬 챕터

- 핵심 구성:
  1. 반도체의 기본 물성
  2. 전하 운반자의 생성과 이동
  3. pn 접합의 형성과 동작
  4. 항복(Breakdown) 현상

---

## 🔑 핵심 개념 총정리

---

### ✅ 고유 반도체와 도핑

- 고유 반도체: 전자 = 정공, $np = n_i^2$
- 도핑:
  - n형: donor 원소 추가 → 전자 증가
  - p형: acceptor 원소 추가 → 정공 증가

📐 고유 관계:
$$
np = n_i^2
$$

---

### ✅ 전하 이동 메커니즘

#### 1. Drift (전기장에 의한 이동)
- 전류 밀도:
  $$
  J_n = q n \mu_n E, \quad J_p = q p \mu_p E
  $$

#### 2. Diffusion (농도 구배에 의한 이동)
- 전류 밀도:
  $$
  J_n = q D_n \frac{dn}{dx}, \quad J_p = - q D_p \frac{dp}{dx}
  $$

#### 3. Einstein 관계식
- drift와 diffusion 연결:
  $$
  \frac{D_n}{\mu_n} = \frac{D_p}{\mu_p} = V_T
  $$

---

### ✅ pn 접합

- 형성: 확산 → 고정 이온 → 전기장 형성 → 공핍층 형성
- 전류 = 확산 + 드리프트

#### 동작 모드:

| 모드 | 특징 |
|------|------|
| 평형 (Equilibrium) | $I_{\text{total}} = 0$ |
| 순방향 바이어스 | 공핍층 얇아짐, 전류 지수 증가 |
| 역방향 바이어스 | 공핍층 넓어짐, 전류 거의 없음 |

📐 내장 전위:
$$
V_0 = \frac{kT}{q} \ln\left( \frac{N_A N_D}{n_i^2} \right)
$$

📐 순방향 전류:
$$
I = I_S \left( e^{V/V_T} - 1 \right)
$$

---

### ✅ Reverse Breakdown

- **Zener Breakdown** (고도핑, 얇은 공핍층, 터널링)
- **Avalanche Breakdown** (저도핑, 두꺼운 공핍층, 충돌 이온화)

---

## ✅ 다이오드 해석 요령 요약

1. 전류 흐름 메커니즘: Drift vs. Diffusion
2. 공핍층의 역할: 전기장 형성 및 전류 제한
3. 바이어스에 따른 전류 반응:  
   순방향 → 지수 증가, 역방향 → 거의 0, 항복 시 급증
4. 다이오드 모델링: 지수 모델, Constant-Voltage Model (응용 시)

---

## ✅ 한줄 요약

> “**pn 접합 다이오드는 확산과 드리프트의 상호작용으로 형성되며,  
전압 조건에 따라 전류 특성이 극적으로 달라지는 반도체의 핵심 소자이다.**”

