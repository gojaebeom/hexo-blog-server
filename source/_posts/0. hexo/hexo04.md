---
title: github Blog 만들기 - icarus 테마 커스터마이징
thumbnail: https://github.com/gojaebeom/hexo-blog-server/blob/master/themes/icarus/source/images/github/thumbnail.png?raw=true
date: 2020-04-20 20:00:00
tags: 
- hexo
- hexo icarus theme
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

### **icarus 테마 살펴보기**
테마를 적용하고난 이후 기쁜마음에 이곳저곳 살펴보다보면 아래 사진처럼 뭐지 싶은 박스들을 볼 수 있습니다. <!-- more -->

<img src="/images/github/05.jpg" alt="너네들은 뭐냐.." style="border-radius:5px; border:3px dotted #F2F2F2;"/>

저도 github 사이트를 만들때 여러 블로그의 글을 보면서 도움을 받았지만, 사실 상 이 부분이 까다로웠습니다.  icarus 테마를 다루는 블로거 분들은 모두 ejs 파일로 만들어진 icarus에 대하여 다루고있지만 본인이 다운받은 파일은 모두 react로 만들어져 있다는 것.. 현재 icarus 공식 github 사이트에 업로드 되어있는 파일은 react로 리팩토링되어 있는 것 같습니다.

react를 조금이나마 흥미를 가지고 배운적이 있기에 긍정적인 마음으로 임하였지만 가장 큰 문제는 블로그에서 다루는 커스터마이징 파일은 ejs 또는 pug등의 파일들로 제공되어있는데, react 로 수정된 버전은 방법이 조금 달라진 것 같습니다. 다행이도 어느정도 시간을 두고 삽질을 하니 많은 부분이 해결이 되었습니다.

### **테마 일부 기능 삭제 / 추가하기**
위의 사진의 박스들이 어느정도 짐작이 가시나요? 각자 광고, 공유, 후원, 댓글기능 등을 추가할 수 있는 카드들이라는 것 입니다. 일단 광고와 후원은 현재로서는 사용하지 않을 예정이니 기능을 꺼놓도록 하겠습니다.

**-구글 광고 카드 삭제**
hexo 블로그 폴더에 있는 config 파일이 아닌 icarus 테마 폴더에 있는 _config.yml 파일을 열어주세요. *# Google AdSense unit configurations* 주석을 찾아 아래 내용과 같이 수정해주세요.
 ```yml
  # Google AdSense unit configurations
  # 구글 광고 카드 / 사용시 adsense 앞의 #을 제거해주세요.
    -
        # Where should the widget be placed, left sidebar or right sidebar
        position: left
        type: #adsense
        # AdSense client ID
        client_id: ''
        # AdSense AD unit ID
        slot_id: ''
 ```
 <br>

**-후원 기능 삭제**
위와 같이 _config.yml 파일을 열어 *# Donate plugin configurations* 주석 이하 내용을 삭제 또는 주석처리 해주세요.
 ```yml
 # Donate plugin configurations
# https://blog.zhangruipeng.me/hexo-theme-icarus/categories/Plugins/Donation/
donates:
    # Alipay donate button configurations
    -
        type: alipay
        # Alipay qrcode image URL
        qrcode: ''
    # "Buy me a coffee" donate button configurations
    -
        type: buymeacoffee
        # URL to the "Buy me a coffee" page
        url: ''
    # Patreon donate button configurations
    -
        type: patreon
        # URL to the Patreon page
        url: ''
    # Paypal donate button configurations
    -
        type: paypal
        # Paypal business ID or email address
        business: ''
        # Currency code
        currency_code: USD
    # Wechat donate button configurations
    -
        type: wechat
        # Wechat qrcode image URL
        qrcode: ''
 ```
 <br>

**-ShareThis(공유) 기능 연결하기**
ShareThis는 방문자가 여러 sns 등에 글을 공유할 수 있게 해주는 기능을 서비스 합니다. icarus(리액트 버전)테마 에서는 sharethis를 연결하는 방법이 조금 다릅니다.

[sharethis](https://sharethis.com/) 사이트를 방문하여 원하는 공유 버튼을 제출을 하고 코드를 받습니다.
```html
<script 
type='text/javascript' 
src='blablablabla:example_code' 
async='async'>
</script>
```
원래는 위의 코드전체를 ejs 파일에 붙여야 하지만 저희는 저 코드에서 src의 코드부분만 복사를 해둡니다. 위의 src내용은 임시로 작성한 것입니다. 본인이 본인 사이트의 주소를 입력하고 발급을 받아야합니다!

복사한 코드를 install_url 부분에 붙여넣어 줍시다.
```yml
# Share plugin configurations
# https://ppoffice.github.io/hexo-theme-icarus/categories/Plugins/Share/
share:
    type: sharethis
    # URL to the ShareThis share plugin script
    install_url: '' 
```
<br>

**-Disqus를 사용하여 댓글 기능 셋팅하기**
[Disqus](https://disqus.com/)는 소셜 댓글 서비스 입니다. 소셜 댓글 서비스란 소셜미디어(SNS)를 활용한 댓글 시스템으로 페이스북,트위터 와 같은 SNS와 연동해서 댓글을 달 수 있게 만들어 주는 서비스입니다. 소셜 댓글 서비스를 활용하여 댓글을 달면 동시에 해당 댓글이 자신이 연동한 SNS에도 발행이 됩니다. 위의 사이트에 들어가 회원가입을하고 무료버전 서비스를 받아봅시다. 

이번에도 ShareThis처럼 다른 테마들과는 다르게 태그 등은 필요하지 않고 'short-name' 값만 가져오면 됩니다. short-name은 회원가입한 ShareThis 아이디에 운영중인 홈페이지 URL을 연결하면 받을 수 있습니다. 그리고 _config.yml의 다음 부분에 short-name의 값을 붙여넣어 주세요.
```yml
# Comment plugin configurations
# https://ppoffice.github.io/hexo-theme-icarus/categories/Plugins/Comment/
comment:
    type: disqus
    # Disqus shortname
    shortname: '' # <- 이 부분에 코드 넣기
```
<br>

여기까지 잘 진행이 되었다면 먼저 hexo server 로 확인을 해주시고 적용이 된 것을 확인하였다면 github에 배포해주시면 됩니다. 남은 프로필을 수정하거나 카드의 배치같은 부분도 _config.yml에서 할 수 있으니 자신만의 느낌대로 적용하시면 될 것 같습니다.

다음 글은 hexo 프레임워크에서 post 하는 방법등을 알아보겠습니다.