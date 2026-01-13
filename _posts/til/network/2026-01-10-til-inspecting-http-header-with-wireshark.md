---
title: HTTP헤더를 Wireshark로 보는 법
description: Wireshark로 패킷 다이어그램 보기
author: bin
date: 2026-01-10 09:00:00 +0800
categories: [TIL, Network]
tags: [Network, Wireshark, HTTP, Header]
pin: true
math: true
mermaid: true
image:
 path: https://bangjeongbin.github.io/TIL-Blog/assets/img/posts/common/til-logo.png
 alt: Today I Learnd
---

![Wireshark Logo](https://images.velog.io/images/joosing/post/3cdc3aec-0b8c-48c5-8607-ea8203998306/wireshark-1.png)

와이어샤크[^1]

## HTTP 접속
---
![apache2_debian_defulat_page](https://lh3.googleusercontent.com/d/1TBGI9FZl1oNpwKVq7lLQ5jxTtCvNiY4y)


- http://210.179.28.214

해당 URL은 Apache2 Debian Default Page로 이동된다. HTTP로 접속되는 페이지 이므로 Wireshark를 이용하여 HTTP 패킷을 확인 할 수 있다.

아래는 Wireshark의 Packet Diagram으로 확인한 데이터다.

<br>

## HTTP GET Header
---
![wireshark_diagram_get](https://lh3.googleusercontent.com/d/1f2G8Hz1W94n4lg4FmF30wU5_kMsY0A2C)

<br>

## HTTP POST Header
---
![wireshark_diagram_post](https://lh3.googleusercontent.com/d/16_fGakmIVoQXWWt001fNJvDTnmXVioz8)

- POST Message는 body의 길이가 너무 길어서 중략함

<br>

## Header 구성
---
- 위와 같이 각 Layer의 식별자 마다 Header를 구성하고 있고, 캡슐화 되어있는 각 Header에는 데이터들에 대한 정보들로 이루어져 있다.

<br>

## Related Posts
---
- [패킷의 구조](https://bangjeongbin.github.io/TIL-Blog/posts/til-structure-of-a-packet)
- [HTTP 상태 코드의 종류](https://bangjeongbin.github.io/TIL-Blog/posts/til-type-of-http-response-status-codes)

<br>

## Reference
---
- [웹 요청 종류에 따라 와이어샤크 분석하기](https://youtu.be/K3fMMW6AM1w?si=ErjPN_DNwEM4M6-_)

[^1]: 출처 : https://velog.io/@joosing/Wireshark-%ED%8C%A8%ED%82%B7-%ED%95%84%ED%84%B0-A-to-Z
