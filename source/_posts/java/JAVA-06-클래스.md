---
title: JAVA - 06. 객체지향 프로그래밍과 클래스
thumbnail: https://github.com/gojaebeom/hexo-blog-server/blob/master/themes/icarus/source/images/%EC%9E%90%EB%B0%94/thumbnail.png?raw=true
author: JaeBeom Go
date: 2020-04-27 19:08:00
tags:
  - 자바
  - 인스턴스
  - 객체
  - 클래스
  - 객체지향 프로그래밍
  - 힙
  - 메모리 구조
categories:
  - 웹 개발
  - java
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
## 객체지향 프로그래밍(Object Oriented Programming )이란?
객체지향은 프로그램 설계방법론중 하나 이다. 프로그램을 수많은 '객체'라는 기본 단위로 나누고 이 객체들의 상호작용으로 서술하는 방식이다. 
<!-- more -->

## 객체(Object) 란?
객체란 물리적으로 존재하거나 추상적으로 생각할 수 있는 것 중에서 자신의 속성을 가지고 있고 다른것과 식별 가능한 것을 의미한다.

## 클래스(Class) 란?
클래스는 객체지향 프로그래밍의 가장 기본적인 요소이며, '속성(변수)과 기능(메소드)'의 묶음으로 나뉜다. 그리고 객체를 생성하기 위한 설계도라고 할 수 있다. 

클래스와 객체가 햇갈리는 부분이 있을 수 있는데 클래스는 '설계도', 객체는 '설계도로 구현한 모든 대상'을 의미한다. 다음 예제를 보자.

### 클래스 정의하기
```java
public class Student {
    //맴버변수
	int studentId;
	String studentName;
    
    //메소드
    public void showStudentInfo(){
    	//학생 정보 출력
    }
}
```
위 예제는 학생을 추상화 한 Student 클래스의 정의 이다. 클래스는 정의 할때 다음과 같은 규칙이 있다.

- 이름의 앞글자는 대문자를 사용(일반적인 관례)
- 클래스명은 파일명과 같아야 하고 public 키워드가 붙어야 한다.
(한 java 파일 안에 여러 클래스를 정의하는 것은 가능하지만 파일명과 같은 클래스만 public 키워드를 붙일 수 있다)

위에도 언급하였지만, 클래스를 설계할 때 클래스는 속성과 기능의 묶음이고, 그 클래스로 부터 생성될 객체들은 서로 식별이 가능하도록 설계해야 한다. 그래서 맴버변수에 각 학생들이 식별될 수 있는 고유번호 studentNum을 만든 것을 알 수 있다.

위 Student 클래스는 정의만 하였고 사용되지 않았다. 이를 사용하는 예제를 보자.


### 클래스 사용하기
```java
public class StudentTest {
	public static void main(String[] args) {

		Student studentLee = new Student();
        studentLee.studentId = 1;
        studentLee.studentName = "이형석";
     	studentLee.showStudentInfo();
        
		Student studentKim = new Student();
        studentKim.studentId = 2;
        studentKim.studentName = "김종원";
        studentKim.showStudentInfo();
	}
}
```
Student 클래스는 `new Student()`라는 선언을 통해 비로소 `Student 객체`로 생성된 것이다.(객체의 생성을 '인스턴스화 되었다' 라고 불리기도 한다) 그리고 Student 객체를 사용하기 위해 `Student 타입`의 studentLee 라는 참조 변수로 참조하고 있는 것을 볼 수 있다.(객체를 참조한다고 하였는데, 정확한 뜻은 객체의 주솟값을 참조하고 있는 것 이다)

이처럼 정의한 클래스를 객체로 생성할 때는 `new` 키워드를 통해 생성할 수 있다. 이때 '객체를 생성한다' 또는 '인스턴스화 한다'라고 한다. 

그리고 위의 예제에서 전달하고자 하는 다른 부분은 똑같은 Student 클래스의 객체를 참조하는 studentLee와 studentKim은 서로 다른 객체라는 것 이다. 두 객체는 서로 다른 공간에 생성되어 다른 주소 값을 가지는 것을 알아두자.

## 인스턴스(Instance), 메모리 힙(Heap)

![메모리 구조](https://github.com/gojaebeom/hexo-blog-server/blob/master/themes/icarus/source/images/%EC%9E%90%EB%B0%94/%EB%A9%94%EB%AA%A8%EB%A6%AC%EA%B5%AC%EC%A1%B0.png?raw=true)

위 사진은 메모리의 구조를 나타낸다.

위 예제와 같이 새로운 객체를 생성하게 되면
```java
new Student();
```
메모리의 힙이란 곳에 새로운 인스턴스가 만들어진다. (그래서 객체는 인스턴스라 불리기도 한다) 우리는 이것을 인스턴스화 한다라고 하고, 이 인스턴스는 자신의 주소 값을 가지고있다.
```java
new Student();  // ex) 3fb6a447
```

그리고 참조 변수는 이 인스턴스(객체)의 주소 값을 참조받는 것 이다.
```java
Student student = new Student(); // 3fb6a447 라는 주소 값을 참조한다.
```

조금 더 살을 붙이자면 이렇듯 new 로 생성된 인스턴스들은 각자 다른 공간에 만들어지고 주솟값도 다르기때문에, 같은 클래스로 만들어진 인스턴트들은 서로 다르다고 할 수 있다.
```java
new Student();// 객체 1, 주소 값 ex) 3fb6a447
new Student();// 객체 2, 주소 값 ex) 79b4d0f
```

*그리고 힙 영역은 프로그래머가 관리해야하는 영역이다. 생성된 객체가 사용되지 않으면 메모리에서 제거해주어야하는데, 자바는 가비지 컬랙터(Garbage Collector)가 필요한 타이밍에 알아서 관리해준다.*

메모리 구조에 관한 내용은 원래 더욱 복잡한데, 다른 글에서 자세히 다루도록 하겠다.