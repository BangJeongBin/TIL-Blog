---
title: 2026년 21주차 IT보안 뉴스 분석 보고서
description: 21주차의 IT보안 키워드는 "Exchange·Defender 제로데이, 코드 서명 인증서 남용, AI 프레임워크 Langflow RCE, BitLocker 우회(YellowKey)”으로 요약됩니다.
author: bin
date: 2026-05-24 09:00:00 +0800
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

## 2026년 21주차 전 세계 IT보안 뉴스 분석 보고서

21주차의 IT보안 키워드는 **“Exchange·Defender 제로데이, 코드 서명 인증서 남용, AI 프레임워크 Langflow RCE, BitLocker 우회(YellowKey)”**으로 요약됩니다.

---

### 🌎 1. 글로벌 IT보안 트렌드 요약

#### 핵심 온프레미스 및 보안 인프라 대상 제로데이 파상 공격
- **주요 내용**
    - MS Exchange Server(CVE-2026-42897), MS Defender(CVE-2026-41091/45498), Cisco Secure Workload 등 주요 기업용 인프라에서 능동 악용 제로데이가 연달아 보고됨.
- **분석 및 시사점**
	- 보안 백신과 중앙 메시징 서버 자체의 취약점을 노리는 표적 공격이 심화되고 있어, 패치 배포 전 긴급 완화 도구(EEMS) 배포 및 실시간 탐지 레이어 강화가 시급함.

#### 디지털 서명 신뢰 체계(Trust Infrastructure) 무력화
- **주요 내용**
    - MS 공식 아티팩트 서명 인프라를 악용한 'OpFauxSign' 서비스 적발 및 CISA 수탁업체의 비밀 리포지토리(Private-CISA) 6개월간 공공 노출 사고 발생.
- **분석 및 시사점**
	- 보안 도구가 의존하는 디지털 서명과 공공 기관 신뢰 자산 자체를 악용·우회하는 '신뢰 기반 공격 벡터'가 악성코드 유포의 주요 통로로 악용되고 있음.

#### AI 개발 파이프라인 및 물리적 접속 영역으로의 위협 다각화
- **주요 내용**
    - AI 오케스트레이션 오픈소스 Langflow(CVE-2025-34291)의 CISA KEV 등록 및 Silent Ransom Group의 오프라인 현장 직접 침투 전술 도입.
- **분석 및 시사점**
	- AI 파이프라인이 APT 공격 통로로 부상함과 동시에, 네트워크 차단을 우회하기 위한 물리 현장 USB 삽입 등 다차원(Hybrid) 공격 전술이 기업 방어망을 위협함.

---

### 💡 2. 주요 뉴스 Top 10 요약

**(1) Microsoft Exchange Server OWA 제로데이(CVE-2026-42897) 능동 공격 포착**

* **출처:** Medium / Microsoft Security Advisory
* **내용:** Exchange Server 2016, 2019 및 Subscription Edition의 OWA에서 자바스크립트 임의 실행 및 세션 토큰 탈취를 유발하는 XSS 제로데이(CVE-2026-42897)가 발견되어 능동 악용 중임.
* **의의:** 정식 패치 배포 전까지 긴급 완화 도구(EEMS) 적용이 시급하며, 온프레미스 이메일 인프라가 B2B 침투의 진입점으로 지속 악용되고 있음을 입증함.

**(2) Microsoft Defender 제로데이 2종(CVE-2026-41091, CVE-2026-45498) 긴급 패치 및 CISA KEV 지정**

* **출처:** BleepingComputer / CISA KEV
* **내용:** 엔드포인트 보안 도구인 MS Defender에서 SYSTEM 권한 상승(CVE-2026-41091) 및 DoS(CVE-2026-45498)를 유발하는 제로데이 취약점 2종이 능동 공격에 악용되어 CISA KEV 목록에 등록됨.
* **의의:** 보안 방어 솔루션 자체가 공격자의 권한 상승 통로로 반전될 수 있어 엔드포인트 솔루션의 실시간 위협 통제 검증이 중요함.

**(3) 마이크로소프트 코드 서명 인프라 남용 'OpFauxSign' 적발 및 1,000여 개 인증서 박탈**

* **출처:** DIESEC / Microsoft Threat Intelligence
* **내용:** 위협 집단 Fox Tempest가 마이크로소프트 공식 아티팩트 서명 인프라를 악용해 Rhysida 랜섬웨어 및 스틸러 악성코드를 정식 서명된 바이너리로 위장·유포한 'OpFauxSign' 서비스가 적발되어 C2 및 1,000여 개 인증서가 차단됨.
* **의의:** EDR 및 백신의 디지털 서명 신뢰 메커니즘을 무력화하는 '코드 서명 서비스의 무기화' 현상을 차단하기 위해 인증서 발급 보안 절차가 대대적으로 재점검됨.

**(4) AI 오케스트레이션 프레임워크 'Langflow' RCE 취약점(CVE-2025-34291) CISA KEV 등록**

* **출처:** DIESEC / Check Point Research
* **내용:** AI LLM 앱 개발 프레임워크인 Langflow의 RCE 취약점(CVE-2025-34291)이 국가 배후 공격 그룹(Iran-linked MuddyWater)에 의해 능동 악용됨에 따라 CISA KEV에 긴급 등록됨.
* **의의:** AI 애플리케이션 파이프라인의 오픈소스 구성 요소가 글로벌 APT 조직의 주요 침투 타깃이 되고 있어 AI Supply Chain 보안 조치가 시급함.

**(5) Windows BitLocker 우회 'YellowKey' 제로데이(CVE-2026-45585) 완화 조치 발표**

* **출처:** Medium / Microsoft Security
* **내용:** 실물 USB를 통해 Windows 복구 환경(WinRE)에서 무제한 쉘을 획득하여 BitLocker 암호화를 우회하는 물리적 제로데이(CVE-2026-45585) 완화책이 공지됨.
* **의의:** 단일 TPM 인증의 한계를 드러내며, 데이터 보호를 위한 물리적 접근 통제 및 TPM+PIN 다중 인증의 필요성이 재입증됨.

**(6) CISA 수탁업체, 비밀 기밀 리포지토리(Private-CISA) GitHub 6개월간 공공 노출**

* **출처:** DIESEC
* **내용:** 미국 CISA 보안 감사를 담당하는 외주 수탁업체가 작업 편의를 위해 자격 증명과 내부 키가 포함된 리포지토리를 GitHub에 6개월간 공공 개방한 사실이 드러남.
* **의의:** 최고 수준의 정부 보안 기관조차 제3자 수탁업체(Third-party)의 수동적 보안 부주의로 인해 치명적 공급망 위협에 직면할 수 있음을 입증함.

**(7) Silent Ransom Group, 피싱 실패 시 '물리적 현장 침투'로 USB 해킹 시도 전술 전환**

* **출처:** DIESEC / FBI FLASH Alert
* **내용:** FBI가 레거시 피싱 공격에 실패한 랜섬웨어 그룹(SRG)이 IT 지원 기사로 위장하여 법률 사무소 등 목표 건물에 직접 들어가 USB를 꽂는 물리적 침투를 감행 중이라고 경고함.
* **의의:** 사이버 경계 방어가 강화됨에 따라 공격자가 오프라인 물리 보안 및 사회공학적 기만을 결합하는 이중 침투 기법을 다각화하고 있음.

**(8) Cisco Secure Workload 최고 심각도(CVSS 10.0) REST API 취약점(CVE-2026-20223) 긴급 패치**

* **출처:** Medium / Cisco Security Advisory
* **내용:** 워크로드 보호 플랫폼인 Cisco Secure Workload에서 비인증 공격자가 최고 관리자(Site Admin) 권한을 획득할 수 있는 REST API 취약점이 공개되어 온프레미스 패치가 긴급 배포됨.
* **의의:** 클라우드/데이터센터 세그멘테이션 솔루션의 API 권한 검증 미흡이 전체 인프라 권한 상실로 이어질 수 있음을 대변함.

**(9) SonicWall VPN MFA 우회(CVE-2024-12802)를 통한 랜섬웨어 침투 지속 발생**

* **출처:** Medium / Security Research
* **내용:** SonicWall Gen6 SSL-VPN 장비의 MFA 우회 취약점에 대해 수동 재설정 단계를 누락한 기업들을 노린 랜섬웨어 침투가 연이어 보고됨.
* **의의:** 단순 펌웨어 패치 적용 후에도 수동 재설정 및 설정 오남용을 방지하는 정교한 취약점 관리(Vulnerability Lifecycle)가 필수적임을 보여줌.

**(10) Linux 커널 cryptographic 서브시스템 LPE 취약점(CVE-2026-31431) 발견**

* **출처:** Recast Software / Security Research
* **내용:** Linux 커널의 암호화 서브시스템 내 페이지 캐시 메모리를 손상시켜 일반 사용자 권한을 root로 상승시키는 LPE 취약점이 공개되어 Docker Desktop 등 가상화 환경에 영향을 미침.
* **의의:** 컨테이너 및 가상화 환경의 기초가 되는 리눅스 커널 레벨 취약점이 클라우드 네이티브 공급망 전반에 미치는 영향력을 강조함.

---

### 📊 3. IT보안 산업별 트렌드 분석

#### 엔드포인트 & OS 보안
- **핵심 트렌드**: Defender 제로데이, BitLocker 우회(YellowKey), 코드 서명 인증서 남용(OpFauxSign)에 대응하는 보안 신뢰성 재정립.
	
- **전망**: 정적 디지털 서명 검증을 넘어 하드웨어 기반 TPM+PIN 강화 및 커널·보안 모듈 자체의 행위 기반 인라인 차단이 필수화될 것입니다.

#### AI & 애플리케이션 파이프라인 보안
- **핵심 트렌드**: Langflow 등 AI 오케스트레이션 오픈소스 RCE(CVE-2025-34291)의 CISA KEV 등록 및 AI 개발 공급망 타깃 공격 본격화.
	
- **전망**: Enterprise AI 도입 확산에 맞춰 LLM 파이프라인 및 개발 프레임워크 대상의 AI-SBOM(소프트웨어 자재명세서) 검증 체계가 빠르게 안착할 것입니다.

#### 물리 보안 & 공급망 거버넌스
- **핵심 트렌드**: CISA 외주업체 리포지토리 노출 및 Silent Ransom Group의 오프라인 현장 직접 침입 등 물리·수탁업체 보안 취약점 대두.
	
- **전망**: 전통적 사이버 방화벽을 넘어 서드파티 통합 위험 관리(TPRM) 및 출입 통제와 연계된 융합 보안(Converged Security) 정책이 수립될 것입니다.

---

### 📈 4. 향후 전망

1. **디지털 서명 및 신뢰 체계(Trust Infrastructure) 재검증의 보편화:** OpFauxSign 적발 사례처럼 정상 서명 인증서의 획득 및 남용이 증가함에 따라, 엔드포인트 보안 도구는 디지털 서명 유무와 무관하게 동적 위협 분석 기능을 대폭 강화할 것입니다.
2. **AI 파이프라인(LLM Orchestration) 대상 보안 패치 단축:** Langflow RCE의 KEV 지정이 보여주듯, AI 애플리케이션 개발 프레임워크의 취약점이 APT 조직의 최우선 공격 통로가 되면서 AI 공급망 취약점 관리 SLA가 72시간 이내로 단축될 것입니다.
3. **사이버-물리 융합(Phygital) 사회공학 공격에 대응한 복합 방어 체계:** 피싱 차단을 우회하기 위해 물리적 방문 및 USB 꽂기 전술을 구사하는 공격에 대비해 기업은 물리적 출입 통제와 내부 단말 USB 포트 통제 강화를 결합할 것입니다.
4. **엔터프라이즈 레거시·보안 인프라의 '자동 완화(Auto-Mitigation)' 시스템 내재화:** Exchange 및 Defender 제로데이처럼 즉각적인 패치 배포 전 긴급 완화책(EEMS 등)을 자동 적용하는 보안 운용 인프라 도입이 급증할 것입니다.

---

### 🧭 5. 결론 요약

2026년 21주차 전 세계 IT보안 시장은 **Exchange·Defender 등 핵심 인프라 제로데이 파상 공격**과 **코드 서명 및 AI 파이프라인 취약점을 노린 신뢰 체계 무력화**, 그리고 **물리 침투까지 동원하는 고도화된 위협 전술**이 대두된 한 주였습니다. 기업 보안 조직은 디지털 인증서 관리와 AI 공급망의 안전성을 조속히 재점검하고, 물리·사이버가 결합된 다차원적 복원력을 구축해야 합니다.
