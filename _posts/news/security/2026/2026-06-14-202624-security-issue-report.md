---
title: 2026년 24주차 IT보안 뉴스 분석 보고서
description: 24주차의 IT보안 키워드는 "Microsoft Defender RoguePlanet 제로데이, CISA KEV 23개 취약점 추가, Amadey·StealC 인포스틸러 소탕, 데이터센터 HVAC·UPS 보안 위협”으로 요약됩니다.
author: bin
date: 2026-06-14 09:00:00 +0800
categories: [NEWS, Security]
tags: [NEWS, Security]
pin: true
math: true
mermaid: true
image:
 path: https://bangjeongbin.github.io/TIL-Blog/assets/img/posts/common/news-logo.png
 alt: Weekly News
---

> **해당 포스트는 생성형 AI를 활용하여 작성하였음을 알려드립니다.**
{: .prompt-info }

## 2026년 24주차 전 세계 IT보안 뉴스 분석 보고서

24주차의 IT보안 키워드는 **“Microsoft Defender RoguePlanet 제로데이, CISA KEV 23개 취약점 추가, Amadey·StealC 인포스틸러 소탕, 데이터센터 HVAC·UPS 보안 위협”**으로 요약됩니다.

---

### 🌎 1. 글로벌 IT보안 트렌드 요약

#### 엔드포인트 보안 및 브라우저 제로데이의 잇따른 노출
- **주요 내용**
    - Microsoft Defender의 권한 상승 제로데이(RoguePlanet)와 Google Chrome V8 엔진 결함이 잇따라 공개됨.
- **분석 및 시사점**
	- 보안을 담당하는 차단 솔루션 자체의 취약점이 공격자의 권한 상승 경로로 악용되는 역설적 상황이 지속되고 있어 딥 디펜스(Deep Defense) 레이어링이 필수적입니다.

#### 네트워크·원격 관리 장비 최고 심각도(CVSS 10.0) 취약점 집결
- **주요 내용**
    - Ivanti Sentry, Ubiquiti UniFi OS, Cisco 장비 등 기업 인프라 핵심 장비의 최고 심각도 결함이 CISA KEV 카탈로그에 대거 등재됨.
- **분석 및 시사점**
	- 외부 경계 장비 및 네트워크 통합 관리 시스템이 APT 조직과 랜섬웨어 그룹의 최우선 침투 경로로 고착화되고 있어 수동적 패치를 넘어선 관리 인터페이스 격리가 요구됩니다.

#### 글로벌 공조를 통한 인포스틸러 소탕 및 OT/데이터센터 위협 부각
- **주요 내용**
    - 국제 사법기관의 'Operation Endgame'을 통한 Amadey·StealC 봇넷 소탕과 함께 데이터센터 HVAC/UPS 등 물리적 인프라 대상 공격 위험이 공개됨.
- **분석 및 시사점**
	- 인프라 위협이 사이버 공간을 넘어 데이터센터 냉각·전력 등 물리 인프라로 확장됨에 따라 IT/OT 통합 보안 통제권 확보가 급선무로 부상했습니다.

---

### 💡 2. 주요 뉴스 Top 10 요약

**(1) Microsoft Defender 권한 상승 제로데이 'RoguePlanet'(CVE-2026-50656) 공개 및 긴급 패치**

* **출처:** BleepingComputer
* **내용:** 연구자 'Nightmare Eclipse'가 Windows 10/11 전반에 영향을 미치는 Microsoft Defender 레이스 컨디션 LPE 제로데이를 공개했으며, Microsoft는 Malware Protection Engine 업데이트(v1.1.26060.3008)를 통해 긴급 조치함.
* **의의:** 엔드포인트 보안 제품의 자체 취약점이 SYSTEM 권한을 탈취하는 무기로 전락할 수 있음을 증명하며 보안 소프트웨어에 대한 지속적인 공격 표면 관리가 필수임을 상기시킵니다.

**(2) CISA, 6개 제로데이 포함 총 23개 능동 악용 취약점 KEV 카탈로그 전격 추가**

* **출처:** Hive Pro / CISA
* **내용:** CISA가 2026년 6월 한 달간 6개의 제로데이와 CVSS 최고 10.0에 달하는 총 23개의 능동 악용 취약점을 Known Exploited Vulnerabilities(KEV) 카탈로그에 대거 등재함.
* **의의:** 연방 기관 및 민간 기업에 최우선 패치 의무를 부여하는 인텔리전스 기반 패치 관리의 중요성이 더욱 증대되었습니다.

**(3) Ivanti Sentry 최고 심각도(CVSS 10.0) OS 명령 주입 취약점(CVE-2026-11645) CISA KEV 지정**

* **출처:** Hive Pro / SecurityWeek
* **내용:** 모바일 게이트웨이 및 보안 컨트롤러인 Ivanti Sentry에서 원격 코드 실행이 가능한 최고 심각도 OS Command Injection 취약점이 실전 공격에 악용되어 CISA KEV에 추가됨.
* **의의:** 모바일 및 게이트웨이 통제 솔루션의 경계 무력화 시도가 급증하고 있음을 보여주며 엄격한 접근 제어가 요구됩니다.

**(4) Ubiquiti UniFi OS 최고 심각도(CVSS 10.0) 입력 검증 무력화 및 경로 이탈 취약점 포착**

* **출처:** Hive Pro
* **내용:** 네트워크 장비 관리 플랫폼인 Ubiquiti UniFi OS의 입력 검증 무력화(CVE-2026-34910) 및 경로 이탈(CVE-2026-34909) 취약점이 CVSS 10.0을 기록하며 CISA KEV에 등재됨.
* **의의:** 네트워킹 인프라 장비의 관제 소프트웨어가 무단 공격자의 네트워크 전체 장악 거점이 되고 있음을 입증합니다.

**(5) 국제 사법당국, 'Operation Endgame' 작전으로 Amadey 및 StealC 인포스틸러 봇넷 인프라 대거 소탕**

* **출처:** BleepingComputer / CM Alliance
* **내용:** 국제 공조 사법기관들이 'Operation Endgame' 작전을 시행하여 대규모 계정 정보 탈취 악성코드인 Amadey와 StealC의 C2 서버 및 공격 인프라를 대거 차단 및 무력화함.
* **의의:** 계정 정보 탈취형 악성코드(Infostealer) 생태계에 대한 전 지구적 사법 집행이 가속화되고 있음을 의미합니다.

**(6) 데이터센터 HVAC 및 UPS 무정전 전원장치 대상 물리·사이버 융합 취약점 대거 공개**

* **출처:** Claroty / Cimetrics
* **내용:** 보안 연구진이 데이터센터에서 광범위하게 사용되는 HVAC(냉난방 공조) 및 UPS 장비의 심각한 원격 공격 취약점을 공개하며, 데이터센터 물리 셧다운 위험을 경고함.
* **의의:** 사이버 공격의 목표가 데이터 유출을 넘어 AI 및 클라우드 데이터센터의 물리적 운용을 중단시키는 하이브리드 위협으로 확산되고 있습니다.

**(7) 미국 정부, 안보 우려로 제한했던 Anthropic 'Claude Mythos' AI 모델 접근성 조건부 완화**

* **출처:** Cimetrics / Tech Policy
* **내용:** 미 정부가 강력한 오펜시브 보안 기능으로 국가 안보 우려를 샀던 Anthropic의 'Claude Mythos' AI 모델에 대해 지정된 기업 및 기관 대상으로 제한적 허용 조치를 취함.
* **의의:** AI 모델의 위협 탐지 역량과 오펜시브 무기화 가능성 사이에서 글로벌 국가 통제 및 AI 안보 규제 정책이 구체화되고 있습니다.

**(8) Google Chrome V8 엔진 메모리 손상 제로데이 취약점(CVE-2026-7473) CISA KEV 등재**

* **출처:** Hive Pro / Google Bulletin
* **내용:** Google Chrome의 V8 JavaScript 엔진에서 발견된 Out-of-bounds Read/Write 취약점(CVE-2026-7473)이 표적 공격에 악용되어 긴급 패치와 함께 KEV 카탈로그에 포함됨.
* **의의:** 웹 브라우저가 기업 내 최초 침입(Initial Access)의 주된 통로로 계속 활용되고 있어 엔드포인트 브라우저 보안 격리가 필수적입니다.

**(9) cPanel/WHM(CVE-2026-41940) 및 LiteSpeed cPanel 플러그인(CVE-2026-48172) 실전 악용 지속**

* **출처:** Senthorus Blog / SecurityWeek
* **내용:** 웹호스팅 인프라의 cPanel/WHM 세션 우회 및 LiteSpeed 플러그인 Root 권한 상승 취약점을 악용한 SORRY 랜섬웨어 유포와 봇넷 포섭이 계속되며 긴급 패치가 재권고됨.
* **의의:** 호스팅 플랫폼에 대한 공격이 단일 서버 침해를 넘어 연쇄적인 서드파티 공급망 피해로 확대되고 있음을 보여줍니다.

**(10) CISA, Schneider Electric·Yokogawa 등 주요 OT/ICS 산업제어시스템 보안 권고안 대거 발령**

* **출처:** CISA / Cimetrics
* **내용:** CISA가 Schneider Electric, Yokogawa, Delta Electronics 등 주요 OT 및 ICS 제조사의 산업제어시스템 취약점에 대한 무더기 보안 권고안을 발표함.
* **의의:** 에너지, 제조 등 국가 핵심 기반시설 대상 OT 영역의 취약점 보완이 국가 사이버 안보의 시급한 과제로 부상했습니다.

---

### 📊 3. IT보안 산업별 트렌드 분석

#### 엔드포인트 & OS 보안
- **핵심 트렌드**: Defender 'RoguePlanet' 등 백신 자체 취약점을 노린 LPE 공격 급증 및 Chrome 브라우저 메모리 결함 악용.
	
- **전망**: 보안 에이전트 소프트웨어 자체에 대한 가상화 기반 샌드박싱 및 최소 권한 실행 환경 적용이 보편화될 것입니다.

#### 네트워크 & 게이트웨이 보안
- **핵심 트렌드**: Ivanti, Ubiquiti, Cisco 등 외부 접속 및 네트워킹 장비의 CVSS 10.0급 초고위험 결함 집중 악용.
	
- **전망**: 경계 기반 네트워크 통제의 한계가 드러남에 따라, ZTNA(Zero Trust Network Access) 전환 및 관리 포털 비공개화가 가속화될 것입니다.

#### 데이터센터 & OT 인프라 보안
- **핵심 트렌드**: HVAC, UPS 등 물리 데이터센터 시설 및 Schneider/Yokogawa 제어장치 대상 사이버 위협 증대.
	
- **전망**: AI 데이터센터 및 산업 시설을 보호하기 위한 IT-OT-물리 인프라 통합 보안 관제(XDR/OT-SOC) 시장이 급성장할 전망입니다.

---

### 📈 4. 향후 전망

1. **보안 솔루션 자체에 대한 표적 공격(Exploiting Security Software) 상시화:** Microsoft Defender 사례처럼 보안 제품 자체의 레이스 컨디션이나 권한 상승 결함을 노린 공격이 주요 기법으로 안착할 것입니다.
2. **AI 데이터센터 물리 인프라 대상 킬체인 형성:** HVAC 및 UPS 제어 장치를 마비시켜 물리적 데이터센터 가동을 중단시키는 파괴적 attack vector가 현실화될 전망입니다.
3. **CISA KEV 중심의 긴급 위협 대응 체계 정착:** CVSS 점수뿐만 아니라 실전 악용 여부(KEV)에 기반하여 24~48시간 이내에 패치를 적용하는 우선순위 대응 패러다임이 확립될 것입니다.
4. **오펜시브 AI 모델 규제 및 허가제 도입 가속화:** Anthropic 'Claude Mythos' 접근 제한 완화 사례처럼, 고도화된 AI 취약점 탐지/공격 모델의 국가 차원 안보 규제 및 비대칭 통제 조치가 한층 강화될 것입니다.

---

### 🧭 5. 결론 요약

2026년 24주차 전 세계 IT보안 시장은 **엔드포인트 보안 제품 및 브라우저 제로데이의 위협**, **네트워크·게이트웨이 장비의 CVSS 10.0급 초고위험 취약점 속출**, 그리고 **데이터센터 물리 인프라 대상 공격의 가시화**가 핵심 이슈였습니다. 기업과 기관은 보안 인프라 자체에 대한 지속적인 검증을 실시하고, Zero Trust 접근 통제와 인텔리전스 기반의 신속한 KEV 패치 체계를 정립해야 합니다.
