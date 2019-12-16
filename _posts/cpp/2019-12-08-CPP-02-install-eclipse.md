---
layout: single
title:  "02.C++ IDE Eclipse 설치하기"
permalink: /categories/:categories/:title:output_ext
taxonomy: {title}
date:   2019-12-08 22:17:13
categories: C++
tags: C++ introduction 이클립스 Eclipse
comments: true
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---
<br>

# Eclipse IDE for C/C++ Developers

<br>

## 1. 자바 JDK 설치하기


사용 가능한 표준 설치 유형은 JDK와 JRE입니다. JDK (Java Development Kit)는 Java 컴파일러를 포함하여 새로운 Java 응용 프로그램을 개발할 수있는 기능을 제공합니다. JRE (Java Runtime Environment)는 애플릿이있는 Java 응용 프로그램에 대한 런타임 환경을 제공합니다. Java 개발자는 새로운 Java 응용 프로그램을 만들려면 시스템에 JDK와 JRE를 모두 설치해야했습니다.

> 중요 : Oracle Java 8은 더 이상 공개적으로 다운로드 할 수 없습니다. 아래 링크를 사용하여 Java 11을 설치할 수 있습니다.이 자습서를 계속 진행하여 OpenJDK 8을 설치할 수도 있습니다.

이 튜토리얼을 사용하여 PPA를 사용하여 Ubuntu 19.10, 18.04 LTS, 16.04 LTS, LinuxMint 19, 18에 OpenJDK Java 8을 설치하십시오. 명령 행을 통해 Ubuntu에 Java 8을 설치하려면 아래 단계를 따르십시오.


### 1 단계 – 우분투에 Java 8 설치

OpenJDK 8은 기본 Apt 저장소에서 사용 가능합니다. 다음 명령을 사용하여 Ubuntu 시스템에 Java 8을 간단히 설치할 수 있습니다.

Ubuntu 및 LinuxMint에 Java 8을 설치하려면 아래 명령을 실행하십시오.

```
$ sudo apt update
$ sudo apt install openjdk-8-jdk openjdk-8-jre
```

### 2 단계 – Java 버전 확인

위의 단계를 사용하여 Oracle Java 8을 성공적으로 설치 한 후 다음 명령을 사용하여 설치된 버전을 확인하십시오.

```
$ java -version
```


### 3 단계 – JAVA_HOME 및 JRE_HOME 변수 설정

Linux 시스템에 Java를 설치 한 후 JAVA_HOME 및 JRE_HOME 환경 변수 를 설정해야합니다. JAVA_HOME 및 JRE_HOME 환경 변수는 많은 Java 응용 프로그램에서 런타임 중에 Java 라이브러리를 찾기 위해 사용합니다. 다음 명령을 사용하여 / etc / environment 파일 에서 이러한 변수를 설정할 수 있습니다 .

```
$ sudo gedit /etc/environment
```

{% highlight bash linenos %}
JAVA_HOME="/usr/lib/jvm/java-8-openjdk-amd64"
JRE_HOME="/usr/lib/jvm/java-8-openjdk-amd64/jre"
{% endhighlight %}

모든 작업이 완료되었으며 Linux 시스템에 Java 8이 성공적으로 설치됐다. 

[출처][tecadmin](https://tecadmin.net/install-oracle-java-8-ubuntu-via-ppa/)

<br>

## 2. 이클립스(Eclipse IDE) 설치하기(Oxygen)


CPP IDE를 찾던 중 다양한 이야기가 있는데, 어떤 포럼에선 IDE를 받지 말고, vim + gcc 뭐 이런 조합으로 가라는 등의 이야기가 있었다. 하지만, 기존에 IDE를 쓰면서 워낙 장점이 많았던 것을 경험한 터라, 쉽게 커맨드 라인 기반의 시스템으로 가기 쉽지 않았다. 특히 vim은 사용하려면 에디팅 방법을 익혀야 하는 상당한 스트레스가 있다. 
그래서 가장 익숙한 이클립스를 활용하여, 개발을 해보기로 한다.

[이클립스 IDE 받으러 가기](https://www.eclipse.org/downloads/packages/release/oxygen/3a)


> 각자 시스템에 맞춰 다운로드를 합니다. 단, "Eclipse IDE for C/C++ Developers" 를 다운로드 하는 것을 잊지 말자.

<img src="/assets/img/cpp/eclipse01.png" title="이클립스 CPP 개발자 IDE 다운로드">

<img src="/assets/img/cpp/eclipse02.png" title="이클립스 Oxygen 버전 받기">


### 1 단계 – 압축풀기

```
$ tar xvzf ./eclipse-cpp-oxygen-3a-linux-gtk-x86_64.tar.gz
```

### 2 단계 – Eclipse 폴더를 /opt 폴더로 이동

```
$ sudo mv eclipse /opt
```



### 3 단계 – 터미널 실행 설정
```
$ sudo gedit /usr/bin/eclipse
```
{% highlight bash linenos %}
#! /bin/sh
export ECLIPSE_HOME=/opt/eclipse
$ECLIPSE_HOME/eclipse $*
{% endhighlight %}


> 중간중간 warning이 떠서 찝찝하지만, 진행했다.

```
$ source /etc/environment
```
```
$ sudo chmod 755 /usr/bin/eclipse
```
### 4 단계 – X윈도우 바로가기 설정

```
$ sudo gedit /usr/share/applications/eclipse.desktop
```

{% highlight bash linenos %}
[Desktop Entry]

Encoding=UTF-8
Name=Eclipse
Comment=Eclipse IDE
Exec=eclipse
Icon=/opt/eclipse/icon.xpm
Terminal=false
Type=Application
Categories=Development
StartupNotif=true
{% endhighlight %}


<img src="/assets/img/cpp/eclipse03.png" title="바로가기 설정">


### 5 단계 - Eclipse CDT 설치

```
$ eclipse
```
<img src="/assets/img/cpp/eclipse04.png"  title="바로가기 설정">

<img src="/assets/img/cpp/eclipse05.png"  title="바로가기 설정">

> 난 CDT를 설치하여 위에 작업 아이콘이 보인다. 하지만, 처음에 Eclipse를 설치하면 없기 때문에 설치를 해야한다.

<img src="/assets/img/cpp/Menu_011.png"  title="Install New Software">


<img src="/assets/img/cpp/cpp_cdt.png"  title="CDT설치 1단계">

<img src="/assets/img/cpp/cpp_cdt02.png"  title="CDT설치 2단계 설정">

<img src="/assets/img/cpp/cpp_cdt03.png"  title="CDT설치 3단계 설정">


