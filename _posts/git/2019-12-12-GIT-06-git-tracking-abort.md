---
layout: single
title:  "06.GIT 파일 트랙킹 중지 및 재시작"
permalink: /categories/:categories/:title:output_ext
taxonomy: {title}
categories: GIT
tags: GIT 트래킹중지 트래킹재시작
comments: true
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---

## 1. 들어가며

git을 쓰면서 트랙킹되고 있는 파일 즉, git의 인덱스에 등록된 파일을 **.gitignore**로 등록해도 작동이 안되는 경우가 있다. 사실 gitignore와 다른 개념이기 때문에 이 명령어가 작동 안되는 것이다.

지금같은 경우는 `로컬에 파일은 있지만, 이 파일을 리모트로 올리지 않겠다(리모트는 있으면 삭제됨)`가 아니라, `로컬의 파일과 리모트의 파일의 내용을 다르게 유지하고 싶은 경우`에 해당한다.

```
git add .
```
이렇게 쓰면, 기존에 해당 폴더에 있는 모든 파일과 하위 폴더 내용이 모두 git index에 등록이 된다. 

그래서 우리는 .gitignore라는 파일을 활용하게 되는데, 이미 등록이 된 경우 인덱스에서 빠져나오지 않는다.


## 2. .gitignore 만들기 (참고)

이 경우는 사실 로컬 디렉토리에는 존재하는 파일이지만, 리모트(github)에는 올리고 싶지 않은 *.log파일이나 기타 파일들에 해당할 수 있다.

* 로컬 **.gitignore**를 만듭니다.

저장소에 **.gitignore** 라는 파일을 생성하면 Git은 커밋하기 전에 파일을 사용하여 무시할 파일과 디렉토리를 결정한다.

**.gitignore**의 파일은 저장소로 **git add**를 수행할 때, 추적하지 않고, **git commit**을 통해 인덱싱 되지 않고, **git push**를 통해 리모트 리포지토리에도 저장되지 않는다.

### (1) 터미널에서 Git 저장소의 위치로 이동
### (2) .gitignore 파일 생성

```
$ touch .gitignore
```


파일이 이미 체크인되어 있고 무시하려는 경우 나중에 규칙을 추가해도 Git 은 파일을 무시하지 않는다. 이 경우 터미널에서 다음 명령을 실행하여 파일을 먼저 추적 해제해야 한다.

```
$ git rm --cached FILENAME
```

이렇게 하면 git index에서 파일이 삭제되고, 디스크 상에 파일은 존재한다. 이후  commit과 push를 하면, 리모트에 존재하는 파일도 사라지게 된다.

[출처][GitHub Help](https://help.github.com/en/github/using-git/ignoring-files)

## 3. 리모트 파일과 로컬 파일 다르게 유지하기

작업을 하다보면, 서버로 올라가서 작동하는 파일이 개발자가 로컬에서 테스트하는 환경과 다르게 유지해야 되는 경우가 비일비재하다.
그럴 경우, 로컬에서 파일을 테스트하고 올리기 전에 세팅파일을 변경해서 커밋하는 번거로움을 중단하고, git index에서 추적을 중단시켜 놓는 방법이 있다. 즉, git의 index에서 파일 트래킹을 중지 시키는 것이다.

```
git update-index --assume-unchanged <file>
```

만약 다시 트랙킹이 필요할 경우 아래 명령어로 트래킹 유지로 복구 시킬 수 있다.

```
git update-index --no-assume-unchanged <file>
```

만약 폴더 자체를 트래킹 중지를 하고자 하면,

```
git ls-files -z .settings | xargs -0 git update-index --assume-unchanged
```



[출처][seotory](https://seotory.tistory.com/5)