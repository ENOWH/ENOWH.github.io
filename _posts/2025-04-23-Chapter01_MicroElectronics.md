---
title: "Chapter01_MicroElectronics"
excerpt: "전자회로 Chap01"

categories:
  - MicroElectronics
tags:
  - [MicroElectronics]

permalink: /categories/MicroElectronics/Chapter01_MicroElectronics

toc: true
toc_sticky: true

date: 2025-04-23
last_modified_at: 2025-04-23
---

# 🧭 Chapter 1: Introduction to Microelectronics

## 📑 세션 구성

---

### 🟦 1.1 Electronics vs. Microelectronics (pp. 3–8)

- 전자공학의 역사: 진공관 → 트랜지스터 → 집적회로(IC)
- Moore's Law: 트랜지스터 집적 밀도는 2년마다 2배
- IC의 발전이 성능/전력/부피 혁신에 미친 영향

---

### 🟦 1.2 Examples of Electronic Systems (pp. 9–18)

- 마이크로프로세서 / 셀룰러 폰 / 디지털 카메라 시스템
- 송신기-수신기의 기본 구조: 변조, 주파수 변환
- ADC(Analog-to-Digital Converter), 시간 공유 구조 등

---

### 🟦 1.3 Basic Concepts (pp. 19–37)

- 아날로그 vs 디지털 신호
- 증폭기(Amplifier)의 이득, 전력 소비, 대역폭
- KCL, KVL, gm 모델, Thevenin/Norton 등 **기본 회로 해석 도구들**

---

## ✅ 전체 요약 흐름

| 세션 | 핵심 주제 | 내용 요약 |
|------|-----------|-----------|
| 1.1 | 전자공학의 발전 | 트랜지스터의 진화와 집적화의 역사 |
| 1.2 | 실제 응용 예시 | 무선 통신, 카메라, ADC, DSP |
| 1.3 | 회로 이론 기초 | 증폭기 이득, 회로 해석 법칙, 등가 회로 |

---


# 🔬 1.1 Electronics vs. Microelectronics

## 🌱 개념 흐름 요약

- 전자공학은 **진공관 → 트랜지스터 → 집적회로(IC)** 순으로 발전
- Microelectronics란?  
  → **반도체 위에 수백~수십억 개의 소자를 집적**하여 기능을 구현하는 전자공학
- 집적도가 높아지며 **부피↓, 성능↑, 소비전력↓, 가격↓** 동시에 달성

---

## 🔑 개념별 정리 (개념 ↔ 수식 연결 중심)

---

### ✅ 진공관 vs 트랜지스터 vs 집적회로

| 세대 | 핵심 기술 | 특징 |
|------|-----------|------|
| 1세대 | 진공관 (Vacuum Tube) | 크고 무겁고 전력 많이 소모 |
| 2세대 | 트랜지스터 (1947) | 작고 효율적, 신뢰성 향상 |
| 3세대 | 집적회로(IC, 1958~) | 수천 → 수십억 트랜지스터 집적 가능 |

---

### ✅ 집적회로 (Integrated Circuit, IC)

- **단일 반도체 칩** 안에 **저항, 커패시터, 트랜지스터** 등을 집적
- 1958년 Jack Kilby (Germanium)
- 1961년 Robert Noyce (Silicon + SiO₂ 절연층, Al 금속선 사용)

📌 IC는 “많은 단순 기능”을 조합하여 “복잡한 시스템”을 구현함

---

### ✅ 집적도 증가: Moore’s Law

- **무어의 법칙**:  
  $$
  \text{Transistor 개수} \propto 2^{\text{년수}/2}
  $$
- 즉, **2년마다 집적도 2배 증가**

- 트랜지스터 크기: 매년 ×0.7씩 감소  
  → 면적은 $0.7^2 = 0.5$ → 절반 감소

---

### ✅ IC 없으면 어떻게 될까? (Example 1.1)

- 1억 개의 트랜지스터를 discrete 소자로 구성한다면?

| 항목 | 계산 결과 |
|------|------------|
| 부피 | $3^3$ mm³ × $10^8$ = $2.7$ m³ (약 1.4m 큐브) |
| 무게 | $1g × 10^8$ = 100 tons |
| 가격 | 1 cent × $10^8$ = 1 million dollars |

📌 IC 없이는 지금과 같은 컴퓨터/스마트폰 상상도 못 했을 것!

---

## ✅ 핵심 요약

| 항목 | 내용 |
|------|------|
| 전자공학 발전사 | 진공관 → 트랜지스터 → 집적회로 |
| Microelectronics 정의 | 수많은 소자를 하나의 칩에 집적 |
| Moore’s Law | 집적도 2년마다 2배 |
| IC 도입 효과 | 가격↓, 전력↓, 속도↑, 부피↓ |
| 현대적 의미 | 오늘날 거의 모든 시스템이 microelectronics 기반 |

🧠 이 세션은 전자공학을 왜 "마이크로"로 발전시켰는지를 이해하는 배경 지식이야!

---

# 📡 1.2 Examples of Electronic Systems

## 🌱 개념 흐름 요약

- Microelectronics는 실제로 **스마트폰, 컴퓨터, 통신, 센서 시스템 등**  
  거의 모든 전자제품에 사용됨
- 복잡한 시스템도 **기본 구성 요소(블록)** 들의 조합으로 구현됨
- 이 세션에서는 시스템 수준에서 **회로의 역할과 흐름**을 이해하는 것이 목적

---

## 🔑 주요 시스템 예제 (개념 ↔ 구조 중심)

---

### ✅ 1. Microprocessor System

- 마이크로프로세서는 **제어 중심의 디지털 시스템**
- 주요 구성 요소:
  - **Processor Core**: 연산, 제어
  - **Memory**: 데이터 저장
  - **I/O Interface**: 센서, 외부 장치와의 연결
  - **Clock Generator**: 타이밍 제공
  - **Power Management**: 전력 제어

📌 전원은 아날로그 회로 / 나머지는 디지털 회로로 구성됨

---

### ✅ 2. Cellular Phone System

- 다양한 기능 통합: 통신 + 연산 + 인터페이스
- 신호 흐름 요약:
  1. **마이크**로부터 입력된 아날로그 신호
  2. **ADC** → 디지털 변환
  3. **DSP (Digital Signal Processor)** 처리
  4. **DAC** → 아날로그 출력
  5. **RF 송수신기 (Transceiver)**

📐 주파수 변환:
- 신호 $x(t)$를 고주파로 옮기는 과정: **변조(Modulation)**
  $$
  x_{\text{mod}}(t) = x(t) \cdot \cos(\omega_c t)
  $$

---

### ✅ 3. Digital Camera System

- 신호 흐름:
  - **CMOS Image Sensor**: 광 → 전기 변환
  - **ADC**: 전기 신호 → 디지털 변환
  - **Image Processor**: 필터, 압축 등 처리
  - **DSP**: JPEG 등 인코딩
  - **Memory**: 저장

📌 대부분의 카메라 이미지 센서는 **CMOS 기반**

---

### ✅ 4. Analog-to-Digital Converter (ADC)

- ADC는 **아날로그 → 디지털 변환기**
- 변환 단계:
  1. **Sampling** (시간 이산화)
  2. **Quantization** (값 이산화)
  3. **Encoding** (디지털 출력)

📐 샘플링 주파수 조건 (Nyquist):
$$
f_s > 2f_{\text{max}}
$$

---

### ✅ 5. Time-Sharing and Multicore

- 하나의 DSP가 **여러 기능을 번갈아 수행 (time-multiplexing)**
- 또는 **Multicore 구조**로 기능을 분산 → 속도 향상

---

## ✅ 핵심 요약

| 항목 | 시스템 블록 | 설명 |
|------|--------------|------|
| 마이크로프로세서 | Core, I/O, Memory, Power | 디지털 제어 |
| 셀룰러폰 | ADC + DSP + RF | 통신 시스템 |
| 디지털 카메라 | Sensor + ADC + DSP | 영상 처리 |
| ADC | Sampling → Quantization → Encoding | 신호 변환의 핵심 |
| 타임 쉐어링 | 하나의 하드웨어로 다중 기능 수행 | 효율적 사용 |

🧠 이 세션은 시스템 관점에서 Microelectronics 회로가 어디에 어떻게 들어가는지를 보여주는 실용 사례집이야!

---

# 🧮 1.3 Basic Concepts

## 🌱 개념 흐름 요약

- Microelectronics 회로 해석을 위해 꼭 알아야 할 **전기회로의 핵심 법칙과 모델** 소개
- 주요 주제:
  1. 아날로그 vs 디지털 신호
  2. 전압, 전류의 정의와 방향성
  3. 회로 해석 법칙: KCL, KVL
  4. 증폭기의 개념: Gain, Power
  5. 등가 모델: Thevenin, Norton

---

## 🔑 개념별 정리 (개념 ↔ 수식 연결 중심)

---

### ✅ 아날로그 vs 디지털

| 구분 | 설명 |
|------|------|
| 아날로그 신호 | 연속적인 값 (e.g., 오디오, 센서) |
| 디지털 신호 | 불연속적인 0/1 값 (e.g., 컴퓨터 신호) |

---

### ✅ 전압과 전류

- **전압 $v$**: 전하가 가진 위치 에너지 차이  
  $$
  v = \frac{dw}{dq}
  $$

- **전류 $i$**: 단위 시간당 전하의 흐름  
  $$
  i = \frac{dq}{dt}
  $$

📌 방향성 주의: 전류는 **양전하가 이동하는 방향** 기준

---

### ✅ KCL / KVL

- **KCL (Kirchhoff’s Current Law)**:  
  한 노드에 들어오는 전류 총합 = 나가는 전류 총합  
  $$
  \sum i_{\text{in}} = \sum i_{\text{out}}
  $$

- **KVL (Kirchhoff’s Voltage Law)**:  
  루프 내 전압의 총합 = 0  
  $$
  \sum_{\text{loop}} v = 0
  $$

---

### ✅ Amplifier의 Gain

- 증폭기란 입력 신호의 크기를 키우는 회로
- 전압 이득 $A_v$:
  $$
  A_v = \frac{v_{\text{out}}}{v_{\text{in}}}
  $$

- 전력 이득 $G$:
  $$
  G = 10 \log_{10} \left( \frac{P_{\text{out}}}{P_{\text{in}}} \right)\ \text{[dB]}
  $$

📌 실제 회로에서는 **전력, 대역폭, 선형성, 효율성** 등을 종합적으로 고려해야 함

---

### ✅ 등가 회로 모델

#### Thevenin Equivalent

- 임의 회로를 **전압원 + 직렬 저항**으로 단순화

📐 Thevenin 모델:
$$
v_{\text{out}} = V_{\text{th}} - i R_{\text{th}}
$$

#### Norton Equivalent

- **전류원 + 병렬 저항**으로 표현

📐 Norton 모델:
$$
i_{\text{out}} = I_{\text{no}} - \frac{v}{R_{\text{no}}}
$$

- 두 모델은 변환 가능:
  $$
  V_{\text{th}} = I_{\text{no}} R_{\text{no}}, \quad R_{\text{th}} = R_{\text{no}}
  $$

---

## ✅ 핵심 요약

| 항목 | 내용 |
|------|------|
| 전압/전류 | 위치에너지 차이 / 전하 흐름 속도 |
| 회로 해석 | KCL, KVL 적용 |
| 증폭기 | Gain = $v_{\text{out}} / v_{\text{in}}$ |
| Power Gain | dB 단위로 비교 |
| 등가 회로 | Thevenin/Norton 모델로 간단화 |

🧠 이 세션은 이후 모든 회로 해석과 증폭기 설계의 기초가 되는 **전자회로의 언어**를 익히는 파트야!