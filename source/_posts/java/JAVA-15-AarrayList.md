---
title: JAVA - 15. ArrayList
thumbnail: https://github.com/gojaebeom/hexo-blog-server/blob/master/themes/icarus/source/images/%EC%9E%90%EB%B0%94/java-thumbnail.jpg?raw=true
author: JaeBeom Go
date: 2020-04-30 21:20:00
tags:
  - 자바
  - ArrayList
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

## ArrayList
ArrayList는 순차적인 여러 값들을 저장하기 위해 자바에서 기본적으로 제공하는 자료구조중 하나이다. <!-- more -->

이전에 배웠던 배열의 특징과 비교하자면, 배열은 ArrayList에 비해 속도는 빠르지만 선언시에 크기를 정하고 한번 정한 값을 바꿀 수 없다. 즉 할당한 크기보다 값이 적게 들어가면 그만큼 공간을 낭비하는 것이고, 할당한 크기 이상의 값을 저장할 수 없기때문에 이러한 부분도 불편한점이 아닐 수 없다. 

반면 ArrayList는 속도는 배열에 비해 느리지만 값을 추가하거나 삭제함에 따라 그 크기를 유동적으로 변화시키는 장점이 있다. 이제 ArrayList를 사용하는 방법에 대하여 알아보자.

## ArrayList 사용법

### 선언 방법
```java
ArrayList list = new ArrayList();
```
기본적인 선언 방법은 위와 같다.(ArrayList는 java.util.ArrayList에 포함되어 있으므로 사용시 import 가 필요하다)

만약 VScode나 이클립스와 같은 코드 에디터를 사용하고 있다면 ArrayList에 경고줄이 떠있는 것을 볼 수 있다. ArrayList는 사용시 어떠한 데이터 타입을 넣을 것 인가 선언 시에 지정할 수 있는데, 이것은 이후에 배울 제네릭때 더 자세히 알아보자. 지금은 그냥 아래 예제와 같이 선언 한다는 것만 알아두자.

```java
ArrayList<T> list = new ArrayList<T>(); //<> 사이에 사용할 유형의 타입을 적는다.

// ex 
ArrayList<String> list = new ArrayList<String>(); // 문자열 타입만 넣을 경우

ArrayList<Integer> list = new ArrayList<Integer>(); // 정수형 타입만 넣을 경우

ArrayList<Subject> list = new ArrayList<Subject>(); // 특정 클래스형으로 사용할 경우
``` 

### 데이터 추가
```java
ArrayList<String> list = new ArrayList<String>();
list.add("hello");
list.add("world");
```

### 추가한 데이터 조회
```java
System.out.println(list.get(0));

for(int i = 0; i < list.size(); i++){
  System.out.println(list.get(i));
}

for(String str : list){
  System.out.println(str);
}
```

## ArrayList 사용 예제
이전의 학생과 과목 클래스를 정의를 하고 학생클래스에서 과목클래스를 사용한 적이 있었다.
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
}
```
과목을 별도의 클래스로 나눈것 까지는 좋았지만 과목명을 직접 정의하여 나열하고있는 것은 좋은 코드가 아닐 것 이다. 과목 수가 많아짐에 따라 서로 중복되는 코드를 가지는 메소드들을 계속 생성해야 할 것 이다.

위와 같은 단점을 ArrayList를 사용하는 것으로 리팩토링해보자.

**Subject 클래스의 정의**
```java
public class Subject{
	private String name; //과목 이름
	private int score;//과목 점수
	
	public String getName() {
		return name;
	}
	public void setName(String name) {
		this.name = name;
	}

	public int getScore() {
		return score;
	}

	public void setScore(int score) {
		this.score = score;
	}
}
```

**Student 클래스의 정의**
```java
class Student{
	private static int serialNum = 0;
	private int id;//학생 번호
	private String name;//학생 이름
	
	private ArrayList<Subject> subjectList;
	
	public Student(String name) {
		this.name = name;
		this.id = ++serialNum;
		subjectList = new ArrayList<Subject>();
	}
	
	public void addSubject(String name, int score) {
		Subject subject = new Subject();
		subject.setName(name);
		subject.setScore(score);
		subjectList.add(subject);
	}
	
	public void showStudentInfo() {
		System.out.println("학생 번호: "+ id);
		System.out.println("학생 이름: "+ name);

		if(subjectList.size() == 0) {
			System.out.println("수강중인 과목이 없습니다.");
		}else {
			int total = 0;
			for(Subject subject : subjectList) {
				total += subject.getScore();
			
				System.out.println("수강 과목 "+subject.getName() + ": "+ subject.getScore());
			}
			System.out.println("과목 총합점수는 " + total +" 이고 평균은 " + total/subjectList.size() + " 입니다." );
		}
	}
}
```
Student 클래스의 맴버변수 `private ArrayList<Subject> subjectList;` 를 선언, 그리고 생성자에서 초기화 시킨다. 예제와 같이 ArrayList는 Subject 클래스를 타입으로 받고 있다. 

그리고 `addSubject` 메소드가 호출될때마다 subject 객체를 새로 생성해 매개변수로 받은  과목이름과 과목점수를 저장시킨다. 이후에 subject 타입의 subjectList에 추가시킨다.

`showStudentInfo` 메소드는 기본적인 학생정보를 출력하고, subjectList에 값이 저장되지 않았다면 안내 문구를 출력하고 subjectList에 값이 존재하면 출력해주는 기능을 담당한다.

**StudentTest 클래스에서 테스트해보기**
```java
public class StudentTest {
	public static void main(String[] args) {
		Student studentLee = new Student("Lee");
		studentLee.addSubject("수학", 80);
		studentLee.addSubject("영어", 70);
		studentLee.showStudentInfo();
		
		System.out.println("-----------------------------------------");
		
		Student studentGo = new Student("Go");
		studentGo.addSubject("수학", 50);
		studentGo.addSubject("영어", 90);
		studentGo.addSubject("과학", 90);
		studentGo.showStudentInfo();
	}
}
```
이전의 ArrayList를 사용하지 않을때와의 차이점은 addSubject라는 메소드를 사용하여 과목을 필요한만큼 정의하여 추가하고 있다는 점이다. 이전의 코드에서 수학, 영어등의 과목명을 직접 정의하여 중복되는 코드를 계속사용하는 것을 수정하여 좀더 프로그램다운 코드가 되었다.

ArrayList는 이후의 컬랙션에서 한번더 다룰 예정이다.

