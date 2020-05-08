---
title: JAVA - 09. 참조 자료형
thumbnail: https://github.com/gojaebeom/hexo-blog-server/blob/master/themes/icarus/source/images/%EC%9E%90%EB%B0%94/java-thumbnail.jpg?raw=true
author: JaeBeom Go
date: 2020-04-27 19:20:00
tags:
  - 자바
  - 참조 자료형
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

## 참조 자료형(Reference Data Type)
처음 자바에 대한 글을 작성할때 변수와 자료형에 대해 알아보았다.<!-- more --> 그리고 자료형에는 기본 자료형과 참조 자료형이 있다고 하였다. 참조형에 대해선 그 당시에 다루지 않았는데, 참조 자료형은 클래스에 대한 기본적인 지식을 가지고 있어야 이해하기 편하다고 생각하였다. 

참조 자료형은 자료형이 클래스이다. 우리가 자주 사용하는 String, 그리고 우리가 직접 정의한 Student 클래스도 참조 자료형이 될 수 있다. 기본 자료형은 int, char, double, boolean 과 같이 그 크기가 이미 정해져 있지만, 참조자료형은 참조하는 클래스에 따라 그 크기가 다르다. 

## 참조 자료형 사용 예제
이전에 학생 클래스를 만들어 학생의 고유번호와 이름을 받아 학생의 정보를 보여주는 일을 하는 클래스를 정의하였다. 

```java
public class StudentTest{
    public static void main(String[] args){
        Student studentGo = new Student();
    }
}
```
그리고 만든 학생 클래스를 객체로 생성하여 위와 같이 참조변수에 할당하였다. 이렇듯 참조변수를 main 메소드 안에서만 정의 하였는데, 참조변수는 클래스의 내부에 맴버변수로써도 사용할 수 있다. 

학생 클래스를 만들었으니 학생마다 수강하는 과목을 만들고 싶다. 그리고 그 과목에 대한 점수도 받고싶다. 그렇다면 다음과 같이 작성하면 될까?

```java
public class Student{
    int studentId;
    String studentName;

    String subjectEng;//영어
    int subjectEngScore;//영어점수
    String subjectMath;//수학
    int subjeectMathScore;//수학점수
    ...
}
```
위와 같이 과목을 하나하나 적는 것은 비효율 적일 것 같다. 게다가 과목이 갖는 점수 역시 따로 명시해주어야 한다. 우리는 위의 클래스를 Student 라 정의 하였다. 여기서 알 수 있는 것은 학생에 관련된 클래스라는 것 이다. 그렇다면 과목에 관련된 클래스 역시 따로 정의 할 수 있지 않을까? 한번 과목 클래스를 만들어보자.

```java
public class Subject{
    int subjectId;//과목 번호
    String sbujectName;//과목 이름
    int subjectScore;//과목 점수
}
```

위와 같이 따로 과목에 대한 클래스를 정의할 수 있다. 그렇다면 학생 클래스에서 이 과목 클래스를 가져와 사용하는 예를 보자.
```java
public class Student{
    int studentId;
    String studentName;

    //Subject형 참조변수
    Subject eng;
    Subject math;

    Student(int id, String name){
        studentId = id;
        studentName = name;
        Subject eng = new Subject();
        Subject math = new Subject();
    }
}
```
Subject 타입의 참조변수 eng와 math를 맴버변수로 선언한 뒤, 학생 객체의 생성자가 호출될때 동시에 Subject 객체가 생성되고 참조값을 참조하게 된다. 이로써 Student 객체가 생성이 되면 Subject 객체도 같이 생성되는것을 알 수 있다. (사실 위의 Subject를 통해 과목을 직접 나누는 것도 좋은 예는 아니지만 우리는 아직 배열과 리스트를 배우지 않았기 때문에 일단은 위와 같이 작성하자) 
```java
public class Student{
    ...

    void setEngSubject(int id, String name, int score) {
        eng.subjectId = id;
        eng.subjectName = name;
        eng.subjectScore = score;
    }

    void setMathSubject(int id, String name, int score) {
        math.subjectId = id;
        math.subjectName = name;
        math.subjectScore = score;
    }

    void showStudentScore() {
        System.out.println("학생번호:"+studentId);
        System.out.println("학생이름:"+studentName);
    
        System.out.println("과목1:"+eng.subjectName);
        System.out.println("점수:"+eng.subjectScore);

        System.out.println("과목2:"+math.subjectName);
        System.out.println("점수:"+math.subjectScore);

        System.out.println("총 점수"+(eng.subjectScore + math.subjectScore));
    }
}
```
그리고 Subject를 참조하긴 했지만, 과목번호와 , 과목이름, 과목점수등을 설정하지 않았기때문에 과목의 정보를 입력할 수 있는 메소드와, 학생정보 그리고 수강과목점수등을 보여주는 메소드를 만들었다. 이제 StudentTest에서 Student 객체를 생성하여 사용해보자.

```java
public class StudentTest {
    public static void main(String[] args) {

        Student sJaebeom = new Student(1, "재범");
        sJaebeom.setEngSubject(1, "영어", 50);
        sJaebeom.setMathSubject(2, "수학", 30);
        sJaebeom.showStudentScore();

        System.out.println();

        Student sJongwon = new Student(2, "종원");
        sJongwon.setEngSubject(1, "영어", 40);
        sJongwon.setMathSubject(2, "수학", 70);
        sJongwon.showStudentScore();
    }
}
```

StudentTest 클래스에서 테스트해보면 위와 같이 작성할 수 있다. 이번 글의 주제는 참조변수이지만, 참조변수를 다른 클래스에서 사용하여 객체끼리 상호작용을 하는 예제를 살짝 다루었다. 객체지향적인 프로그래밍은 이와 같이 서로 다른 객체가 맞물려서 작동하는 프로그램을 나타낸다.