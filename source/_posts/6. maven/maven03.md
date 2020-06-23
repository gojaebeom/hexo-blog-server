---
title: POM.xml

thumbnail: images/maven/thumbnail.png
date: 2020-06-17 19:09:00

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

pom은 project object model의 약자로써 메이븐은 pom에 기술된 내용을 바탕으로 빌드를 진행한다. 즉 pom은 maven에서 사용하는 빌드 파일이다.
<!-- more -->
아래의 코드는 이전 글의 메이븐 생성하기에서 만든 프로젝트의 pom.xml을 열었을 때 볼 수 있는 내용이다.
```xml
<?xml version="1.0" encoding="UTF-8"?>

<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <groupId>com.example</groupId>
  <artifactId>demo</artifactId>
  <version>1.0-SNAPSHOT</version>

  <name>demo</name>
  <!-- FIXME change it to the project's website -->
  <url>http://www.example.com</url>

  <properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <maven.compiler.source>1.7</maven.compiler.source>
    <maven.compiler.target>1.7</maven.compiler.target>
  </properties>

  <dependencies>
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>4.11</version>
      <scope>test</scope>
    </dependency>
  </dependencies>

  <build>
    <pluginManagement><!-- lock down plugins versions to avoid using Maven defaults (may be moved to parent pom) -->
      <plugins>
        <!-- clean lifecycle, see https://maven.apache.org/ref/current/maven-core/lifecycles.html#clean_Lifecycle -->
        <plugin>
          <artifactId>maven-clean-plugin</artifactId>
          <version>3.1.0</version>
        </plugin>
        <!-- default lifecycle, jar packaging: see https://maven.apache.org/ref/current/maven-core/default-bindings.html#Plugin_bindings_for_jar_packaging -->
        <plugin>
          <artifactId>maven-resources-plugin</artifactId>
          <version>3.0.2</version>
        </plugin>
        <plugin>
          <artifactId>maven-compiler-plugin</artifactId>
          <version>3.8.0</version>
        </plugin>
        <plugin>
          <artifactId>maven-surefire-plugin</artifactId>
          <version>2.22.1</version>
        </plugin>
        <plugin>
          <artifactId>maven-jar-plugin</artifactId>
          <version>3.0.2</version>
        </plugin>
        <plugin>
          <artifactId>maven-install-plugin</artifactId>
          <version>2.5.2</version>
        </plugin>
        <plugin>
          <artifactId>maven-deploy-plugin</artifactId>
          <version>2.8.2</version>
        </plugin>
        <!-- site lifecycle, see https://maven.apache.org/ref/current/maven-core/lifecycles.html#site_Lifecycle -->
        <plugin>
          <artifactId>maven-site-plugin</artifactId>
          <version>3.7.1</version>
        </plugin>
        <plugin>
          <artifactId>maven-project-info-reports-plugin</artifactId>
          <version>3.0.0</version>
        </plugin>
      </plugins>
    </pluginManagement>
  </build>
</project>
```

뭔가 내용들이 많은데 간단하게 요약하자면 다음과 같다.

```xml
<?xml version="1.0" encoding="UTF-8"?>

<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">

  <!-- 필수 : 프로젝트 정보 기재 -->
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.example</groupId>
  <artifactId>demo</artifactId>
  <version>1.0-SNAPSHOT</version>
  <name>demo</name>
  <url>http://www.example.com</url>

  <!-- 선택 : 프로젝트에 대한 설명란 -->
  <description>demo project!</description>

  <!-- 선택 : pom.xml에서 공통적으로 사용할 버전, 설정 정보 -->
  <properties>
        <!-- 각 dependency에 지정할 값들을 properties에 써두고
             변수처럼 활용할 수 있음. 
             밑의 servelt.version 태그는 사용자가 임의로 지정한것
             이후의 dependency에서 사용하는 것을 보자
         -->
        <servlet.version>3.0.1</servlet.version>
  </properties>

  <!-- 선택: 의존성 설정은 선택이지만 
       메이븐의 주 사용이유인 만큼 필수적으로 사용된다.
   -->
  <dependencies>
    <!-- dependencies안에 dependency로 구분지어 라이브러리를 추가할 수 있다 -->
    <dependency>
        <groupId>javax.servlet</groupId>
        <artifactId>javax.servlet-api</artifactId>
        <!-- properties에 작성해 놓은 servlet.version 태그의 값을 사용함 -->
        <version>${servlet.version}</version>
    </dependency>
  </dependencies>

  <!-- 필수내용 : 프로젝트 build 정보 기재 -->
  <build>

    <!-- 선택사항 : resource 파일의 경로를 지정할 수 있음 -->
    <resources>
        <resource>
            <directory>src/main/webapp</directory>
        </resource>
    </resources>

    <!-- 선택사항 : maven의 라이프사이클을 개별의 플러그인으로 관리함으로써 
    필요한 부분만 넣어 사용할 수 있다.
     -->
    <plugin>
        <artifactId>maven-resources-plugin</artifactId>
        <version>3.0.2</version>
    </plugin>
  </build>
</project>
```

이 밖에 다른 기술들도 많이 있겠지만 기본 틀만 잡아놓고 이 후에 필요시 찾아볼 생각이다. 

## project 기본정보
보통 상단에 
modelVersion, groupId, artifactId, version, name, url를 기재하는데 필수적이다. 추가로 프로젝트에 관한 설명을 적기위해 description 속성을 추가할 수 있다.

## properties
- 프로젝트의 주요 설정들을 쉽게 모아보기 위해 정리한다. 
- pom.xml 내에서 자주 사용되는 정보들을 변수처럼 만들어서 사용할 수 있다.

## dependency 관리
pom.xml을 자주 들락날락 거리게 만들 이유이다. maven을 통해 불러온 라이브러리들은 java built path에서 maven dependencies 하위 목록으로 들어가게 된다. 그리고 그것들은 pom.xml을 통해서만 추가, 삭제, 버전 변경 등을 할 수 있다. 

해당 경로에 추가된 라이브러리가 필요한 다른 라이브러리들이 있다면 해당하는 라이브러리까지 참조해서 불러들이는 기능이 있다. 이것을 의존성 전의라 한다.

### dependency태그 속성
- groupId : 필수, 라이브러리의 그룹명을 적는다.
- artifactId : 필수, 라이브러리의 이름을 적는다.
- version: 필수? 라이브러리의 버전을 적는다.
- type : 선택, 라이브러리의 유형을 적는다. defulat값은 jar이다.
- scope : 라이브러리가 적용될 범위를 지정할 수 있다.
    - compile(default): 모든 클래스 경로에서 사용할 수 있음. 컴파일 및 배포시 같이 재공
    - provided : jdk 또는 컨테이너가 런타임 시에만 해당 라이브러리를 제공. 컴파일 혹은 테스트 경로에서만 사용할 수 있다.
    - test : 태스트 시에만 해당 라이브러리를 사용한다.
    - system : 저장소에서 관리되지 않고 직접 관리하는 jar를 추가함
- optional : 선택, 의존성 정보를 다른 프로젝트에 전달하고 싶지 않을 때 true로 설정하자. 

## build
빌드할 때 사용할 플러그인 목록을 기록할 수 있다. 그밖에 build 속성 내부에 resources 속성을 추가해 정적파일 경로를 설정할 수 있다.

정리랍시고 했지만 귀찮아서 생략한 부분도 많다.. https://maven.apache.org/guides/getting-started/index.html#How_do_I_setup_Maven <-- 공식 홈페이지 문서이다. 글쓴이는 영어를 잘 못해 번역으로 돌려놓고 이해하려고 애쓰는데 영어 잘하시는 분들은 가서 보길 바란다. 설명 정말 잘 되어있다..