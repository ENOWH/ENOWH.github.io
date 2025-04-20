---
title: "Chapter04_MicroElectronics"
excerpt: "전자회로 Chap04 전체 흐름"

categories:
  - MicroElectronics
tags:
  - [MicroElectronics]

permalink: /categories/MicroElectronics/Chapter04_MicroElectronics

toc: true
toc_sticky: true

date: 2025-04-20
last_modified_at: 2025-04-20
---

# ⚙️ Chapter 4: Physics of Bipolar Transistors (`Ch4 Physics of Bipolar Transistors.pdf`)

## 📑 세션별 구성 및 주요 주제 정리

---

### 🟦 4.1 General Considerations

- BJT는 **전압에 의해 제어되는 전류원**
- 전압 이득 정의:
  $$
  A_v = \frac{V_{\text{out}}}{V_{\text{in}}} = -KR_L
  $$
- BJT 회로에서의 이상적인 증폭 조건 및 개념 도입

---

### 🟦 4.2 Structure of Bipolar Transistor

- BJT는 두 개의 pn 접합으로 구성
- **Carrier injection & electric field**에 의한 전류 제어
- Minority carrier가 majority 영역으로 확산됨 (diffusion 주도)

---

### 🟦 4.3 Operation of Bipolar Transistor in Active Mode

- Forward Active 조건: $V_{BE} > 0$, $V_{BC} < 0$
- **Collector current**는 exponential:
  $$
  I_C = I_S \cdot \exp\left( \frac{V_{BE}}{V_T} \right)
  $$
- 베이스 전류: $I_B = \frac{I_C}{\beta}$
- $\beta = \frac{I_C}{I_B}$, $\alpha = \frac{I_C}{I_E}$

---

### 🟦 4.4 Bipolar Transistor Models and Characteristics

- **Large-Signal 모델**: 다이오드 + 전류원
- **Small-Signal 모델**:
  - 트랜스컨덕턴스: $g_m = \frac{I_C}{V_T}$
  - 입력 저항: $r_\pi = \frac{\beta}{g_m}$
  - 출력 저항도 포함 가능
- **Early Effect**:
  - 전류 증가: $I_C \approx I_S \cdot \exp\left(\frac{V_{BE}}{V_T}\right)\left(1 + \frac{V_{CE}}{V_A}\right)$

---

### 🟦 4.5 Operation of Bipolar Transistor in Saturation Mode

- 포화 영역: $V_{CE} < V_{BE}$
- B-C 접합도 **forward-biased**
- $\beta$ 감소 및 응답 속도 저하
- **디지털 회로에서 주로 동작**

---

### 🟦 4.6 The PNP Transistor

- pnp 트랜지스터는 npn과 **동일한 물리 모델** 적용 가능
- VBE → VEB로 바뀌는 점만 주의
- **Small-signal 모델도 동일**, 방향성만 반대

---

## 🧭 전체 흐름 요약

1. BJT는 **전압으로 제어되는 전류원**이며 증폭기로 이상적
2. **Carrier injection과 diffusion**으로 동작
3. Active mode에서는 **exponential current law**가 중심
4. Small-signal & large-signal 모델 모두 존재하며, **트랜스컨덕턴스가 핵심 파라미터**
5. Saturation에서는 증폭 능력이 떨어지고 디지털 스위칭에 적합
6. pnp 트랜지스터는 npn의 **거울상(mirror counterpart)**로 동일한 수식 구조를 갖는다

---
---

# 🔌 4.1 General Considerations

## 🌱 개념 흐름 요약

- Bipolar Junction Transistor (BJT)는 **전압에 의해 제어되는 전류원**
- 입력 전압 $V_{\text{in}}$에 비례하는 전류 $I_1$이 흐르고,  
  출력 전압 $V_{\text{out}}$는 부하 저항 $R_L$을 통해 이 전류에 의해 형성됨
- BJT는 기본적으로 **전압 제어형 전류원 (Voltage-Controlled Current Source)**로 동작

---

## 🔑 개념별 정리 (개념 ↔ 수식 연결)

### ✅ BJT의 기본 증폭 작동 원리

- 입력 전압에 따라 흐르는 전류:
  $$
  I_1 = K V_1 = K V_{\text{in}}
  $$

- 출력 전압:
  $$
  V_{\text{out}} = - R_L I_1 = - K R_L V_{\text{in}}
  $$

- 따라서, **전압 이득 (Voltage Gain)**:
  $$
  A_v = \frac{V_{\text{out}}}{V_{\text{in}}} = - K R_L
  $$

📌 **전압이득의 절댓값이 클수록 증폭률이 높다**

---

### ✅ 내부 저항이 있는 전압 제어 전류원 회로 (예: Example 4.1)

- 내부 저항 $r_{\text{in}}$이 있는 회로에서도 입력 전압 $V_{\text{in}}$이 그대로 $V_1$이 되기 때문에  
  전압 이득은 변하지 않음

- 이득은 여전히:
  $$
  A_v = - K R_L
  $$

---

### ✅ BJT의 본질적 특성

- **출력 전류가 입력 전압의 지수 함수 형태**로 결정됨
- 3단자 디바이스 (Base, Collector, Emitter)이므로 회로 분석이 다소 복잡해질 수 있음

- 요약:
  - 입력 전압이 전류를 유도하고
  - 그 전류가 출력 전압을 생성
  - 결국, **전압 → 전류 → 전압**의 연쇄 구조

---

## ✅ 핵심 요약

| 항목 | 설명 |
|------|------|
| BJT 역할 | 전압 제어형 전류원 |
| 출력 전압 | $V_{\text{out}} = -K R_L V_{\text{in}}$ |
| 전압 이득 | $A_v = \frac{V_{\text{out}}}{V_{\text{in}}} = -K R_L$ |
| 의미 | 입력 전압에 비례하는 전류가 흐르고, 출력은 그 전류로 결정됨 |

📌 이 기본 개념을 기반으로 다음 세션에서는 BJT의 구조와 carrier 이동 원리를 살펴본다.

---
---

# 🧱 4.2 Structure of Bipolar Transistor

## 🌱 개념 흐름 요약

- BJT는 **Emitter–Base–Collector**로 구성된 **3단자 반도체 소자**
- 내부적으로는 **두 개의 pn 접합**으로 구성되어 있음
- **전하 운반자 (carrier)의 주입과 확산(diffusion)**이 BJT의 동작의 핵심
- Reverse-biased 영역이 만들어내는 **전기장**이 carrier를 이동시키는 주체

---

## 🔑 개념별 정리 (개념 ↔ 수식 연결 중심)

### ✅ 구조 개요

- BJT는 다음 두 가지 접합으로 구성됨:
  - **Emitter–Base (E-B)**: forward-biased
  - **Base–Collector (B-C)**: reverse-biased

- 전류 흐름 방향 (NPN 기준):
  - **전자는 Emitter → Collector 방향으로 이동**
  - **Base 영역은 얇고 lightly doped → 소수 carrier만 존재**

---

### ✅ Carrier Injection Mechanism

- Emitter에서 **전자(majority carrier)**가 Base로 주입됨  
- Base에서는 전자의 밀도 차이로 인해 **확산(diffusion current)** 발생
- Collector 측 pn 접합은 **reverse bias** → 주입된 전자를 Collector로 **흡수**

📐 전류 흐름 요약:
- $I_E$: Emitter current (입력)
- $I_B$: Base current (작음)
- $I_C$: Collector current (거의 $I_E$에 가까움)

---

### ✅ 전류 제어의 핵심 원리

- BJT의 **Collector current는 Emitter에서 Base로 주입되는 전자 양에 비례**
- 이는 **Base–Emitter 전압 $V_{BE}$**에 따라 지수적으로 증가

📐 핵심 수식:
$$
I_C \approx I_S \cdot \exp\left( \frac{V_{BE}}{V_T} \right)
$$

- $I_S$: saturation current (아주 작은 상수)
- $V_T$: thermal voltage ≈ 26 mV (상온 기준)

---

### ✅ 전기장에 의한 이동

- B–C 접합은 reverse bias → **강한 전기장** 생성
- 이 전기장은 Base 내에서 주입된 전자를 Collector 방향으로 **끌어당김**

📌 **기억할 것**:  
BJT의 핵심 동작은 “**Base가 Emitter로부터 전자를 받아들이고, Collector로 흘려보내는 다리 역할**”

---

## ✅ 핵심 요약

| 항목 | 내용 |
|------|------|
| BJT 구조 | Emitter–Base–Collector (2개의 pn 접합) |
| 작동 조건 | E-B: forward bias / B-C: reverse bias |
| 전류 흐름 | $I_E \to I_C$, $I_B$는 매우 작음 |
| 전류 제어 방식 | $I_C$는 $V_{BE}$에 의해 지수적으로 증가 |
| Carrier 이동 원리 | 주입(injection) + 확산(diffusion) + 전기장에 의한 수송 |

🧠 이 구조는 다음 세션의 **Active Mode 동작**을 위한 물리적 기반이 된다!

---
---

# ⚡ 4.3 Operation of Bipolar Transistor in Active Mode

## 🌱 개념 흐름 요약

- BJT가 증폭기로 동작하는 영역 = **Forward Active Region**
- 이때 조건은 다음과 같다:
  - $V_{BE} > 0$ (E-B 접합 forward bias)
  - $V_{BC} < 0$ (B-C 접합 reverse bias)
- 이 조건이 만족되면 Emitter에서 주입된 전자들이 거의 손실 없이 Collector로 이동
- **Base 영역은 매우 얇고 희박하게 도핑되어 있음 → 전류 손실 최소화**

---

## 🔑 개념별 정리 (개념 ↔ 수식 연결 중심)

### ✅ Collector Current 수식

- Emitter → Base → Collector 방향으로 전자 이동
- **전류는 $V_{BE}$에 대해 지수적으로 증가**

📐 수식:
$$
I_C = I_S \cdot \exp\left( \frac{V_{BE}}{V_T} \right)
$$

- $I_S$: saturation current (소자 특성에 따라 결정)
- $V_T$: thermal voltage ≈ 26 mV

---

### ✅ Base Current, Current Gain (β, α)

- **Base current**는 작고, 대부분의 전자는 Collector로 감

📐 관련 수식:

- $\beta$ (DC current gain):
  $$
  \beta = \frac{I_C}{I_B}
  $$

- $\alpha$ (common-base current gain):
  $$
  \alpha = \frac{I_C}{I_E} = \frac{\beta}{\beta + 1}
  $$

> 일반적으로 $\beta \in [100, 500]$, $\alpha \approx 0.99$

---

### ✅ Active Mode 동작 조건 정리

| 조건 | 설명 |
|------|------|
| $V_{BE} > 0$ | Emitter → Base로 다수 carrier 주입 |
| $V_{BC} < 0$ | Collector 쪽은 전자를 흡수할 준비가 되어 있음 |
| 결과 | 전류는 $I_E \to I_C$, $I_B$는 작고 증폭 효과 발생 |

---

### ✅ 이상적인 전류원처럼 동작

- $I_C$는 $V_{CE}$에 **거의 영향을 받지 않음** → 전류원처럼 동작
- 이상적인 전류원은 출력 전압($V_{CE}$)이 변해도 출력 전류($I_C$)가 일정해야 함

📌 요약:
- **입력 전압 $V_{BE}$에 의해 출력 전류 $I_C$가 결정되는 증폭기 구조**

---

## ✅ 핵심 요약

| 항목 | 내용 |
|------|------|
| 동작 영역 | Forward Active Region |
| 접합 상태 | $V_{BE} > 0$, $V_{BC} < 0$ |
| 핵심 수식 | $I_C = I_S \cdot \exp(V_{BE}/V_T)$ |
| 전류 관계 | $\beta = I_C/I_B$, $\alpha = I_C/I_E$ |
| 증폭 조건 | $I_C$가 입력 $V_{BE}$에 의해 제어됨 |

🧠 이 구조를 기반으로 BJT는 **증폭기, 스위치 등 다양한 회로 요소로 활용 가능**

---
---

# 🔧 4.4 Bipolar Transistor Models and Characteristics

## 🌱 개념 흐름 요약

- 지금까지의 동작 원리를 바탕으로, BJT를 **회로 모델**로 표현
- DC 동작을 위한 **Large-Signal Model**
- 소신호 해석을 위한 **Small-Signal Model**
- 트랜스컨덕턴스 $g_m$, 입력 저항 $r_\pi$, 출력 저항 $r_o$ 등 파라미터 정의

---

## 🔑 개념별 정리 (개념 ↔ 수식 연결 중심)

### ✅ Large-Signal Model

- **Base-Emitter**: 다이오드로 모델링 (forward bias)
- **Collector–Emitter**: 전류원으로 모델링

📐 수식:
$$
I_C = I_S \cdot \exp\left( \frac{V_{BE}}{V_T} \right)
$$

- $I_C$는 $V_{BE}$에 의해 지수적으로 결정됨
- $I_B = \frac{I_C}{\beta}$

---

### ✅ Small-Signal Model (중심 개념)

- DC 바이어스 점 근처에서 **미세한 변화를 선형적으로 모델링**

#### 트랜스컨덕턴스 ($g_m$)

- 출력 전류 변화율:
  $$
  g_m = \frac{dI_C}{dV_{BE}} = \frac{I_C}{V_T}
  $$
  - $V_T \approx 26$ mV (상온 기준)
  - 단위: S (Siemens), 즉 $\Omega^{-1}$

#### 입력 저항 ($r_\pi$)

- Base–Emitter 소신호 저항:
  $$
  r_\pi = \frac{V_{BE}}{I_B} = \frac{\beta}{g_m}
  $$

#### 출력 저항 ($r_o$)

- Early Effect 고려 시:
  $$
  r_o = \frac{V_A}{I_C}
  $$

---

### ✅ Complete Hybrid-π Model 구성요소

- $g_m v_\pi$: 전류원
- $r_\pi$: 입력 저항
- $r_o$: 출력 저항 (Early Effect 고려)
- $v_\pi = v_{be}$: 베이스 입력 전압

📐 전체 모델 회로:  
- 입력: Base → Emitter: $r_\pi$  
- 출력: Collector → Emitter: $g_m v_\pi$ + $r_o$

---

### ✅ Early Effect

- 실제 BJT는 **$V_{CE}$ 증가 시 $I_C$도 소폭 증가** → 완전한 전류원이 아님
- 이를 모델에 반영하기 위해 $r_o$ 추가

📐 모델 확장:
$$
I_C \approx I_S \cdot \exp\left( \frac{V_{BE}}{V_T} \right) \left( 1 + \frac{V_{CE}}{V_A} \right)
$$

---

### ✅ 트랜스컨덕턴스 예시

- $I_C = 1$ mA일 때:
  $$
  g_m = \frac{1\ \text{mA}}{26\ \text{mV}} \approx 38.5\ \text{mS}
  $$
- $\beta = 100$일 때:
  $$
  r_\pi = \frac{100}{38.5\ \text{mS}} \approx 2.6\ \text{k}\Omega
  $$

---

## ✅ 핵심 요약

| 파라미터 | 정의 | 수식 |
|----------|------|------|
| $g_m$ (트랜스컨덕턴스) | $\frac{dI_C}{dV_{BE}}$ | $g_m = \frac{I_C}{V_T}$ |
| $r_\pi$ (입력 저항) | $v_{be}/i_b$ | $r_\pi = \frac{\beta}{g_m}$ |
| $r_o$ (출력 저항) | Early Effect 고려 | $r_o = \frac{V_A}{I_C}$ |

🧠 이 모델을 통해 BJT 기반 증폭기를 정확히 분석할 수 있게 됨!

---
---

# 🧯 4.5 Operation of Bipolar Transistor in Saturation Mode

## 🌱 개념 흐름 요약

- BJT가 **증폭기 역할을 멈추고, 스위치처럼 동작**하는 영역
- **포화 영역(Saturation Region)** 조건:
  - $V_{CE} < V_{BE}$
  - 즉, Collector가 Base보다 더 낮은 전압 → B–C 접합이 forward-biased
- 이때는 $I_C$가 $V_{BE}$에 대해 **지수적으로 증가하지 않음**  
  → **Current gain $\beta$가 급격히 감소**하고, 증폭 특성도 사라짐

---

## 🔑 개념별 정리 (개념 ↔ 수식 연결 중심)

### ✅ 포화 영역(Saturation Region) 조건

- **정의**:
  $$
  V_{CE} < V_{BE} \quad \text{or} \quad V_{CB} > 0
  $$

- E–B 접합: forward-biased  
- **B–C 접합도 forward-biased** (정상적인 증폭기 동작 아님)

---

### ✅ 동작 특성 변화

- **Base에서 Collector로의 전하 흐름이 비효율적**
- 다수 carrier의 recombination 증가 → $\beta$ 감소
- 전류 증폭 기능이 현저히 줄어듦 → **Switch-like 동작**

---

### ✅ Soft Saturation vs. Deep Saturation

| 구분 | 설명 | 기준 |
|------|------|------|
| **Soft Saturation** | $V_{BC} \lesssim 0.4$ V | 증폭기 동작 일부 유지 |
| **Deep Saturation** | $V_{CE} \approx 0.2$ V | 완전히 포화, 증폭 기능 상실 |

- Deep saturation에서는:
  - $V_{CE,\text{sat}} \approx 0.2$ V (실험적으로 측정된 값)
  - $I_C$는 $I_B$ 증가에도 거의 변하지 않음

---

### ✅ 포화 영역에서의 모델링 차이

- 일반적인 $I_C = I_S e^{V_{BE}/V_T}$ 식이 **더 이상 유효하지 않음**
- 전류는 $V_{CE}$의 변화에도 영향을 받음
- **Small-signal 모델 부정확** → **증폭기로 사용 불가**

---

### ✅ 디지털 회로에서의 활용

- 스위치처럼 on/off 동작
- **논리 게이트**, **트랜지스터 로직**에서 활용
- ON 상태: 포화 영역에 진입시켜서 전압 강하 최소화

---

## ✅ 핵심 요약

| 항목 | 내용 |
|------|------|
| 포화 조건 | $V_{CE} < V_{BE}$ |
| 접합 상태 | E–B: forward / B–C: **forward** |
| 증폭 성능 | $\beta$ 급감, 전류 증가 둔화 |
| 모델 유효성 | $I_C$ 지수 관계 무효, small-signal 모델 무효 |
| 용도 | 스위치 회로 (디지털 회로) |

🧠 결론:  
- Active mode → 증폭기  
- Saturation mode → 스위치  
→ BJT는 **증폭기와 스위치 모두 가능**한 핵심 소자!

---
---

# 🔄 4.6 The PNP Transistor

## 🌱 개념 흐름 요약

- **pnp 트랜지스터는 npn 트랜지스터의 극성 반대 버전**
- 회로 동작 원리, 수식, 모델링 방식 모두 동일  
  → 단, **전압·전류 방향이 반대**
- 실질적으로 **npn BJT 모델을 그대로 쓸 수 있음**  
  (단, 전류 방향과 $V_{EB}$ vs $V_{BE}$ 주의!)

---

## 🔑 개념별 정리 (개념 ↔ 수식 연결 중심)

### ✅ pnp 구조 및 동작 방향

- 구조: **Emitter (p) → Base (n) → Collector (p)**
- 다수 carrier: **정공(hole)**
- 전류 흐름: **Emitter → Collector**  
  → npn과 반대 방향

---

### ✅ 전압 및 전류 방향 비교

| 항목 | npn BJT | pnp BJT |
|------|---------|---------|
| 다수 carrier | 전자 | 정공 |
| Emitter current | 들어옴 | 나감 |
| Base-Emitter 전압 | $V_{BE}$ > 0 | $V_{EB}$ > 0 |
| Collector current | 나감 | 들어옴 |

📌 회로 해석할 때는 npn 모델을 사용하되, **전압과 전류 방향만 뒤집어주면 됨**

---

### ✅ Large-Signal Model

- pnp도 동일한 exponential 관계를 가짐:
  $$
  I_C = I_S \cdot \exp\left( \frac{V_{EB}}{V_T} \right)
  $$

- Early Effect도 동일하게 적용 가능:
  $$
  I_C \approx I_S \cdot \exp\left( \frac{V_{EB}}{V_T} \right) \left(1 + \frac{V_{EC}}{V_A} \right)
  $$

---

### ✅ Small-Signal Model

- 구조는 npn BJT와 동일  
- 단지 모든 **전류 방향과 전압 극성**이 반대

📌 $g_m$, $r_\pi$, $r_o$ 계산법 전부 동일  
→ 해석 시 **부호만 주의**하면 됨

---

## ✅ 핵심 요약

| 항목 | 내용 |
|------|------|
| pnp 구조 | p → n → p |
| 동작 원리 | npn과 동일, 극성 반대 |
| 수식 | 모두 동일, $V_{BE} \to V_{EB}$ 로 대체 |
| 모델링 | Large/Small Signal 모델 동일 |
| 전류 방향 | Emitter → Base → Collector (정공 흐름 기준) |

🧠 정리:  
- **npn과 pnp는 대칭 구조**
- 모델·수식·회로 해석은 동일 → **극성만 반대로 해석하면 됨**