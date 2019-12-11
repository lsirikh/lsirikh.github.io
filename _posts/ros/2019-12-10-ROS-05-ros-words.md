---
layout: single
title:  "05.ROS 용어 정리 및 개념"
permalink: /categories/:categories/:title:output_ext
taxonomy: {title}
categories: ROS
tags: ROS words concept
comments: true
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---

## 1. ROS 란?

ROS는 로봇의 응용프로그램을 개발하기 위한 운영체제와 같은 로봇 소프트웨어 플랫폼이다. ROS는 로봇 응용프로그램을 개발할 때 필요한 하드웨어 추상화, 디바이스 제어, 센싱 및 인식, SLAM 등 다양한 기능을 라이브러리 형태로 제공하고 있으며, 디버깅 도구 및 시뮬레이션 도구를 제공하는 메타 OS이다.

<img src="/assets/img/ros/ros_communication.png" title="ROS 개념">
출처:[ROS 하루에 입문하기](https://robertchoi.gitbook.io/ros/untitled-2)

> 메타 OS는 사실 실제로 존재하는 말이기 보다는 ROS를 설명하기 위해서 등장한 용어라고 보여진다. Linux, Windos, OS X와 같은 다른 운영체제간 통신을 기반으로 이기종 디바이스 컨트롤이 가능하게 만든 것이 ROS이기 때문이다. 

## 2. 마스터

마스터(master)란 노드와 노드사이를 연결하여 메시지 통신이 가능하게 하는 일종의 커멘드 센터이다. 흔히 네임 서버로 비교하여 설명을 한다. 

```
roscore
```

위 명령어를 실행하여 마스터를 실행하고, 각각의 패키지 노드들을 연결하여 ROS프로그램이 동작하게 된다.
또한, 마스터는 마스터에 접속한 슬레이브들과의 접속상태를 지속적으로 유지하는 것이 아니라 HTTP기반의 프로토콜인 XMLRPC(XML-Remote Procedure Call)를 이용하여 슬레이브들과 통신한다.

로봇은 매우 복잡한 센서와 모듈들이 통합되어 있어서, 통신을 지속적으로 연결하고 있으면 리소스의 낭비가 심각해질 수 있지만, 이러한 통신 방식은 자원을 효율적으로 활용할 수 있도록 돕니다. 게다가 XMLRPC는 매우 가볍고, 다양한 프로그래밍 언어를 지원하기 때문에 여러 종류의 하드웨어와 언어를 지원해야 하는 ROS에 매우 적합하다고 볼 수 있다.

설정시 유의해야 할 점은 ROS를 구동하면서 마스터는 사용자가 정해 놓은 ROS_MASTER_URI 변수에 기재된 URI 주소와 포트를 가진다.

## 3. 노드

노드(node)는 ROS에서 실행되는 최소 단위의 프로세서를 지칭한다. 즉, 최소 단위의 실행 가능한 프로그램으로 반드시 roscore가 등록된 이후에 실행을 시켜야 한다.
모든 프로그램에서 권장하는 방법이겠지만, 프로그램을 모듈단위로 잘 구성하여 재사용성을 높이도록 하는 것이 좋은 노드를 구성하는 방법이 될 것이다. 예를 들면, 로봇을 구동하기 위해서 필요한 모터와 엔코더 등을 각각 세분화하여 노드로 구성하는 것을 권장한다.

노드에는 다양한 정보가 들어간다.
* 노드 명칭
* 퍼블리셔(Publisher), 서브스크라이버(Subscriber), 서비스 서버(Service server), 서비스 클라이언트(Service Client) 구분
* 사용되는 토픽 및 서비스 이름
* 메시지 형태
* URI 주소
* 포트 번호 등

노드는 마스터와 통신할 때 XMLRPC를 활용하고, 노드간에도 XMLRPC 혹은 TCP/IP 통신 방식을 활용한 TCPROS를 이용한다.

## 4. 패키지

패키지(Package)는 ROS를 구성하는 기본 단위가 된다. 
ROS의 응용프로그램은 패키지 단위로 개발되며 패키지는 최소한 하나 이상의 노드를 포함하거나 다른 패키지의 노드를 싱행하기 위한 설정파일 및 의존성 라이브러리, 데이터 셋 등이 있을 수 있다.

## 5. 메타패키지

메타패키지(metapackage)는 공통된 목적을 가진 패키지 집합이다. 대단위 기능을 수행하는 프로그램의 경우 단일 패키지로 불가능하고 복수 개의 패키지를 연동 실행하여 수행 할 수 있다.

## 6. 메시지

노드는 메시지(message)를 통해 노드 간의 데이터를 주고 받을 수 있다. 메시지의 종류는 integer, floating point, boolean과 같은 변수 형태에서 메시지를 품은 메시지이거나 배열도 메시지로 송수신이 가능하다.

메시지의 통신 방식은 TCPROS, UDPROS 등의 방식이 있다.

단방향 메시지 송수신 방식을 토픽(Topic)이라고 한다.
양방향 메시지 송수신 방식을 서비스(Service)라고 한다.

## 7. 토픽

토픽(topic)은 로봇 혹은 로봇 연관 시스템에서 작업을 수행하기 위한 작업 내용(ROS프로그래밍 책에서는 '이야깃거리'라 칭함)을 말한다고 보면 된다. 퍼블리셔(Publisher) 노드가 하나의 작업 내용에 대해 마스터에 등록한 후, 이 작업 내용에 대한 메시지를 퍼블리시(출판 혹은 발송)하게 된다. 

<img src="/assets/img/ros/ros_topic.jpeg" title="토픽 개념">
출처:[ROS 하루에 입문하기](https://robertchoi.gitbook.io/ros/untitled-2)

> 용어나 말이 굉장히 낯설게 느껴질 수 있다. ROS를 설계자가 나름 통신 프로토콜(일종의 통신 약속)을 규정하기 위해서 들고 나온 개념이라고 보면 된다. 이러한 용어는 자주 보고 쓰다보면 익숙해질 수 있을 것이라고 생각한다.

이 작업 내용을 구독해주시는 열혈 독자가 있는데, 이를 서브스크라이버(subscriber)라고 한다. 각각 노드별로 역할이 있고,명칭이 있다고 보면된다.


## 8. 퍼블리시 및 퍼블리셔

퍼블리시(publish)는 작업 내용에 해당하는 토픽의 메시지 형태의 데이터를 발송(송신)하는 것을 말한다. 퍼블리셔(publisher)는 이러한 퍼블리시(publish)라는 행위를 하는 노드를 말한다. 

> 골키퍼가 공을 잡고, 다른 선수들은 공을 발로 찬다. 이렇게 하면 말이 되지만, 공격수가 공을 잡는다 하면 말도 안되는 행위가 될 것이다. 머 이렇게 일단 이해해보자. 사실 어려운 내용도 아니니 말이다.

퍼블리셔는 자신의 노드 정보와 토픽으로 보낼 정보 등을 마스터 ROSCORE에 등록한다. 그리고 subscriber를 할 노드에게 메시지를 보낸다.

<img src="/assets/img/ros/ros_publisher.png" title="퍼블리셔 개념">
<br>
출처:[김빠진사이다](https://m.blog.naver.com/PostView.nhn?blogId=0323lena&logNo=220357703221&proxyReferer=https%3A%2F%2Fwww.google.com%2F)

## 9. 서브스크라이브 및 서브스크라이버

> 야구에 투수가 있으면, 당연히 포수가 있고, 타자도 있다. 그렇지만, 토픽(TOPIC)의 개념에서 보면 투수와 포수만 있다고 볼 수 있다. 야구공은 메시지라고 볼 수 있을 것 같다.

<img src="/assets/img/ros/ros_subscriber.png" title="서브스크라이버 개념">
<br>
출처:[sk와이번스](https://wyvernsstory.tistory.com/entry/%EA%B3%B5%EA%B0%90%E5%85%B1%E6%84%9F-W-%EC%95%BC%EA%B5%AC%EC%9E%A5%EC%97%90%EC%84%9C-%EA%B7%B8%EB%A6%AC%EB%8A%94-%EB%82%98%EC%9D%98-%EB%AF%B8%EB%9E%98-SK-%ED%8F%AC%EC%88%98-%EC%9D%B4%EC%9C%A4%EC%9E%AC)

서브스크라이버는 퍼블려서와 같은 프로세스를 따른다. 먼저 마스터에 자신의 정보를 등록하고, 서브스크라이브를 수행하기 위한 토픽을 포함한 자신의 정보들을 등록하고, 해당 토픽을 퍼블리시하는 퍼블리셔 노드의 정보를 마스터로 부터 받게 된다.

> 야구를 예로 들어서 설명을 하지만, 다수의 퍼블리셔가 있을 수 있고, 다수의 서브스크라이버가 있을 수 있다.

토픽 개념의 통신방식(퍼블리시와 서브스크라이브)은 비동기 방식이라서 전송이 필요할 때만, 데이터를 보낼 수 있기 때문에 매우 효율적인 방식이다.

> 보통 센서로부터 데이터를 받을 때, 패시브한 방식으로 데이터를 받기만 한다. 물론 일부 I2C 통신으로 COMMAND를 날리는 센서도 있긴 하지만, 대부분의 패시브 센서 (온도, 습도, 조도 등)는 데이터를 보내는 핀(Tx)만 활용하기 때문에 이러한 센서는 토픽 방식을 쓰면 매우 효율적이다. 

## 10. 서비스(service)

서비스(service)는 작업 내용(특수 목적 포함)에 대해 서비스 클라이언트(service client)와 서비스 서버(service server)간의 양방향 동기적 통신을 말한다. 클라이언트는 요청하고, 서버는 응답하게된다.

> 흔히 대화를 주고 받는 만담(conversation)과는 좀 다르다고 볼 수 있는데, 작업 내용에 대한 메시지를 보내고 그 결과를 주는 형식이라고 보면 된다.

<img src="/assets/img/ros/ros_service.jpeg" title="서비스 개념">
출처:[ROS 하루에 입문하기](https://robertchoi.gitbook.io/ros/untitled-2)

## 11. 서비스 서버(service server)

서비스 서버(service server)는 서비스 클라이언트(service client)로 부터 작업 내용의 요청(메시지;request)를 받고, 작업을 한 후에 작업 내용의 완료결과(메시지)를 응답(메시지;response)하게 된다. 따라서, 서비스 서버가 응답 주체(노드)가 된다.

## 12. 서비스 클라이언트(service client)

서비스 클라이언트(service client)는 작업 내용의 요청(메시지;request)을 서비스 서버(service server)로 보내고 그 결과 응답(메시지;response)를 받는 요청 주체(노드)가 된다.


## 13. 액션(action)

액션(action)은 서비스처럼 양방향을 통신방식이지만, 중간 중간에 작업 상황을 피드백을 해주는 처리가 들어간 통신 방식이라고 할 수 있다.

> 파일을 옮기기 하면, 파일이 이동하는 Progress bar가 보인다. 이러한 기능도 액션의 개념과 유사하다고 볼 수 있다.

액션도 서비스와 비슷한 면이 있지만, 요청과 응답을 달리 표현한다.

* 목표(goal)
* 결과(result)

액션의 목표를 정하는 액션 클라이언트(action client)와 목표에 따라 임무를 수행하고, 임무가 끝나기 전까지 계속 피드백을 보내는 액션 서버(action server)가 서로 비동기 양방향 통신을 하게 된다.


## 14. 액션 서버(action server)

액션 서버(action server)는 앞서 설명한 바와 같이 액션 클라이언트로 부터 목표를 전달 받고, 해당 목표를 수행하는 노드(주체)가 된다. 또한, 목표(임무)를 완료하기 전까지 중간 중간 액션 클라이언트로 부터 받은 목표에 맞게 피드백을 보내주게 된다. 

## 15. 액션 클라이언트(action client)

액션 클라이언트(action client)는 목표를 출력하고, 액션 서버에서 보내는 결과와 피드백을 입력받는 노드이다. 액션 클라이언트가 목표를 액션 서버에 보내고 피드백을 받다가 취소명령을 보낼 수 있고, 완료 메시지를 액션 서버로부터 받으면 다음 명령을 보낼 수도 있다. 

## 16. 파라미터

ROS에서 parameter(매개변수)는 보통 노드에서 활용되는 파라미터를 말하게 된다. 예를 들면, 윈도우에서 활용되는 ***.ini**파일이라고 볼 수도 있을 것 같다.
보통은 디폴트(default) 값을 활용하게 되는 데, 상황에 따라 외부에서 설정 값을 밀어 넣을 수 있기 때문에 실시간 변경이 매우 용이하고 유용한 기능이다. 

>외부 장치와 연결되는 USB포트, 카메라 캘리브레이션 값, 모터 속도 등등

## 17. 파라미터 서버

파라미터 서버(parameter server)는 패키지에서 파라미터를 사용할 때, 이 곳에 등록하여 활용한다. 이는 마스터의 기능 중 하나이기도 하다.

## 18. Catkin

캐킨(Catkin)은 ROS의 빌드 시스템이다. ROS의 빌드 시스템은 기본적으로 CMake(Cross Platform Make)를 이용하고 있어서 패키지 폴더에 CMakeLists.txt라는 파일에 빌드를 하기 위한 다양한 설정 내용들을 작성해야 한다. ROS에서 CMake를 ROS에 맞게 변경하여 ROS만의 특ㄹ화된 Catkin Build System을 구축하였다.
캐킨 빌드 스스템은 ROS와 관련된 빌드, 패키지 관리, 패키지 간의 의존관계 등을 편리하게 사용할 수 있게 한다.








<img src="/assets/img/ros/ros_communication2.jpeg" title="ROS 통신 개념">
출처:[ROS 하루에 입문하기](https://robertchoi.gitbook.io/ros/untitled-2)




<img src="/assets/img/ros/ros_communication3.jpeg" title="ROS 통신 개념">
출처:[ROS 하루에 입문하기](https://robertchoi.gitbook.io/ros/untitled-2)





<img src="/assets/img/ros/ros_TF.jpeg" title="TF 개념">
출처:[ROS 하루에 입문하기](https://robertchoi.gitbook.io/ros/untitled-2)


