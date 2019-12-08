---
layout: single
title:  "02.GIT 초기 설정하기"
date:   2019-12-07 22:17:13 +0800
permalink: /categories/GIT/{title}
categories: GIT
tags: GIT initial commit 초기 커밋
comments: true
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---

##### Git 시작하기 위한 설정하기

<br>

##### Git 최초 설정

<hr>

Git을 설치하고 나면 Git의 사용 환경을 적절하게 설정해 주어야 한다. 환경 설정은 한 컴퓨터에서 한 번만 하면 된다. 설정한 내용은 Git을 업그레이드해도 유지된다. 언제든지 다시 바꿀 수 있는 명령어도 있다.

> 'git config’라는 도구로 설정 내용을 확인하고 변경할 수 있다. Git은 이 설정에 따라 동작한다. 이때 사용하는 설정 파일은 세 가지나 된다.

- /etc/gitconfig 파일: 시스템의 모든 사용자와 모든 저장소에 적용되는 설정이다. git config --system 옵션으로 이 파일을 읽고 쓸 수 있다. (이 파일은 시스템 전체 설정파일이기 때문에 수정하려면 시스템의 관리자 권한이 필요하다.)

- ~/.gitconfig, ~/.config/git/config 파일: 특정 사용자(즉 현재 사용자)에게만 적용되는 설정이다. git config --global 옵션으로 이 파일을 읽고 쓸 수 있다. 특정 사용자의 모든 저장소 설정에 적용된다.

- .git/config : 이 파일은 Git 디렉토리에 있고 특정 저장소(혹은 현재 작업 중인 프로젝트)에만 적용된다. --local 옵션을 사용하면 이 파일을 사용하도록 지정할 수 있다. 하지만 기본적으로 이 옵션이 적용되어 있다. (당연히, 이 옵션을 적용하려면 Git 저장소인 디렉토리로 이동 한 후 적용할 수 있다.)


각 설정은 역순으로 우선시 된다. 그래서 **.git/config** 가 **/etc/gitconfig** 보다 우선한다.

Windows에서는 **$HOME** 디렉토리에서 **.gitconfig** 파일을 찾는다(아마도 **C:\Users\\$USER** 디렉토리). Windows에서도 **/etc/gitconfig** 파일은 그 경로에서 찾는다. 이 경로는 아마도 MSys 루트의 상대경로일 텐데, MSys 루트는 인스톨러로 Git을 Windows에 설치할 때 결정된다. Git for Windows 2.x 버전에서는 조금 다르다. Windows XP 사용자는 **C:\Documents and Settings\All Users\Application Data\Git\config** 디렉토리에서 찾을 수 있고 Windows Vista 이후 버전 사용자는 **C:\ProgramData\Git\config** 에서 찾을 수 있다. 이 시스템 설정 파일의 경로는 **git config -f \<file\>** 명령으로 변경할 수 있다. 관리자 권한이 필요하다.

<br>

##### 사용자 정보 설정

<hr>

Git을 설치하고 나서 가장 먼저 해야 하는 것은 사용자이름과 이메일 주소를 설정하는 것이다. Git은 커밋할 때마다 이 정보를 사용한다. 한 번 커밋한 후에는 정보를 변경할 수 없다.

```
$ git config --global user.name "lsirikh"
$ git config --global user.email lsirikh@naver.com
```

다시 말하자면 **--global** 옵션으로 설정하는 것은 딱 한 번만 하면 된다. 해당 시스템에서 해당 사용자가 사용할 때는 이 정보를 사용한다. 만약 프로젝트마다 다른 이름과 이메일 주소를 사용하고 싶으면 **--global** 옵션을 빼고 명령을 실행한다.

[GUI 도구들은 처음 실행할 때 이 설정을 묻는다.]


<br>

##### 편집기 설정

<hr>
사용자 정보를 설정하고 나면 Git에서 사용할 텍스트 편집기를 고른다. 기본적으로 Git은 시스템의 기본 편집기를 사용한다.

하지만, Emacs 같은 다른 텍스트 편집기를 사용할 수 있고 아래와 같이 실행하면 된다.

**꼭 이것을 쓰라는 얘기는 아니고 바꿀수 있는 참고로 활용**

```
$ git config --global core.editor emacs
```
Windows 사용자라면 다른 텍스트 편집기를 사용할 수 있다. 실행파일의 전체 경로를 설정해주면 된다. 실행파일의 전체 경로는 사용하는 편집기에 따라 다르다.

Windows 환경에서 많이 사용되는 Notepad **편집기의 경우 주로 32비트 버전을 사용하게 된다. 현재 기준으로 64비트 버전을 사용하면 동작하지 않는 플러그인이 많다. 32비트 Windows 시스템이거나, 64비트 Windows 시스템에서 64비트 Notepad**을 설치했다면 다음과 같이 설정한다.


```
$ git config --global core.editor "'C:/Program Files/Notepad++/notepad++.exe' -multiInst -nosession"
```
64비트 Windows 시스템에서 32비트 Notepad++을 설치했다면 `C:\Program Files (x86)`에 설치된다.


```
$ git config --global core.editor "'C:/Program Files (x86)/Notepad++/notepad++.exe' -multiInst -nosession"
```
<br>


---|:---:
`Note`|Vim과 Emacs, Notepad++은 꽤 인기 있는 편집기로 개발자들이 즐겨 사용한다. Mac이나 Linux 같은 Unix 시스템, Windows 시스템에서 사용 가능하다. 여기서 소개하는 편집기들이 불편해서 다른 편집기를 사용하고자 한다면 해당 편집기를 Git 편집기로 설정하는 방법을 찾아봐야 한다.|
`Warning`|자신의 편집기를 설정하지 않으면 갑자기 실행된 편집기에 당황할 수 있다. 그땐 당황하지 말고 편집기를 그냥 종료하면 Git 명령을 취소할 수 있다.|


<br>

##### 설정 확인

<hr>

**git config --list** 명령을 실행하면 설정한 모든 것을 보여주어 바로 확인할 수 있다.


```
$ git config --list
user.name=John Doe
user.email=johndoe@example.com
color.status=auto
color.branch=auto
color.interactive=auto
color.diff=auto
...
```

Git은 같은 키를 여러 파일(**/etc/gitconfig** 와 **~/.gitconfig** 같은)에서 읽기 때문에 같은 키가 여러 개 있을 수도 있다. 그러면 Git은 나중 값을 사용한다.

**git config \<key\>** 명령으로 Git이 특정 Key에 대해 어떤 값을 사용하는지 확인할 수 있다.


```
$ git config user.name
lsirikh
```

---|:---:
`Note`|Git이 설정된 값을 읽을 때 여러 파일에서 동일한 키에 대해 다른 값을 설정하고 있을 수 있다. 값이 기대한 값과 다를 수 있는데 값만 보고 쉽게 그 원인을 찾을 수 없다. 이 때 키에 설정된 값이 어디에서 설정되었는지 확인할 수 있는데 다음과 같은 명령으로 어떤 파일로부터 설정된 값인지를 확인할 수 있다.

```
$ git config --show-origin rerere.autoUpdate
file:/home/lsirikh/.gitconfig	false
```
[출처]https://git-scm.com/book/ko/v2/%EC%8B%9C%EC%9E%91%ED%95%98%EA%B8%B0-Git-%EC%B5%9C%EC%B4%88-%EC%84%A4%EC%A0%95