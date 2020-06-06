---
title: war 파일 톰캣에 배포하기

thumbnail: images/maven/thumbnail.png
date: 2020-06-05 20:00:00

tags: 
- maven

category:
- 자바 튜토리얼
- 2. maven

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

이번 글에선 maven-quickstart 프로젝트를 생성하여 톰캣에 배포하여 웹을 띄우기까지의 과정을 처음부터 작성하려고 한다. 물론 메이븐을 이해하기 위해 이클립스나 인텔리J는 사용하지 않고 vscode와 터미널 기능만 이용하려고 한다.<!-- more -->

이번 글의 내용은 기본적으로 maven tool과 톰캣이 설치되어 있다는 가정 하에 진행하도록 하겠다. 

## maven 프로젝트 생성
먼저 파일이 생성되어질 경로를 잡고 터미널에서 기본 프로젝트 생성 코드를 입력한다.
```
$ mvn archetype:generate 
```

수 많은 프로젝트들이 뜨고 난 이후 어떤 프로젝트 기반으로 만들지 입력하라고 한다. 그냥 enter를 누르면 quickstart 프로젝트로 진행
```
$ Choose a number or apply filter (format: [groupId:]artifactId, case sensitive contains): 1610:
```

이후 quickstart 프로젝트의 버전을 입력하라고 한다. default 값은 최신 버전인 1.4 이다. 그대로 enter 눌러주자.
```
Choose org.apache.maven.archetypes:maven-archetype-quickstart version: 
1: 1.0-alpha-1
2: 1.0-alpha-2
3: 1.0-alpha-3
4: 1.0-alpha-4
5: 1.0
6: 1.1
7: 1.3
8: 1.4
Choose a number: 8:
```

이후 차례대로 groupId, artifactId, version, package 등을 물어본다. groupId는 com.example로 artifactId는 demo로 적어주자. 이후 버전부터 enter를 눌러주면 된다. (혹시 같은 폴더 내에 동일한 이름의 demo 프로젝트 폴더가 있다면 에러가 나니 주의)
```
Define value for property 'groupId': com.example
Define value for property 'artifactId': demo
Define value for property 'version' 1.0-SNAPSHOT: : 
Define value for property 'package' com.example: : 
Confirm properties configuration:
groupId: com.example
artifactId: demo
version: 1.0-SNAPSHOT
package: com.example
 Y: :
```

다음과 같이 뜨면 정상적으로 프로젝트가 만들어졌다.
```
[INFO] ----------------------------------------------------------------------------
[INFO] Using following parameters for creating project from Archetype: maven-archetype-quickstart:1.4
[INFO] ----------------------------------------------------------------------------
[INFO] Parameter: groupId, Value: com.example
[INFO] Parameter: artifactId, Value: demo
[INFO] Parameter: version, Value: 1.0-SNAPSHOT
[INFO] Parameter: package, Value: com.example
[INFO] Parameter: packageInPathFormat, Value: com/example
[INFO] Parameter: package, Value: com.example
[INFO] Parameter: version, Value: 1.0-SNAPSHOT
[INFO] Parameter: groupId, Value: com.example
[INFO] Parameter: artifactId, Value: demo
[INFO] Project created from Archetype in dir: C:\_achive\java\maven\demo
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  16.241 s
[INFO] Finished at: 2020-06-05T15:03:24+09:00
[INFO] ------------------------------------------------------------------------
```

## webapp 폴더 생성
기본적인 폴더 구조는 다음과 같다.

```
demo
|-- pom.xml
`-- src
    |-- main
    |   `-- java
    |       `-- com
    |           `-- example
    |                   `-- App.java
    `-- test
        `-- java
            `-- com
                `-- example
                        `-- AppTest.java
```

위의 main 폴더에 다음 같이 폴더를 만들어주자. 우리가 직접 만들어 주었지만 webapp과 WEB-INF는 maven 웹프로젝트를 만들때 사용되는 폴더 구조이다. 이름을 반드시 동일하게 입력하자.

```
demo
|-- pom.xml
`-- src
    |-- main
    |   |-- java
    |   |    `-- com
    |   |         `-- example
    |   |                `-- App.java
    |   `-- webapp
    |       |`-- index.html
    |       |`-- WEB-INF
    |              `-- web.xml
    `-- test
        `-- java
            `-- com
                `-- example
                        `-- AppTest.java
```

webapp 내부에 WEB-INF 폴더와 index.html, 그리고 WEB-INF 폴더에 web.xml이 있다. 먼저 index.html 파일은 단순하게 다음과 같이 만들어 주자.

```html
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <h1>hello maven!</h1>
</body>
</html>
```

그리고 web.xml 기본 양식은 톰캣 폴더의 webapps -> ROOT -> WEB-INF -> web.xml를 복사해 가져오면 된다. 내용은 다음과 같다.
```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee
                      http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
  version="4.0"
  metadata-complete="true">

  <display-name>Welcome to Tomcat</display-name>
  <description>
     Welcome to Tomcat
  </description>

</web-app>
```

## war file 배포하기
maven의 기본 패키징타입은 jar이다. 우리는 web 프로젝트가 목적이기 때문에 war로 패키징 타입을 바꾸어 주어야 한다. 

pom.xml에 따로 명시 되지 않았는데 상단의 기본정보들을 입력하는 태그 밑에 다음 내용을 넣어주자.
```xml
<packaging>war</packaging>
```

이제 메이븐은 페키징을 할때 pom.xml에 기술된 위의 내용대로 war파일을 만들어줄 것이다. demo 프로젝트의 pom.xml이 있는 경로에서 다음과 같이 입력해주자.

```
$ mvn package
```

에러가 없이 잘 완료 되었다면 target 폴더 하위에 `demo-1.0-SNAPSHOT.war` 라는 war 확장자 파일이 생겼을 것 이다. 우리는 이제 이 파일을 톰캣에 배포해주면 된다.

## 톰캣에 war파일 배포하기
- 톰캣 최상위 디렉토리에서 webapps 폴더 하위에 `demo-1.0-SNAPSHOT.war` 파일을 옮겨준다. 이 파일은 톰캣이 구동시에 저절로 압축이 풀린다.
- 톰캣 최상위 디렉토리에서 bin 폴더 하위에 startup.bat 파일을 실행시켜준다. 
- 브라우저에서 localhost:8080에 접속해보자. 톰캣 서비스가 뜨면 서버는 정상적으로 실행되고 있다는 것
- 브라우저에서 localhost:8080/demo-1.0-SNAPSHOT/index.html 와 같이 입력해보자. hello maven! 이 뜬다면 성공이다.
  - 실제 위의 주소명은 톰캣의 webapps 를 기본 경로로 하여 압축이 풀린 demo-1.0-SNAPSHOT 내부의 index.html이 보이는 것을 알 수 있다. 

## maven webapp 프로젝트 쉽게 만들기
사실 위의 maven 프로젝트 생성하기 단계는 처음 생성시에 옵션을 주는것으로 빠르게 만들 수 있다.

```
$ mvn archetype:generate -DinteractiveMode=false  -DgroupId=<패키지명> -DartifactId=<프로젝트명> -DarchetypeArtifactId=maven-archetype-webapp
```
<sup>*줄을 임의로 내리면 안된다. 옆으로 계속 이어서 써야한다.</sup>

위와 같이 프로젝트를 만들게 되면 다음과 같이 기본적인 webapp 구조가 잡히게 된다.

```
demo
|-- pom.xml
|
 `-- src
      `-- main
            |`-- resources
            |
             `-- webapp
                  |`-- WEB-INF
                  |       `-- web.xml
                   `-- index.jsp
```
