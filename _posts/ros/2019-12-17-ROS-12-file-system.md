---
layout: single
title:  "12.ROS 파일 시스템"
permalink: /categories/:categories/:title:output_ext
taxonomy: {title}
categories: ROS
tags: ROS 파일시스템
comments: true
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---


## 1. 파일 구성

ROS에서 소프트웨어 구성을 위한 기본 단위는 패키지(package)로써 ROS의 응용프로그램은 패키지 단위로 개발된다.

각 패키지에는 이름, 작성자, 라이센스 및 종속 패키지를 포함하여 패키지에 대한 정보가 들어있는 XML 파일인 `package.xml`이 포함되어 있다. 또한, ROS 빌드 시스템 인 Catkin은  CMake를 이용하고 있어서 패키지 폴더의 `CMakeLists.txt`를 사용하여 빌드 환경을 설명한다. 그리고 패키지는 노드의 소스 코드와 노드 간의 메시지 통신을 위한 메시지 파일로 구성된다.

>ROS 패키지를 설치하는 방법에는 두 가지가 있다. 첫 번째는 빌드 프로세스없이 즉시 실행할 수 있는 바이너리 형식으로 제공된 패키지를 설치하는 것이다. 두 번째는 사용자가 패키지의 소스 코드를 다운로드하여 설치하기 전에 빌드하는 것이다. 패키지를 수정하거나 소스 코드의 내용을 확인하려면 두 번째 설치 방법을 사용할 수 있다. 

다음은 TurtleBot3 패키지의 예이며 두 가지 설치 방법의 차이점을 설명한다.

* 바이너리 설치 방법
```
$ sudo apt-get install ros-kinetic-turtlebot3
```

* 소스코드 설치 방법
```
$ cd ~/catkin_ws/src
$ git clone https://github.com/ROBOTIS-GIT/turtlebot3.git
$ git clone https://github.com/ROBOTIS-GIT/turtlebot3_msgs.git
$ cd ~/catkin_ws/
$ catkin_make
```

## 2. 설치 폴더

ROS는 다음과 같은 폴더에 설치를 하게 된다.

`opt/ros/[버전이름]`

> kinetic kame 버전은 ‘/opt/ros/kinetic’

* 디렉토리 및 파일 구성

<img src="/assets/img/ros/ros_install_folder_configuration.png"  title="ROS 디렉토리 및 파일 구성 "><br>

* 디렉토리 특징

1. /bin        - 실행 가능한 바이너리 파일
2. /etc        - ROS 및 catkin 관련 설정 파일
3. /include    - 헤더 파일
4. /lib        - 라이브러리 파일
5. /share      - ROS 패키지
6. env.*       - 환경설정 파일
7. setup.*     - 환경설정 파일

## 3. 작업 폴더

대부분의 프로그램이나 프레임워크에서 그렇듯이 작업폴더는 사용자가 원하는 곳에 생성이 가능하다. 하지만, `~/catkin_ws/`를 작업폴더로 지정하고 ROS를 작성하도록 한다.

> 작업폴더 경로 : `home/memaker/catkin_ws/`

* 디렉토리 및 파일 구성

<img src="/assets/img/ros/ros_workspace_folder_configuration.png"  title="ROS workspace 디렉토리 및 파일 구성 "><br>

* 디렉토리 특징

작업 폴더는 사용자가 작성한 패키지와 공개된 다른 개발자의 패키지를 저장하고 빌드하는 공간을 활용된다.

1. /build   - 빌드 관련 파일 
2. /devel   - msg, srv 헤더파일 과 사용자 패키지 라이브러리, 실행 파일
3. /src     - 사용자 패키지

## 4. 사용자 패키지

`~/catkin_ws/src`폴더는 사용자 소스 코드를위한 공간이다. 이 폴더에서 다른 개발자가 개발한 자체 ROS 패키지 또는 패키지를 저장하고 빌드할 수 있다.

* 디렉토리 및 파일 구성

<img src="/assets/img/ros/ros_user_package_folder_configuration.png"  title="ROS 사용자 패키지 디렉토리 및 파일 구성 "><br>

* 디렉토리 특징

1. /include         - 헤더파일
2. /launch          - roslaunch에 사용되는 launch 파일
3. /node            - rospy용 스크립터
4. /msg             - 메시지 파일
5. /src             - 소스코드 파일
6. /srv             - 서비스 파일
7. CMakeLists.txt   - 빌드 설정 파일
8. Package.xml      - 패키지 설정 파일


출처:[ROS_Robot_Programming_EN]
