---
title: JAVA - 12. static 변수와 메소드
thumbnail: https://github.com/gojaebeom/hexo-blog-server/blob/master/themes/icarus/source/images/%EC%9E%90%EB%B0%94/java-thumbnail.jpg?raw=true
author: JaeBeom Go
date: 2020-04-29 20:20:00
tags:
  - 자바
  - static
categories:
  - 웹 개발
  - java 객체지향
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

## static 변수
static 변수는 클래스를 설계할 때, 멤버변수 중 모든 인스턴스에 공통적으로 사용해야하는 것에 static을 붙인다. 인스턴스를 생성하면, 각 인스턴스들은 서로 독립적기 때문에 서로 다른 값을 유지하게된다. 경우에 따라서는 각 인스턴스들이 공통적으로 같은 값이 유지되어야 하는 경우가 있는데 이때 static 변수를 사용하면 된다. 다음 예제를 보자.

```java
public class Student{
    private int studentId;
    private String studentName;

    public Student(int studentId, String studentName){
        this.studentId = studentId;
        this.studentName = studentName;
    }
}

public class StudentTest{
    public static void main(String[] args){
        Student student1 = new Student(1, "jaebeom");
        Student student2 = new Student(2, "jongwon");
    }
}
```
이전에 다루었던 학생 클래스이다. 위와 같이 학생을 식별하기위한 학생번호라는 속성을 주고 사용자가 직접 학생번호를 입력하고있다. 위와 같은 상황에 일어날 수 있는 일이 무엇이 있을까?

먼저 값을 하나하나 입력하기때문에 학생이 1000명일 경우 1부터 1000까지 직접 입력해야한다. 그리고 사용자가 직접 번호를 적다보면 잘못 입력하여 중복되는 값들이 생길 수 있다. 이것은 치명적인 문제가 될 것 이다. 이것을 개선한 다음 예제를 보자.

```java
public class Student{

    private static int serialNum = 0;
    private int studentId;
    private String studentName;

    public Student(String studentName){
        this.studentName = studentName;
        serialNum++;
        studentId = serialNum;
    }
}

public class StudentTest{
    public static void main(String[] args){
        Student student1 = new Student("jaebeom");
        student1.showStudentInfo();

        Student student2 = new Student("jongwon");
        student2.showStudentInfo();
    }
}
```
Student 클래스의 속성으로 `serialNum` 이라는 static 변수(클래스 변수)가 추가되었다. 그리고 생성자가 호출될때마다 `serialNum`의 값을 1씩 증가시키고 `studentId`에 그 값을 할당하고있다. 위의 코드를 메모리의 구조와 연관 지어보면 다음과 같이 될 것 이다.