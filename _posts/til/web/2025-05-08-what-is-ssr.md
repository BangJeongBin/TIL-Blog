---
title: SSR(Server Side Rendering)이란?
description: SSR(Server Side Rendering)과 CSR(Client Side Rendering)에 대하여
author: bin
date: 2025-05-08 09:00:00 +0800
categories: [TIL, Front-End]
tags: [Front-End, Architecture, Server]
pin: true
math: true
mermaid: true
image:
 path: https://bangjeongbin.github.io/TIL-Blog/assets/img/posts/common/http-main-image.png
 alt: Baekjoon Online Judge
---

`Next.js`를 비롯한 다양한 프레임워크에서 **SSR**을 쉽게 구축 할 수 있도록 도와주고 있다. 과연 **SSR**은 무엇이고 이 아키텍처를 사용하여 기대할 수 있는 효과는 무엇이 있는지 알아보자.

<br>
## SSR(Server Side Rendering)이란?
---
**SSR**이란 Server Side Rendering의 약자로 기존의 **CSR**(Client Side Rendering) 방식의 문제점을 보완하기 위해 나온 아키텍쳐이다.

직역하면 화면의 렌더링이 서버에서 이루어지는 아키텍처를 의미하는데 일반적으로 현대의 **SSR**은 <u>“첫 HTML 렌더링을 서버에서 처리하고, 이후의 렌더링 사이클은 클라이언트에서 처리”</u>하는 하이브리드 형태의 SSR을 말한다.

<br>

## SSR의 구동 방식
---
**SSR**은 “첫 HTML 렌더링을 서버에서 처리”하기 때문에, 사용자의 화면에 컨텐츠가 로드되는데 걸리는 시간(FCP, First Contentful Paint)가 더 짧다.

이전에 자주쓰던 방식인 **CSR**(Client Side Rendering) 아키텍처는 사용자의 화면에 `JavaScript` 번들이 모두 다운로드된 다음 첫 렌더링을 실행하면서 인증, 데이터 요청 등의 과정을 거치다보니 화면이 렌더링되는 시간이 상대적으로 긴 경우가 많다.

토스(toss)에서 작성한 아래 사진을 보고 **SSR** 방식을 도입 후 차이를 알아보자

![toss_ssr1](https://static.toss.im/ipd-tcs/toss_core/live/48fd1cb9-abd9-44e7-92ad-ca90a6bacd08/Untitled.png)

토스의 SSR 아키텍처 도입 전[^1]

<br>

![toss_ssr2](https://static.toss.im/ipd-tcs/toss_core/live/9655432a-c949-4337-b5b5-bb81e8e46e56/Untitled.png)

토스의 SSR 아키텍처 도입 후[^1]

<br>

위 사진과 같이 인증과 데이터 처리의 첫 과정이 서버에서 먼저 모두 이루어진 다음 사용자는 완성된 `HTML`을 받아보면 로딩 속도를 상당히 감축한 것을 볼 수 있다.

<br>

## SSR의 장점
---
#### 1. **빠른 초기 로딩 속도**

- 서버 측에서 이미 렌더링된 `HTML`을 보내기 때문에 사용자는 브라우저에서 `JavaScript`가 실행되기 전에도 즉시 콘텐츠를 볼 수 있다. 특히 네트워크 속도가 느리거나 저성능 기기에서도 체감 속도가 빠른 장점이 있다.

<br>

#### 2. **SEO(검색 엔진 최적화)에 유리**

- 사용자가 웹 사이트에 방문하는 순간 서버는 `HTML`, `CSS`, `JavaScript` 리소스를 브라우저에 전달하는데 **CSR**의 경우에는 빈 `HTML` 화면만 표시되어 검색 엔진 크롤러가 인식하지 못하게 된다. 하지만  SSR은 <u>서버에서 완성된 HTML을 반환</u>하므로, 검색 엔진 크롤러가 콘텐츠를 바로 읽을 수 있다.

<br>

#### 3. **보안 측면에서 유리**

- 데이터 렌더링을 서버에서 처리하기 때문에, 클라이언트로 민감한 로직이나 데이터가 그대로 노출될 위험이 줄어든다.

<br>

## SSR의 단점
---
#### 1. **서버 부하 증가**

- <u>모든 요청마다 서버가 렌더링을 수행</u>해야 하므로 서버에 굉장한 부하가 된다. 트래픽이 많을수록 서버 자원 사용량이 커지고 응답 속도가 느려지는 등의 위험이 있다.

- 서비스의 규모가 클수록 서버의 개수를 늘리거나 최적화를 하는 등 유연한 대처가 필요하다. 캐싱, CDN, 정적 페이지 미리 렌더링(SSG) 등을 함께 사용하는 하이브리드 전략을 사용하기도 한다.

<br>

#### 2. **개발 복잡도 증가**

- 서버와 클라이언트 양쪽에서 코드를 실행해야 하므로 <u>코드 구조가 복잡해진다.</u> 또한 상태 관리, API 호출 타이밍, hydration(서버 렌더링 후 클라이언트에서 재활성화) 등의 이슈도 발생한다.

<br>

#### 3. **서버 렌더링 시간 지연**

- 사용자가 페이지를 요청할 때마다 `HTML`을 생성해야 하므로, 초기 응답까지 시간이 더 걸릴 수 있다. 특히 데이터 **fetching** 과정이 길면 **TTFB(Time To First Byte)**가 느려진다.

<br>

## SSR과 CSR의 차이
---

| 구분         | SSR       | CSR         |
| ---------- | --------- | ----------- |
| 렌더링 위치     | 서버        | 클라이언트(브라우저) |
| 초기 로딩 속도   | 빠름        | 느림          |
| SEO        | 유리        | 불리          |
| 서버 부하 / 비용 | 큼         | 적음          |
| 개발 난이도     | 복잡        | 단순          |
| 데이터 최신화    | 요청 시마다 갱신 | 클라이언트에서 관리  |

<br>

![ssr_logic_image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdna%2FctbYqm%2FbtrE8OfqPyZ%2FAAAAAAAAAAAAAAAAAAAAABmU8v-ErsO23DB6f_INjs5J_8e6rEpPoaCqUtHkoUHB%2Fimg.png%3Fcredential%3DyqXZFxpELC7KVnFOS48ylbz2pIh7yKj8%26expires%3D1764514799%26allow_ip%3D%26allow_referer%3D%26signature%3DC%252BUAxfiJ9SO15OkecLCUeTuzI8k%253D)

SSR 로직[^2]

<br>

![csr_logic_image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdna%2FEk28V%2FbtrFde42IHr%2FAAAAAAAAAAAAAAAAAAAAADllkJpr5LkodXaR6-BQmJ8yq_QLazYC4xz-TP9pzwiM%2Fimg.png%3Fcredential%3DyqXZFxpELC7KVnFOS48ylbz2pIh7yKj8%26expires%3D1764514799%26allow_ip%3D%26allow_referer%3D%26signature%3DT9oHPaMdta%252BDX9wJro2ITqZkgRc%253D)

CSR 로직[^2]

<br>

## Reference
---
- [SSR 서버 최적화로 비용 아끼기](https://toss.tech/article/ssr-server)
- [SSR을 사용할 수 밖에 없는 이유 (Feat. CSR과의 차이)](https://www.elancer.co.kr/blog/detail/263)

<br>

[^1]: 출처 : https://toss.tech/article/ssr-server
[^2]: 출처 : https://hahahoho5915.tistory.com/52
