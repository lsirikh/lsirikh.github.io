---
layout: single
title:  "13.ROS 빌드 시스템"
permalink: /categories/:categories/:title:output_ext
taxonomy: {title}
categories: ROS
tags: ROS 빌드시스템
comments: true
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---


## 1. 들어가며

ROS 빌드 시스템은 기본적으로 CMake(Cross Platform Make)를 사용하며, 빌드 환경은 패키지 폴더의 `CMakeLists.txt`파일에 설명되어 있다.

ROS에서 CMake를 사용하는 이유는 여러 플랫폼에서 ROS 패키지를 빌드 할 수 있기 때문이다.

## 2. 패키지 만들기

다음과 같은 명령어를 통해 패키지를 생성할 수 있다.

```
$ catkin_create_pkg [PACKAGE_NAME] [DEPENDENT_PACKAGE_1] [DEPENDENT_PACKAGE_N]
```

`catkin_create_pkg`명령은 Cake빌드 시스템에 필요한 `CMakeLists.txt`및 `package.xml`파일이 포함 된 패키지 폴더를 만든다.

다음과 같이 입력하고, 실행하면, 패키지를 생성할 수 있다.

```
$ cs
~/catkin_ws/src$ 
~/catkin_ws/src$ catkin_create_pkg my_first_ros_pkg std_msgs roscpp
```

>만들 패키지 이름은‘my_first_ros_pkg’이다. ROS의 패키지 이름은 모두 소문자 여야하며 공백을 포함해서는 안된다. 이름 지정 지침에서는 대시(-) 또는 공백 대신 각 단어 사이에 **밑줄(_)**을 사용한다. 

`std_msgs` 및 `roscpp`는 이전에 선택적 종속 패키지로 추가되었다.
명령. 즉, ROS의 표준 메시지 패키지 인 `std_msgs`와 ROS에서 C/C++를 사용하는 데 필요한 클라이언트 라이브러리 인 `roscpp`가 패키지를 작성하기 전에 설치되어 있어야한다.

```
~/catkin_ws/src$ cd my_first_ros_pkg
~/catkin_ws/src$ ls
include 			 → Include Folder
src 				 → Source Code Folder
CMakeLists.txt 		 → Build Configuration File
package.xml 		 → Package Configuration File
```

<img src="/assets/img/ros/ros_my_first_package.png"  title="ROS 패키지 생성 "><br>


## 3. 패키지 내용 살펴보기

ROS의 필수 설정 파일 중 하나인 `package.xml`은 패키지의 정보를 담는 XML 파일로 패키지의 이름, 저작자, 라이센스, 의존성 패키지 등을 기술하고 있다.

다음은 생성된 `package.xml`파일을 그대로 가져온 내용이다.

{% highlight xml linenos %}
<?xml version="1.0"?>
<package format="2">
  <name>my_first_ros_pkg</name>
  <version>0.0.0</version>
  <description>The my_first_ros_pkg package</description>

  <!-- One maintainer tag required, multiple allowed, one person per tag -->
  <!-- Example:  -->
  <!-- <maintainer email="jane.doe@example.com">Jane Doe</maintainer> -->
  <maintainer email="memaker@todo.todo">memaker</maintainer>


  <!-- One license tag required, multiple allowed, one license per tag -->
  <!-- Commonly used license strings: -->
  <!--   BSD, MIT, Boost Software License, GPLv2, GPLv3, LGPLv2.1, LGPLv3 -->
  <license>TODO</license>


  <!-- Url tags are optional, but multiple are allowed, one per tag -->
  <!-- Optional attribute type can be: website, bugtracker, or repository -->
  <!-- Example: -->
  <!-- <url type="website">http://wiki.ros.org/my_first_ros_pkg</url> -->


  <!-- Author tags are optional, multiple are allowed, one per tag -->
  <!-- Authors do not have to be maintainers, but could be -->
  <!-- Example: -->
  <!-- <author email="jane.doe@example.com">Jane Doe</author> -->


  <!-- The *depend tags are used to specify dependencies -->
  <!-- Dependencies can be catkin packages or system dependencies -->
  <!-- Examples: -->
  <!-- Use depend as a shortcut for packages that are both build and exec dependencies -->
  <!--   <depend>roscpp</depend> -->
  <!--   Note that this is equivalent to the following: -->
  <!--   <build_depend>roscpp</build_depend> -->
  <!--   <exec_depend>roscpp</exec_depend> -->
  <!-- Use build_depend for packages you need at compile time: -->
  <!--   <build_depend>message_generation</build_depend> -->
  <!-- Use build_export_depend for packages you need in order to build against this package: -->
  <!--   <build_export_depend>message_generation</build_export_depend> -->
  <!-- Use buildtool_depend for build tool packages: -->
  <!--   <buildtool_depend>catkin</buildtool_depend> -->
  <!-- Use exec_depend for packages you need at runtime: -->
  <!--   <exec_depend>message_runtime</exec_depend> -->
  <!-- Use test_depend for packages you need only for testing: -->
  <!--   <test_depend>gtest</test_depend> -->
  <!-- Use doc_depend for packages you need only for building documentation: -->
  <!--   <doc_depend>doxygen</doc_depend> -->
  <buildtool_depend>catkin</buildtool_depend>
  <build_depend>roscpp</build_depend>
  <build_depend>std_msgs</build_depend>
  <build_export_depend>roscpp</build_export_depend>
  <build_export_depend>std_msgs</build_export_depend>
  <exec_depend>roscpp</exec_depend>
  <exec_depend>std_msgs</exec_depend>


  <!-- The export tag contains other, unspecified, tags -->
  <export>
    <!-- Other tools can request additional information be placed here -->

  </export>
</package>
{% endhighlight %}

* `<?xml>`                - 문서 문법을 정의하는 문구로 아래의 내용은 xml 버전 1.0을 따르고 있다는 것을 표시한다.
* `<package>`             - 이 구문부터 맨 끝의 \</package> 까지가 ROS 패키지 설정 부분이다.
* `<name>`                - 패키지의 이름이다. 패키지를 생성할 때 입력한 패키지의 이름이 사용된다. 다른 옵션도 마찬가지지만 이는 사용자가 원할 때 언제든지 바꿀 수 있다.
* `<version>`             - 패키지의 버전이다. 역시 자유롭게 변경 가능하다.
* `<description>`         - 패키지의 간단한 설명을 기술 할 수 있다. 보통 2~3 무장으로 기술하고 있다.
* `<maintainer>`          - 패키지의 관리자의 이름과 메일 주소를 작성한다.
* `<license>`             - 라이선스를 작성한다. BSD, MIT, Apache, GPLv3, LGPLv3 등을 기재하면 된다.
* `<url>`                 - 패키지를 설명하는 웹 페이지 또는 버그 관리, 저장소 등의 주소를 기재한다. 이 종류에 따라 type에 website, bugtracker, repository를 대입하면 된다.
* `<author>`              - 패키지 개발에 참여한 개발자의 이름과 이메일 주소를 적는다. 복수의 개발자가 참여한 경우에는 바로 다음줄에 \<autor> 태그를 이용하여 추가하면 된다.
* `<buildtool_depend>`    - 빌드 시스템의 의존성을 기술한다. 지금은 Catkin build system을 이용하고 있으므로 `catkin`을 입력한다.
* `<build_depend>`        - 패키지를 빌드할 때 의존하는 패키지의 이름을 적는다.
* `<run_depend>`          - 패키지를 실행할 때 의존하는 패키지의 이름을 적는다.
* `<test_depend>`         - 패키지를 테스트할 때 의존하는 패키지의 이름을 적는다.
* `<export>`              - ROS에서 명시하지 않는 태그명을 사용할 때 쓰인다. 제일 널리 쓰이는 것은 메타패키지일 때 `<export><metapackage/></export>`
* `<metapackage>`         - export 태그 안에서 사용하는 공식적인 태그로 현재의 패키지가 메타패키지면 이를 선언한다.


직접 커스터마이징 하면 아래와 같이 기술 할 수 있다. 

{% highlight xml linenos %}
<?xml version="1.0"?>
<package>
<name>my_first_ros_pkg</name>
<version>0.0.1</version>
<description>The my_first_ros_pkg package</description>
<license>Apache License 2.0</license>
<author email="lsirikh@gmail.com">Kiho Lee</author>
<maintainer email="lsirikh@gmail.com">Kiho Lee</maintainer>
<url type="bugtracker"></url>
<url type="repository"></url>
<url type="website">https://lsirikh.github.io</url>
<buildtool_depend>catkin</buildtool_depend>
<build_depend>std_msgs</build_depend>
<build_depend>roscpp</build_depend>
<run_depend>std_msgs</run_depend>
<run_depend>roscpp</run_depend>
<export></export>
</package>
{% endhighlight %}


## 4. 빌드 설정 파일(CMakeLists.txt) 수정

ROS의 빌드 시스템인 Catkin은 기본적으로 CMake를 이용하고 있어서 패키지의 폴더의 `CMakeLists.txt`라는 파일에 빌드 환경을 기술하고 있다.

```
cmake_minimum_required(VERSION 2.8.3)
project(my_first_ros_pkg)

## Compile as C++11, supported in ROS Kinetic and newer
# add_compile_options(-std=c++11)

## Find catkin macros and libraries
## if COMPONENTS list like find_package(catkin REQUIRED COMPONENTS xyz)
## is used, also find other catkin packages
find_package(catkin REQUIRED COMPONENTS
  roscpp
  std_msgs
)

## System dependencies are found with CMake's conventions
# find_package(Boost REQUIRED COMPONENTS system)


## Uncomment this if the package has a setup.py. This macro ensures
## modules and global scripts declared therein get installed
## See http://ros.org/doc/api/catkin/html/user_guide/setup_dot_py.html
# catkin_python_setup()

################################################
## Declare ROS messages, services and actions ##
################################################

## To declare and build messages, services or actions from within this
## package, follow these steps:
## * Let MSG_DEP_SET be the set of packages whose message types you use in
##   your messages/services/actions (e.g. std_msgs, actionlib_msgs, ...).
## * In the file package.xml:
##   * add a build_depend tag for "message_generation"
##   * add a build_depend and a exec_depend tag for each package in MSG_DEP_SET
##   * If MSG_DEP_SET isn't empty the following dependency has been pulled in
##     but can be declared for certainty nonetheless:
##     * add a exec_depend tag for "message_runtime"
## * In this file (CMakeLists.txt):
##   * add "message_generation" and every package in MSG_DEP_SET to
##     find_package(catkin REQUIRED COMPONENTS ...)
##   * add "message_runtime" and every package in MSG_DEP_SET to
##     catkin_package(CATKIN_DEPENDS ...)
##   * uncomment the add_*_files sections below as needed
##     and list every .msg/.srv/.action file to be processed
##   * uncomment the generate_messages entry below
##   * add every package in MSG_DEP_SET to generate_messages(DEPENDENCIES ...)

## Generate messages in the 'msg' folder
# add_message_files(
#   FILES
#   Message1.msg
#   Message2.msg
# )

## Generate services in the 'srv' folder
# add_service_files(
#   FILES
#   Service1.srv
#   Service2.srv
# )

## Generate actions in the 'action' folder
# add_action_files(
#   FILES
#   Action1.action
#   Action2.action
# )

## Generate added messages and services with any dependencies listed here
# generate_messages(
#   DEPENDENCIES
#   std_msgs
# )

################################################
## Declare ROS dynamic reconfigure parameters ##
################################################

## To declare and build dynamic reconfigure parameters within this
## package, follow these steps:
## * In the file package.xml:
##   * add a build_depend and a exec_depend tag for "dynamic_reconfigure"
## * In this file (CMakeLists.txt):
##   * add "dynamic_reconfigure" to
##     find_package(catkin REQUIRED COMPONENTS ...)
##   * uncomment the "generate_dynamic_reconfigure_options" section below
##     and list every .cfg file to be processed

## Generate dynamic reconfigure parameters in the 'cfg' folder
# generate_dynamic_reconfigure_options(
#   cfg/DynReconf1.cfg
#   cfg/DynReconf2.cfg
# )

###################################
## catkin specific configuration ##
###################################
## The catkin_package macro generates cmake config files for your package
## Declare things to be passed to dependent projects
## INCLUDE_DIRS: uncomment this if your package contains header files
## LIBRARIES: libraries you create in this project that dependent projects also need
## CATKIN_DEPENDS: catkin_packages dependent projects also need
## DEPENDS: system dependencies of this project that dependent projects also need
catkin_package(
#  INCLUDE_DIRS include
#  LIBRARIES my_first_ros_pkg
#  CATKIN_DEPENDS roscpp std_msgs
#  DEPENDS system_lib
)

###########
## Build ##
###########

## Specify additional locations of header files
## Your package locations should be listed before other locations
include_directories(
# include
  ${catkin_INCLUDE_DIRS}
)

## Declare a C++ library
# add_library(${PROJECT_NAME}
#   src/${PROJECT_NAME}/my_first_ros_pkg.cpp
# )

## Add cmake target dependencies of the library
## as an example, code may need to be generated before libraries
## either from message generation or dynamic reconfigure
# add_dependencies(${PROJECT_NAME} ${${PROJECT_NAME}_EXPORTED_TARGETS} ${catkin_EXPORTED_TARGETS})

## Declare a C++ executable
## With catkin_make all packages are built within a single CMake context
## The recommended prefix ensures that target names across packages don't collide
# add_executable(${PROJECT_NAME}_node src/my_first_ros_pkg_node.cpp)

## Rename C++ executable without prefix
## The above recommended prefix causes long target names, the following renames the
## target back to the shorter version for ease of user use
## e.g. "rosrun someones_pkg node" instead of "rosrun someones_pkg someones_pkg_node"
# set_target_properties(${PROJECT_NAME}_node PROPERTIES OUTPUT_NAME node PREFIX "")

## Add cmake target dependencies of the executable
## same as for the library above
# add_dependencies(${PROJECT_NAME}_node ${${PROJECT_NAME}_EXPORTED_TARGETS} ${catkin_EXPORTED_TARGETS})

## Specify libraries to link a library or executable target against
# target_link_libraries(${PROJECT_NAME}_node
#   ${catkin_LIBRARIES}
# )

#############
## Install ##
#############

# all install targets should use catkin DESTINATION variables
# See http://ros.org/doc/api/catkin/html/adv_user_guide/variables.html

## Mark executable scripts (Python etc.) for installation
## in contrast to setup.py, you can choose the destination
# install(PROGRAMS
#   scripts/my_python_script
#   DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
# )

## Mark executables for installation
## See http://docs.ros.org/melodic/api/catkin/html/howto/format1/building_executables.html
# install(TARGETS ${PROJECT_NAME}_node
#   RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
# )

## Mark libraries for installation
## See http://docs.ros.org/melodic/api/catkin/html/howto/format1/building_libraries.html
# install(TARGETS ${PROJECT_NAME}
#   ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
#   LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
#   RUNTIME DESTINATION ${CATKIN_GLOBAL_BIN_DESTINATION}
# )

## Mark cpp header files for installation
# install(DIRECTORY include/${PROJECT_NAME}/
#   DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
#   FILES_MATCHING PATTERN "*.h"
#   PATTERN ".svn" EXCLUDE
# )

## Mark other files for installation (e.g. launch and bag files, etc.)
# install(FILES
#   # myfile1
#   # myfile2
#   DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}
# )

#############
## Testing ##
#############

## Add gtest based cpp test target and link libraries
# catkin_add_gtest(${PROJECT_NAME}-test test/test_my_first_ros_pkg.cpp)
# if(TARGET ${PROJECT_NAME}-test)
#   target_link_libraries(${PROJECT_NAME}-test ${PROJECT_NAME})
# endif()

## Add folders to be run by python nosetests
# catkin_add_nosetests(test)
```
이제 하나씩 분석을 해보도록 하자.








출처:[ROS_Robot_Programming_EN]
