---
title: 2026년 25주차 IT보안 뉴스 분석 보고서
description: 25주차의 IT보안 키워드는 "Microsoft Defender RoguePlanet, Splunk·OT 장비 최고 심각도 결함, 수자원·농업 기반시설 Cyber-Physical 공격, FIRST 6만 6천 건 CVE 전망”으로 요약됩니다.
author: bin
date: 2026-06-21 09:00:00 +0800
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

## 2026년 25주차 전 세계 IT보안 뉴스 분석 보고서

25주차의 IT보안 키워드는 **“Microsoft Defender RoguePlanet, Splunk·OT 장비 최고 심각도 결함, 수자원·농업 기반시설 Cyber-Physical 공격, FIRST 6만 6천 건 CVE 전망”**으로 요약됩니다.

---

### 🌎 1. 글로벌 IT보안 트렌드 요약

#### 보안 솔루션 및 로그 관제 솔루션의 고위험 취약점 노출
- **주요 내용**
    - Microsoft Defender의 권한 상승 제로데이(RoguePlanet)와 Splunk Enterprise의 미인증 기능 접근 결함(CVSS 9.8)이 잇따라 포착됨.
- **분석 및 시사점**
	- 엔드포인트 보안 제품 및 SIEM/관제 플랫폼 자체가 위협 조직의 주요 공격 경로로 전락하고 있어, 보안 통제 도구에 대한 자산 격리 및 최소 권한 가드레일이 시급함.

#### 공공 유틸리티 및 스마트 제어(OT/ICS) 대상 실전 공격 확대
- **주요 내용**
    - 미국 수자원 기업(Cal Water) 데이터 유출, 호주 설탕 제조소(Mackay Sugar) 공장 중단, Lantronix 시리얼 변환기 실전 악용 발생.
- **분석 및 시사점**
	- 이란 배후 공격 그룹 및 사이버 범죄자들의 공격 목표가 IT 자산을 넘어 국가 핵심 물리 인프라와 공급망으로 확산되고 있음.

#### 취약점 폭증 속 대응 병목(Find-to-Fix Bottleneck) 현상 심화
- **주요 내용**
    - FIRST 제38회 연례 컨퍼런스에서 2026년 CVE 연간 발행량이 66,000건에 달할 것으로 수정 전망됨.
- **분석 및 시사점**
	- 단순 탐지 중심 보안을 넘어 CISA KEV 및 EPSS 지표 기반의 위협 우선순위 자동화 패치 관리 체계 정착이 필수가 됨.

---

### 💡 2. 주요 뉴스 Top 10 요약

**(1) Microsoft Defender 권한 상승 제로데이 'RoguePlanet'(CVE-2026-50656) 공식 패치**

* **출처:** BleepingComputer
* **내용:** Microsoft가 연구자 'Nightmare Eclipse'에 의해 공개된 Defender 레이스 컨디션 LPE 제로데이에 대해 Malware Protection Engine 업데이트(v1.1.26060.3008)를 통해 긴급 조치함.
* **의의:** 완벽히 패치된 Windows 10/11 시스템에서도 보안 에이전트를 매개로 SYSTEM 권한을 탈취당할 수 있음을 증명함.

**(2) Splunk Enterprise 인증 미흡 최고 심각도 결함(CVE-2026-20253, CVSS 9.8) CISA KEV 추가**

* **출처:** Hive Pro / CISA
* **내용:** Splunk Enterprise의 핵심 기능 미인증 접근 취약점(CVE-2026-20253, CVSS 9.8)이 실전 공격에 악용됨에 따라 CISA KEV 카탈로그에 긴급 등재됨.
* **의의:** 기업의 중앙 로그 집계 및 보안 관제 중심 시스템이 방어선의 약점으로 부상함.

**(3) Lantronix 시리얼-to-IP 변환기 취약점(CVE-2025-67038, CVSS 9.8) OT 네트워크 공격 악용**

* **출처:** SecurityWeek / CISA
* **내용:** CISA가 Lantronix EDS5000 등 시리얼 변환 장치의 코드 인젝션 결함이 OT 및 산업제어 시스템 침투에 실전 악용되고 있음을 공식 경고함.
* **의의:** 레거시 시리얼 인터페이스를 이더넷에 연결하는 에지 장비가 IT-OT 경계 융합부의 가장 취약한 고리임을 보여줌.

**(4) PTC Windchill PLM 제품 수명주기 관리 플랫폼 최초 실전 악용 포착**

* **출처:** RubyComm / SecurityWeek
* **내용:** 글로벌 제조업체에서 사용되는 PTC Windchill PLM 소프트웨어의 취약점이 최초로 야생(In-the-wild)에서 실전 악용된 사례가 확인됨.
* **의의:** 제조 산업의 지식재산(IP) 및 도면 정보가 보관된 PLM 플랫폼이 지능형 위협 조직의 주요 표적이 됨.

**(5) 이란 배후 Handala 그룹, 미국 대형 수자원 기업 Cal Water 사이버 공격 및 데이터 유출**

* **출처:** SecurityWeek / Dataminr
* **내용:** 이란 연계 해킹 그룹 Handala가 미국 캘리포니아 수자원 서비스(Cal Water) 침해를 주장하며 5GB 분량의 내부 데이터 유출을 공개함.
* **의의:** 지정학적 갈등이 공공 수자원 인프라에 대한 물리적·정보기술적 연쇄 교란 시도로 이어짐.

**(6) 호주 2위 설탕 생산기업 Mackay Sugar 사이버 공격으로 공장 가동 전면 중단**

* **출처:** RubyComm / ZDNet
* **내용:** 호주 Mackay Sugar사의 주요 정제 공장(Farleigh 및 Racecourse)이 사이버 공격을 받으며 제당 작업 및 원수확 작업이 전면 정지됨.
* **의의:** 농업 및 식량 공급망 인프라가 랜섬웨어 및 사이버 공작 공격에 극도로 취약함을 입증함.

**(7) FIRST 38th 연례 컨퍼런스, 2026년 CVE 66,000건 상향 조정 및 '패치 병목' 경고**

* **출처:** FIRST / MODA Cybersecurity Report
* **내용:** FIRST가 연간 CVE 전망치를 66,000건으로 대폭 상향하며, 취약점 '탐지'보다 패치 실행 '용량'이 핵심 병목으로 작용한다고 발표함.
* **의의:** 자동화된 패치 검증 체계와 실전 악용성 지표(KEV, EPSS) 기반의 리스크 관리가 불가피해짐.

**(8) Check Point Security Gateway 및 SolarWinds Serv-U 고위험 결함 KEV 등재**

* **출처:** Hive Pro / CISA
* **내용:** Check Point 보안 게이트웨이의 인증 우회(CVE-2026-28318, CVSS 9.3) 및 SolarWinds Serv-U 파일 전송 서비스 결함이 KEV 카탈로그에 포함됨.
* **의의:** 파일 전송 및 경계 게이트웨이 장비가 침투 거점(Initial Access)으로 지속 활용됨.

**(9) NIST SP 1800-45 수자원·폐수 처리 OT 원격 접근 보안 지침 공식 발표**

* **출처:** NIST / RubyComm
* **내용:** 미 NIST가 수자원 시설의 디지털 전환에 따른 사이버 위협 증대에 대응하여 OT 원격 접속 보안을 강황하는 SP 1800-45 가이드라인을 공표함.
* **의의:** 공공 유틸리티 산업 전반에 제로 트러스트 원격 접속 통제 도입이 제도화되고 있음.

**(10) Claroty 연구진, 데이터센터 HVAC 냉각 및 UPS 전력 시스템 고위험 취약점 공개**

* **출처:** Claroty / Cimetrics
* **내용:** 데이터센터에서 사용되는 냉난방 공조(HVAC) 및 무정전 전원장치(UPS)의 원격 제어 취약점이 공개되어 물리적 서버 셧다운 위험성이 지적됨.
* **의의:** AI 데이터센터 및 IT 인프라 방어가 건물 관리 물리 제어 시스템(BMS) 영역까지 확장되어야 함을 보여줌.

---

### 📊 3. IT보안 산업별 트렌드 분석

#### 엔드포인트 & 관제 인프라(SOC/SIEM)
- **핵심 트렌드**: Defender RoguePlanet 패치 및 Splunk 등 SIEM 솔루션 대상 직접 공격 폭증.
	
- **전망**: 보안 통제 소프트웨어 자체에 대한 가상화 격리 및 특권 세션 관리(PAM) 적용이 필수화될 것입니다.

#### 공공 유틸리티 & 스마트 제어(OT/ICS)
- **핵심 트렌드**: 수자원·농업 기반시설 타격 및 Lantronix 시리얼 변환기, PTC Windchill 악용.
	
- **전망**: NIST SP 1800-45 지침 수용 및 IT/OT 네트워크 경계에 세그멘테이션과 인라인 패킷 검사가 의무화될 것입니다.

#### 데이터센터 & 물리 인프라 보안
- **핵심 트렌드**: 데이터센터 HVAC, UPS 등 전력·냉각 시설 물리 제어 장치의 원격 공격 위협 공개.
	
- **전망**: 전통적 IT 보안팀과 건물 관리/OT 운영팀 간 통합 관제 센터(Unified Physical-Cyber SOC) 구축이 급증할 전망입니다.

---

### 📈 4. 향후 전망

1. **보안 솔루션 자체의 표적 공격화 지지대 형성:** Defender 및 Splunk 사례에서 보듯 방어 도구를 역이용하는 레이스 컨디션 및 인증 우회 공격이 고도화될 것입니다.
2. **OT 시리얼 및 PLM 관리 소프트웨어로의 공격 표면 확장:** Lantronix, PTC Windchill 등 산업 현장의 깊은 레이어 솔루션을 노린 사이버 스파이 활동이 본격화될 것입니다.
3. **'Find-to-Fix' 대응 자동화 및 AI 가상 패치 정착:** 연간 66,000건의 CVE 속에서 KEV/EPSS 기반 자동화 패치 테스팅 및 인라인 WAF 가상 패치가 핵심 방어책으로 부상할 것입니다.
4. **데이터센터 Cyber-Physical 안보 강화 규제화:** AI 데이터센터의 전력 및 냉각 설비(HVAC/UPS) 보안 검증이 국가 차원의 중요 기반시설 안보 규제 항목으로 편입될 전망입니다.

---

### 🧭 5. 결론 요약

2026년 25주차 전 세계 IT보안 시장은 **보안 제품 및 관제 인프라 자체의 최고 심각도 결함**, **수자원·식량 등 물리적 핵심 기반시설을 향한 사이버 공격의 본격화**, 그리고 **폭증하는 CVE 속 패치 대응 용량의 한계**가 극명하게 드러난 시기였습니다. 기업과 공공기관은 관제 시스템 자산에 대한 접근 통제를 엄격히 재정비하고, 위협 인텔리전스(KEV) 기반의 패치 자동화 체계를 신속히 도입해야 합니다.
