---
title: Wireshark로 이미지파일 다운받는 법
description: Wireshark로 패킷을 분석하여 Hex 데이터를 PNG 파일로 변환하기
author: bin
date: 2026-01-14 09:00:00 +0800
categories: [TIL, Tools]
tags: [Tools, Wireshark, Network, HTTP, PNG, Packet]
pin: true
math: true
mermaid: true
image:
 path: https://bangjeongbin.github.io/TIL-Blog/assets/img/posts/common/til-logo.png
 alt: Today I Learnd
---

> 해당 포스트는 학습 목적으로 작성되었으며 <<[Wireshark: Packet Analysis and Ethical Hacking: Core Skills](https://www.udemy.com/course/wireshark-packet-analysis-and-ethical-hacking-core-skills/)>>을 참고하여 작성하였음을 알려드립니다.

<br>

> ⚠️ 【면책 고지】
> 
> 본 글은 정보보안 학습을 목적으로 작성되었으며, 사용된 모든 데이터는 합법적으로 취득한 교육용 샘플이며, 실제 운영 중인 네트워크나 개인정보가 포함되지 않았음을 밝힙니다.
> 
> 이 글을 보는 분들께서는 다음 사항을 유념해 주시기 바랍니다:
> - 본 기술은 반드시 합법적인 범위 내에서만 사용되어야 합니다.
> - 타인의 네트워크 트래픽을 무단으로 캡처하거나 분석하는 행위는 정보통신망법 및 통신비밀보호법 위반에 해당할 수 있습니다.
> - 반드시 자신이 관리하는 네트워크 또는 허가받은 환경에서만 실습하시기 바랍니다.
> 
> 본 자료를 참고한 모든 실습 및 그로 인한 결과는 전적으로 본인의 책임이며, 작성자는 이에 대해 어떠한 법적 책임도 지지 않습니다.

<br>

## About
---
실습 데이터(.pcapng)를 가지고 Wireshark를 사용하여 패킷을 분석하기

- 클라이언트 측에서 보낸 요청 메세지 `GET /gns3.png HTTP/1.1`를 서버측에서 응답하는 패킷 `HTTP/1.1 200 OK (PNG)`을 분석하여 PNG 파일을 내 Local에 다운로드 받기

<br>

## 실습
---
![image1](https://lh3.googleusercontent.com/d/1aeeHkS2iJwFwZmBCZq0qickaxBeANghi)

- 해당 강의에서 제공받은 자료에서 `http`를 필터링한다. 그럼 다양한 HTTP 형식의 프로토콜이 보이는데 여기서 주목할 패킷은 서버에서 PNG파일을 응답한 패킷이다

- 해당 패킷 리스트를 클릭하면 좌측 하단에 마킹해 놓은 것처럼 해당 패킷의 Detail이 나온다. Detail을 내리다보면 `Potable Network Graphics`라는 항목이 보이는데 이것의 약자가 바로 PNG이다

<br>

![image2](https://lh3.googleusercontent.com/d/1RMDlNDevdT935luNr8Gf7yqc7FDfitdi)

- 해당 데이터에서 우클릭을 하면 보이는 것처럼 많은 옵션들이 나오는데 우리는 그 중에서 `Export Packet Bytes`를 선택

<br>

![image3](https://lh3.googleusercontent.com/d/1F7FlzgaQUhJ7FHx-5f0FVHUZ7KL_5Pwy)

- 옵션을 클릭 후 파일이름을 지정하고 `Save`

<br>

![image4](https://lh3.googleusercontent.com/d/1Eyfx_WEM_UjUyOpHMc42OMBfgEABUbv8)

- Export가 정상적으로 수행된 것이 보인다

<br>

![image5](https://lh3.googleusercontent.com/d/1xoN0QTpzyeMmao470YS7R-fhQZImsM1_)

- 기존에 설정된 확장자 `.bin`을 `.png`로 수정

<br>

![image6](https://lh3.googleusercontent.com/d/1jXyBuOLY2_OLg60XGyY8Vf0FTq5hxCI5)

- 파일을 열어보면 이미지가 정상적으로 보이는 것을 확인 할 수있다

<br>

<!-- ## Related Posts
---
- 

<br> -->

## Reference
---
- [Wireshark: Packet Analysis and Ethical Hacking: Core Skills](https://www.udemy.com/course/wireshark-packet-analysis-and-ethical-hacking-core-skills/)
