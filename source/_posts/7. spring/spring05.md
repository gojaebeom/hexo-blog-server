---
title: Annotation으로 Bean 등록하기

thumbnail: images/spring/thumbnail.png
date: 2020-06-25 03:39:00

tags: 
- spring
- spring bean


category:
- 자바 튜토리얼
- 4. spring

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

어노테이션으로 스프링 빈들을 관리할 경우 `@ComponentScan` 을 지정한 클래스에서 관리를 할 수 있지만, 먼저 이전에 다루었던 xml 파일에서 하나씩 어노테이션으로 바꾸면서 알아가 보도록 하겠다.
<!-- more -->

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

  <!-- Exam exam = new Exam();  -->
  <bean id="exam" class="spring.di.entity.Exam">
    <!-- 오버로드 생성자를 통해 주입 -->
    <constructor-arg value="30"/>
    <constructor-arg value="40"/>
    <constructor-arg value="20"/>
    <constructor-arg value="20"/>
  </bean> 

  <!-- ExamConsole console = new InlinExamConsole();  -->
  <bean id="console" class="xml.spring.di.ui.InlineExamConsole">
    <!-- 오버로드 생성자를 통해 주입 -->
    <constructor-arg name="exam" ref="exam" />
  </bean>
</beans>
```

이전의 xml 파일 내용이다. 먼저 Exam객체에서 일반 자료형의 값을 주입 받고 있는데 과감하게 위의 부분은 지우도록 한다. 그리고 다음과 같이 `<context:annotation-config/>`을 명시해준다. context 네임스페이스를 사용하기 위해선 상단의 빈의 속성에 `xmlns:context="http://www.springframework.org/schema/context"`를 명시해 주어야 한다.
```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
xmlns:context="http://www.springframework.org/schema/context"
xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

<!-- 등록한 객체들에게 어노테이션이 있는지 확인 하라는 네임스페이스 -->
<context:annotation-config/>

  <!-- Exam exam = new Exam();  -->
  <!-- 과목의 점수를 오버로드 생성자로 받는 부분이 사라짐 -->
  <bean id="exam" class="spring.di.entity.Exam"/>

  <!-- ExamConsole console = new InlinExamConsole();  -->
  <bean id="console" class="xml.spring.di.ui.InlineExamConsole">
    <!-- 오버로드 생성자를 통해 주입 -->
    <constructor-arg name="exam" ref="exam" />
  </bean>
</beans>
```
각 과목의 점수를 받는 부분이 사라졌다 위의 값은 어떻게 받을 수 있을까?

## @Value 어노테이션
Exam.java 파일의 맴버변수들에 `value` 어노테이션을 통해 위 xml 부분을 대체할 수 있다.
```java
import org.springframework.beans.factory.annotation.Value;

public class Exam
{
  @Value("30")
  private int kor;
  @Value("40")
  private int eng;
  @Value("40")
  private int math;
  @Value("40")
  private int com;

  ...
}
```

## @Autowired 어노테이션
- 객제의 의존성 주입을 해주는 어노테이션이다.
- 맴버변수, 생성자, setter 모두 명시해 줄 수 있다.

먼저 xml 파일에서 다시 InlineExamConsole의 생성자로 exam객체를 주입받는 부분을 제거해 준다.
```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
xmlns:context="http://www.springframework.org/schema/context"
xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

<!-- 등록한 객체들에게 어노테이션이 있는지 확인 하라는 네임스페이스 -->
<context:annotation-config/>

  <!-- Exam exam = new Exam();  -->
  <!-- 과목의 점수를 오버로드 생성자로 받는 부분이 사라짐 -->
  <bean id="exam" class="spring.di.entity.Exam"/>

  <!-- ExamConsole console = new InlinExamConsole();  -->
  <!-- exam 객체를 주입받는 오버로드 생성자 부분이 사라짐 -->
  <bean id="console" class="xml.spring.di.ui.InlineExamConsole" />
</beans>
```

그리고 다음과 같이 해당 클래스에서 의존성을 주입 받는 생성자, setter, 또는 맴버변수중 `@Autowired`를 명시해주면 된다.
```java
public class InlineExamConsole implements ExamConsole
{

  private Exam exam; //맴버변수를 통해 주입

  public ExamConsole(){}

  public ExamConsole(Exam exam) //오버로드 생성자를 통해 주입
  {
    this.exam = exam;
  }

  @Autowired //세터를 통해 주입
  public void setExam(Exam exam)
  {
    this.exam = exam;
  }
}
```

## @Component 어노테이션
이제 xml 파일에 남은 등록된 빈들을 모조리 지워주자. 그리고 `<context:component-scan base-package=""/>` 태그만 정의 해주면 되는데 설명은 다음과 같다.
```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
xmlns:context="http://www.springframework.org/schema/context"
xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

  <!-- 
  - 이 페키지 경로에 컴포넌트가 있는지 찾아달라, 있으면 객체화 시키기 
  - 만약 해당 컴포넌트를 찾을 경우, 클래스를 읽으면서 Autowired 어노테이션이 붙은
    맴버변수또는 생성자 또는 세터를 찾기때문게 굳이 annotation-config 태그를 사용할
    필요가 없다.
  -->
  <context:component-scan base-package="spring.di2.ui, spring.di2.entity"/>

</beans>
```
위와 같이 컴포넌트가 존재하는 페키지 경로를 `component-scan` 태그에 명시해 줄 경우, 해당 패키지에 @Component 어노테이션이 붙은 클래스 파일을 찾고 그 클래스에 있는 어노테이션들을 다 채크하기 때문에 이제 xml 파일에 spring bean 파일을 따로 명시해 주지 않아도 된다.

```java
@Component
public class ExamConsole implements Console{...}

@Component
public class Exam{...}
```
위와 같이 빈으로 등록할 클래스에 `@Component`를 붙여주면 된다. 이제 `spring bean configuration` 파일에는 component-scan에 대한 태그만 등록되어 있고 빈 태그들은 존재하지 않게 되었다. 하지만 bean configuration 파일에서 컴포넌트들이 있는 패키지를 명시하기 때문에 @Component 클래스를 읽을 수 있는 것 이다. 이제 완전히 어노테이션으로만 작성하려면 어떻게 해야할까? 

xml 대신 @ComponentScan을 사용하는 클래스를 만들어주고 해당 클래스에서 스프링 빈들을 생성하고 의존성을 주입할 수 있다.

## @ComponentScan
DIConfig.java
```java
@ComponentScan("spring.di.ui")
@Configuration
public class DIConfig
{
  @Bean
  public Exam exam()
  {
      return new StudyExam();
  }
}
```
Test.java
```java
public class Test
{
  public static void main(String[] args)
  {
    
    ApplicationContext context = new AnnotationConfigApplicationContext(DIConfig.class);
    
    ExamConsole console = context.getBean(ExamConsole.class);
    
    console.print();
  }
}
```




## 마무리 글
오랜만에 많은 내용을 입력하다보니, 점점 설명하는 글이 줄어들었다..
나에게 보여주는 공부 블로그이긴 하지만 혹시 나중에 이글을 보는 사람들에게 너무 부끄러운 글이다.😨

다음 글에서는 AOP 에 대한 내용을 다루어보도록 하겠다.

<br>
<hr style="border:0px; border-bottom:2px dotted #D8D8D8">

*개인적인 공부 내용을 정리하는 것을 목적으로 하고 있습니다.*
*설명이 부족하거나 틀린 부분은 지적해 주시기 바랍니다.* 🐥