---
layout: single
title:  "01.GIT이란 무엇인가?"
date:   2019-12-07 19:00:13
permalink: /categories/:categories/:title:output_ext
taxonomy: {title}
categories: GIT
tags: GIT introduction
teaser: "/assets/img/git/480px-Octocat_GitHub_Mascot.png"
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---

## 1. Git 이란 무엇인가???

<img src="/assets/img/git/480px-Octocat_GitHub_Mascot.png" width="40%" height="40%" alt="image">

<img src="/assets/img/git/git.png" title="image">

GitHub를 이해하려면 먼저 Git을 이해해야합니다. Git은 리눅스를 만든 사람인 Linus Torvalds에 의해 시작된 오픈 소스 버전 관리 시스템입니다. Git은 Subversion , CVS 및 Mercurial 과 같은 다른 버전 제어 시스템과 유사합니다.

Git은 버전 관리 시스템이지만 무엇일까? 

> 예를 들어, 개발자가 무언가 앱을 만들면 코드가 지속적으로 변경되어 첫 번째 공식 (베타 이외) 릴리스 이후에 새 버전이 릴리스됩니다.

버전 제어 시스템은 이러한 개정을 똑바로 유지하여 수정 사항을 중앙 저장소에 저장합니다. 이를 통해 개발자는 새로운 버전의 소프트웨어를 다운로드하고 변경하며 최신 버전을 업로드 할 수 있으므로 쉽게 협업 할 수 있습니다. 모든 개발자는 이러한 새로운 변경 사항을 보고 다운로드하여 제공 할 수 있습니다.

마찬가지로, 프로젝트 개발과 관련이 없는 사람들도 공개된 GIT ​​파일을 다운로드하여 사용할 수 있습니다. Git이 시작된 배경이 Linux 환경이기 때문에 Linux에서 좀 더 활용도가 용이 할 수 있지만, 현재 Windows나 OS X에도 많은 지원이 되는 관계로 이제는 크게 무관한 것으로 보입니다.

Git은 사용 가능한 다른 시스템에 비해 여러 가지 장점이 있기 때문에 대부분의 개발자가 선호하는 버전 제어 시스템입니다. 파일 변경 사항을보다 효율적으로 저장하고 파일 무결성을 향상시킵니다. 세부 사항을 알고 싶다면  Git 기본 페이지  에 Git 작동 방식에 대한 자세한 설명이 있습니다.


## 2. GitHub의 "허브"

Git와 함께 사용하여 더 나은 버전 제어 시스템을 확립했습니다. 그렇다면 GitHub는 무엇일까요? Git은 명령 줄 도구이지만 Git revolve와 관련된 모든 것은 프로젝트와 관련된 내용을 저장하는 허브 (GitHub.com)입니다.


## 3. repository (저장소)

repository (일반적으로 "repo"로 약칭)는 특정 프로젝트의 모든 파일이 저장되는 위치입니다. 각 프로젝트에는 자체 저장소가 있으며 고유 한 URL로 액세스 할 수 있습니다.

<img src="/assets/img/git/repository_example.png" title="리포지토리 저장소">

## 4. Fork

“Forking”(발음주의;뽀킹아님)은 이미 존재하는 다른 프로젝트를 기반으로 새 프로젝트를 만들 때 사용합니다. 이것은 프로그램 및 기타 프로젝트의 추가 개발을 손쉽게 할 수 있는 굉장히 놀라운 컨셉인 것 같습니다. GitHub에서 기여하고 싶은 프로젝트를 찾으면 저장소(Repo)를 Fork 하고 원하는대로 변경하고 수정 된 프로젝트를 새 Repo로 릴리스 할 수 있습니다. 새 프로젝트를 작성하기 위해 Fork(분기) 한 원래 저장소가 업데이트되면 해당 업데이트를 현재 분기에 쉽게 추가 할 수 있습니다. 분기 추가의 권한은 원천 개발자에게 있습니다.

## 5. Pull

어떤 개발자가 Repository(repo)를 Fork(분기)하고 프로젝트를 크게 수정 한 후 원래 Repository 주인 혹은 개발자가 이를 인정해주고 원래 프로젝트에 참여시켜주기 원할 수도 있습니다. 그럴 경우 풀 요청을 하면 프로젝트에 참여가 가능합니다. 물론 원본 Repository(이하 리포지토리)의 작성자는 자신의 작업을보고 공식 프로젝트에 수락할지 여부를 선택할 수 있습니다. Pull 요청을 발행 할 때마다 GitHub는 사용자와 기본 프로젝트 관리자가 통신 할 수있는 완벽한 수단을 제공합니다.

## 6. Social networking

사회적 네트워킹 측면에서 GitHub가 가장 강력한 특징을 지닌듯 합니다. 특히, GitHub가 가지는 다양한 특징과 장점을 압도하는 가장 중요한 점이기도 합니다. GitHub의 각 사용자는 이력서처럼 작동하는 자체 프로필을 가지고 있으며 과거 작업 및 풀 요청을 통해 다른 프로젝트에 대한 기여를 보여줍니다. 한마디로 기여도에 무임승차자가 없고, 기여도로 평가할 수 있는 중요한 지표를 제공해줍니다.

GitHub를 통해 프로젝트 revision은 공개적으로 논의 될 수 있고, 많은 전문가들이 해당 프로젝트를 발전시키기 위해 지식을 제공하고 협력 할 수 있습니다. GitHub가 등장하기 전에, 어떤 프로젝트에 관심이있는 개발자는 대개 프로젝트 리딩 개발자와 연락 할 수있는 방법을 수소문 한 후, 자신의 신뢰도와 신력을 입증하여야만 참여가능 했으리라 생각됩니다. 아마도 너무나 높은 난관과 진입장벽으로 협업은 거의 불가능 했던 것 같습니다. 그러나 GitHub는 일종의 협력과 상생의 헤게모니를 열었다는 측면에서 굉장한 사회적 충격을 주는 듯 합니다.


## 7. Changelogs

여러 사람이 한 프로젝트에서 공동 작업 할 때 해당 파일이 저장되는 대상,시기 및 위치를 변경 한 수정본을 추적하기가 어렵습니다. GitHub는 리포지토리에 푸시 된 모든 변경 사항을 추적하여이 문제를 처리합니다.


[출처][howtogeek](https://www.howtogeek.com/180167/htg-explains-what-is-github-and-what-do-geeks-use-it-for/)