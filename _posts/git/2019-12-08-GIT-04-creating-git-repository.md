---
layout: single
title:  "04.GIT 저장소 만들기"
date:   2019-12-08 10:17:13 +0800
permalink: /categories/GIT/4/
taxonomy: {title}
categories: GIT
tags: GIT 기초 저장소
comments: true
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---

##### Git의 기초 - Git 저장소 만들기

Git에서 자주 사용하는 명령어는 모두 이후에 올리게 될 것이다. 추후 업데이트 되는 내용을 다 읽으면 저장소를 만들고 설정하는 방법, 파일을 추적하거나(Track) 추적을 그만두는 방법, 변경 내용을 Stage 하고 커밋하는 방법을 알게 된다. 파일이나 파일 패턴을 무시하도록 Git을 설정하는 방법, 실수를 쉽고 빠르게 만회하는 방법, 프로젝트 히스토리를 조회하고 커밋을 비교하는 방법, 리모트 저장소에 Push 하고 Pull 하는 방법을 살펴본다.

<br>

##### Git 저장소 만들기

<hr>

주로 다음 주 가지 중 한 가지 방법으로 Git 저장소를 쓰기 시작한다.

1. 아직 버전관리를 하지 않는 로컬 디렉토리 하나를 선택해서 Git 저장소를 적용하는 방법

2. 다른 어딘가에서 Git 저장소를 **Clone** 하는 방법

어떤 방법을 사용하든 로컬 디렉토리에 Git 저장소가 준비되면 이제 뭔가 해볼 수 있다.

<br>

##### 기존 디렉토리를 "Git 저장소"로 만들기

버전관리를 하지 아니하는 기존 프로젝트를 Git으로 관리하고 싶은 경우 우선 프로젝트의 디렉토리로 이동한다. 이러한 과정을 처음 해보는 것이라면 시스템마다 조금 다른 점을 주의하자.

Linux:
```
$ cd /home/user/my_project
```

Mac:

```
$ cd /Users/user/my_project
```

Windows:

```
$ cd /c/user/my_project
```

그리고 아래와 같은 명령을 실행한다:

```
$ git init
```

이 명령은 **.git** 이라는 하위 디렉토리를 만든다. **.git** 디렉토리에는 저장소에 필요한 뼈대 파일(Skeleton)이 들어 있다. 이 명령만으로는 아직 프로젝트의 어떤 파일도 관리하지 않는다. (**.git** 디렉토리가 막 만들어진 직후에 정확히 어떤 파일이 있는지에 대한 내용은 **Git의 내부**에서 다룬다)

Git이 파일을 관리하게 하려면 저장소에 파일을 추가하고 커밋해야 한다. **git add** 명령으로 파일을 추가하고 **git commit** 명령으로 커밋한다:

```
$ git add *.c
$ git add LICENSE
$ git commit -m 'initial project version'
```
> 위의 명령어를 통해 *.c로 된 파일을 추가하고, LICENSE 파일을 추가하는 작업을 한 후 에 git commit이 이루어진 것이다. 해당 폴더의 모든 파일을 추가할 경우 아래와 같이 하는 경우가 내 경우에는 더 많다. (단, 제외 파일 목록 관리를 잘해야한다. 추후에 다루겠다.)

```
$ git add .
```



명령어 몇 개로 순식간에 Git 저장소를 만들고 파일 버전 관리를 시작했다.

<br>

##### 기존 저장소를 Clone 하기

다른 프로젝트에 참여하려거나(Contribute) Git 저장소를 복사하고 싶을 때 **git clone** 명령을 사용한다. 이미 Subversion 같은 VCS에 익숙한 사용자에게는 "checkout" 이 아니라 "clone" 이라는 점이 도드라져 보일 것이다. Git이 Subversion과 다른 가장 큰 차이점은 서버에 있는 거의 모든 데이터를 복사한다는 것이다. **git clone** 을 실행하면 프로젝트 히스토리를 전부 받아온다. 실제로 서버의 디스크가 망가져도 클라이언트 저장소 중에서 아무거나 하나 가져다가 복구하면 된다(서버에만 적용했던 설정은 복구하지 못하지만 모든 데이터는 복구된다 - 서버에 Git 설치하기에서 좀 더 자세히 다룬다).

**git clone \<url\>** 명령으로 저장소를 Clone 한다. **libgit2** 라이브러리 소스코드를 Clone 하려면 아래과 같이 실행한다.

```
$ git clone https://github.com/libgit2/libgit2
```
이 명령은 “libgit2” 라는 디렉토리를 만들고 그 안에 **.git** 디렉토리를 만든다. 그리고 저장소의 데이터를 모두 가져와서 자동으로 가장 최신 버전을 Checkout 해 놓는다. **libgit2** 디렉토리로 이동하면 Checkout으로 생성한 파일을 볼 수 있고 당장 하고자 하는 일을 시작할 수 있다.

아래과 같은 명령을 사용하여 저장소를 Clone 하면 `libgit2`이 아니라 다른 디렉토리 이름으로 Clone 할 수 있다.

```
$ git clone https://github.com/libgit2/libgit2 mylibgit
```

디렉토리 이름이 **mylibgit** 이라는 것만 빼면 이 명령의 결과와 앞선 명령의 결과는 같다.

Git은 다양한 프로토콜을 지원한다. 이제까지는 **https://** 프로토콜을 사용했지만 **git://** 를 사용할 수도 있고 **user@server:path/to/repo.git** 처럼 SSH 프로토콜을 사용할 수도 있다. 자세한 내용은 서버에 Git 설치하기에서 다루며 각 프로토콜의 장단점과 Git 저장소에 접근하는 방법을 설명한다.

<span style="color:red;font-size:20px;"> **Git을 시작하기에 매우 중요한 내용이기 때문에 이 내용을 모르고 Git을 시작한다는 것은 거의 불가능하다. 따라서, 본 내용을 반드시 숙지하는 것이 좋다.** </span>

[출처]https://git-scm.com/book/ko/v2/Git%EC%9D%98-%EA%B8%B0%EC%B4%88-Git-%EC%A0%80%EC%9E%A5%EC%86%8C-%EB%A7%8C%EB%93%A4%EA%B8%B0