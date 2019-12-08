---
layout: single
title:  "02.ROS environmental settings for beginners ROS 환경설정 우분투 16.04 Kinetic Kame"
date:   2019-12-05 16:36:13 +0800
permalink: /categories/ROS/{title}
categories: ROS
tags: ROS installation
comments: true
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---

##### 1. ROS 환경설정

ROS 설치 과정에서 사용된 다음 명령어는 터미널 창을 실행할 때마다 계속 입력해야한다.

```
$ source /opt/ros/kinetic/setup.bash
$ source ~/catkin_ws/devel/setup.bash
```

이러한 번거로운 작업을 없애기 위해서 새로운 터미널 창을 열 때 마다 정해진 환경설정 파일을 읽어오도록 할 수 있다. 이외 ROS 네트워를 설정하고 자주 사용하는 명령어를 단축 명령어로 만들어 보자.

```
$ sudo gedit ~/.bashrc
```

or

```
$ sudo nano ~/.bashrc
```

잠깐!

내 IP주소를 잠깐 확인해보자.

ROS 네트워크 설정을 위해서 IP 주소가 필요할 수 있다. 

```
$ ifconfig
```

<img src="/assets/img/ros/ifconfig.png" width="40%" height="30%" alt="image">

wlp2s0(무선일 때)의  inet addr:xxx.xxx.xx.xx? 여기를 확인하자.<br>
enp3s0(유선일 때)의  inet addr:xxx.xxx.xx.xx? 여기를 확인하자.


> [참고]리눅스에서 자신의 IP를 확인하기 위해 ifconfig 명령어를 사용한다. 유선인 경우 enp3s0, 무선일 경우 wlp2s0의 inet addr에 자신의 IP 주소가 표시된다.

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

> (만약, 현재 터미널 창에 바로 반영을 하려면 아래와 같이 해보자)

```
$ source ~/.bashrc
```

##### 1.1. ROS 환경설정 내용 분석(bashrc)


{% highlight bash linenos %}
# Set ROS Kinetic
source /opt/ros/kinetic/setup.bash
source ~/catkin_ws/devel/setup.bash
{% endhighlight %}

위 두 코드는 환경설정을 불러오는 명령이다.


{% highlight bash linenos %}
# Set ROS Network
export ROS_HOSTNAME=192.168.0.44
export ROS_MASTER_URI=http://{ROS_HOSTNAME}:11311
{% endhighlight %}

ROS는 네트워크 통신 기반의 플랫폼이기 때문에 메세지 통신을 위해서 네트워크 설정은 반드시 선행되어야 합니다.


##### 1.2. 단축 명령어 분석(bashrc)

{% highlight bash linenos %}
# Set ROS alias command
alias cw='cd ~/catkin_ws'
alias cs='cd ~/catkin_ws/src'
alias cs='cd ~/catkin_ws && catkin_make'
{% endhighlight %}

alias는 별명 혹은 숏컷 네이밍이라고 볼 수 있습니다. 따라서, 해당 키워드를 사용하면 =''에 들어있는 명령이 실행되는 거죠.

> ROS 환경설정 확인 방법

```
$ export | grep ROS
```
<img src="/assets/img/ros/export_grep_ros.png" width="60%" height="60%" alt="image">


