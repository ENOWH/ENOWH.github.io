---
title: "Chapter05_MicroElectronics"
excerpt: "전자회로 Chap05 전체 흐름"

categories:
  - MicroElectronics
tags:
  - [MicroElectronics]

permalink: /categories/MicroElectronics/Chapter05_MicroElectronics

toc: true
toc_sticky: true

date: 2025-04-20
last_modified_at: 2025-04-24
---

# 🔊 Chapter 5: Bipolar Amplifiers (시험범위: p.1–29)

---

## 🟦 5.1 General Considerations

### 🌱 개요
- **증폭기(Amplifier)**: 입력 신호의 전압/전류를 **확대(magnify)**하는 회로
- BJT는 **전압으로 제어되는 전류원** 역할 → 저항과 함께 증폭기 구성 가능

### ✅ 이상적인 전압 증폭기 조건

| 조건 | 설명 |
|------|------|
| 입력 임피던스 $Z_{in}$ | 무한대 → 이전 회로에 부하를 주지 않음 |
| 출력 임피던스 $Z_{out}$ | 0 → 어떤 부하에도 일정한 출력을 제공 |

---

## 🟦 5.1 예제 문제들 (Example 5.1–5.4)

- 입력 임피던스가 클수록, 출력 임피던스가 작을수록 **이득 손실 없이 전송 가능**

📐 임피던스 측정 기본 원리:
- 입력 임피던스: 출력 open 상태에서 $R_{in} = \frac{V_x}{I_x}$
- 출력 임피던스: 입력 short 상태에서 $R_{out} = \frac{V_x}{I_x}$

---

### ✅ 트랜지스터 단자별 임피던스 정리

| 단자 | 입력 임피던스 (기준 조건) |
|------|----------------------------|
| Base | $r_\pi = \frac{\beta}{g_m}$ (Emitter 접지 시) |
| Collector | $r_o = \frac{V_A}{I_C}$ (Emitter 접지 시) |
| Emitter | $1/g_m$ (Base 접지 시) |

---

## 🟦 5.2 Operating Point Analysis and Design

### 🌱 개요

- 트랜지스터가 **Active Mode**에서 동작하기 위해 **바이어스 설정(biasing)** 필요
- **DC bias current**를 설정하면 $g_m$, $r_\pi$, $r_o$ 등의 소신호 파라미터 결정됨

---

### ✅ 증폭기 해석 절차

1. **DC 해석**: 동작 영역(Active or Saturation), 바이어스점 설정
2. **Small-Signal 해석**: Gain, 입력/출력 임피던스 계산

📌 **중첩의 원리(superposition)** 적용:
- 모든 DC 전원은 0으로 설정 (ac ground)
- 입력 신호만 고려하여 해석

---

### ✅ Small-Signal 조건

- 전류 변동량 $\Delta I_C$가 전체의 10% 이하일 때 **선형 근사** 가능
- $g_m = \frac{I_C}{V_T}$, $r_\pi = \frac{\beta}{g_m}$, $r_o = \frac{V_A}{I_C}$ 등 활용

---

## 🟦 5.2 Biasing Techniques

### ✅ 1. Base Resistor Biasing

- 단순하지만 **$\beta$에 매우 민감**
- 수식:
  $$
  I_B = \frac{V_{CC} - V_{BE}}{R_B}, \quad I_C = \beta I_B
  $$

---

### ✅ 2. Resistive Divider Biasing

- 분압 저항 $R_1, R_2$로 Base 전압 $V_X$ 결정:
  $$
  V_X = \frac{R_2}{R_1 + R_2} V_{CC}
  $$
- $I_C = I_S e^{V_{BE}/V_T}$ 적용
- **IB가 무시 가능할 정도로 작아야 정확도 높음**

---

### ✅ 3. Accounting for Base Current

- $V_{BE}$가 base current $I_B$로 인해 떨어짐:
  $$
  I_C = I_S \exp\left(\frac{V_X - I_B R_{Thev}}{V_T}\right)
  $$

---

### ✅ 4. Emitter Degeneration Biasing

- Emitter에 저항 $R_E$ 추가 → **$V_{BE}$ 변화에 둔감**, $\beta$ 변화 영향 적음
- $V_E = I_E R_E \approx I_C R_E$, $V_B = V_E + V_{BE}$

---

### ✅ 5. Self-Biasing

- Collector 전압 $V_C$를 분압에 이용하여 Base 바이어스를 설정
- 조건:
  - $R_C \gg \frac{R_B}{\beta}$
  - $V_{CE} > V_{BE}$ → Active Mode 유지

---

### ✅ Biasing 정리

| 방식 | 장점 | 단점 |
|------|------|------|
| Base Resistor | 간단 | $\beta$ 민감 |
| Divider | $\beta$ 무관 | 저항 정밀도 요구 |
| With $R_E$ | 안정적, 선형성↑ | Gain 감소 가능 |
| Self-Bias | 간단한 구성 | 조건 만족 필수 |

---

## ✅ 한 줄 요약

> “**트랜지스터 증폭기를 제대로 동작시키기 위해서는 Active Mode 바이어스 설정이 중요하고,  
그 바이어스는 여러 방식(Base, Divider, $R_E$, Self)을 통해 설정할 수 있으며 각각 trade-off가 있다.**”