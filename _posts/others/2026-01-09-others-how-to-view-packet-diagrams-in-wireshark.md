---
title: Wireshark에서 패킷 다이어그램 보는법
description: Packet Diagram 설정
author: bin
date: 2026-01-09 09:00:00 +0800
categories: [Others]
tags: [Network, Wireshark, Packet]
pin: true
math: true
mermaid: true
---

![Wireshark Logo](https://images.velog.io/images/joosing/post/3cdc3aec-0b8c-48c5-8607-ea8203998306/wireshark-1.png)

와이어샤크[^1]

## about
---
![image1](https://lh3.googleusercontent.com/d/1qPVgyL1gVBuF0uAbyAp9hfojsUAey2Jy)

기존의 Wireshark는 디폴트 Layout이 이렇게 되어있다.

최상단에 패킷 리스트, 그 아래로는 해당 패킷의 상세내용, 헥사덤프값으로 구성되어있다.

<br>

![image2](https://lh3.googleusercontent.com/d/185GyRKxzPH6MKzODvMd3mYuoj30pD2HQ)

와이어샤크의 설정으로 들어간다. 맥 기준으론 `cmd + ,`

이후 사이드바에서 Appearance의 Layout 카테고리로 진입한다.

<br>

![image3](https://lh3.googleusercontent.com/d/1QwiRDQ-XhBcHKd4p_IoXPyRWdAX7AoxM)

원하는 위치와 Layout 구성을 선택하고 Packet Diagram을 선택한 뒤 OK를 눌러 적용한다.

<br>

![image4](https://lh3.googleusercontent.com/d/1_J_ut1bKnmyZ5WFWtDJAl18yEcBQ73sL)

다시 메인으로 넘어오면 Packet Diagram이 잘 적용된 것을 볼 수있다.

Wireshark를 많이 사용하지 않은 사람들은 Packet Diagram을 사용하여 각 Header의 구성들을 직관적으로 확인하기 쉽기에 해당 설정이 유용할 것 같다.

<br>

## Related Posts
---
- [패킷의 구조](https://bangjeongbin.github.io/TIL-Blog/posts/til-structure-of-a-packet)
- [HTTP헤더를 Wireshark로 보는 법](https://bangjeongbin.github.io/TIL-Blog/posts/til-inspecting-http-header-with-wireshark)

<br>

## Reference
---
[^1]: 출처 : https://velog.io/@joosing/Wireshark-%ED%8C%A8%ED%82%B7-%ED%95%84%ED%84%B0-A-to-Z
