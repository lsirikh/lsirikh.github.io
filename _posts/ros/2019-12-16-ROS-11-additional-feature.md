---
layout: single
title:  "11.ROS 추가적 특징(라이브러리, 이기종 디바이스 통신)"
permalink: /categories/:categories/:title:output_ext
taxonomy: {title}
categories: ROS
tags: ROS 라이브러리 이기종디바이스통신
comments: true
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---


## 1. 클라이언트 라이브러리

ROS는 다양한 언어들을 활용하여 목적에 맞게 개발할 수 있도록 지원하고 있다. 

노드는 각각의 언어로 작성이 가능하고 노드 간의 메시지 통신을 통해 정보를 교환하는 방법을 이용하고 있다. 이처럼 각각의 언어로 작성 가능하게 해주는 소프트웨어 모듈이 클라이언트 라이브러리(client library)이다. 

* C++ - roscpp
* Python - rospy
* LISP - roslisp
* Java - rosjava
* etc


그 외에도 많은 언어에 대한 클라이언트 라이브러리를 지원하고 있다.


## 2. 이기종 디바이스 통신

ROS가 설치되어 사용하는 운영체제의 종류와도 상관없고, 사용하는 프로그래밍 언어도 상관없이 ROS가 설치되어 각 노드가 개발되어있다면 각 노드들 간의 통신은 매우 쉽게 이용 가능하다.

예를 들어 Linux 배포판 인 Ubuntu가 로봇에 설치되어 있어도 MacOS에서 로봇의 상태를 모니터링 할 수 있다. 동시에 사용자는 Android 기반 앱에서 로봇에게 명령을 내릴 수 있다.

<img src="/assets/img/ros/ros_cross_platform.png"  title="이기종 디바이스 통신"><br>

