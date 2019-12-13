---
layout: single
title:  "09.ROS 웹캠 실행 해보기"
permalink: /categories/:categories/:title:output_ext
taxonomy: {title}
categories: ROS
tags: ROS 카메라 uvc_camera 웹캠
comments: true
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---


## 1. 카메라 확인

일단 삼성 USB camera를 USB 포트에 연결 하고, 아래의 명령어를 입력하면 다음과 같이 확인 할 수 있다.

<img src="/assets/img/ros/samsung_web_cam.png"  title="삼성 웹캠 화면"><br>


```
$ ls -ltr /dev/video*
```
<img src="/assets/img/ros/camera_device.png"  title="USB 카메라 장치"><br>


## 2. 패키지 설치

이제부터 활용할 ROS 패키지는 uvc_camera 라는 것이다.

<img src="/assets/img/ros/uvc_camera_wiki.png"  title="uvc_camera package"><br>
출처:[uvc_camera](http://wiki.ros.org/uvc_camera)


cs를 하여 catkin_ws/src로 이동하자.(환경설정에서 다루었던 내용)
```
$ cs
~/catkin_ws/src$ git clone https://github.com/ros-drivers/camera_umd
```
git으로 데이터 패키지를 다운받고 받은 폴더를 ls를 이용하여 확인해보자

```
~/catkin_ws/src$ ls
camera_umd      my_first_ros_pkg  turtlebot3_msgs
CMakeLists.txt  turtlebot3        turtlebot3_simulations
```
## 3. 패키지 빌드

이제 패키지를 빌드해보자.

```
~/catkin_ws/src$ cm
```
<img src="/assets/img/ros/ros_uvc_install_fail.png"  title="uvc_camera package 설치실패"><br>

*젠장 에러뜬다.*

의존성 문제로 해당 문제를 해결하기 위해서는 아래의 커멘드를 입력해야 한다.

```
rosdep install --from-paths src --ignore-src --rosdistro=kinetic -y
```

<img src="/assets/img/ros/ros_uvc_install_success.png"  title="uvc_camera package 설치성공"><br>


```
~/catkin_ws$ rospack profile
Full tree crawl took 0.045761 seconds.
Directories marked with (*) contain no manifest.  You may
want to delete these directories.
To get just of list of directories without manifests,
re-run the profile with --zombie-only
-------------------------------------------------------------
0.037673   /opt/ros/kinetic/share
0.005741   /home/memaker/catkin_ws/src
0.002084   /home/memaker/catkin_ws/src/turtlebot3
0.001374   /home/memaker/catkin_ws/src/camera_umd
0.000856   /home/memaker/catkin_ws/src/turtlebot3_simulations
0.000228 * /opt/ros/kinetic/share/OpenCV-3.3.1-dev
0.000049 * /opt/ros/kinetic/share/OpenCV-3.3.1-dev/haarcascades
0.000049 * /opt/ros/kinetic/share/doc
0.000021 * /opt/ros/kinetic/share/OpenCV-3.3.1-dev/lbpcascades
0.000009 * /opt/ros/kinetic/share/doc/liborocos-kdl
```

## 4. launch 파일 편집하기

launch 파일이 저장된 위치로 열심히 이동을 한다.
카메라 스펙에 맞게 몇가지 항목을 변경 할 필요가 있다.(**물론 그냥 실행해도 무관하다고 봄**)

```
~/catkin_ws$ cd ./src/camera_umd/uvc_camera/launch/
~/catkin_ws/src/camera_umd/uvc_camera/launch$ gedit ./camera_node.launch
```

카메라에 따라 해상도 지원하는 스펙이 다를 수 있다. 확인하고 설정하자.

```
<launch>
  <node pkg="uvc_camera" type="uvc_camera_node" name="uvc_camera" output="screen">
    <param name="width" type="int" value="640" />
    <param name="height" type="int" value="480" />
    <param name="fps" type="int" value="30" />
    <param name="frame" type="string" value="wide_stereo" />

    <param name="auto_focus" type="bool" value="False" />
    <param name="focus_absolute" type="int" value="0" />
    <!-- other supported params: auto_exposure, exposure_absolute, brightness, power_line_frequency -->

    <param name="device" type="string" value="/dev/video0" />
    <param name="camera_info_url" type="string" value="file://$(find uvc_camera)/example.yaml" />
  </node>
</launch>
```
편집하고 꼭 저장을 하자.

## 5. 실행

실행해보자.

```
~/catkin_ws/src/camera_umd/uvc_camera/launch$ cw
~/catkin_ws$ roslaunch uvc_camera camera_node.launch
```

## 6. rqt_image_view 실행

퍼블리셔 노드를 roslaucn로 실행했기 때문에 서브스크라이버로 rqt_image_view를 이용해서 확인해보자.

```
~/catkin_ws$ rqt_image_view
```

<img src="/assets/img/ros/rqt_image_view_uvc_camera.png"  title="uvc_camera 화면"><br>

색감조절이 필요할 듯하지만, 일단 화면이 나오는 것은 확인할 수 있다.



## 7. roscore와 rosrun 활용(더 좋은 화면 제공)

기존에 roslaunch를 활용하면 색감이 좀 나간 것 처럼 나오는 효과가 있어서, roscore를 활용해 보았다.


```
$ roscore
```
그리고, 퍼블리셔 노드를 실행해줘야 한다.

```
$ rosrun uvc_camera uvc_camera_node _device:=/dev/video0
```
이제 서브스크라이버 역할을 할 rqt_image_view 를 실행해보자


```
$ rqt_image_view
```
<img src="/assets/img/ros/rqt_image_uvc_camera2.png"  title="uvc_camera roscore rosrun 실행시"><br>


당연히 rosrun과 rosluanch 상관없이 몇 가지 옵션을 손 보면 더 좋은 화면과 이미지가 제공될 수 있을 것이다. 







