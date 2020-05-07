---
title: JAVA - 07. 정보은닉과 캡슐화
thumbnail: https://user-images.githubusercontent.com/62233873/78540149-aa58da80-782e-11ea-9754-33ae5e40ec43.jpg
date: 2020-04-26 14:55:00
tags: 
- java
- 클래스
- class
- 인스턴트
- 객체
- 생성자
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

## 정보은닉
자바에서 말하는 정보는 클래스의 인스턴스 변수를 의미한다. 따라서 정보를 은닉한다는 것은 인스턴스 변수를 숨긴다는 뜻이다. 다음 예제를 다루어보면서 정보은닉이 필요한 이유에 대해서 알아보자.
<!-- more -->

```java
class 정보은닉_예제{

    public static void main(String[] args) {
        Circle c = new Circle(1.5);
        System.out.println(c.getArea());

        c.setRad(2.5);
        System.out.println(c.getArea());

        c.radius = 5;//옳지 않은 접근 방법, 그리고 문제가 되는 부분
        System.out.println(c.getArea());

    }
}

//원의 너비를 구하는 클래스
class Circle{
    double radius = 0;//원의 반지름
    final double PI = 3.14;//원주율

    public Circle(double r) {
        setRad(r);
    }

    public void setRad(double r) {

        if(r<0) {//반지름은 0보다 작을 수 없으므로
            radius = 0;
            return;//아무것도 반환하지 않고 메소드에서 빠저나간다.
        }

        radius = r;
    }

    public double getArea() {
        return (radius * radius) * PI;//원의 너비 반환
    }
}
```
위 예제 18, 19번째 줄에서 보이듯이 인스턴스 변수는 선언과 동시에 초기화를 할 수 있다. 특히 PI의 경우 그 값이 상수이므로 생성자를 통한 초기화보다 위의 방식의 초기화가 더 어울린다. 

그렇다면 25번째 줄의 setRad 메소드를 보자. 위 메소드 정의를 통해서 Circle 클래스를 정의한 이의 다음 의도를 읽을 수 있다.

- 반지름의 길이 radius에 0 보다 작은 값이 저장되는 일이 발생하지 않도록 하겠다.

때문에 이러한 의도를 따르기 위해서라도 반지름의 길이를 변경할 때에는 반드시 위의 메소드 호출을 통해서만 변경을 진행해야 한다. 이렇듯 인스턴스 변수에 저장되는 값의 종류와 범위는 해당 클래스를 정의한 사람이 가장 정확히 안다. 따라서 클래스 사용자가 잘못된 값을 인스턴스 변수에 저장하지 않도록 위와 같은 유형의 메소드를 제공해야한다. 그런데 위의 예제에서는 프로그램 사용자의 실수로 다음과 같은 잘못된 접근이 발생하였다.

- 10번째 줄의 c.radius = 5;

이렇듯 인스턴스 변수의 직접적인 접근을 허용하면, 컴파일 과정에서 드러나지 않는 중대한 실수가 발생할 수 있다. 이러한 오류는 실행 결과에서도 드러나지 않아 더 큰 문제가 된다. 때문에 위와 같은 접근을 허용하지 않도록 클래스를 설계할 필요가 있다. 그리고 이러한 클래스의 설계를 가리켜 '정보 은닉' 이라 한다.

## Getter 와 Setter

```java
public class Getter와Setter {
	
	/**
	 * 이전에서 만든 클래스를 '정보 은닉'의 조건을 충족하게 다시 만들어보자. 
	 */

	public static void main(String[] args) {
		Circle02 c = new Circle02(3);
		System.out.println("반지름: " + c.getRadius());
		System.out.println("넓 이:" + c.getArea());
		
		c.setRadius(3.5);
		System.out.println("반지름: " + c.getRadius());
		System.out.println("넓 이:" + c.getArea());
		
	}
}

class Circle02{
	
	private double radius = 0;
	private final double PI = 3.14;
	
	public Circle02(double r) {
		setRadius(r);
	}
	
	public void setRadius(double r) {
		if(r<0) {
			radius = 0;
			return;
		}
		radius = r;
	}
	
	public double getRadius() {
		return radius;
	}
	
	public double getArea() {
		return (radius*radius)*PI;
	}
}
```
<br>
이전과 다른점들을 살펴보자. 일단 21, 22 번줄의 인스턴스 변수의 선언 앞에 private라는 접근 수준 지시자(접근제한자가 붙어있다.) 그리고 이것이 의미하는 바는 다음과 같다.

- 클래스 내부에서만 접근을 허용하겠다.
 
따라서 클래스 외부에서 prviate으로 선언된 변수에 접근할 경우 컴파일 오류가 발생한다. 그렇다면 저 변수를 어떻게 사용해야 할까?

자바에서는 상태는 외부로부터 숨기고 오직 동작(메소드)를 통해서만 상태를 제어할 수 있는 방식을 권장하고 있다. 따라서 위의 두 유형의 메소드를 통해 값을 설정하고, 전달하는 일을 할 수있다.

상단의 setRadius는 값의 설정을 위한 메소드이고, 메소드 getRadius는 값의 참조를 위한 메소드이다. 이렇듯 값의 설정과 참조를 위한 메소드를 가리켜 각각 다음과 같이 부른다. 

- getter
    - 인스턴스 변수의 값을 참조하는 용도로 정의된 메소드
    - 변수의 이름이 name일 때, 메소드의 이름은 getName으로 짓는 것이 관계
 
- setter
    - 인스턴스 변수의 값을 설정하는 용도로 정의된 메소드
    - 변수의 이름이 name일 때 , 메소드의 이름은 setName으로 짓는 것이 관례

private으로 선언된 모든 인스턴스 변수를 대상으로 게터와세터를 반드시 정의해야 하는 것은 아니다. 필요에 따라 정의하면 된다. 그러나 당장 필요하지 않더라도 나중을 고려하여 게터와 세터를 정의하기도 한다.

## 접근 수준 지시자
앞의 예제에서 인스턴스 변수를 대상으로 private 선언을 하였는데, 이러한 유형의 키워드를 가리켜 '접근 수준 지시자 (Access-level Modifiers)' 라 한다. 또는 '접근 제한자' 라고도 한다. 이름 그대로 접근의 허용 수준을 결정할 때 선언하는 키워드이다.

접근제한자의 종류는 다음과 같이 4가지 이다.
- public, protected, private, default

이중에서 default는 키워드가 아닌, 아무런 선언도 하지 않은 상황을 의미한다. 비록 이는 키워드가 아닌 일종의 상황이지만 이 역시 접근 제한자의 한 종류로 구분을 한다. 

그리고 이러한 선언을 할 수 있는 대상은 다음 두 가지이다.
- 클래스의 정의
- 클래스의 인스턴스 변수와 메소드
 
클래스의 정의를 대상으로는 다음 두 가지 선언이 가능하다.
- 클래스 정의대상 : public ,default

그리고 인스턴스 변수와 메소드를 대상으로는 다음 네 가지 선언이 모두 가능하다.
- public, protected, private, default

그럼 이제 각각의 기능을 알아보자. 

### 클래스 정의 대상의 public 과 default 선언이 갖는 의미
- public : 어디서든 인스턴스(객체) 생성이 가능하다. 
- default : 동일 패키지로 묶인 클래스 내에서만 인스턴스 생성을 허용한다.

### 인스턴스 멤버 대상의 public , protected, private, default 선언이 갖는 의미
 
|  접근제한자 |   클래스 내부  |  동일 패키지  |  상속 받은 클래스  |  이외의 영역|
|------------|:-------------- :|-------------:|:------------------:|-------------:|
|    private  |        o       |        x      |         x         |       x
|    default  |        o       |        o      |         x         |       x
|   protected |        o       |        o      |         o         |       x
|    public   |        o       |        o      |         o         |       o 
    
위의 표에서 말하는 이외의 영역은 다른 패키지에 속한 클래스를 뜻한다. 즉 서로 다른 패키지에 속한 두 클래스 사이의 접근을 의미한다. 그리고 위 표의 내용을 기준으로 접근 허용 범위에 대하여 다음과 같이 이해하고 있는 것도 도움이 된다. 

- public >  protected > default > private

## 캡슐화
캡슐화는 정보 은닉과 더불어 객체지향 기반의 클래스 설계에 있어 가장 기본이면서 중요한 원칙 중 하나이다. 캡슐화는 문법적인 내용은 아니다. 클래스 안에 '무엇을 넣을까' 에 대한 이론을 제시한는 내용이다.

캡슐화를 다음과 같이 정의할 수 있다. 
- 하나의 목적을 이루기 위해 관련 있는 모든 것을 하나의 캡슐에 담아 두는 것

물론 객체지향 관점에서 위의 캡슐은 클래스에 해당한다. 즉 위의 문장은 다음과 같이 다시 쓸 수 있다.
- 하나의 목적을 이루기 위해 관련 있는 모든 것을 하나의 클래스에 담아 두는 것

무조건 많이 담는다고 해서 캡슐화가 아니다. 부족해도 안되고 넘쳐도 문제가 된다. 그리고 상황 및 목적에 따라서 동일한 이름의 클래스에도 담기는 내용이 달라진다. 캡슐화에 대한 예제들은 github 에 올려두었던 다음 예제들을 참고하면 괜찮을 것 같다.
- [캡슐화 예제 01](https://github.com/gojaebeom/java_tutorial/blob/master/src/ch06_%EC%A0%95%EB%B3%B4%EC%9D%80%EB%8B%89%EA%B3%BC%EC%BA%A1%EC%8A%90%ED%99%94/%EC%BA%A1%EC%8A%90%ED%99%9401.java)
- [캡슐화 예제 02](https://github.com/gojaebeom/java_tutorial/blob/master/src/ch06_%EC%A0%95%EB%B3%B4%EC%9D%80%EB%8B%89%EA%B3%BC%EC%BA%A1%EC%8A%90%ED%99%94/%EC%BA%A1%EC%8A%90%ED%99%9402.java)
- [캡슐화 예제 03](https://github.com/gojaebeom/java_tutorial/blob/master/src/ch06_%EC%A0%95%EB%B3%B4%EC%9D%80%EB%8B%89%EA%B3%BC%EC%BA%A1%EC%8A%90%ED%99%94/%EC%BA%A1%EC%8A%90%ED%99%9403.java)

> 본 문서는 책의 일부 내용을 발췌한 것으로서 온오프라인 상의 무단 배포를 금합니다.
