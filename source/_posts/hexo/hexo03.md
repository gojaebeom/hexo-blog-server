---
title: github Blog 만들기 - hexo 테마 적용하기
thumbnail: https://cdn-images-1.medium.com/max/1600/1*pv5LukDtyQx5JXQee2uNgA.jpeg
date: 2020-04-20 19:00:00
tags: 
- hexo
- hexo icarus theme
- nodejs
- git
- git page
- github
category: 
- 웹 개발
- github page & hexo

#카탈로그 생성 및 위치
toc: true
widgets:
  - type: toc
    position: right
  - type: category
    position: right
  - type: tagcloud
    position: right
#위치고정 여부
sidebar:
  right:
    sticky: true
---

### **Hexo 테마 설치하기**
hexo에서는 수많은 [테마](https://hexo.io/themes/index.html)들이 존재합니다. 본인이 원하는 테마를 찾아 다운받을 수 있습니다. <!-- more --> 저는 그중에서도 [icarus](https://github.com/ppoffice/hexo-theme-icarus) 라는 테마를 사용하였습니다. icaurs는 material 스러운 디자인으로 저의 취향에 딱 맞는 느낌이더라고요ㅎㅎ

자신이 원하는 테마를 적용할 때는 해당 사이트에서 시키는 방법대로 적용하면 됩니다. 처음 테마를 설치하는 방법은 다 비슷한데 이번 글에서는 icarus theme를 적용하는 방법으로 글을 작성하겠습니다.

**-테마 다운로드**
hexo 블로그 디렉토리 위치에서 터미널을 통해 다음 명령어를 입력 해주세요.
```
$ git clone https://github.com/ppoffice/hexo-theme-icarus.git themes/icarus
```
다운로드가 완료되면 hexo 블로그 폴더에 themes 폴더에 icarus 폴더가 생성된 것을 볼 수 있습니다.
<br>

**-테마 바꾸기**
처음 hexo를 실행시켰을때 보였던 블로그 테마는 landscape 라는 기본 테마인데요. 이것을 다운받은 icarus 테마로 바꿔주어야 합니다. _config.yml 파일을 열어 다음 부분을 수정해주세요.
```yml
# Extensions
## Plugins: https://hexo.io/plugins/
## Themes: https://hexo.io/themes/
theme: landscape # <- 이부분을 icarus로 바꾸어주세요.
```
<br>

**-github에 hexo 블로그 재배포하기**
이전 글에서 다루었던 방법으로 지금까지 수정한 내용을 저장하고 다시 github에 올리면 github page가 바뀐것을 볼 수 있습니다. 다음과 같이 명령어를 입력해주세요.
```
$ hexo g -d
```
<br>

아마 **ERROR: pakage [패키지명] is not installed.** 라는 에러가 몇개 뜨는 것을 볼 수 있는데요. icarus 테마에서 필요로하는 패키지들이 인스톨되지 않았다는 것 입니다. 당황하지말고 로그에 필요하다고 하는 패키지들을 다음과같이 install 해주세요.
```
$ npm install [패키지명]
```
이 이후에 다시 **hexo g -d** 를 통해 github에 배포 후 사이트에 접속해보세요. icarus테마가 적용되어 보이면 성공입니다! 
<br>
이번 글에서는 hexo 블로그에 icarus 테마를 적용하는 방법에 대하여 알아 보았습니다. 다음 글에서는 icarus 테마의 일부분을 커스터마이징 하는 방법에 대해서 알아보겠습니다.