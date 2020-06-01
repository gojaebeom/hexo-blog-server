---
title: JAVA - 12. static 변수와 메소드
thumbnail: https://github.com/gojaebeom/hexo-blog-server/blob/master/themes/icarus/source/images/%EC%9E%90%EB%B0%94/thumbnail.png?raw=true
author: JaeBeom Go
date: 2020-04-29 20:20:00
tags:
  - 자바
  - static
categories:
  - 자바 튜토리얼
  - 1. java
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

## static 변수
static 변수는 클래스를 설계할 때, 멤버변수 중 모든 인스턴스에 공통적으로 사용해야하는 것에 static을 붙인다.<!-- more --> 인스턴스를 생성하면, 각 인스턴스들은 서로 독립적기 때문에 서로 다른 값을 유지하게된다. 경우에 따라서는 각 인스턴스들이 공통적으로 같은 값이 유지되어야 하는 경우가 있는데 이때 static 변수를 사용하면 된다. 다음 예제를 보자.

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
Student 클래스의 속성으로 `serialNum` 이라는 static 변수(클래스 변수)가 추가되었다. 그리고 생성자가 호출될때마다 `serialNum`의 값을 1씩 증가시키고 `studentId`에 그 값을 할당하고있다. 위의 코드를 메모리 상태와 연관 지어보면 다음과 같이 될 것 이다.

![이미지](https://github.com/gojaebeom/hexo-blog-server/blob/master/themes/icarus/source/images/%EC%9E%90%EB%B0%94/static.png?raw=true)

위의 두 `student1`, `student2` 참조변수는 서로 다른 인스턴트를 참조하고 있기 때문에 맴버변수 또한 서로 다른 메모리를 사용한다. 하지만 static 변수는 선언 시 메모리 영역에 따로 할당이 되기때문에 Student 클래스를 통해 생성된 모든 인스턴트들은 이 값을 모두 공유하게 되는 것이다.

결론적으로 static 변수가 모든 인스턴스에 공유되는 특징을 이용하여 사용자가 직접 학생번호를 입력하지 않고도 생성자가 호출될 때 마다 알아서 학생의 번호가 증가되게 만들었다. 이렇듯 static 변수는 객체가 공유해야하는 값을 필요로 할 때 사용할 수 있다.

## static 변수 접근 방법
static 변수도 '접근 수준 지시자' 의 규칙을 그대로 적용받기 때문에 public으로 선언되면 어디서든 접근이 가능하다. 물론 접근 방법에 있어서는 차이를 보이는데 이와 관련된 내용은 이어서 설명하겠다.

static 변수에 접근하는 방법은 접근 영역을 기준으로 다음과 같이 크게 두 가지로 나뉜다.
- 클래스 내부 접근 : 변수의 이름을 통해 직접 접근
- 클래스 외부 접근 : 클래스 또는 인스턴스의 이름을 통해 접근

다음예제를 보면서 static 변수의 접근 방법을 알아보자.
```java
class AccessWay{
	static int num = 0;
	
	AccessWay(){
		incrCnt();
	}
	
	void incrCnt() {
		num++; //클래스 내부에서 이름을 통한 접근
	}
}

public class AccessWayTest{
	public static void main(String[] args) {
		AccessWay way = new AccessWay();
		way.num++; //외부에서 인스턴스의 이름을 통한 접근
		AccessWay.num++; //외부에서 클래스의 이름을 통한 접근
		System.out.println("num = " + AccessWay.num);// 총 3이 찍힌다.
		
		AccessWay way2 = new AccessWay();//way2라는 새로운 AccessWay의 인스턴스를 생성하였다.
		System.out.println(way2.num);//그리고 way2의 클래스변수 num을 조회 하였는데 값은 4가 찍힌다.
	}
}
```
인스턴스의 이름을 통한 접근 방법을 보면서, static 변수를 인스턴스 내부에 위치한 것으로 오해하면 안된다. 그리고 static 변수 num은 default로 선언되었다. 따라서 클래스 내부는 물론 클래스 외부이더라도 동일 패키지로 묶여 있으면 접근이 가능하다.

## 인스턴트 변수(맴버 변수)와 static 변수(클래스 변수)의 차이
### 맴버 변수
- 공간적 특성: 인스턴트 변수는 객체마다 별도로 존재한다.
인스턴스 멤버 라고 부른다.
- 시간적 특성: 객체 생성 시에 인스턴트 변수가 생성된다.
    - 객체가 생길 때 인스턴트 변수도 생성된다.
    - 객체 생성 후 인스턴트 변수 사용이 가능하다.
    - 객체가 사라지면 인스턴트 변수도 사라진다.
- 공유의 특성: 공유되지 않는다.
    - 인스턴트 변수는 객체 내에 각각의 공간을 유지한다.

### static 변수
- 공간적 특성: static 변수는 클래스당 하나가 생성된다.
    - static 변수는 객체 내부가 아닌 별도의 공간에 생성된다.
- 시간적 특성: 클래스 로딩 시에 static 변수가 생성된다.
    - 객체가 생기기 전에 이미 생성된다.
    - 객체가 생기기 전에도 사용이 가능하다. (객체를 생성하지 않고도 사용할 수 있다)
    - 객체가 사라져도 static 변수는 사라지지 않는다.
    - static 변수는 프로그램이 종료될 때 사라진다.
- 공유의 특성: 동일한 클래스의 모든 객체들에 의해 공유된다.

### 클래스로딩
앞서 설명에서 static 변수는 클래스 로딩시 생성된다고 하였는데, 이렇듯 가상머신이 특정 클래스 정보를 읽는 행위를 가리켜 클래스 로딩 이라 한다. 그리고 특정 클래스의 인스턴스 생성을 위해서는 해당 클래스가 반드시 가상머신에 의해 로딩되어야 한다. 즉 인스턴스 생성보다 클래스 로딩이 먼저이다.

## static 메소드
클래스 내에 정의된 메소드에 static 선언을 하면 static 메소드(클래스 메소드)가 된다. 그리고 static 메소드는 그 성격이 static 변수와 유사하다. 접근 방법도 동일하며 인스턴스 생성 이전부터 호출이 가능한, 그리고 어느 인스턴스에도 속하지 않는 메소드라는 점도 static 변수와 동일하다.

### static 메소드의 정의와 호출
static 변수의 특성 두 가지는 다음과 같다.
- 인스턴스 생성 이전부터 접근이 가능하다.
- 어느 인스턴스에도 속하지 않는다.

이 두 가지는 static 메소드도 동일하게 갖는 특성이다. 따라서 이 사실을 다음 예제를 통해서 확인해보겠다.
```java
public class NumberPrinter{
	private int myNum = 0;
	
	static void showInt(int n) {//static 메소드
		System.out.println(n);
	}
	static void showDouble(double n) {//static 메소드
		System.out.println(n);
	}
	
	void setMyNumber(int n) {//인스턴스 메소드
		myNum = n;
	}
	void showMyNumber() {//인스턴스 메소드
		showInt(myNum);
	}
}
public class NumberPrinterTest {
	public static void main(String[] args) {
		NumberPrinter.showInt(50);// 클래스 이름을 통한 클래스 메소드 호출
		/**
		 * 사실 위의 문장만 보더라도 static 메소드가 어느 인스턴스에도 속하지 않는다는 사실을 알 수 있다.
		 * 인스턴스 생성 이전에 호출이 되었기 때문이다. 
		 * 그리고 예제의 주석에서 설명하고 있듯이 클래스의 내부와 외부에서 static 메소드를 호출하는 방법은
		 * static 변수에 접근하는 방법과 차이가 없다.
		 */
		
		NumberPrinter np = new NumberPrinter();
		np.showDouble(3.15); // 인스턴스 이름을 통한 클래스 메소드 호출
		np.setMyNumber(30);
		np.showMyNumber();
	}
}
```

다음 질문에 답해보자. 
- static 메소드에서 같은 클래스에 선언된 인스턴스 변수에 접근이 가능한가?

이는 다음과 같은 코드의 작성이 가능한지를 묻는 질문이다.
```java
public class Example {
	int num =0;
	
	static void addNum(int n) {
		num = n;
    }
}
```
위의 코드는 에러가 난다. 논리적으로 생각을 하면 위와 같은 문장 구성이 불가능하다는 것을 알 수 있다.

인스턴스 변수는 인스턴스에 속한다. 더불어 인스턴스가 생성이 되어야 메모리 공간에 존재하게 된다. 반면 static 메소드는 인스턴스 생성 이전부터 호출이 가능하다. 따라서 위 질문에 대해서 다음과 같이 대답할 수 있다.
- static 메소드는 인스턴스에 속하지 않으므로 인스턴스 변수에 접근이 불가능하다.
- 같은 이유로 static 메소드는 인스턴스 메소드의 호출도 불가능하다.

그러나 static 메소드 같은 클래스에 정의되어 있는 다른 static 메소드나 성격이 동일한 static 변수에는 접근이 가능하다.(당연한 얘기지만)

## System.out.println 그리고 main 메소드
지금까지 main 메소드를 정의할 때 그 앞에 static 선언을 붙여왔다. 그리고 인스턴스의 생성 없이 println 메소드를 호출해 왔다.

### System.out.println()에서 out과 println의 정체는? 
static 선언의 의미를 알았으니 System.out.println()의 구성을 이해할 수 있다. 일단 System은 자바에서 제공하는 클래스로 java.lang 패키지에 묶여있다. 따라서 원칙적으로는 다음과 같이 호출해야 한다.

- java.lang.System.out.println(...);

그러나 컴파일러가 다음 문장은 삽입 해주기때문에 패키지의 이름부분은 생략할 수 있다. 

- import java.lang.*;

그리고 out은 System.out으로 접근을 하니, 이는 분명 static으로 선언된 static 변수가 분명하다. 클래스의 이름을 통해 접근하니 말이다.   실제로 out은 System 클래스 내에 다음과 같이 선언된 static 변수이다.
```java
public final class System extends Object{
	public static final PrintStream out; //참조변수

}
```
마지막으로 println은 PrintStream 클래스의 인스턴스 메소드이다. 따라서 다음 문장을 보면서,

- System.out.println(...);

다음과 같이 이해 할 수 있어야 한다.

- System에 위치한 클래스 변수 out이 참조하는 인스턴스의 println 메소드를 호출하는 문장

### main 메소드가 public 이고 static인 이유에 대해서 알아보자.
main 메소드는 반드시 다음의 모양새를 갖춰야 한다.

```java
public static void main(String[] args) {
		
}
```
이렇듯 main 메소드는 public 으로 그리고 static으로 선언해야 한다. 이는 일종의 약속이다. 

main메소드의 호출이 이뤄지는 영역은 클래스 외부이다. 따라서 public으로 선언하는 것이 타당함을 알 수 있다. 그리고 main메소드는 인스턴스가 생성되기 이전에 호출된다. 따라서 static 선언하는 것이 옳음을 알 수 있다.

다음의 예제를 보자. Car클래스와 Boat 클래스를 정의 하였다. 다음의 main 메소드가 호출이 되어 실제 실행이 되게 하려고 한다면 어떤 클래스에 두어야 할까?

```java
class Car{
	void myCar() {
		System.out.println("밴츠");
	}
}

class Boat{
	void myBoat() {
		System.out.println("보트");
	}
}
```
main 메소드는 static 메소드이기 때문에, 즉 특정 인스턴스의 맴버로 존재하는 메소드가 아니기 때문에 정답은 어디든 상관은 없다. (물론 실행방식에선 차이가 발생한다. Car클래스에 두었으면 java Car 를 호출, Boat면 java Boat 호출)
 
그렇다면 Car클래스에 두었다고 가정해보자. main 메소드를 Car 클래스 내에 위치시켰는데 그 안에서 Car 인스턴스를 생성하고 있다. 혹시 이부분이 조금 난해하게 느껴지는가? 그렇다면 다음과 같이 생각하자.

- Car클래스와 static으로 선언된 main메소드는 사실상 별개다.
- 다만 Car 클래스가 main 메소드에게 공간을 제공했을 뿐이다. 

