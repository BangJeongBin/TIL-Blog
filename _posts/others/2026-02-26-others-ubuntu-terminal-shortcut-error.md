---
title: Ubuntu 터미널 단축키 장애 해결
description: Mac 환경에서 VM으로 Ubuntu Desktop 사용시 터미털 단축키 안되는 현상 해결
author: bin
date: 2026-02-26 09:00:00 +0800
categories: [Others]
tags: [Mac, Ubuntu, Ubuntu Desktop, Terminal]
pin: false
math: true
mermaid: true
---

> **한줄 요약**    
> "Mac 환경에서 VMware Fusion으로 띄운 Ubuntu Desktop에서 `Ctrl + Alt + T`(터미널 열기) 단축키가 동작 안함. Ubuntu의 Profile 설정으로 간단하게 해결.
{: .prompt-info }

<br>

|     항목      | 내용                                           |
| :---------: | -------------------------------------------- |
|   [Host] OS   | Mac M1 Pro - Golden Gate 27.2.1 |
|   [Guest] OS   | Ubuntu 26.04.1 LTS - ARM 64-bit architecture |
| 사용 도구 / 서비스 | VMware Fusion - V13.6.4                      |

<br>
<br>
<br>

## 𝙸. 문제 상황 (Problem)
---
- Ubuntu Desktop 에서 `Ctrl + Alt + T` 단축키를 입력하여 터미널을 실행하려 했으나 실행이 안되고 Window 크기만 변경됨

<br>

![image-1](https://lh3.googleusercontent.com/d/1x_V0WiUYgIB_X96LTSVILri_sTBbD6C7)
_[그림 1-1]_
{: .text-center }

<br>
<br>
<br>

## 𝙸𝙸. 해결 과정 (Solution)
---
- VMware Fusion의 Keyboard & Mouse 설정이 잘못 설정되어 있어 Mac Profile로 변경

<br>

\1. 화면 우측 상단에 스패너 아이콘을 눌러 `설정` 메뉴로 진입

![image-2](https://lh3.googleusercontent.com/d/1Oaqd-LJvp-wXuniL48xnYI1FsULjCTsm)
_[그림 2-1]_
{: .text-center }

<br>

\2. 시스템 설정에서 `Keyboard & Mouse` 설정 진입

![image-3](https://lh3.googleusercontent.com/d/18715ItT3EOI2B1Hg1IBodQrlgFxT0YhO)
_[그림 2-2]_
{: .text-center }


\3. 나같은 경우는 `Profile - Default`로 설정되어 있었는데 `Mac Profile`로 변경

![image-4](https://lh3.googleusercontent.com/d/1pM0jhtRfR0ZFzm1IIECOWq1we5bOGUAV)
_[그림 2-3]_
{: .text-center }

<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>

## Reference
---
