---
layout: post
title:  "ROS environmental settings for beginners ROS 환경설정 우분투 16.04 Kinetic Kame"
date:   2019-12-05 16:36:13 +0800
categories: ROS
tags: ROS installation
---

ROS 설치 과정에서 사용된 다음 명령어는 터미널 창을 실행할 때마다 계속 입력해야한다.

```

source /opt/ros/kinetic/setup.bash
source ~/catkin_ws/devel/setup.bash
```

이러한 번거로운 작업을 없애기 위해서 새로운 터미널 창을 열 때 마다 정해진 환경설정 파일을 읽어오도록 할 수 있다. 이외 ROS 네트워를 설정하고 자주 사용하는 명령어를 단축 명령어로 만들어 보자.

```
sudo gedit ~/.bashrc
```

or

```
sudo nano ~/.bashrc
```

잠깐!

네 IP주소를 잠깐 확인해보자.

ROS 네트워크 설정을 위해서 IP 주소가 필요할 수 있다. 

```
ifconfig
```

wlp2s0의  inet addr:xxx.xxx.xx.xx? 여기를 확인하자.

다시 환경설정으로 돌아가서...

```
# Set ROS Kinetic
source /opt/ros/kinetic/setup.bash
source ~/catkin_ws/devel/setup.bash

# Set ROS Network
export ROS_HOSTNAME = xxx.xxx.xxx.xxx
export ROS_MASTER_URI = http://${ROS_HOSTNAME}:11311

# Set ROS alias command
alias cw='cd ~/catkin_ws'
alias cs='cd ~/catkin_ws/src'
alias cm='cd ~/catkin_ws && catkin_make'
```

이제 터미널창을 열면 자동으로 환경설정이 실행된다.