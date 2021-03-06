---
layout: single
title:  "04.ROS를 GUI 기반 IDE 툴 qt creator 설치(우분투 16.04 Kinetic Kame)"
date:   2019-12-06 22:12:13 
permalink: /categories/:categories/:title:output_ext
taxonomy: {title}
categories: ROS
tags: ROS qt creator
comments: true
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---

## 1. Qt Creator란?

Qt Creator는 Qt GUI 애플리케이션 개발 프레임 워크 용 SDK의 일부인 크로스 플랫폼 C ++, JavaScript 및 QML 통합 개발 환경입니다. 시각적 디버거와 통합 GUI 레이아웃 및 양식 디자이너가 포함되어 있습니다.

<img src="/assets/img/ros/QtProject-creator-icon.png" title="QT logo">


Qt는 컴퓨터 프로그래밍에서 GUI 프로그램 개발에 널리 쓰이는 크로스 플랫폼 프레임워크이다. 서버용 콘솔과 명령 줄 도구와 같은 비GUI 프로그램 개발에도 사용된다. 그래픽 사용자 인터페이스를 사용하는 경우에는 Qt를 위젯 툴킷으로 분류한다. 회사 내부에서는 Qt를 "cute"로 발음하고 있으며 비공식적으로는 "큐티"로 발음한다. Qt는 KDE, Qtopia, OPIE에 이용되고 있다,

노르웨이 회사 트롤텍에 의해서 개발되었다. 2008년 1월에는 노키아에 인수되었다.[2] 이후, 2012년 8월에 핀란드 회사 Digia에 인수되었다.[3]

Qt는 C++를 주로 사용하지만, 파이썬, 루비, C, 펄, 파스칼과도 연동된다. 수많은 플랫폼에서 동작하며, 상당히 좋은 국제화를 지원한다. SQL 데이터베이스 접근, XML 처리, 스레드 관리, 단일 크로스 플랫폼 파일 관리 API를 제공한다.

[출처] [위키백과](https://ko.wikipedia.org/wiki/Qt_(%ED%94%84%EB%A0%88%EC%9E%84%EC%9B%8C%ED%81%AC))

## 2. Qt Creator 설치하기

```
$ sudo apt-get install qtcreator
```
리눅스가 좋은 점은 바로 이런 apt-get install이란 간편한 방법으로 설치가 가능하다는 점이다.

일단 설치하고 실행하면 다음과 같이 나오는 것을 확인 할 수 있다.

<img src="/assets/img/ros/qtcreator_ide.png" title="Qt 크리에이터 실행화면">
