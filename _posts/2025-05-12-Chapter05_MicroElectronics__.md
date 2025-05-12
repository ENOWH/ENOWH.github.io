---
title: "Chapter05_MicroElectronics"
excerpt: "전자회로 Chap05 Bipolar Amplifiers"

categories:
  - MicroElectronics
tags:
  - [MicroElectronics]

permalink: /categories/MicroElectronics/Chapter05_MicroElectronics__

toc: true
toc_sticky: true

date: 2025-05-12
last_modified_at: 2025-05-12
---

# Chapter 5. Bipolar Amplifiers

## 5.1 General Considerations
- Amplifier basics
- Input and Output Impedance
- Measurement of I/O Impedance
- Impedances seen at terminals of a transistor

## 5.2 Operating Point Analysis and Design
- Biasing and small-signal analysis
- Bad biasing examples
- Biasing with base resistor
- Improved biasing with resistive divider
- Emitter degeneration biasing
- Self-biasing technique
- Design procedure
- PNP biasing techniques

## 5.3 Bipolar Amplifier Topologies
- Possible amplifier topologies
- Common-Emitter (CE) topology
  - Voltage gain, input/output impedance
  - Early effect
  - Emitter degeneration
- Common-Base (CB) topology
  - Voltage gain, input/output impedance
  - Biasing, impedance matching
- Emitter Follower (Common-Collector)
  - Voltage buffer characteristics
  - Input/output impedance
  - Emitter follower with biasing

## 5.4 Summary and Additional Examples
- Summary of amplifier properties
- Thevenin equivalent analysis
- Example circuits

## 5.5 Chapter Summary
- Key points recap



# 5.1 General Considerations

## ✅ 주요 개념 흐름
Bipolar Amplifier의 기본 동작 원리와 설계 고려 요소, 입력/출력 임피던스 개념 및 측정 방법을 소개한다.  
트랜지스터의 단자별 임피던스를 정의하고 실제 회로 설계에 필요한 특성을 정리한다.

---

## ✅ 개념과 수식 정리

### 🎯 Amplifier (증폭기)
- **정의**: 입력 신호 (V 또는 I)를 증폭하여 출력하는 회로.
- **구성**: Voltage-controlled current source + Load resistor
- **설계 고려사항**
  - 전력 소모 (power dissipation)
  - 속도 (speed)
  - 잡음 (noise)
  - 입력/출력 임피던스 (I/O impedances)

---

### 🎯 Ideal Voltage Amplifier
1. **입력 임피던스**  
→ 이전 stage의 신호를 방해하지 않도록 매우 커야 함  
$$ Z_{in} = \infty $$

2. **출력 임피던스**  
→ 어떤 load impedance에도 일정한 신호를 전달하려면 매우 작아야 함  
$$ Z_{out} = 0 $$

---

### 🎯 Impedance Measurement (입출력 임피던스 측정 방법)
1. **입력 임피던스 측정**  
출력 open → test 전압 소스를 입력에 연결 후 측정
$$ Z_{in} = \frac{v_x}{i_x} $$

2. **출력 임피던스 측정**  
입력 short → test 전압 소스를 출력에 연결 후 측정
$$ Z_{out} = \frac{v_x}{i_x} $$

---

### 🎯 Impedance Seen at a Node
- 특정 노드에 test voltage source를 연결 → impedance 계산
- AC ground 기준으로 single-ended 측정

---

### 🎯 Transistor Terminals에서 본 임피던스
(Forward Active Region, Early effect 무시)
1. **Base (Emitter grounded)**  
$$ Z_{in} = r_{\pi} = \frac{\beta V_T}{I_C} $$

2. **Collector (Emitter grounded)**  
$$ Z_{out} = r_O $$

3. **Emitter (Base grounded)**  
$$ Z_{in} = \frac{1}{g_m} = \frac{V_T}{I_C} $$

---

## ✅ 정리 포인트
- 전압 증폭기에서는 **입력 임피던스는 크고** $$ (Z_{in} \to \infty) $$, **출력 임피던스는 작아야 한다** $$ (Z_{out} \to 0) $$
- 트랜지스터에서 각 단자별 small-signal 모델을 통해 입력/출력 임피던스를 정의한다.



# 5.2 Operating Point Analysis and Design

## ✅ 주요 개념 흐름
Bipolar Transistor가 증폭기로 동작하기 위해서는 **적절한 Biasing (동작점 설정)**이 필수.  
잘못된 biasing → 증폭 불가 → 회로 설계 시 반드시 적절한 bias 회로 구성 필요.  
본 파트는 biasing 방법과 small-signal analysis 과정을 다룬다.

---

## ✅ 개념과 수식 정리

### 🎯 Biasing (동작점 설정)
- **Active mode 유지 필요**
  - Base-Emitter: Forward biased
  - Base-Collector: Reverse biased
- **Small-Signal Parameters는 I_C에 의해 결정**
  - $$ g_m = \frac{I_C}{V_T} $$
  - $$ r_{\pi} = \frac{\beta V_T}{I_C} $$
  - $$ r_O = \frac{V_A}{I_C} $$

---

### 🎯 Amplifier Analysis 순서
1. **DC Analysis**  
→ Active/Saturation 상태 확인, small-signal parameter 계산  
2. **Small-Signal Analysis**  
→ Small-signal 입력에 대한 반응, voltage gain, I/O impedance 계산

---

### 🎯 Bad Biasing Examples
(예시로 잘못된 biasing의 문제점을 보여줌)
- DC bias current 없음 → transconductance (g_m) 존재 X → 증폭 불가
- Base를 Vcc에 연결 → 마이크 신호가 power supply로 short → 신호 전달 불가

---

### 🎯 Biasing with Base Resistor
- β 변화에 매우 민감
$$ I_B = \frac{V_{CC} - V_{BE}}{R_B} $$
$$ I_C = \beta I_B = \beta \frac{V_{CC} - V_{BE}}{R_B} $$

---

### 🎯 Resistive Divider Biasing (Improved Biasing)
- **Base Voltage**
$$ V_X = \frac{R_2}{R_1 + R_2} V_{CC} $$
- **Collector Current**
$$ I_C = I_S e^{\left(\frac{V_X}{V_T}\right)} $$
(단, IB는 매우 작다고 가정)

---

### 🎯 Accounting for Base Current
$$ I_C = I_S e^{\left(\frac{V_{Thev} - I_B R_{Thev}}{V_T}\right)} $$

---

### 🎯 Emitter Degeneration Biasing
- RE를 추가 → VBE를 안정화 → β 변화 및 VBE 변화에 덜 민감  
(단, gain 감소)
$$ V_{RE} = I_E R_E $$
$$ I_C \approx I_E $$

---

### 🎯 Design Procedure
1. Small-signal parameter를 결정하는 I_C 선택
2. V_{RE} 결정 → VBE 계산 → V_X 결정
3. R1, R2 선택 → V_X 제공

---

### 🎯 Self-Biasing Technique
- Collector voltage를 이용해 V_X와 I_B 설정
$$ R_C \gg \frac{R_B}{\beta} $$
$$ V_{CE} > V_{BE} $$ → 항상 forward active 유지

---

### 🎯 PNP Biasing Techniques
- NPN biasing 원리를 **polarity만 반대로 적용**

---

## ✅ 정리 포인트
- **Biasing은 small-signal parameter (g_m, r_{\pi}, r_O)를 결정**
- **Emitter degeneration**: 안정성을 높이는 대신 voltage gain 감소
- **Self-biasing**: 안정적인 bias current 제공


# 5.3 Bipolar Amplifier Topologies

## ✅ 주요 개념 흐름
Bipolar Amplifier는 입력과 출력 위치에 따라 **3가지 대표 topology**로 구분된다.  
각 topology 별로 voltage gain, input/output impedance, current gain 특성이 다르며, 적절한 상황에 맞춰 선택한다.

- Common-Emitter (CE): Voltage amplifier
- Common-Base (CB): Current buffer + impedance matching
- Emitter Follower (Common-Collector, CC): Voltage buffer

---

## ✅ 개념과 수식 정리

### 🎯 Common-Emitter (CE) Topology
**Voltage Amplifier (Phase Inversion: 180°)**

1. **Voltage Gain**
$$ A_v = \frac{v_{out}}{v_{in}} = -g_m R_C = -\frac{I_C}{V_T} R_C $$
(또는 emitter degeneration 적용 시)
$$ A_v = -\frac{g_m R_C}{1 + g_m R_E} = -\frac{R_C}{\frac{1}{g_m} + R_E} $$

2. **Input Impedance**
$$ R_{in} = r_{\pi} = \frac{\beta V_T}{I_C} $$
(degeneration 포함 시)
$$ R_{in} = r_{\pi} + (\beta + 1) R_E $$

3. **Output Impedance**
$$ R_{out} = R_C \parallel r_O $$
(degeneration 시에도 동일)

4. **Emitter Degeneration 효과**
- Linearity 향상
- Gain 감소
- Input impedance 증가

5. **Early Effect 포함 시**
$$ A_v = -g_m (R_C \parallel r_O) $$

---

### 🎯 Common-Base (CB) Topology
**Current Buffer + Impedance Matching**

1. **Voltage Gain**
$$ A_v = g_m R_C = \frac{I_C}{V_T} R_C $$

2. **Input Impedance**
$$ R_{in} = \frac{1}{g_m} = \frac{V_T}{I_C} $$  
(매우 낮음 → RF/High-frequency에서 impedance matching 용도로 활용)

3. **Output Impedance**
$$ R_{out} = R_C \parallel r_O $$

4. **CB Stage with Source Resistance (R_S)**
$$ A_v = \frac{R_C}{\frac{1}{g_m} + R_S} $$

5. **CB with base resistor (R_B 포함)**
$$ R_{in} = \frac{1}{g_m} + \frac{R_B}{\beta + 1} $$

---

### 🎯 Emitter Follower (Common-Collector, CC)
**Voltage Buffer (No phase inversion)**

1. **Voltage Gain**
$$ A_v = \frac{v_{out}}{v_{in}} = \frac{R_E}{R_E + \frac{1}{g_m}} \approx 1 $$  
(또는 R_E → ∞ 시)
$$ A_v = 1 $$

2. **Input Impedance**
$$ R_{in} = r_{\pi} + (\beta + 1) R_E $$

3. **Output Impedance**
$$ R_{out} = \frac{R_S}{\beta + 1} + \frac{1}{g_m} \parallel R_E \parallel r_O $$

4. **특징**
- High input impedance (good voltage sensor)
- Low output impedance (good voltage source)
- “Current gain = β + 1”

5. **Emitter Follower with Biasing**
- R1, R2 → base voltage 제공
- Bypass capacitor → high-frequency에서 R1, R2 영향 제거

---

## ✅ 정리 포인트
- **CE Stage**: Moderate voltage gain, moderate input/output impedance  
- **CB Stage**: Low input impedance, moderate output impedance → impedance matching  
- **Emitter Follower**: Voltage gain ≈ 1, High input impedance, Low output impedance → voltage buffer



# 5.4 Summary and Additional Examples

## ✅ 주요 개념 흐름
앞서 배운 Bipolar Amplifier의 모든 특성을 종합 정리하고,  
추가 예제를 통해 실제 회로 해석 및 설계 방법을 연습한다.

---

## ✅ 개념과 수식 정리

### 🎯 Bipolar Amplifier 종합 특성

| Topology | Voltage Gain | Input Impedance | Output Impedance |
|---------|--------------|-----------------|------------------|
| CE      | Moderate     | Moderate        | Moderate         |
| CB      | Moderate     | Low             | Moderate         |
| CC (Follower) | < 1    | High            | Low              |

- CE Stage: 증폭용으로 가장 널리 사용
- CB Stage: RF circuit에서 impedance matching 용도로 사용
- CC Stage: Voltage buffer (high input, low output impedance)

---

### 🎯 트랜지스터 Terminal 임피던스 요약
1. Base (Emitter grounded)
$$ Z_{in} = r_{\pi} = \frac{\beta V_T}{I_C} $$
2. Collector (Emitter grounded)
$$ Z_{out} = r_O $$
3. Emitter (Base grounded)
$$ Z_{in} = \frac{1}{g_m} = \frac{V_T}{I_C} $$

---

### 🎯 Thevenin Equivalent (회로 간소화)
1. Thevenin Voltage
$$ V_{Thev} = \frac{R_1 \parallel R_2}{(R_1 \parallel R_2) + R_S} V_{in} $$

2. Thevenin Resistance
$$ R_{Thev} = R_1 \parallel R_2 \parallel R_S $$

3. Voltage Gain with Thevenin source
$$ A_v = -\frac{R_C \parallel R_L}{\frac{1}{g_m} + R_E + \frac{R_{Thev}}{\beta + 1}} \times \frac{R_1 \parallel R_2}{(R_1 \parallel R_2) + R_S} $$

---

### 🎯 Additional Examples 요약
(Example 5.27, 5.29, 5.30 등)

- **CE stage output impedance**
$$ R_{out} = (1 + g_m (R_2 \parallel r_{\pi})) r_O \parallel R_1 $$

- **Cascode Structure**
$$ R_{out} = (1 + g_{m1} (r_{O2} \parallel r_{\pi1})) r_{O1} $$

- **Degenerated CE Stage**
$$ A_v = -\frac{R_C}{\frac{1}{g_{m1}} + R_E + \frac{1}{\beta + 1} + \frac{1}{g_{m2}}} $$

---

## ✅ 정리 포인트
- **Thevenin 변환**을 통해 복잡한 회로를 간단한 single-stage로 치환
- **Emitter degeneration → Gain 감소, Linearity 향상**
- **Cascode → Very high output impedance**


# 5.5 Chapter Summary

## ✅ 주요 개념 흐름
Chapter 5에서는 Bipolar Transistor Amplifier의 원리, Biasing 방법,  
3가지 주요 topology (CE, CB, CC) 및 Small-Signal Model을 통한 해석 방법을 종합적으로 다루었다.

---

## ✅ 개념과 수식 정리

### 🎯 Bipolar Transistor 임피던스 정리
- Base → Emitter grounded
$$ Z_{in} = r_{\pi} = \frac{\beta V_T}{I_C} $$
- Collector → Emitter grounded
$$ Z_{out} = r_O $$
- Emitter → Base grounded
$$ Z_{in} = \frac{1}{g_m} = \frac{V_T}{I_C} $$

---

### 🎯 Common-Emitter (CE) Stage
1. Moderate voltage gain
$$ A_v = -g_m R_C = -\frac{I_C}{V_T} R_C $$
2. Moderate input impedance
$$ R_{in} = r_{\pi} $$
3. Moderate output impedance
$$ R_{out} = R_C \parallel r_O $$
4. Emitter degeneration → Gain 감소, Linearity 향상, Output impedance 증가

---

### 🎯 Common-Base (CB) Stage
1. Moderate voltage gain
$$ A_v = g_m R_C $$
2. Low input impedance
$$ R_{in} = \frac{1}{g_m} = \frac{V_T}{I_C} $$
3. Moderate output impedance
$$ R_{out} = R_C \parallel r_O $$

---

### 🎯 Emitter Follower (Common-Collector, CC)
1. Voltage gain ≈ 1
$$ A_v = \frac{R_E}{R_E + \frac{1}{g_m}} $$
2. High input impedance
$$ R_{in} = r_{\pi} + (\beta + 1) R_E $$
3. Low output impedance
$$ R_{out} = \frac{R_S}{\beta + 1} + \frac{1}{g_m} \parallel R_E \parallel r_O $$

---

## ✅ 정리 포인트
- **CE**: 일반적인 증폭기 → moderate gain, moderate I/O impedance
- **CB**: RF 회로, impedance matching → low input impedance
- **CC (Emitter Follower)**: Buffer용 → high input, low output impedance, unity gain
- Small-Signal Model → 전류 이득, 전압 이득, 입출력 임피던스 계산에 필수