---
title: "Chapter04_Virtualization"
excerpt: "Chapter04. System Programming"

categories:
  - SystemProgramming
tags:
  - [SystemProgramming]

permalink: /categories/SystemProgramming/Chapter04_Virtualization

toc: true
toc_sticky: true

date: 2025-04-26
last_modified_at: 2025-04-26
---

# Chapter 4: 가상머신 소개

## 1. 가상화란
- 1-1. 가상화 개념
- 1-2. 가상화 종류
  - VM 가상화 (CPU, RAM, Storage, Network 등)
  - 네트워크 가상화 (SDN, NFV)
  - 스토리지 가상화
  - 데스크탑 가상화 (VDI, DaaS)
  - 애플리케이션 가상화
  - 데이터 가상화

## 2. 가상화의 장단점
- 2-1. 가상화의 단점 (성능 저하, 비용 증가, 전문 인력 부족)
- 2-2. 가상화의 장점 (유연성, 가용성, 민첩성, 효율성)

## 3. 하이퍼바이저 (Hypervisor)
- 3-1. 하이퍼바이저 개념
- 3-2. 하이퍼바이저의 구조적 특징

## 4. 컨테이너(Container)
- 4-1. 컨테이너 기술 등장 배경
- 4-2. 컨테이너 역사
  - 1979년 Chroot
  - 2000년 FreeBSD Jail
  - 2003년 Google Borg
  - 2008년 LXC
  - 2013년 Docker
  - 2015년 Kubernetes

## 5. 가상머신(Virtual Machine) 개념
- 5-1. 가상머신의 정의
- 5-2. 가상머신과 멀티부팅 차이
- 5-3. Host OS와 Guest OS 개념

## 6. 가상머신 소프트웨어
- 6-1. 가상머신 소프트웨어의 역사
- 6-2. VM Ware 회사 연혁 간략 소개


---

# Chapter 4: 가상머신 소개

## 1. 가상화란

### 1-1. 가상화 개념
- **가상화(Virtualization)**:  
  실체가 없는 것을 **존재하는 것처럼 보이게 만드는 기술**.
- 물리적 자원을 소프트웨어적으로 추상화하여 여러 가상의 자원처럼 운용할 수 있음.

### 1-2. 가상화 종류
- **VM 가상화**: CPU, RAM, Storage, Network 등의 자원을 가상화하여 별개의 컴퓨터처럼 사용.
- **Network Virtualization**:
  - SDN(Software Defined Network)
  - NFV(Network Functions Virtualization)
- **Storage Virtualization**: 여러 스토리지 장비를 하나의 가상 스토리지처럼 통합 관리.
- **Desktop Virtualization**:
  - VDI(Virtual Desktop Infrastructure)
  - DaaS(Desktop as a Service)
- **Application Virtualization**: 앱 자체를 가상화하여 OS에 독립적으로 동작.
- **Data Virtualization**: 물리적으로 분산된 데이터를 통합된 뷰로 제공.

---

## 2. 가상화의 장단점

### 2-1. 가상화의 단점
- **성능 저하**:
  - 중간 처리 계층(하이퍼바이저 등)이 리소스 분배를 위해 추가 동작 필요.
  - 리소스 부족 시 성능 저하가 심각할 수 있음.
- **비용 증가**:
  - 초기 구축비용이 높음.
  - 리소스 사용량이 증가할수록 비용도 함께 상승.
- **운영 복잡성**:
  - 고가용성을 위해 전문 인력 필요.
  - 유지보수 및 관리 포인트 증가.

### 2-2. 가상화의 장점
- **유연성 (Flexibility)**:
  - 환경 변화에 빠르게 대응 가능.
  - 필요에 따라 **Scale Up**(성능 확장), **Scale Out**(서버 수 증가) 가능.
- **가용성 (Availability)**:
  - 무중단 서비스 지원을 위한 인프라 구성.
  - **IaC(Infrastructure as Code)**를 통한 빠른 프로비저닝.
- **민첩성 (Agility)**:
  - 하드웨어 준비 시간 감소.
  - 장애 발생 시 DownTime 최소화.
- **효율성 (Efficiency)**:
  - 자원 최적화 및 비용 절감 가능.

---

## 3. 하이퍼바이저 (Hypervisor)

### 3-1. 하이퍼바이저 개념
- 하이퍼바이저는 **물리적 하드웨어 위에 여러 개의 가상 머신(VM)을 생성하고 운영**할 수 있도록 지원하는 소프트웨어 계층.

### 3-2. 하이퍼바이저의 특징
- **Host OS** 위에 여러 개의 **Guest OS**를 구동 가능.
- 각 가상 머신은 독립적으로 운영체제와 애플리케이션을 실행.

> ⚡ 하이퍼바이저는 강력하지만, **시스템이 Heavy-Weight**가 되는 단점이 있음.  
> ⚡ VM당 별도 OS를 구동하기 때문에 **부팅 시간과 리소스 소모**가 큼.

---

## 4. 컨테이너 (Container)

### 4-1. 컨테이너 기술 등장 배경
- 하이퍼바이저 기반 가상화의 **리소스 소비 문제**를 해결하기 위해 등장.
- **OS 레벨 가상화** 방식으로, 하나의 커널을 공유하며 프로세스를 격리하여 실행.

### 4-2. 컨테이너의 역사
- **1979년 Chroot**: 파일 시스템의 루트 디렉터리를 변경하여 격리.
- **2000년 FreeBSD Jail**: 프로세스와 리소스 격리 강화.
- **2003년 Google Borg**: 대규모 컨테이너 관리 시스템 개발.
- **2008년 LXC(Linux Containers)**: 리눅스 컨테이너 기술 등장.
- **2013년 Docker**: 사용자가 쉽게 다룰 수 있는 컨테이너 도구 등장 → 폭발적 성장.
- **2015년 Kubernetes**: Google이 개발한 오픈소스 컨테이너 오케스트레이션 시스템.

> ✅ **컨테이너**는 하이퍼바이저보다 가볍고 빠르며, **시작 속도가 훨씬 빠르고 리소스 소모가 적다**.

---

## 5. 가상머신(Virtual Machine) 개념

### 5-1. 가상머신의 정의
- **현재 사용 중인 운영체제(Host OS)** 안에 **가상의 컴퓨터**를 만들고,
- 그 위에 **다른 운영체제(Guest OS)**를 설치해 실행하는 기술.

### 5-2. 가상머신과 멀티부팅 차이
- **멀티부팅(Multi-Booting)**:
  - 부팅할 때 하나의 운영체제만 선택해서 사용.
- **가상머신(Virtual Machine)**:
  - 동시에 여러 운영체제를 실행 가능.

### 5-3. Host OS와 Guest OS
- **Host OS**: 실제 물리 하드웨어 위에 설치된 운영체제 (예: Windows).
- **Guest OS**: 가상 머신 내부에 설치한 운영체제 (예: Ubuntu, CentOS 등).

---

## 6. 가상머신 소프트웨어

### 6-1. 가상머신 소프트웨어의 역사
- 1960년대 후반, **메인프레임 컴퓨터의 가상 메모리 관리**에서 시작.
- 이후 다양한 형태의 가상화(스토리지, 네트워크, 서버, 애플리케이션 등)로 발전.

### 6-2. VM Ware 연혁
- VM Ware는 가상화 기술의 선두주자로 발전.
- 가상 머신 생성 및 운영에 있어 가장 널리 사용되는 소프트웨어 제공.

---

## 7. Laboratory Session Syllabus

- 가상머신 및 가상화 환경 구축 실습 예정.
- 다양한 OS 설치 및 가상 환경 세팅을 통한 실습 경험 제공.

---

