---
title: Maven 프로젝트 만들기

thumbnail: images/maven/thumbnail.png
date: 2020-06-16 19:09:00

tags: 
- maven

category:
- 자바 튜토리얼
- 3. maven

#카탈로그 생성 및 위치
toc: true
widgets:
  - type: toc
    position: right
  - type: category
    position: right
sidebar:
  right:
    sticky: true
---

이전 글에서 메이븐이 왜 필요한지 간단히 알아보았다. 이번엔 메이븐을 사용하는 방법에 대해서 다루고자 한다. 학습의 이해를 위해 IDE에서 지원하는 기능은 사용하지 않고 프로젝트를 만들어 보겠다. <!-- more -->

먼저 maven을 사용하기 위해 다운로드를 받아주어야 하는데 두가지 방법을 예로 들겠다. 

### 메이븐 공식 홈페이지
https://maven.apache.org/download.cgi <-- 메이븐 공식 홈페이지의 다운로드 페이지에 접속하여 본인의 컴퓨터에 맞는 압축파일을 다운로드 받으면 된다. 현재 메이븐은 3.6.3 버전을 공식적으로 지원하고 있다.(참고로, 메이븐 3.3 이후부터는 자바 1.7 이상을 요구한다)

### chocolatey 패키지 매니저
보통 리눅스에서 파일을 쉽게 다운로드하고 관리하기위해 패키지 매니저인 apt를 사용한다. 윈도우도 이러한 이점을 반영하기 위해 생긴 것이 choco라는 패키지 매니저 이다. 이 프로그램을 사용하고 있다면 위의 방법보다 간편하게 cmd(관리자 모드)에서  `choco install maven` 을 입력하는것으로 다운 받을 수 있다. 공식 홈페이지와 동일하게 3.6.3 버전을 다운받는다.

파일을 받았다면 공식홈페이지에서 받은 파일은 압축파일로, choco 패키지 매니저로 받은 파일은 폴더로 풀려져 있을 것 이다. 압축파일은 풀어서 원하는 경로에 위치하면 된다. 

## Maven path setting
메이븐을 실행하기 위해선 사용자 경로\다운받은 메이븐 폴더\bin 의 mvn을 실행 시켜주어야 한다. 하지만 메이븐을 사용하기 위해 매번 긴 경로를 매번 입력하는것은 힘든 일이다.

윈도우 기준으로 환경변수를 등록하는 것으로 이를 해결할 수 있다.
- 폴더의 왼쪽 디렉토리 아이콘사이의 내 PC의 우클릭을 하여 속성 클릭
- 고급 시스템 설정 클릭
- 환경 변수 클릭
- 시스템 변수 부분의 path를 찾아 path부분을 편집해준다.
- maven의 bin 디렉토리 경로를 복사하여 입력해준다. 예) C:\apache-maven-3.6.3\bin
- 저장해주고 cmd에서 mvn -v 을 입력

```
$ mvn -v
Apache Maven 3.6.3 (cecedd343002696d0abb50b32b541b8a6ba2883f)
Maven home: C:\_tools\apache-maven-3.6.3\bin\..
Java version: 1.8.0_251, vendor: Oracle Corporation, runtime: C:\Program Files\Java\jdk1.8.0_251\jre
Default locale: ko_KR, platform encoding: MS949
OS name: "windows 10", version: "10.0", arch: "amd64", family: "windows"
PS C:\Users\gojaebeom>
```

- 위와 같은 문장들이 출력되면 성공이다.

## maven 프로젝트 생성하기
mvn 명령어를 사용하여 프로젝트를 생성할 수 있다. 물론 생성시 여러 옵션을 줄 수 있지만, 우리는 기본 생성 명령어인 `archetype:generate` 만 입력하도록 한다.
```
$ mvn archetype:generate
```

위의 명령어 입력시 엄청나게 많은 로그들이 나타난다. 먼저 mvn은 다른 사람이 만들어 놓은 프로젝트를 이어서 개발하는 것이 가능하다. 나열되는 프로젝트들은 해당 번호를 입력시 사용할 수 있지만, 우리는 현재 아무것도 모르기 때문에 그냥 엔터를 눌러주자. 

번호를 따로 입력해주지 않으면 defulat값인 quick-start 프로젝트로 진행된다(기본 설정만 있는 프로젝트이다). 그 이후에는 quick-start 프로젝트의 버전을 정하라고 하는데 defulat 값은 항상 가장 최신 버전으로 되어 있다. 현재 2020-06-05일 기준으로 1.4 버전이 최신버전이다. 그대로 진행해 주자. 

그다음 그룹아이디, 아티팩트 아이디는 다음과 같이 적었다.
- groupId: com.example
- artifactId: demo

그다음 부터는 무시하고 계속 엔터를 눌러주자.

- version: 1.0-SNAPSHOT (snapshot은 개발중인 프로젝트를 말한다. 그대로 넘어가자)
- package: com.example

## maven 프로젝트 기본 구조
프로젝트 생성시 기본 구조는 다음과 같다.
```
demo
├─src
│   ├─main
│   │  └─java
│   │      └─com
│   │          └─example
│   │              └─App.java
│   ├─test
│       └─java
│           └─com
│               └─example
│                   └─AppTest.java
└─pom.xml
```

기본적으로 생성되는 폴더를 포함한 Maven 프로젝트의 주요 폴더는 다음과 같다.
- src/main/java - 자바 소스 파일이 위치한다.
- src/main/resources - 프로퍼티나 XML 등 리소스 파일이 위치한다. 클래스패스에 포함된다.
- src/main/webapp - 웹 어플리케이션 관련 파일이 위치한다. (WEB-INF 폴더, JSP 파일 등)
- src/test/java - 테스트 자바 소스 파일이 위치한다.
- src/test/resources - 테스트 과정에서 사용되는 리소스 파일이 위치한다. 테스트 시에 사용되는 클래스패스에 포함된다.

기본적으로 생성되지 않은 폴더라 하더라도 직접 생성해주면 된다. 예를 들어 src/main 폴더에 resources 폴더를 생성해주면 Maven은 리소스 폴더로 인식한다.

## Maven의 lifecycle

- generate-sources 
    - 컴파일 과정에 포함될 소스를 생성
- process-sources	
    - 필터와 같은 작업을 소스 코드에 처리 
- generate-resources	
    - 패키지에 포함될 자원을 생성 	 
- process-resources	
    - 필터와 같은 작업을 자원 파일에 처리하고, 자원 파일을 클래스 출력 디렉토리에 복사
- **compile**
    - 소스 코드를 컴파일해서 클래스 출력 폴더에 클래스를 생성
- generate-test-sources	
    - 테스트 소스 코드를 생성
- process-test-sources	
    - 필터와 같은 작업을 테스트 소스 코드에 처리
- generate-test-resources	
    - 테스트를 위한 자원 파일을 생성	 
- process-test-resources	
    - 필터와 같은 작업을 테스트 자원 파일에 처리, 테스트 자원 파일을 테스트 클래스 출력 폴더에 복사 
- test-compile	
    - 테스트 소스 코드를 컴파일해서 테스트 클래스 추력 폴더에 클래스를 생성
- **test**	
    - 테스트를 실행
- **package**
    - 컴파일 된 코드와 자원 파일들을 jar, war와 같은 배포 형식으로 패키징
- **install**	
    - 로컬 리포지토리에 패키지를 복사
- **deploy**	
    - 생성된 패키지 파일을 원격 리포지토리에 등록하여, 다른 프로젝트에서 사용할 수 있도록 함

위의 라이프사이클중 굵게 표시된 단계는 명령어로 사용할 수 있다. 만약 `mvn compile` 입력시 처음부터 compile까지 순차적으로 실행된다. `mvn install` 입력시 처음부터 install까지 순차적으로 실행하게 되는 것 이다. 만약 그렇다면 위와 같은 라이프사이클은 항상 순차적으로 진행해야 하는것 인가? 라고 한다면 그것은 아니다. 

maven은 위의 과정들을 각각 개별적인 플러그인으로 만들어 부품과 같이 사용하지 않을 플러그인은 무시하고 넘어갈 수 있도록 만들어져있다. 

그리고 clean 명령어는 다음과 같은 상황에서 사용할 수 있다.
- clean
    - 메이븐 빌드를 통하여 생성된 모든 산출물을 삭제한다.

라이프사이클에 관한 내용을 잘 정리해주셔서 자바캔님의 블로그 내용을 인용하였습니다.
출처: https://javacan.tistory.com/entry/MavenBasic [자바캔]




