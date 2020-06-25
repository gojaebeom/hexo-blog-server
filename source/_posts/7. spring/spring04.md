---
title: XML으로 Bean 등록하기

thumbnail: images/spring/thumbnail.png
date: 2020-06-24 23:27:00

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
```java
public class Test
{
  public static void main(String[] args)
  {
    Exam exam = new Exam(90, 80, 60, 50);//국어, 영어, 수학, 컴퓨터 점수를 받는다.

    //Console 인터페이스를 InlineExamConsole 클래스가 구현받음 : 다형성
    ExamConsole console = new InlineExamConsole(exam);//exam 객체를 받아 점수의 총점과 평균을 inline으로 출력한다.
  }
}
```
위 예제는 시험점수 객체에 값을 넣고 시험점수 출력 객체에 주입하는 코드의 일부분이다.
<!-- more -->

위 Exam 객체와 InlineExamConsole 객체를 스프링 빈에 등록한다고 하면, 먼저 `spring bean configuration xml` 파일을 만들어주고 그곳에 등록해주면 된다.

## configuration xml 형식
이클립스에서 관련 모듈들을 설치했다면 `spring bean configuration` 파일을 통해서 다음과 같은 파일을 만들 수 있지만, 아니라면 일반 xml 파일에 위 내용을 붙여 넣어도 된다.
```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

</beans>
```
기본 형식인 bean은 이와 같은 모습이다. 여기에 Exam과 InlineExamConsole 객체를 등록하겠다.

## spring binz 등록하기
```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

  <!-- Exam exam = new Exam();  -->
  <bean id="exam" class="spring.di.entity.Exam"/>

  <!-- ExamConsole console = new InlineExamConsole();  -->
  <bean id="console" class="spring.di.ui.InlineExamConsole"/>
</beans>
```
위와 같이 bean 태그로 id 값과 class 값을 적어준다. 
- id는 xml파일 내부에서 참조변수명과 같이 사용된다.
- class는 생성할 객체의 클래스명을 적으면 되는데, 정확하게 구분하기 위해 패키지명까지 적어주어야 한다.

## 의존성 주입하기
```java
Exam exam = new Exam(90, 80, 60, 50);
Console console = new InlineExamConsole(exam);
```
main 메서드에서 Exam 객체를 생성하고 오버로드 생성자를 통해 값들을 입력 받는다. 그후 InlineExamConsole 객체에게 오버로드 생성자를 통해 Exam 객체를 주입해주고 있는 부분이다. 다음과 같은 코드를 xml로 구현해보자.

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

### 생성자로 주입하기
- bean 파일의 닫는 태그를 분리하여 내부에 `constructor-arg` 태그를 생성했다. 
- constructor-arg는 오버로드 생성자의 매개변수를 지정한다.
- constructor-arg 1개당 매개변수 1개를 의미한다.
- constructor-arg 의 속성으로 `name`, `index`, `value`, `ref` 등이 있다.
  - name : 매개변수명으로 연결(기존의 변수명과 동일해야함)
  - index : 매개변수의 순서, 앞에서 부터 0, 1, 2 .. 
  - value : 일반 자료형이 들어갈 경우 value 속성으로 값을 입력 받는다.
  - ref : 참조 자료형을 받을 경우 ref 속성으로 값을 입력 받는다.

위 코드는 생성자로 의존성을 주입받고 있지만, setter 메서드로도 의존성 주입이 가능하다. 

### setter로 주입하기
```xml
<bean id="console" class="xml.spring.di.ui.ExamConsole">
	<property name="exam" ref="exam"/>
</bean>
```
- `property` 태그는 setter 메서드와 동일 하다.
- 당연하지만 실제 객체에 해당하는 값을 받는 setter가 정의 되어 있어야 한다.
- 일종의 규칙이 있는데 setter 메서드명이 `setExam` 과 같은 형식이라면 앞에 set을 제외하고 앞의 문자를 소문자로 바꾼다. 
- 받는 타입은 생성자와 똑같이 기본 자료형일 경우 value, 참조형일 경우 ref로 받으면 된다.

## xml 불러오기
빈의 설정이 끝났으니 main 메서드에서 이제 코드가 어떻게 바뀔지 예상해보자. 

```java
public class Test
{
  public static void main(String[] args)
  {
    ApplicationContext context = new ClassPathXmlApplicationContext("spring/di/setting1.xml");

    // bean의 id 값으로 참조 (타입캐스팅 해주어야함)
    ExamConsole console = (ExamConsole) context.getBean("console");

    // 위의 방법 또는 클래스타입으로 받을 수 있다.
    ExamConsole console = context.getBean(ExamConsole.class);
    console.print();
  }
}
```
놀라운 점은 두번째 방법으로 생성된 빈을 받을 경우 실제 받는 객체는 `InlineExamConsole` 이지만 보다시피 참조변수와 클래스타입은 ExamConsole.class 라고 되어 있다. 즉 xml에서 `ExamConsole` 인터페이스를 구현하는 클래스를 바꿔 주기만 하면 main 메서드에서는 수정할 필요 없이 구현 클래스를 분리, 조립이 가능한 것 이다.

## 마무리 글
이 밖에도 configuration xml을 다루는 설정들이 더 많지만, 이정도만 알아도(?) 기본적인 설정은 할 수 있을 것 같다.(몇개 더 알고 있지만 작성하지 않는 것도 있다😅)

다음 글에서는 어노테이션 방식으로 스프링 빈을 관리하는 방법을 알아보겠다.

<br>
<hr style="border:0px; border-bottom:2px dotted #D8D8D8">

*개인적인 공부 내용을 정리하는 것을 목적으로 하고 있습니다.*
*설명이 부족하거나 틀린 부분은 지적해 주시기 바랍니다.* 🐥