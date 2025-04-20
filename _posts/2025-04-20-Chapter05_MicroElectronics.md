---
title: "Chapter05"
excerpt: "전자회로 Chap05 전체 흐름"

categories:
  - MicroElectronics
tags:
  - [MicroElectronics, 머신러닝]

permalink: /categories/MicroElectronics/Chapter05_MicroElectronics

toc: true
toc_sticky: true

date: 2025-04-20
last_modified_at: 2025-04-20
---

# 🔊 Chapter 5: Bipolar Amplifiers (시험범위: 전체 페이지 기준 p.1–29)

---

## 🟦 5.1 General Considerations

### 🌱 개념 흐름 요약
- **BJT 증폭기**는 입력 전압에 비례하는 전류를 흐르게 하여  
  부하 저항을 통해 증폭된 출력 전압을 생성
- 증폭기 설계 시 고려 요소:
  - Power dissipation
  - Speed
  - Noise
  - Input/output impedance

### ✅ 전압 증폭기의 이상적인 특성

| 항목 | 이상적 조건 |
|------|--------------|
| 입력 임피던스 | 무한대 ($\infty$) |
| 출력 임피던스 | 0 |

---

## 🟦 5.2 Operating Point Analysis and Design

### 🌱 개념 흐름 요약
- **Biasing**이란 트랜지스터를 **active mode**에 고정시키기 위해  
  DC 작동점을 설정하는 것
- 적절한 바이어스 설정은 $g_m$, $r_\pi$ 등 소신호 파라미터 결정에 직접 영향
- 바이어스 회로는 크게 3가지로 나뉜다:
  1. Base 저항
  2. 저항 분할
  3. Emitter degeneration 포함

---

### ✅ Biasing 방법별 특징 정리

#### ① Base Resistor Biasing

- 간단한 구성: Base에 저항 $R_B$만 연결
- 문제: $\beta$ 변화에 **매우 민감**
- 수식:
  $$
  I_C = \beta \cdot I_B = \beta \cdot \frac{V_{CC} - V_{BE}}{R_B}
  $$

#### ② Resistive Divider Biasing

- 두 저항 $R_1$, $R_2$로 분압하여 Base 전압 설정
- $\beta$에 **덜 민감**, 더 안정적
- $V_X = \frac{R_2}{R_1 + R_2} V_{CC}$  
  $I_C \approx I_S \exp\left( \frac{V_X - V_{BE}}{V_T} \right)$

#### ③ Emitter Degeneration Biasing

- Base에 분압, Emitter에 저항 $R_E$ 삽입
- $R_E$는 바이어스 안정성과 입력 임피던스를 모두 개선
- 전류 관계:
  $$
  V_{RE} = I_E R_E \approx I_C R_E
  $$

---

### ✅ Self-Biasing

- **Collector 전압을 이용해 Base 전압 생성**
- $R_B$와 $R_C$만으로 구성 가능
- 조건:
  - $R_C \gg \frac{R_B}{\beta}$  
  - $V_{CE} > V_{BE}$ 유지로 active mode 보장

---

### ✅ Bias 설계 절차 요약

1. 원하는 $I_C$ 선택 → $g_m$, $r_\pi$ 정해짐
2. $V_{RE}$ 선택 (보통 1V 내외)
3. $V_B = V_{RE} + V_{BE}$ 설정
4. $R_1$, $R_2$ 선택 (분압 공식)
5. $R_C$ 선택해 $V_{CE}$ 유지

---

## 🟦 5.3 PNP Biasing Techniques (p.29)

### 🌱 개념 흐름 요약
- **pnp 바이어싱**도 npn과 동일한 원리로 적용 가능
- 단지 **극성과 전류 방향**만 반대
- 모든 공식은 npn 공식을 다음처럼 변환:
  - $V_{BE} \rightarrow V_{EB}$
  - 전류 방향 반전
  - 회로 상단을 기준으로 분석

📌 즉, **회로는 동일하게 해석 가능**, 단 **방향만 조정하면 됨**

---

## ✅ 전체 요약 정리

| Bias 기법 | 장점 | 단점 |
|-----------|------|------|
| Base Resistor | 구조 단순 | $\beta$에 매우 민감 |
| Resistive Divider | 비교적 안정적 | 저항 변화에 민감 |
| Emitter Degeneration | $\beta$, $V_{BE}$ 변화에 둔감 | Gain 감소 |
| Self-Biasing | 소자 수 적음 | 설계 시 조건 만족 필요 |
| PNP Biasing | npn과 동일 방식 | 극성 반전 고려 필요 |