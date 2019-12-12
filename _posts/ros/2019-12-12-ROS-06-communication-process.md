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

## 2. 메시지 통신의 흐름

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

퍼블리셔 노드는 서브스크라이버 노드의 연결 요청에 대한 응답으로 TCP 서버의 URI 주소와 포트 번호를 보냅니다.

<img src="/assets/img/ros/ros_publisher_response.png"  title="퍼블리셔 노드의 연결 응답"><br>
출처:[ROS_Robot_Programming_EN]


