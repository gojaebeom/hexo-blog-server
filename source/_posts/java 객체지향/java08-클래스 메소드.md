---
title: JAVA - 08. 클래스 메소드
thumbnail: https://user-images.githubusercontent.com/62233873/78540149-aa58da80-782e-11ea-9754-33ae5e40ec43.jpg
date: 2020-04-26 16:09:00
tags: 
- java
- 클래스 변수
- static 메소드
category:
- 웹 개발
- java

#카탈로그 생성 및 위치
toc: true
widgets:
  - type: toc
    position: right
  - type: category
    position: right
  - type: tagcloud
    position: right
#위치고정 여부
sidebar:
  right:
    sticky: true
---
## 클래스 메소드(static 메소드)
클래스 내에 정의된 메소드에 static 선언을 하면 '클래스 메소드'가 된다. 그리고 클래스 메소드는 그 성격이 클래스 변수와 유사하다.
접근 방법도 동일하며 인스턴스 생성 이전부터 호출이 가능한, 그리고 어느 인스턴스에도 속하지 않는 메소드라는 점도 클래스 변수와 동일하다.<!-- more -->

### 클래스 메소드의 정의와 호출
이전 글에서 공부한 클래스 변수의 특성 두 가지는 다음과 같다.
- 인스턴스 생성 이전부터 접근이 가능하다.
- 어느 인스턴스에도 속하지 않는다.

이 두 가지는 클래스 메소드도 동일하게 갖는 특성이다. 따라서 이 사실을 다음 예제를 통해서 확인해보겠다.
```java
public class 클래스메소드_정의 {

	public static void main(String[] args) {
		NumberPrinter.showInt(50);// 클래스 이름을 통한 클래스 메소드 호출
		
		/**
		 * 사실 위의 문장만 보더라도 클래스 메소드가 어느 인스턴스에도 속하지 않는다는 사실을 알 수 있다.
		 * 인스턴스 생성 이전에 호출이 되었기 때문이다. 
		 * 그리고 예제의 주석에서 설명하고 있듯이 클래스의 내부와 외부에서 클래스 메소드를 호출하는 방법은
		 * 클래스 변수에 접근하는 방법과 차이가 없다.
		 */
		
		NumberPrinter np = new NumberPrinter();
		np.showDouble(3.15); // 인스턴스 이름을 통한 클래스 메소드 호출
		
		np.setMyNumber(30);
		np.showMyNumber();
	}
}

class NumberPrinter{
	private int myNum = 0;
	
	static void showInt(int n) {//클래스 메소드
		System.out.println(n);
	}
	static void showDouble(double n) {//클래스 메소드
		System.out.println(n);
	}
	
	void setMyNumber(int n) {//인스턴스 메소드
		myNum = n;
	}
	void showMyNumber() {//인스턴스 메소드
		showInt(myNum);
	}
}
```

다음 질문에 답해보자. 

- 클래스 메소드에서 같은 클래스에 선언된 인스턴스 변수에 접근이 가능한가?

이는 다음과 같은 코드의 작성이 가능한지를 묻는 질문이다.
```java
public class 클래스메소드_심화 {
	
	//int num =0;
	
	//static void addNum(int n) {
	//	num = n;
    //}
}
```
위의 문장에 주석을 풀면 에러가 난다. 논리적으로 생각을 하면 위와 같은 문장 구성이 불가능하다는 것을 알 수 있다.

인스턴스 변수는 인스턴스에 속한다. 더불어 인스턴스가 생성이 되어야 메모리 공간에 존재하게 된다. 반면 클래스 메소드는 인스턴스 생성 이전부터 호출이 가능하다. 따라서 위 질문에 대해서 다음과 같이 대답할 수 있다.

- 클래스 메소드는 인스턴스에 속하지 않으므로 인스턴스 변수에 접근이 불가능하다.
- 같은 이유로 클래스 메소드는 인스턴스 메소드의 호출도 불가능하다.

그러나 클래스 메소드 같은 클래스에 정의되어 있는 다른 클래스 메소드나 성격이 동일한 클래스 변수에는 접근이 가능하다.(당연한 얘기지만..)

## System.out.println 그리고 main 메소드
지금까지 main 메소드를 정의할 때 그 앞에 static 선언을 붙여왔다. 그리고 인스턴스의 생성 없이 println 메소드를 호출해 왔다.

### System.out.println()에서 out과 println의 정체는? 
static 선언의 의미를 알았으니 sysout의 구성을 이해할 수 있다. 일단 System은 자바에서 제공하는 클래스로 java.lang 패키지에 묶여있다.  따라서 원칙적으로는 다음과 같이 호출해야 한다.

- java.lang.System.out.println(...);

그러나 컴파일러가 다음 문장은 삽입 해주기때문에 패키지의 이름부분은 생략할 수 있다. 

- import java.lang.*;

그리고 out은 System.out으로 접근을 하니, 이는 분명 static으로 선언된 클래스 변수가 분명하다.
클래스의 이름을 통해 접근하니 말이다. 
실제로 out은 System 클래스 내에 다음과 같이 선언된 클래스 변수이다.
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

> 본 문서는 책의 일부 내용을 발췌한 것으로서 온오프라인 상의 무단 배포를 금합니다.


 

