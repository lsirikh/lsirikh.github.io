---
layout: single
title:  "05.GIT 저장소 수정하기와 저장하기"
date:   2019-12-08 10:50:13
permalink: /categories/:categories/:title:output_ext
taxonomy: {title}
categories: GIT
tags: GIT 기초 수정하기 저장하기
comments: true
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---

<br>

# Git의 기초 - 수정하고 저장소에 저장하기

실제 존재하는 Git 저장소를 하나 만들었고 워킹 디렉토리에 Checkout도 했다. 이제는 파일을 수정하고 파일의 스냅샷을 커밋해 보자. 파일을 수정하다가 저장하고 싶으면 스냅샷을 커밋한다.

> Checkout은 처음 Git을 접하면 생소할 수 있다. Git은 스냅샷을 기반으로 데이터의 내용을 저장하고 추적한다. Checkout이 되어있는 디렉토리란(워킹디렉토리)는 현재 .git 폴더에서 관리하는 워킹 트리에 데이터가 업데이트 되어 워킹트리, 워킹트리의 선택 브랜치, 워킹 디렉토리 모두 최신화 되어 있는 상태를 말한다. (이렇게 설명하면 처음 접하는 사람은 더 헷갈릴 수 있을 것 같네...)

*이제부터 설명하는 내용이 Git에 매우 중요한 내용이지만, 이해하기 쉽지 않을 수 있다. 차근차근 보도록 해보자.*

워킹 디렉토리의 모든 파일은 크게 Tracked(관리대상임)와 Untracked(관리대상이 아님)로 나눈다. Tracked 파일은 이미 스냅샷에 포함돼 있던 파일이다. Tracked 파일은 또 Unmodified(수정하지 않음)와 Modified(수정함) 그리고 Staged(커밋으로 저장소에 기록할) 상태 중 하나이다. 간단히 말하자면 Git이 알고 있는 파일이라는 것이다.

그리고 나머지 파일은 모두 Untracked 파일이다. Untracked 파일은 워킹 디렉토리에 있는 파일 중 스냅샷에도 Staging Area에도 포함되지 않은 파일이다. 처음 저장소를 Clone 하면 모든 파일은 Tracked이면서 Unmodified 상태이다. 파일을 Checkout 하고 나서 아무것도 수정하지 않았기 때문에 그렇다.

마지막 커밋 이후 아직 아무것도 수정하지 않은 상태에서 어떤 파일을 수정하면 Git은 그 파일을 Modified 상태로 인식한다. 실제로 커밋을 하기 위해서는 이 수정한 파일을 Staged 상태로 만들고, Staged 상태의 파일을 커밋한다. 이런 라이프사이클을 계속 반복한다.

<img src="/assets/img/git/git-lifecycle.png"  title="Git 파일의 라이프 사이클">

<br>

## 1. 파일의 상태 확인하기


파일의 상태를 확인하려면 보통 **git status** 명령을 사용한다. Clone 한 후에 바로 이 명령을 실행하면 아래과 같은 메시지를 볼 수 있다.

```
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
nothing to commit, working directory clean
```
위의 내용은 파일을 하나도 수정하지 않았다는 것을 말해준다. Tracked 파일은 하나도 수정되지 않았다는 의미다. Untracked 파일은 아직 없어서 목록에 나타나지 않는다. 그리고 현재 작업 중인 브랜치를 알려주며 서버의 같은 브랜치로부터 진행된 작업이 없는 것을 나타낸다. 기본 브랜치가 master이기 때문에 현재 브랜치 이름이 “master” 로 나온다. 브랜치 관련 내용은 차차 알아가자. Git 브랜치 에서 브랜치와 Refs에 대해 자세히 다룬다.

프로젝트에 **README** 파일을 만들어보자. **README** 파일은 새로 만든 파일이기 때문에 **git status** 를 실행하면 `Untracked files`에 들어 있다:

```
$ echo 'My Project' > README
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
Untracked files:
  (use "git add <file>..." to include in what will be committed)

    README

nothing added to commit but untracked files present (use "git add" to track)
```

**README** 파일은 “Untracked files” 부분에 속해 있는데 이것은 **README** 파일이 Untracked 상태라는 것을 말한다. Git은 Untracked 파일을 아직 스냅샷(커밋)에 넣어지지 않은 파일이라고 본다. 파일이 Tracked 상태가 되기 전까지는 Git은 절대 그 파일을 커밋하지 않는다. 그래서 일하면서 생성하는 바이너리 파일 같은 것을 커밋하는 실수는 하지 않게 된다. **README** 파일을 추가해서 직접 Tracked 상태로 만들어 보자.

<br>

## 2. 파일을 새로 추적하기


**git add** 명령으로 파일을 새로 추적할 수 있다. 아래 명령을 실행하면 Git은 README 파일을 추적한다.

```
$ git add README
```
**git status** 명령을 다시 실행하면 README 파일이 Tracked 상태이면서 커밋에 추가될 Staged 상태라는 것을 확인할 수 있다.

```
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

    new file:   README
```
“Changes to be committed” 에 들어 있는 파일은 Staged 상태라는 것을 의미한다. 커밋하면 git add 를 실행한 시점의 파일이 커밋되어 저장소 히스토리에 남는다. 앞에서 git init 명령을 실행한 후, git add (files) 명령을 실행했던 걸 기억할 것이다. 이 명령을 통해 디렉토리에 있는 파일을 추적하고 관리하도록 한다. git add 명령은 파일 또는 디렉토리의 경로를 아규먼트로 받는다. 디렉토리면 아래에 있는 모든 파일들까지 재귀적으로 추가한다.

<br>

## 3. Modified 상태의 파일을 Stage 하기



이미 Tracked 상태인 파일을 수정하는 법을 알아보자. **CONTRIBUTING.md** 라는 파일을 수정하고 나서 **git status** 명령을 다시 실행하면 결과는 아래와 같다.

```
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

    new file:   README

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

    modified:   CONTRIBUTING.md
```
이 **CONTRIBUTING.md** 파일은 “Changes not staged for commit” 에 있다. 이것은 수정한 파일이 Tracked 상태이지만 아직 Staged 상태는 아니라는 것이다. Staged 상태로 만들려면 **git add** 명령을 실행해야 한다. **git add** 명령은 파일을 새로 추적할 때도 사용하고 수정한 파일을 Staged 상태로 만들 때도 사용한다. Merge 할 때 충돌난 상태의 파일을 Resolve 상태로 만들때도 사용한다. add의 의미는 프로젝트에 파일을 추가한다기 보다는 다음 커밋에 추가한다고 받아들이는게 좋다. **git add** 명령을 실행하여 **CONTRIBUTING.md** 파일을 Staged 상태로 만들고 **git status** 명령으로 결과를 확인해보자.


```
$ git add CONTRIBUTING.md
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

    new file:   README
    modified:   CONTRIBUTING.md
```

두 파일 모두 Staged 상태이므로 다음 커밋에 포함된다. 하지만 아직 더 수정해야 한다는 것을 알게 되어 바로 커밋하지 못하는 상황이 되었다고 생각해보자. 이 상황에서 CONTRIBUTING.md 파일을 열고 수정한다. 이제 커밋할 준비가 다 됐다고 생각할 테지만, Git은 그렇지 않다. git status 명령으로 파일의 상태를 다시 확인해보자.

> 사실 이 부분이 어떻게 보면 복잡하게 staged 상태를 구분하는 이유가 생기는 큰 원인일 수 있다. 직접 만들어서 비교해보면 그 차이를 쉽게 이해할 수 있을 것 같다.

```
$ vim CONTRIBUTING.md
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

    new file:   README
    modified:   CONTRIBUTING.md

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

    modified:   CONTRIBUTING.md
```

> [참고]본래 출처에서 사용한 에디터 도구는 vim이라는 툴이고 매우 유명한 툴이지만, 사용법이 다소 복잡하여 처음 리눅스 환경을 적응해야하는 사람들에게는 다소 어려울 수 있다. 따라서, gedit나 nano와 같은 툴을 사용하는 게 훨씬 수월 할 수 있다. gedit는 윈도우 환경에서 notepad(매모장)과 같은 에디터라고 볼 수 있다.

헉! **CONTRIBUTING.md** 가 Staged 상태이면서 동시에 Unstaged 상태로 나온다. 어떻게 이런 일이 가능할까? **git add** 명령을 실행하면 Git은 파일을 바로 Staged 상태로 만든다. 지금 이 시점에서 커밋을 하면 **git commit** 명령을 실행하는 시점의 버전이 커밋되는 것이 아니라 마지막으로 **git add** 명령을 실행했을 때의 버전이 커밋된다. 그러니까 **git add** 명령을 실행한 후에 또 파일을 수정하면 **git add** 명령을 다시 실행해서 최신 버전을 Staged 상태로 만들어야 한다.


```
$ git add CONTRIBUTING.md
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

    new file:   README
    modified:   CONTRIBUTING.md
```


<br>

## 4. 파일 상태를 짤막하게 확인하기


**git status** 명령으로 확인할 수 있는 내용이 좀 많아 보일 수 있다. 사실 그렇다. 좀 더 간단하게 변경 내용을 보여주는 옵션이 있다. **git status -s** 또는 **git status --short** 처럼 옵션을 주면 현재 변경한 상태를 짤막하게 보여준다.

```
$ git status -s
M README
MM Rakefile
A  lib/git.rb
M  lib/simplegit.rb
?? LICENSE.txt
```
아직 추적하지 않는 새 파일 앞에는 ?? 표시가 붙는다. Staged 상태로 추가한 파일 중 새로 생성한 파일 앞에는 **A** 표시가, 수정한 파일 앞에는 **M** 표시가 붙는다. 위 명령의 결과에서 상태정보 컬럼에는 두 가지 정보를 보여준다. 왼쪽에는 Staging Area에서의 상태를, 오른쪽에는 Working Tree에서의 상태를 표시한다. **README** 파일 같은 경우 내용을 변경했지만 아직 Staged 상태로 추가하지는 않았다. **lib/simplegit.rb** 파일은 내용을 변경하고 Staged 상태로 추가까지 한 상태이다. 위 결과에서 차이점을 비교해보자. **Rakefile** 은 변경하고 Staged 상태로 추가한 후 또 내용을 변경해서 Staged 이면서 Unstaged 상태인 파일이다.

> 위의 설명을 들으면서 내용을 이해하면 사실 더 이해가 안될 수도 있다. **Rakefile**만 하더라도 Staged상태이면서 Unstaged상태라는 놀라운 설명이... 다시말해, **Rakefile**을 수정하고, **add Rakefile**이 된 후, 또, **Rakefile**을 수정했다는 얘기다.

<br>

## 5. 파일 무시하기


어떤 파일은 Git이 관리할 필요가 없다. 보통 로그 파일이나 빌드 시스템이 자동으로 생성한 파일이 그렇다. 그런 파일을 무시하려면 **.gitignore** 파일을 만들고 그 안에 무시할 파일 패턴을 적는다. 아래는 **.gitignore** 파일의 예이다.

```
$ cat .gitignore
*.[oa]
*~
```
첫번째 라인은 확장자가 “.o” 나 “.a” 인 파일을 Git이 무시하라는 것이고 둘째 라인은 **~** 로 끝나는 모든 파일을 무시하라는 것이다. 보통 대부분의 텍스트 편집기에서 임시파일로 사용하는 파일 이름이기 때문이다. “.o” 와 “.a” 는 각각 빌드 시스템이 만들어내는 오브젝트와 아카이브 파일이고 **~** 로 끝나는 파일은 Emacs나 VI 같은 텍스트 편집기가 임시로 만들어내는 파일이다. 또 log, tmp, pid 같은 디렉토리나, 자동으로 생성하는 문서 같은 것들도 추가할 수 있다. **.gitignore** 파일은 보통 처음에 만들어 두는 것이 편리하다. 그래서 Git 저장소에 커밋하고 싶지 않은 파일을 실수로 커밋하는 일을 방지할 수 있다.

**.gitignore 파일에 입력하는 패턴은 아래 규칙을 따른다.**

* 아무것도 없는 라인이나, `#`로 시작하는 라인은 무시한다.

* 표준 Glob 패턴을 사용한다. 이는 프로젝트 전체에 적용된다.

* 슬래시(/)로 시작하면 하위 디렉토리에 적용되지(Recursivity) 않는다.

* 디렉토리는 슬래시(/)를 끝에 사용하는 것으로 표현한다.

* 느낌표(!)로 시작하는 패턴의 파일은 무시하지 않는다.

Glob 패턴은 **정규표현식**을 단순하게 만든 것으로 생각하면 되고 보통 쉘에서 많이 사용한다. 애스터리스크(**\***)는 문자가 하나도 없거나 하나 이상을 의미하고, **[abc]** 는 중괄호 안에 있는 문자 중 하나를 의미한다(그러니까 이 경우에는 a, b, c). 물음표(?)는 문자 하나를 말하고, **[0-9]** 처럼 중괄호 안의 캐릭터 사이에 하이픈(-)을 사용하면 그 캐릭터 사이에 있는 문자 하나를 말한다. 애스터리스크 2개를 사용하여 디렉토리 안의 디렉토리 까지 지정할 수 있다. **a/\*\*/z** 패턴은 **a/z, a/b/z, a/b/c/z** 디렉토리에 사용할 수 있다.

아래는 **.gitignore**파일의 예이다.

```
# 확장자가 .a인 파일 무시
*.a

# 윗 라인에서 확장자가 .a인 파일은 무시하게 했지만 lib.a는 무시하지 않음
!lib.a

# 현재 디렉토리에 있는 TODO파일은 무시하고 subdir/TODO처럼 하위디렉토리에 있는 파일은 무시하지 않음
/TODO

# build/ 디렉토리에 있는 모든 파일은 무시
build/

# doc/notes.txt 파일은 무시하고 doc/server/arch.txt 파일은 무시하지 않음
doc/*.txt

# doc 디렉토리 아래의 모든 .pdf 파일을 무시
doc/**/*.pdf
```

--|:--:
**Tip**|GitHub은 다양한 프로젝트에서 자주 사용하는 .gitignore 예제를 관리하고 있다. 어떤 내용을 넣을지 막막하다면 **https://github.com/github/gitignore** 사이트에서 적당한 예제를 찾을 수 있다.
**Note**|**.gitignore**를 사용하는 간단한 방식은 하나의 **.gitignore** 파일을 최상위 디렉토리에 하나 두고 모든 하위 디렉토리에까지 적용시키는 방식이다. 물론 **.gitignore** 파일을 하나만 두는 것이 아니라 하위 디렉토리에도 추가로 둘 수도 있다. **.gitignore** 정책은 현재 **.gitignore** 파일이 위치한 디렉토리와 그 하위 디렉토리에 적용된다. (리눅스 커널 소스 저장소에는 **.gitignore** 파일이 206개나 있음)

다수의 **.gitignore** 파일을 두고 정책을 적용하는 부분은 이 책에서 다루는 범위를 벗어난다. 자세한 내용은 `man gitignore`에서 확인할 수 있다.

<br>

## 6. Staged와 Unstaged 상태의 변경 내용을 보기


단순히 파일이 변경됐다는 사실이 아니라 어떤 내용이 변경됐는지 살펴보려면 git status 명령이 아니라 git diff 명령을 사용해야 한다. 보통 우리는 '수정했지만, 아직 Staged 파일이 아닌 것?'과 '어떤 파일이 Staged 상태인지?'가 궁금하기 때문에 git status 명령으로도 충분하다. 더 자세하게 볼 때는 git diff 명령을 사용하는데 Patch처럼 어떤 라인을 추가했고 삭제했는지가 궁금할 때 사용한다. git diff 는 나중에 더 자세히 다룬다.

README 파일을 수정해서 Staged 상태로 만들고 CONTRIBUTING.md 파일은 그냥 수정만 해둔다. 이 상태에서 git status 명령을 실행하면 아래와 같은 메시지를 볼 수 있다.

```
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

    modified:   README

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

    modified:   CONTRIBUTING.md
```
git diff 명령을 실행하면 수정했지만 아직 staged 상태가 아닌 파일을 비교해 볼 수 있다.

```
$ git diff
diff --git a/CONTRIBUTING.md b/CONTRIBUTING.md
index 8ebb991..643e24f 100644
--- a/CONTRIBUTING.md
+++ b/CONTRIBUTING.md
@@ -65,7 +65,8 @@ branch directly, things can get messy.
 Please include a nice description of your changes when you submit your PR;
 if we have to read the whole diff to figure out why you're contributing
 in the first place, you're less likely to get feedback and have your change
-merged in.
+merged in. Also, split your changes into comprehensive chunks if your patch is
+longer than a dozen lines.

 If you are starting to work on a particular area, feel free to submit a PR
 that highlights your work in progress (and note in the PR title that it's
```
이 명령은 워킹 디렉토리에 있는 것과 Staging Area에 있는 것을 비교한다. 그래서 수정하고 아직 Stage 하지 않은 것을 보여준다.

만약 커밋하려고 Staging Area에 넣은 파일의 변경 부분을 보고 싶으면 git diff --staged 옵션을 사용한다. 이 명령은 저장소에 커밋한 것과 Staging Area에 있는 것을 비교한다.

```
$ git diff --staged
diff --git a/README b/README
new file mode 100644
index 0000000..03902a1
--- /dev/null
+++ b/README
@@ -0,0 +1 @@
+My Project
```
꼭 잊지 말아야 할 것이 있는데 git diff 명령은 마지막으로 커밋한 후에 수정한 것들 전부를 보여주지 않는다. git diff 는 Unstaged 상태인 것들만 보여준다. 수정한 파일을 모두 Staging Area에 넣었다면 git diff 명령은 아무것도 출력하지 않는다.

CONTRIBUTING.md 파일을 Stage 한 후에 다시 수정해도 git diff 명령을 사용할 수 있다. 이때는 Staged 상태인 것과 Unstaged 상태인 것을 비교한다.

```
$ git add CONTRIBUTING.md
$ echo '# test line' >> CONTRIBUTING.md
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

    modified:   CONTRIBUTING.md

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

    modified:   CONTRIBUTING.md
```
git diff 명령으로 Unstaged 상태인 변경 부분을 확인할 수 있다.

```
$ git diff
diff --git a/CONTRIBUTING.md b/CONTRIBUTING.md
index 643e24f..87f08c8 100644
--- a/CONTRIBUTING.md
+++ b/CONTRIBUTING.md
@@ -119,3 +119,4 @@ at the
 ## Starter Projects

 See our [projects list](https://github.com/libgit2/libgit2/blob/development/PROJECTS.md).
+# test line
```
Staged 상태인 파일은 git diff --cached 옵션으로 확인한다. --staged 와 --cached 는 같은 옵션이다.

```
$ git diff --cached
diff --git a/CONTRIBUTING.md b/CONTRIBUTING.md
index 8ebb991..643e24f 100644
--- a/CONTRIBUTING.md
+++ b/CONTRIBUTING.md
@@ -65,7 +65,8 @@ branch directly, things can get messy.
 Please include a nice description of your changes when you submit your PR;
 if we have to read the whole diff to figure out why you're contributing
 in the first place, you're less likely to get feedback and have your change
-merged in.
+merged in. Also, split your changes into comprehensive chunks if your patch is
+longer than a dozen lines.

 If you are starting to work on a particular area, feel free to submit a PR
 that highlights your work in progress (and note in the PR title that it's
```


--|:--:
**Note**|**외부 도구로 비교하기**<br>이 책에서는 계속 **git diff** 명령으로 여기저기서 써 먹는다. 즐겨 쓰거나 결과를 아름답게 보여주는 Diff 도구가 있으면 사용할 수 있다. **git diff** 대신 **git difftool** 명령을 사용해서 **emerge**, **vimdiff** 같은 도구로 비교할 수 있다. 상용 제품도 사용할 수 있다. **git difftool --tool-help** 라는 명령은 사용가능한 도구를 보여준다.


<br>

## 7. 변경사항 커밋하기


수정한 것을 커밋하기 위해 Staging Area에 파일을 정리했다. Unstaged 상태의 파일은 커밋되지 않는다는 것을 기억해야 한다. Git은 생성하거나 수정하고 나서 git add 명령으로 추가하지 않은 파일은 커밋하지 않는다. 그 파일은 여전히 Modified 상태로 남아 있다. 커밋하기 전에 git status 명령으로 모든 것이 Staged 상태인지 확인할 수 있다. 그 후에 git commit 을 실행하여 커밋한다.

```
$ git commit
```
Git 설정에 지정된 편집기가 실행되고, 아래와 같은 텍스트가 자동으로 포함된다 (아래 예제는 Vim 편집기의 화면이다. 이 편집기는 쉘의 EDITOR 환경 변수에 등록된 편집기이고 보통은 Vim이나 Emacs을 사용한다. 또 시작하기 에서 설명했듯이 git config --global core.editor 명령으로 어떤 편집기를 사용할지 설정할 수 있다).

편집기는 아래와 같은 내용을 표시한다(아래 예제는 Vim 편집기).

```
# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
# On branch master
# Your branch is up-to-date with 'origin/master'.
#
# Changes to be committed:
#	new file:   README
#	modified:   CONTRIBUTING.md
#
~
~
~
".git/COMMIT_EDITMSG" 9L, 283C
```
자동으로 생성되는 커밋 메시지의 첫 라인은 비어 있고 둘째 라인부터 git status 명령의 결과가 채워진다. 커밋한 내용을 쉽게 기억할 수 있도록 이 메시지를 포함할 수도 있고 메시지를 전부 지우고 새로 작성할 수 있다 (정확히 뭘 수정했는지도 보여줄 수 있는데, git commit 에 -v 옵션을 추가하면 편집기에 diff 메시지도 추가된다). 내용을 저장하고 편집기를 종료하면 Git은 입력된 내용(#로 시작하는 내용을 제외한)으로 새 커밋을 하나 완성한다.

메시지를 인라인으로 첨부할 수도 있다. commit 명령을 실행할 때 아래와 같이 -m 옵션을 사용한다.

```
$ git commit -m "Story 182: Fix benchmarks for speed"
[master 463dc4f] Story 182: Fix benchmarks for speed
 2 files changed, 2 insertions(+)
 create mode 100644 README
```
이렇게 첫번째 커밋을 작성해보았다. commit 명령은 몇 가지 정보를 출력하는데 위 예제는 (master) 브랜치에 커밋했고 체크섬은 (463dc4f)이라고 알려준다. 그리고 수정한 파일이 몇 개이고 삭제됐거나 추가된 라인이 몇 라인인지 알려준다.

Git은 Staging Area에 속한 스냅샷을 커밋한다는 것을 기억해야 한다. 수정은 했지만, 아직 Staging Area에 넣지 않은 것은 다음에 커밋할 수 있다. 커밋할 때마다 프로젝트의 스냅샷을 기록하기 때문에 나중에 스냅샷끼리 비교하거나 예전 스냅샷으로 되돌릴 수 있다.


<br>

## 8. Staging Area 생략하기


Staging Area는 커밋할 파일을 정리한다는 점에서 매우 유용하지만 복잡하기만 하고 필요하지 않은 때도 있다. 아주 쉽게 Staging Area를 생략할 수 있다. git commit 명령을 실행할 때 -a 옵션을 추가하면 Git은 Tracked 상태의 파일을 자동으로 Staging Area에 넣는다. 그래서 git add 명령을 실행하는 수고를 덜 수 있다.

```
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

    modified:   CONTRIBUTING.md

no changes added to commit (use "git add" and/or "git commit -a")
$ git commit -a -m 'added new benchmarks'
[master 83e38c7] added new benchmarks
 1 file changed, 5 insertions(+), 0 deletions(-)
```
이 예제에서는 커밋하기 전에 git add 명령으로 CONTRIBUTING.md 파일을 추가하지 않았다는 점을 눈여겨보자. -a 옵션을 사용하면 모든 파일이 자동으로 추가된다. 편리한 옵션이긴 하지만 주의 깊게 사용해야 한다. 생각 없이 이 옵션을 사용하다 보면 추가하지 말아야 할 변경사항도 추가될 수 있기 때문이다.

<br>

## 9. 파일 삭제하기


Git에서 파일을 제거하려면 git rm 명령으로 Tracked 상태의 파일을 삭제한 후에(정확하게는 Staging Area에서 삭제하는 것) 커밋해야 한다. 이 명령은 워킹 디렉토리에 있는 파일도 삭제하기 때문에 실제로 파일도 지워진다.

Git 명령을 사용하지 않고 단순히 워킹 디렉터리에서 파일을 삭제하고 git status 명령으로 상태를 확인하면 Git은 현재 “Changes not staged for commit” (즉, Unstaged 상태)라고 표시해준다.

```
$ rm PROJECTS.md
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        deleted:    PROJECTS.md

no changes added to commit (use "git add" and/or "git commit -a")
```
그리고 git rm 명령을 실행하면 삭제한 파일은 Staged 상태가 된다.

```
$ git rm PROJECTS.md
rm 'PROJECTS.md'
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

    deleted:    PROJECTS.md
```
커밋하면 파일은 삭제되고 Git은 이 파일을 더는 추적하지 않는다. 이미 파일을 수정했거나 Staging Area에(역주 - Git Index라고도 부른다) 추가했다면 -f 옵션을 주어 강제로 삭제해야 한다. 이 점은 실수로 데이터를 삭제하지 못하도록 하는 안전장치다. 커밋 하지 않고 수정한 데이터는 Git으로 복구할 수 없기 때문이다.

또 Staging Area에서만 제거하고 워킹 디렉토리에 있는 파일은 지우지 않고 남겨둘 수 있다. 다시 말해서 하드디스크에 있는 파일은 그대로 두고 Git만 추적하지 않게 한다. 이것은 .gitignore 파일에 추가하는 것을 빼먹었거나 대용량 로그 파일이나 컴파일된 파일인 .a 파일 같은 것을 실수로 추가했을 때 쓴다. --cached 옵션을 사용하여 명령을 실행한다.

```
$ git rm --cached README
```
여러 개의 파일이나 디렉토리를 한꺼번에 삭제할 수도 있다. 아래와 같이 git rm 명령에 file-glob 패턴을 사용한다.

```
$ git rm log/\*.log
```
**\*** 앞에 \ 을 사용한 것을 기억하자. 파일명 확장 기능은 쉘에만 있는 것이 아니라 Git 자체에도 있기 때문에 필요하다. 이 명령은 log/ 디렉토리에 있는 .log 파일을 모두 삭제한다. 아래의 예제처럼 할 수도 있다.

```
$ git rm \*~
```
이 명령은 ~ 로 끝나는 파일을 모두 삭제한다.

<br>

## 10. 파일 이름 변경하기


Git은 다른 VCS 시스템과는 달리 파일 이름의 변경이나 파일의 이동을 명시적으로 관리하지 않는다. 다시 말해서 파일 이름이 변경됐다는 별도의 정보를 저장하지 않는다. Git은 똑똑해서 굳이 파일 이름이 변경되었다는 것을 추적하지 않아도 아는 방법이 있다. 파일의 이름이 변경된 것을 Git이 어떻게 알아내는지 살펴보자.

이렇게 말하고 Git에 mv 명령이 있는 게 좀 이상하겠지만, 아래와 같이 파일 이름을 변경할 수 있다.

```
$ git mv file_from file_to
```
잘 동작한다. 이 명령을 실행하고 Git의 상태를 확인해보면 Git은 이름이 바뀐 사실을 알고 있다.

```
$ git mv README.md README
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

    renamed:    README.md -> README
```
사실 git mv 명령은 아래 명령어를 수행한 것과 완전 똑같다.

```
$ mv README.md README
$ git rm README.md
$ git add README
```
git mv 명령은 일종의 단축 명령어이다. 이 명령으로 파일 이름을 바꿔도 되고 mv 명령으로 파일 이름을 직접 바꿔도 된다. 단지 git mv 명령은 편리하게 명령을 세 번 실행해주는 것 뿐이다. 어떤 도구로 이름을 바꿔도 상관없다. 중요한 것은 이름을 변경하고 나서 꼭 rm/add 명령을 실행해야 한다는 것 뿐이다.

[출처][git-scm](https://git-scm.com/book/ko/v2/Git%EC%9D%98-%EA%B8%B0%EC%B4%88-%EC%88%98%EC%A0%95%ED%95%98%EA%B3%A0-%EC%A0%80%EC%9E%A5%EC%86%8C%EC%97%90-%EC%A0%80%EC%9E%A5%ED%95%98%EA%B8%B0)