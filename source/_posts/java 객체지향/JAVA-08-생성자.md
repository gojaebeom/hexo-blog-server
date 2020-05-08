---
title: JAVA - 08. 생성자
thumbnail: https://github.com/gojaebeom/hexo-blog-server/blob/master/themes/icarus/source/images/%EC%9E%90%EB%B0%94/java-thumbnail.jpg?raw=true
author: JaeBeom Go
date: 2020-04-27 19:15:00
tags:
  - 자바
  - 생성자
  - 생성자 오버로딩
categories:
  - 웹 개발
  - java
toc: true
widgets:
  - type: toc
    position: right
  - type: category
    position: right
  - type: tagcloud
    position: right
sidebar:
  right:
    sticky: true
---

## 생성자(Constructor)란 무엇인가?
우리는 이미 생성자를 한번 사용한 적이 있다. 객체를 생성할 때 `new` 키워드 다음에 선언한 `클래스명()` 이 생성자 이다. <!-- more -->
```java
new Example();
```

### 생성자 만들기
생성자는 클래스명과 동일해야한다. 그리고 반환형도 없고 (이후에 배울)상속되지도 않는다. 생성자는 다음과 같이 선언할 수 있다. 

```java
public class Example{
    //생성자
    Example(){...}
}
```
자바에서 클래스를 만들때 내부적으로 반드시 하나 이상의 생성자를 만들어야 하는 규칙이있다. 그런데 우리는 위와같이 생성자를 구현한 적이 없다. 그렇다면 지금까지 만든 클래스는 생성자가 없었는데 규칙을 어겼던 것일까?

자바는 컴파일을 할때 class에 생성자가 정의되어 있지않으면 디폴트 생성자(Default Constructor)라는 것을 만들어준다. 위와 같이 내용이 비어있는 빈껍대기인 생성자이다. 내부적으로 구현된 코드는 없지만 이로써 생성자를 하나 이상 만들어야 하는 규칙은 지켜지는 것 이다.

## 생성자의 사용
생성자는 메소드와 같이 필요할 때 바로바로 호출하여 사용할 수 있는 것은 아니다. 생성자는 객체를 생성할때에만 호출이되며, 주로 맴버변수의 값을 초기와하는 역할을 한다. 다음 예제를 보자

```java
class Student{
    int studentId;
    String studentName;

    void showStudentInfo(){
        System.out.println("학생번호:"+studentId);
        System.out.println("학생이름:"+studentName);
    }
}

class StudentTest{
    public static void main(String[] args){
        Student student = new Student();
        student.studentId = 1;
        student.studentName = "jaebeom";

        student.showStudentInfo();
    }
}
```
위의 예제에선 Student 객체를 생성한 이후 맴버변수에 접근하여 값을 넣고 학생정보를 보이고 있다. 하지만 생성이후 저렇게 정보를 보이기 위해 변수에 하나하나 값을 넣는 것은 비효율적으로 보인다. 그리고 이후에 나오는 '정보은닉'관점에서도 저 방법은 좋은 예제는 아니다. 이제 다음 예제를 보자

```java
class Student{
    int studentId;
    String studentName;

    Student(int id, String name){
        studentId = id;
        studentName = name;
    }

    void showStudentInfo(){
        System.out.println("학생번호:"+studentId);
        System.out.println("학생이름:"+studentName);
    }
}

class StudentTest{
    public static void main(String[] args){
        Student student = new Student(1, "jaebeom");
        student.showStudentInfo();
    }
}
```

위 예제는 생성자를 직접 정의하여 객체 생성 당시에 학생번호와 학생이름을 매개변수로 받아 맴버변수들을 초기화하는 예제이다. 불필요하게 맴버변수들을 불러와 값을 할당할 필요가 없어진 것 이다. 

여기서 한가지 궁금한 적이 있다. 우리가 생성자를 직접 정의하였는데, 그렇다면 아무런 매개변수를 받지 않는 디폴트 생성자는 그대로 존재하는가? 결론은 '존재하지 않는다' 이다. 우리가 직접 생성자를 정의하게되면 디폴트 생성자는 생성되지 않는다. 

```java
class StudentTest{
    public static void main(String[] args){
        new Student(1, "jaebeom"); 
        new Student();//에러
    }
}
```
이전의 Student 클래스의 생성자를 정의했다고 가정하고 위와 같이 작성해보면, 매개변수를 받지 않는 생성자가 호출될 때 에러가 나는 것을 알 수 있다. 우리가 매개변수를 받지 않는 생성자를 정의하지 않았기 때문이다.

## 생성자 오버로딩(Overloading)
생성자 오버로딩은 생성자의 이름을 같게 하고 매개변수의 수, 그리고 타입에 따라 여러개의 생성자를 만들어 내는 것을 말한다. (오버로딩은 이후의 메소드 오버로딩때 자세히 다루도록 한다)

예제를 살펴보자.
```java
class Student{

    Student(){...}

    Student(String name){...}

    Student(String name, int id){...}
}
```

위와 같이 똑같은 이름인 생성자들이 매개변수의 수, 그리고 타입에 따라 여러개를 정의하게 가능한 것을 알 수 있다. 즉 이전 예제인 Student 객체의 생성자 호출 문제는 다음과 같이 해결할 수 있다.

```java
class Student{
    int studentId;
    String studentName;

    Student(){}

    Student(int id, String name){
        studentId = id;
        studentName = name;
    }

    void showStudentInfo(){
        System.out.println("학생번호:"+studentId);
        System.out.println("학생이름:"+studentName);
    }
}

class StudentTest{
    public static void main(String[] args){
        Student student1 = new Student(1, "jaebeom");
        student.showStudentInfo();

        Student student2 = new Student();
        
    }
}
```
아무런 매개변수를 받지 않는 생성자도 따로 정의하여 문제없이 호출하는 것을 알 수 있다. 이것이 생성자 오버로딩이 필요한 이유이다.