---
title: github Blog 만들기 - 글 작성하기
thumbnail: https://github.com/gojaebeom/hexo-blog-server/blob/master/themes/icarus/source/images/github/thumbnail.png?raw=true
date: 2020-04-21 08:00:00
tags: 
- hexo
- hexo post
- markdown
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

### **MarkDown이란?**
github page에서 글을 작성할때는 **MarkDown** 문법을 사용하여 글을 작성합니다. <!-- more --> 마크다운은 일반 텍스트 문서의 양식을 편집하는 문법이에요. README 파일이나 온라인 문서, 혹은 일반 텍스트 편집기로 문서 양식을 편집할 때 쓰입니다. 마크다운을 이용해 작성된 문서는 쉽게 HTML 등 다른 문서형태로 변환이 가능합니다.

마크다운 문법은 구글을 통해 검색하면, 쉽게 찾아볼 수 있습니다. 간단한 문법이니 사용하기 그리 어렵지 않습니다.

### **새로운 글 작성**
우리가 hexo 프레임워크를 이용하여 포스트를 작성한다면, hexo의 명령어로 쉽게 포스트를 생성할 수 있습니다.
```
$ hexo new [레이아웃명] [새 포스트 명]
```
을 통해 파일을 만들 수 있는데요. 여기서 레이아웃명에 post를 쓰면 되지만, 따로 명시하지않아도 default 값이 post로 되어 있어 괜찮습니다.

### **임시저장 글 작성**
만약 바로 발행되지 않는 글을 작성하고 싶다면 레이아웃명에 draft를 적어주세요.
```java
$ hexo new draft [새 포스트명]
// 이후 발행시에는
$ hexo publish [포스트명]
// 으로 발행할 수 있습니다.
```

위의 방법은 hexo에서 제공하는 명령어를 사용하여 만드는 방법입니다. 위와 같은 방법으로 파일을 만들었다면 hexo 폴더의 source 폴더에 _posts 폴더 내부에 파일들이 생성되어 있는 것을 알 수 있습니다. 그렇다면 저희가 직접 생성하는 것도 가능하겠네요!

_posts 폴더 내부에 원하는 파일명.md 형식으로 파일을 만들어도 똑같이 적용이 됩니다. 다만 명령어로 생성시 hexo에서 사용하는 기본 구조가 잡혀있는데요.
```md
---
title: hello
date: 2020-04-21 09:06:30
tags:
---
```
직접 생성시에는 상단에 저런 틀을 넣어주셔야합니다. 

### **tag 생성하기**
위의 문법은 마크다운에서 제공하는 것이 아닌 hexo의 템플릿 양식입니다. 글의 제목, 날짜, 태그를 적어줄 수 있게 되어있네요. title과 date는 예시가 있으니 tag를 만드는 방법을 알아봅시다.
```java
tags:
- example1
- example2
- example3
// 이런식으로 다수의 태그를 지정할 수 있습니다.
```

### **category 만들기**
위의 양식에는 입력이 안되어있지만, 저 속성들 뿐만아니라 다른 다양한 속성들을 사용할 수 있습니다. 저희가 작성한 글의 카테고리를 분류하고싶다면 위의 양식에 속성으로 category: 를 만들어주세요. 그리고 다음과 같이 적어주시면 됩니다.
```java
category:
- 웹 개발
//위의 카테고리에서 한번 더 분류하고 싶다면
- java 
//밑에 두번째 분류 속성을 만들어주시면 됩니다. 이렇게 작성하면 웹 개발/ java 이런식으로 만들 수 있습니다.
```

### **썸네일 이미지 등록**
마찬가지로 thumbnail이라는 속성을 추가하여 썸네일 이미지를 등록할 수 있습니다.
```java
thumbnail: //이부분에 사용할 이미지의 주소를 입력해 주세요. 
```

### **more, excerpt**
인덱스 페이지에 어느부분까지 표시할 건지에 대한 세팅을 할 수 있습니다. 본문에 아래 주석을 이용하면 됩니다.
```
본문이 이렇게 있을 때 여기까지만 인덱스 페이지에 나타납니다.
<!-- more -->
여기서부턴 인덱스에 안나옵니다.
```

```
여기까지의 내용은 인덱스 페이지에만 나타납니다.
<!-- excerpt -->
여기서부턴 본문 시작입니다.
```

지금까지 post를 작성하는 방법에 대하여 알아보았습니다. 물론 이것 말고도 다른 여러가지 기술들이 있지만, 저도 아직 사용한지 얼마 안되어 이것저것 만져보고 이후에 더 추가하도록 하겠습니다. 감사합니다.