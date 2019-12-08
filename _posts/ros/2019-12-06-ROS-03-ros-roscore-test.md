---
layout: post
title:  "03.ROS를 테스트 터틀봇 움직이기(우분투 16.04 Kinetic Kame)"
date:   2019-12-06 20:50:13 +0800
categories: ROS
tags: ROS turtlesim test
---

##### 1. ROS 동작 테스트 해보기

일단 ROS를 설치 했기 때문에 뭐라도 구동하여 ROS가 작동하는 원리를 보고 싶은 마음이 들 것이다. 나도 처음에 설치 했을 때, 로봇에 한 발자국 더 다가간 것 같았다.

일단 거북이라도 돌아다니는 걸 보고 싶다면 함께 해보는 것도 좋을 것 같다.

##### 2. roscore 실행하기

```
$ roscore
```
<img src="/assets/img/ros/roscore_execution.png" width="60%" height="60%" alt="image">

ROS는 기본적으로 CORE를 기반으로 작동하는 시스템이다. 따라서, Supervisor인 Core가 없으면 동작하지 않는다.

##### 2. turtlesim 패키지의 turtlesim_node 실행하기

```
$ rosrun turtlesim turtlesim_node
```
ROS의 노드는 실행하기 위하여 rosrun이라는 커맨드를 활용한다.

통신을 하기 위한 한 명의 노드 클라이언트를 등록했다. turtlesim_node는 turtlesim 패키지에 포함된 visual 기능을 갖고 있는 노드이다. 

따라서, 화면에 보이는 거북이를 움직이기 위해서는 명령 신호를 보내주는 노드를 또 등록해야 한다.

<img src="/assets/img/ros/turtlesim_node.png" width="60%" height="60%" alt="image">

<img src="/assets/img/ros/turtlesim_image.png"  alt="image">


##### 3. turtlesim_node를 콘트롤하기 위한 turtle_teleop_key 노드 실행하기

```
$ rosrun turtlesim turtle_teleop_key
```

<img src="/assets/img/ros/turtle_teleop_key.png" width="60%" height="60%" alt="image">

이제 키보드의 방향키를 움직여 보자.

회전방향을 정하는 좌우 방향키와 병진속도(병신 아님)를 결정하는 앞뒤 방향키로 거북이를 컨트롤 할 수 있게 된다.

<img src="/assets/img/ros/controlled_turtle.png"  alt="image">



##### 4. rqt_graph

현재 ROS 시스템에 맞물려 있는 노드들의 관계와 메세지의 종류 등을 한눈에 이미지로 확인하는 좋은 툴은 ROS에서 제공을 해주고 있다.

처음 ROS를 접하면 다소 투박해 보이는 이미지 일 수 있으나, 추후 많은 노드들 간의 관계를 파악하는데 많이 활용하게 된다.

```
$ rqt_graph
```
<img src="/assets/img/ros/rqt_graph.png"  alt="image">

이제 ROS의 시스템을 대충 이해할 수 있는 상태가 됐을 것 같다. 물론 거북이 움직였다고 ROS를 이해할 수 없겠지만, 뭔가 창이 많이 뜨고, 서로 신호를 보내고 받는 노드들 사이에 프로그래밍이겠구나 라는 이해를 말하는 것이다.