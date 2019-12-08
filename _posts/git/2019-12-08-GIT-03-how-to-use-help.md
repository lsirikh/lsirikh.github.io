---
layout: single
title:  "03.GIT 시작하기에 앞서 알면 좋은 것(도움말 보기)"
date:   2019-12-08 09:30:13 +0800
permalink: /categories/GIT/3/
taxonomy: {title}
categories: GIT
tags: GIT 시작하기 도움말
comments: true
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---

##### Git을 사용하기 앞서 알면 좋은 내용

<br>

##### Git 도움말 보기

<hr>

명령어에 대한 도움말이 필요할 때 도움말을 보는 방법은 두 가지로 동일한 결과를 볼 수 있다.

```
$ git help <verb>
$ man git-<verb>
```

예를 들어 아래와 같이 실행하면 **git config** 명령에 대한 도움말을 볼 수 있다.


```
$ git help config
```



도움말은 언제 어디서나 볼 수 있다. 오프라인으로도 볼 수 있다. 도움말과 이 책으로 부족하면 다른 사람의 도움을 받는 것이 필요하다. Freenode IRC 서버(irc.freenode.net)에 있는 `#git` 이나 `#github` 채널로 찾아가라. 이 채널에는 보통 수백 명의 사람이 접속해 있다. 모두 Git에 대해 잘 알고 있다. 기꺼이 도와줄 것이다.

Git 명령을 사용하기 위해 매우 자세한 도움말 전체를 볼 필요 없이 각 명령에서 사용할 수 있는 옵션들에 대해서 간략히 살펴볼수도 있다. `-h`, `--help` 옵션을 사용하면 다음과 같이 Git 명령에서 사용할 수 있는 옵션들에 대한 간단한 도움말을 출력한다.


<img src="/assets/img/git/git_help_config.png" width="100%" height="100%" title="git_help_config">

```
$ git add -h
usage: git add [<options>] [--] <pathspec>...

    -n, --dry-run         dry run
    -v, --verbose         be verbose

    -i, --interactive     interactive picking
    -p, --patch           select hunks interactively
    -e, --edit            edit current diff and apply
    -f, --force           allow adding otherwise ignored files
    -u, --update          update tracked files
    -N, --intent-to-add   record only the fact that the path will be added later
    -A, --all             add changes from all tracked and untracked files
    --ignore-removal      ignore paths removed in the working tree (same as --no-all)
    --refresh             don't add, only refresh the index
    --ignore-errors       just skip files which cannot be added because of errors
    --ignore-missing      check if - even missing - files are ignored in dry run
    --chmod <(+/-)x>      override the executable bit of the listed files
```

[출처]https://git-scm.com/book/ko/v2/%EC%8B%9C%EC%9E%91%ED%95%98%EA%B8%B0-%EB%8F%84%EC%9B%80%EB%A7%90-%EB%B3%B4%EA%B8%B0