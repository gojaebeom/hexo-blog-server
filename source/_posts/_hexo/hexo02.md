---
title: github Blog 만들기 - hexo 설치 및 배포
thumbnail: https://github.com/gojaebeom/hexo-blog-server/blob/master/themes/icarus/source/images/github/thumbnail.png?raw=true
date: 2020-04-20 18:00:00
tags: 
- hexo
- nodejs
- git
- git page
- github
category: 
- Hexo & Git Pages Blog

#카탈로그 생성 및 위치
toc: true
widgets:
  - type: toc
    position: right
  - type: bgm
    position: right
sidebar:
  right:
    sticky: true
---

### **Hexo 설치**
저번 글에서 github page를 생성하는 것 까지 해보았습니다. 이어서 Hexo를 설치해 보겠습니다.<!-- more --> 다시 Hexo에 대하여 간단히 말하자면 NodeJS 기반으로 만들어진 정적사이트 생성기로써 github page를 좀더 쉽게 관리 및 아름다운 테마를 사용할 수 있게 해줍니다.

먼저 hexo를 설치하기 위해선 nodeJS가 설치되어 있어야 합니다. 
- [Node.JS 공식홈페이지 주소](https://nodejs.org/ko/)

nodejs를 로컬에 설치하면 자동으로 npm도 함께 설치가 되는데 npm은 Node Packaged Manager의 약자로, 많은 사람들이 자바스크립트 패키지들을 만들어 공유하고 그런 오픈소스라이브러리들 쉽게 사용할 수 있게 해주는 프로그램입니다. 우리는 npm을 통해 Hexo를 설치해보겠습니다.

**1. hexo 클라이언트 설치** : _cmd창이나 터미널을 열고 다음을 입력합니다._
```c
$ npm install hexo-cli -g
//install대신 i를 적어도 됩니다.
//-g는 global의 약자로 사용자의 로컬에 전역적으로 설치한다는 뜻 입니다.
```
<br>

**2. hexo 폴더 생성** : _핵소 클라이언트를 설치하였다면 이제 hexo 명령어를 사용할 수 있습니다. hexo를 통해 hexo 폴더를 생성해봅시다._
```c
$ hexo init 폴더명 //폴더명 부분에 원하는 폴더명을 입력하세요
$ cd 폴더명 //cd 는 change directory의 약자로 해당 폴더로 이동하게 해줍니다.
$ npm install // 폴더내부에 package.json 파일의 내용을 읽어 필요한 모듈들을 인스톨하는 과정입니다.
```
error없이 완료되면 성공입니다!
<br>

**3. config.yml 수정** : _정적 사이트 생성기 프레임워크들의 공통적인 특징으로 사용자가 쉽게 사이트의 정보를 수정할 수 있는 config.yml이 존재합니다. 해당 파일을 코드에디터등을 활용하여 열어주세요._
```yml
# Site 수정 : 제일 상단에 있습니다.
# 예시로 적어놓은 것 이니 본인한테맞게 적어주세요
title: Hexo # 사이트 제목
subtitle: 'hexo 블로그' # 사이트 부제
description: 'hexo로 만든 블로그 입니다' # 사이트 설명
keywords: hexo, github, github pages, git # 사이트 검색 키워드
author: JaeBeom Go # 저자
language: ko # 사용 언어
timezone: 'Asia/Seoul' # 표준시간
```
```yml
# URL 수정 : 상단 쪽에 있습니다.
# 예시로 적어놓은 것 이니 본인한테맞게 적어주세요
url: http://example.github.io
root: /
permalink: :year/:month/:day/:title/
permalink_defaults:
pretty_urls:
  trailing_index: true
  trailing_html: true
```
```yml
# Deployment 수정 : 제일 하단에 있습니다.
# 예시로 적어놓은 것 이니 본인한테맞게 적어주세요
deploy:
  type: git
  repo: https://github.com/username/username.github.io.git
  branch: master
```
<br>

**4. hexo 서버 실행시켜 보기** : _기본적인 셋팅은 끝났습니다. 해당 디렉토리 위치의 cmd에서 아래 명령어를 입력해주세요._
```c
$ hexo server
//server는 줄여서 s로 사용가능합니다.
```
서버가 정상적으로 실행되면 [http://localhost:4000](http://localhost:4000)에서 블로그를 볼 수 있습니다.

<img src="/images/github/04.png" alt="img" style="border-radius:5px; border:3px dotted #F2F2F2;"/>

실행시키면 이렇게 우주스러운테마의 홈페이지가 열리면 성공입니다.

**5. hexo 블로그파일 github에 배포하기** 
방금 서버를 실행시킨것은 어디까지나 개인 컴퓨터에서만 보이는 서버입니다. 이제 github에 배포하여 다른 사람들도 볼 수 있도록 해봅시다.

-_정적 웹 리소스 생성하기_
```c
$ hexo generate
//줄여서 hexo g 로도 사용가능합니다.
```
-_github에 배포하기_
```c
$ hexo deploy
//줄여서 hexo -d 로도 사용가능합니다.
//위의 웹 리소스 생성과 배포를 'hexo g -d' 로 동시에 할 수 있습니다.
```

배포시에 **ERROR Deployer not found: git** 라는 에러가 뜬다면 **hexo-deployer-git** 이라는 플러그인을 설치해주세요
```c
$ npm install hexo-deployer-git
```
설치 후 다시 'hexo -d' 를 통해 github에 배포를 하면 됩니다. 그 후 브라우저에서 https://{username}.github.io 주소 입력시 우주스러운 홈페이지가 뜨면 성공입니다.

이번 글에서는 hexo 설치 및 배포하는 방법까지 알아보았습니다. 하지만 블로그 디자인이 너무 우주스러운게 맘에 들지않아요. hexo에서는 타 정적 웹사이트 프레임워크들과 같이 아름다운 테마들을 제공하는데요. 다음시간에는 테마 적용방법에 대하여 포스팅하겠습니다.