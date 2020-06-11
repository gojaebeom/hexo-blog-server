---
title: Maven을 알아보자

thumbnail: images/maven/thumbnail.png
date: 2020-06-01 19:09:00

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
  - type: bgm
    position: right
sidebar:
  right:
    sticky: true
---

메이븐은 자바 프로젝트의 빌드(build)를 자동화 해주는 관리 도구(build tool)이다.<!-- more -->  아파치 소프트웨어 제단에서 만들어졌으며,      이전의 Apache Ant 의 대안으로 만들어졌다. 

`Too Much Information`
- <sup>발표일은 2004년 7월 13일 이다.</sup>
- <sup>안정화 버전은 3.5.3 버전으로 2018년 3월 8일 이다.</sup>

이클립스, 인텔리J 등을 사용하면 메이븐에 관한 설정들을 편하게 할 수 있었기 때문에 메이븐이 뭔지 잘 알지 못하고 넘어갔다. 이번 계기로 Spring 관련 글을 쓰기 이전에 Maven을 조금이나마 공부하고 넘어가고자 글을 쓰게 되었다.

## Maven 없이 Java 빌드하기
메이븐이 왜 필요한지 직접 예제를 만들어 비교해보도록 하자.

### 기본적인 빌드
먼저 파일을 만들 디렉토리를 하나 생성해주자. 경로는 본인이 편한 경로에 생성한다. 본인은 cmd에서 빨리 탐색할 수 있게 `C:\Users\[유저명]>` 의 위치에 java_study 폴더를 생성한것으로 설명하겠다.

cmd를 통해 해당경로에 notepad Main.java 를 입력하여 java 파일을 만들어준다.(직접 메모장을 생성해도 상관없다) 그리고 다음 내용을 입력해주자.

```java
class Main{
    public static void main(String[] args){
        System.out.println("Hello World!");
    }
}
```

cmd에 해당 경로에서 javac Main.java 입력, 이후 Main.class 파일이 잘 나오면 java Main 을 입력하면 Hello World!가 잘 출력될 것이다. 

이것은 아주 단순한 예제다. 이제 위의 파일을 패키지에 담아서 빌드해보자. package는 도메인의 역순으로 만드는 것이 일반적인 관례이다.

### 패키지화하여 빌드하기
study_java 디렉토리(자신이 만든 폴더) 위치에서 다음과 같이 폴더를 만들어 준다.
```
study_java
└── com
    └── example
        └── demo
            └── Main.java
```

그리고 자바 파일도 다음과 같이 패키지를 선언해준다.
```java
package com.example.demo;

class Main{
    public static void main(String[] args){
        System.out.println("Hello World!");
    }
}
```

위와 같은 조건들을 만족한다면 `javac com\example\demo\Main.java` 명령어로 패키지 내부의 Main.java를 Main.class 파일로 컴파일 할 수 있다. 이후 실행시에는 `java com.example.demo.Main` 로 실행 하면된다.

### jar 파일로 만들기
이제 만든 자바파일을 배포한다고 생각해보자. 자바는 자바 클래스 파일과, 클래스 들이 이용하는 관련 리소스및 메타 데이터를 하나의 파일로 모아서 자바 플랫폼에 배포할 수 있게 Jar(Java Archive) 파일로 압축할 수 있다.

다음과 같이 명령어를 입력해보자
```c
> jar -c -f main.jar com\*
```
-c는 create의 약자로 jar파일을 만든다는 뜻이다. 이후 -f Main.jar 는 파일명을 명시하라는 명령어로 Main.jar로 만들겠다는 뜻이다. 이 옵션들을 설정한 이후 공백을 기준으로 담을 파일들을 지정할 수 있는데, `com\*`는 com 하위 디렉토리를 모두 포함한다는 의미이다. 별다른 에러가 뜨지 않았다면 해당 디렉토리에 main.jar파일이 잘 생성되어있는 것을 볼 수 있을 것 이다.

이제 실행해보자.
```c
> java -cp . main.jar com.example.demo.Main
// -cp는 classpath의 약자이다 
```

위의 방법은 현재 디렉토리를 classpath로 잡고 Main.jar의 압축을 푼 뒤 com.example.demo의 Main클래스를 실행한다고 보면 된다. 하지만 jar파일 자체를 실행할 수 도 있다.
```c
> java -jar main.jar
```

위의 방법으로 실행시 `no main manifest attribute, in test.jar`라는 오류 문구가 뜨는 것을 볼 수 있을 것 이다. 이는 매니페스트 파일을 만들어 Main 클래스의 위치를 명시해주면 해결 할 수 있다.

> 메니페스트
> JAR 파일 안에 포함되어 있는 매니페스트 파일은, 메타데이터 정보를 포함하고 있다. 이 메타데이터 정보에는 확장 정보 및 패키지 관련 데이터가 기술되어 있으며, 섹션 형식으로 구성된 키-값 쌍 형태의 문자열이다. JAR이 실행 가능하도록 하기 위해서는, 메니페스트 파일에, 애플리케이션의 메인 클래스의 이름이 기술되어 있어야 한다. 메니페스트 파일의 명칭은 MANIFEST.MF이며, 이 파일이 포함되어 있는 디렉토리는, 압축된 파일의 내용물 가운데 가장 첫번째 위치에 배치되어야 한다.

1. 먼저 java_study 디렉토리에 manifest.txt 파일을 만들어주자.
2. Main-Class: com.example.demo.Main 적어주자.
3. cmd 에서 `jar -c -m manifest.txt  -f main.jar com\*` 를 다시 입력 하여 manifest파일을 포함하여 다시 jar파일로 압축해준다.

```c
> java -jar main.jar
```
다시 명령어를 입력하면 hello world! 가 잘 출력되는 것을 볼 수 있다.

이정도만 했는데도 벌써 찐이 빠진다. 여기에 의존성을 추가해야한다면 어떻게 할 수 있을까?

### logback 라이브러리 추가해보기
logback은 기본적으로 다음 세개의 라이브러리가 필요하다. 각 링크에서 file에 jar파일로 다운받아 보자.
- [logback-classic-1.2.3](https://mvnrepository.com/artifact/ch.qos.logback/logback-classic/1.2.3)
- [logback-core-1.2.3](https://mvnrepository.com/artifact/ch.qos.logback/logback-core/1.2.3)
- [sl4j-api-1.7.30](https://mvnrepository.com/artifact/org.slf4j/slf4j-api/1.7.30)

java_study 의 최상위 경로에 lib 폴더를 생성하고 위의 jar파일들을 위치해준다. 이후 Main.java 파일을 다음과 같이 수정한다.
```java
package com.example.demo;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

class Main{
	private static Logger logger = LoggerFactory.getLogger(Main.class);
	public static void main(String[] args){
		logger.info("Hello World!!");
	}
}
```

이제 위의 java파일을 컴파일 하면 되는데, 이전의 System.out.println은 자바 유틸에서 기본적으로 제공하기때문에 상관 없었지만 우리는 logback 라이브러리를 사용하였기때문에 해당 의존성들을 classpath로 추가해주어야한다. 다음과 같이 입력해보자

```c
> javac -cp lib\logback-classic-1.2.3.jar;lib\logback-core-1.2.3.jar;lib\slf4j-api-1.7.30.jar com\example\demo\Main.java
```
해당 라이브러리들을 클래스패스로 등록하고 컴파일한다. 이후

```c
java -cp lib\logback-classic-1.2.3.jar;lib\logback-core-1.2.3.jar;lib\slf4j-api-1.7.30.jar;. com.example.demo.Main
```
다음과 같이 실행 시 `03:42:58.346 [main] INFO com.example.demo.Main - Hello World!!` 와 같이 현재 시간을 포함한 문구가 뜨면 성공이다. 마지막 관문이 남았다. 이쯤되면 maven이 왜 필요할지 알것 같기도 하지만 의존성을 포함하여 jar로 압축하는 것까지는 끝내보자.

먼저 manifest.txt 파일의 Main-Class 밑에 다음 문장을 추가하자.
`Class-Path: lib\logback-classic-1.2.3.jar lib\logback-core-1.2.3.jar lib\slf4j-api-1.7.30.jar`

cmd에 다음과 같이 작성하자.
```c
> jar -c -m manifest.txt -f test.jar com\*
//에러 없이 잘 압축되면 다음 명령어 실행
> java -jar test.jar
```

오랜만에 IDE를 사용하지 않고 자바를 컴파일하니 기억나지 않는 부분이 많아 이곳 저곳 찾아본것 같다. 다음 글에서는 maven을 사용하여 위의 과정을 메이븐으로 빌드하여 얼마나 간편한지 느껴보도록 하자. 본인도 글을 쓰면서 점점 귀차니즘이 발동되어 갈 수록 내용이 산으로 갔다. 다루고 싶은 내용은 더 있지만 글로써 전달하는게 이렇게 어려운 일인가 싶다..ㅎ



