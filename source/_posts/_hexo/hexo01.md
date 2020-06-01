---
title: github Blog 만들기 - github 페이지 생성
thumbnail: https://github.com/gojaebeom/hexo-blog-server/blob/master/themes/icarus/source/images/github/thumbnail.png?raw=true
date: 2020-04-17 22:09:00
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

### **github blog를 만든 계기**
요즈음 github에 프로젝트를 올리면서 동시에 글을 쓰는 데요. 아무래도 코딩과 동시에 설명을 적으니 주석 때문에 글도 지저분해 보이고<!-- more --> 관리가 필요한 것 같더라고요. 그래서 시작한 github에서 제공하는 github pages 블로그 프레임워크 hexo를 이용하여 현재 블로그를 만들었습니다.

### **github pages란?**
먼저 git과 github에 대한 어느 정도의 지식이 필요합니다. github pages는 github에 저장소의 내용을 (정적인) 웹페이지로 만들어 주는 서비스입니다. 그리고 무료라는 게 큰 장점이지요.
- github pages : [https://pages.github.com/](https://pages.github.com/)

### **hexo란?**
github pages에서 저장소를 웹페이지로써 호스팅할 수 있게 해준다면, 이것을 쉽게 관리하고 사용하게 해주는 프레임워크들이 있습니다. 정적 사이트 생성기(Static site generator)라고도 하며 대중적으로 유명한 hexo, jekyll, hugo 등이 있습니다. 이중의 뭐가 더 좋다~ 라는 건 저도 잘 모르겠습니다. 각 프레임워크들을 만든 프로그래밍언어들이 다른데 hexo는 nodejs, jekyll는 ruby, hugo는 go 언어로 만들어졌다고 합니다. 저는 nodejs를 접해본 경험이 있기 때문에 hexo가 가장 친근하게 다가왔습니다.
- hexo : [https://hexo.io/](https://hexo.io/)

물론 T스토리나 다음 블로거 등등을 사용해도 되지만 github로 블로그에 포스트를 게시하면서 동시에 github의 잔디까지 깔 수 있겠다 싶은게 가장 컷구요. 
(_하지만 블로그에 글을 올리고 github에 업로드하여도 잔디가 채워지지 않았습니다. 이거 어째서입니까..?_ )

### **github page 생성**
본격적으로 github page를 만들어봅시다. 생각보다 엄청 간단한데요, 먼저 github계정이 있다는 전제 하에 github 메인페이지의 우측 상단에 추가버튼 을 누르고 new repository를 눌러주세요.

<img src="/images/github/01.png" alt="img" style="border-radius:5px; border:3px dotted #F2F2F2;"/>

그리고 repository를 만드는데 다음과 같이 repository명을 example.github.io 를 만들어주세요. example 부분에는 꼭 본인의 아이디명을 적어주셔야 합니다!

<img src="/images/github/02.png" alt="img" style="border-radius:5px; border:3px dotted #F2F2F2;"/>

마지막으로 하단의 Initialize this repository with a README 박스를 채크해주시고 create repository를 클릭해주세요. Initialize this repository with a README 을 채크할 경우 github에 바로 README 파일과함께 repository를 생성할 수 있습니다.

<img src="/images/github/03.png" alt="img" style="border-radius:5px; border:3px dotted #F2F2F2;"/>

위의 이미지처럼 {사용자명}/github.io 의 이름으로 repository가 생성되었다면 성공입니다. github page는 생성이 되었지만 아직 기본적인 설정이 하나 더 남았습니다. https://{사용자명}/github.io url로 주소를 치게되면 처음으로 보이는 index페이지를 하나 생성해봅시다.

- 생성된 repository의 클론주소를 복사해줍니다.
- 본인의 로컬의 내려 받고싶은 폴더에 cmd나 터미널, git bash 등을 이용하여 'git clone {복사한 주소}' 해줍니다.
- 로컬에 생성된 폴더에 들어가 index.html 파일을 만들고 hello world 등 예시 문구등을 적어주세요.
- index.html이 만들어진 git 로컬저장소를 다시 github에 push 해줍니다.
- 브라우저에서 https://{사용자명}/github.io url 주소를 입력하면 사용자가 정의한 문구가 보이는 페이지가 뜨는 것을 확인 할 수 있습니다. (바로 생성되지 않을 수 도 있어요. 저의 경우엔 3분가량 소요되었던 것 같습니다.)

여기까지 github page를 생성하는 방법을 알아보았습니다. 생각만큼 친절한 글은 아닌것 같아요. 중간중간 빠진 내용도 많아보이죠. 아마 이 글을 보러 오시는 분들이라면 웹에 관한 선행학습이 어느정도 되어있을 것 이라 괜찮다고 생각 하였습니다.

다음 글은 이어서 hexo 설치 및 배포방법에 대하여 포스팅하겠습니다.