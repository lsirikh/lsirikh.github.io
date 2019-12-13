---
layout: single
title:  "06.ROS 메시지 통신의 흐름"
permalink: /categories/:categories/:title:output_ext
taxonomy: {title}
categories: ROS
tags: ROS 메시지통신 통신프로세스 메시지
comments: true
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---

## 1. 들어가며

메시지 통신의 흐름에 앞서 통신 방식을 간략하게 집고 넘어가면 아래 표와 같다.

<img src="/assets/img/ros/ros_communication3.jpeg" title="ROS 메시지통신">
출처:[ROS 하루에 입문하기](https://robertchoi.gitbook.io/ros/untitled-2)

<img src="/assets/img/ros/Selection_004.png" title="메시지통신 종류와 특징">
출처:[ROS_Robot_Programming_EN]

## 2. 토픽 메시지 통신의 흐름

마스터는 노드의 정보를 관리하고 각 노드는 필요에 따라 다른 노드를 연결하고 통신한다.

### (1) 마스터 실행

노드 간 메시지 통신에서 연결 정보를 관리하는 마스터는 ROS를 사용하기 위해 먼저 실행해야하는 필수 요소이다. ROS 마스터는 **roscore** 명령을 사용하여 실행되며 **XMLRPC**로 서버를 실행한다. 마스터는 노드 네임, 토픽, 서비스, 조치, 메시지 유형, URI 주소 및 노드 간 연결을위한 포트를 등록하고 요청시 다른 노드로 정보를 중계한다.

```
$ roscore
```

<img src="/assets/img/ros/ros_master.png" width="50%" height="50%" title="ROS Master(core) 실행"><br>
출처:[ROS_Robot_Programming_EN]


### (2) 서브스크라이버 노드 실행

서브스크라이버 노드는 **rosrun** 또는 **roslaunch** 명령으로 실행된다. 서브스크라이버 노드는 노드 이름, 토픽 이름, 메시지 유형, URI 주소 및 포트를 마스터가 실행되는 대로 등록한다. 마스터와 노드는 **XMLRPC**를 사용하여 통신을 하게된다.

```
$ rosrun PACKAGE_NAME NODE_NAME
$ roslaunch PACKAGE_NAME LAUNCH_NAME
```

<img src="/assets/img/ros/ros_subscriber_run.png" title="서브스크라이버 실행"><br>
출처:[ROS_Robot_Programming_EN]

### (3) 퍼블리셔 노드 실행

퍼블리셔 노드는 서브스크라이버 노드와 같은 방식(**rosrun** 또는 **roslaunch** 명령)으로 실행된다. 퍼블리셔 노드도 노드 이름, 토픽 이름, 메시지 유형, URI 주소 및 포트를 마스터가 실행되는 대로 등록한다. 마스터와 노드는 **XMLRPC**를 사용하여 통신을 하게된다.


<img src="/assets/img/ros/ros_publisher_run.png"  title="퍼블리셔 노드 실행"><br>
출처:[ROS_Robot_Programming_EN]


### (4) 퍼블리셔 정보 제공

마스터는 퍼블리셔의 이름, 토픽 이름, 메시지 유형, URI 주소 및 포트 번호와 같은 정보를 연결하려는 구독자에게 배포한다.

<img src="/assets/img/ros/ros_publisher_info.png" title="퍼블리셔 정보 제공"><br>
출처:[ROS_Robot_Programming_EN]


### (5) 서브스크라이버 노드의 연결 요청

서브스크라이버 노드는 마스터로부터 수신 된 퍼블리셔 정보에 바탕으로 퍼블리셔 노드에 직접 연결을 요청한다. 요청 절차 중에 서브스크라이버 노드는 노드 이름, 토픽 이름 및 메시지 유형과 같은 정보를 퍼블리셔 노드에 전송한다.

<img src="/assets/img/ros/ros_subscriber_connection.png"  title="서브스크라이버 노드의 연결 요청"><br>
출처:[ROS_Robot_Programming_EN]


### (6) 퍼블리셔 노드의 연결 응답

퍼블리셔 노드는 서브스크라이버 노드의 연결 요청에 대한 응답으로 TCP 서버의 URI 주소와 포트 번호를 보낸다.

<img src="/assets/img/ros/ros_publisher_response.png"  title="퍼블리셔 노드의 연결 응답"><br>
출처:[ROS_Robot_Programming_EN]


### (7) TCPROS Connection

서브스크라이버 노드는 TCPROS를 사용하여 퍼블리셔 노드에 대한 클라이언트를 생성하고 퍼블리셔 노드에 연결한다. 이 시점에서 노드 간 통신은 TCPROS라는 TCP/IP 기반 프로토콜을 사용한다.

<img src="/assets/img/ros/ros_tcpros_connection.png"  title="TCPROS 연결"><br>
출처:[ROS_Robot_Programming_EN]


### (8) 메시지 전송

퍼블리셔 노드는 미리 설정된 메시지를 서브스크라이버 노드로 송신하게 된다. 이 둘 사이의 연결은 TCPROS 연결 방식을 활용하게 된다.

<img src="/assets/img/ros/ros_message_trasmit.png"  title="TCPROS 메시지 전송"><br>
출처:[ROS_Robot_Programming_EN]

## 3. 서비스 메시지 통신의 흐름

서비스에는 두 노드를 중심으로 통신이 이루어 진다.

서비스 클라이언트 : 서비스 요청 및 응답 받기
서비스 서버 : 서비스를 받고 지정된 작업을 실행하고 응답을 반환

서비스 서버와 클라이언트 간의 연결은 위에서 설명한 퍼블리셔 및 서브스크라이버의 TCPROS 연결과 동일하다. 토픽(Topic)과 달리 요청(request) 및 응답(response)이 성공하면 서비스가 연결을 종료합니다. 추가 요청이 필요한 경우 연결 절차를 다시 수행한다.

<img src="/assets/img/ros/ros_service_ex.png"  title="서비스의 메시지 전송"><br>
출처:[ROS_Robot_Programming_EN]



## 4. 액션 메시지 통신의 흐름

액션은 피드백이라는 추가 메시지가 있는 서비스 요청 및 응답과 유사하게 보일 수 있다.
피드백 메시지는 요청(목표)과 응답(결과) 사이에 중간 결과를 제공하지만 실제로는 토픽과 비슷하다. 실제로 'rostopic'명령을 사용하여 주제를 나열하는 경우 액션에 사용되는 목표, 상태, 취소, 결과 및 피드백과 같은 5 가지 토픽이 있다. 액션 서버와 클라이언트 간의 연결은 퍼블리셔 및 서브스크라이버의 TCPROS 연결과 유사하지만 사용법이 약간 다르다. 예를 들어, 액션 클라이언트가 취소 명령을 보내거나 서버가 결과 값을 보내면 연결이 종료된다.

<img src="/assets/img/ros/ros_action_ex.png"  title="액션의 메시지 전송"><br>
출처:[ROS_Robot_Programming_EN]

> ROS 로봇 프로그래밍 책이 한국어판은 3만 2천원에 판매하는데, 영문 판은 무료로 다운로드 가능하다. 번역비용 치고 좀 비싸다는 생각이 들긴 하지만, 한 권정도 갖고 있으면 괜찮을 듯 싶다. 관련된 내용은 대체로 wiki.ros.org에서 확인할 수 있는 듯 하다.