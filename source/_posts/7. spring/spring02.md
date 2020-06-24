---
title: 제어역전과 의존성 주입

thumbnail: images/spring/thumbnail.png
date: 2020-06-23 23:27:00

tags: 
- maven

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

먼저 제어의 역전과 의존성 주입을 설명하기 전에 객체간의 결합도에 대해 다루어보겠다.
<!-- more -->
## 인터페이스와 느슨한 결합
프로그램을 만들다보니 A 클래스와 B 클래스가 생성이 되었다. 프로그램을 만든다는건 수정이 동반되는 작업이 될 수도 있다. A 클래스에서 B클래스를 사용한다고 했을때, B 클래스의 수정이 필요한 시점이 오면 어떻게 해야할까?

B 클래스를 직접 수정하거나 B 클래스를 대신할 B2 클래스를 만들어 B 대신 사용하게 할 수 있을 것 이다. 직접 수정하는 방법은 제외 하고 B2 클래스를 새로 만들어 대신 조립하는 것을 예제로 보자.
```java
public class A
{
	//B b = new B();
	//위 코드를 다음과 같이 바꾼다.

	B2 b2 = new B2();
}
```

위의 코드는 수정된 클래스를 대신 사용하기위해 코드를 바꾼 예제이다. 하지만 다음과 같은 상황에서 객체지향의 특징인 다형성을 사용하면 조금 더 깔끔한 구현이 가능할 것 이다.
```java
public interface B{...}

public class B1 implements B{...}

public class B2 implements B{...}

public class B3 implements B{...}

public class A
{
	B b = new B1();
	//or
	B b = new B2();
	//or
	B b = new B3();
}
```
비슷한 특성을 가진 클래스들을 인터페이스를 미리 만들어 구현받도록 하는 것이다. 이 후 사용할 때 인터페이스를 참조변수로 받아 필요한 구현받은 필요한 클래스를 갈아 끼워주면 된다. 

위의 코드는 느슨한 결합의 결과라 할 수는 없다. A 클래스에서 수정을 해야한다는 것은 아직도 불가피하기 때문이다.

## 제어의 역전(IOC : Inversion of control)
IOC는 제어 흐름의 개념을 거꾸로 뒤집는 개념이다. 
- 오브젝트는 자신이 사용할 오브젝트를 스스로 생성하거나 선택하지 않는다.
- 모든 제어의 권한을 자신이 아닌 다른 대상에게 위임한다.

```java
public class A
{
	private B b;

	public A(B b)
	{
		this.b = b;
	}
}
```
클래스 A는 자신이 직접 B 객체를 생성하지 않는다. 생성자를 통해 외부에서 객체 b를 전달 받아 사용하게 된다. 이처럼 제어의 권한이 다른 곳에 있을때 이를 제어의 역전이라고 말 할 수 있다.

## 의존성 주입(DI: Dependency Injection)
IOC를 만족하기 위해 외부의에서 필요한 부품을 제공을 받아야 한다. 이러한 경우 외부에서 객체를 대신 전달 받을 수 있는데, 이 때 A는 B에 의존적임으로 의존성을 주입한다고 할 수 있다.
```java
public class Test
{
	public static void main(String[] args)
	{
		B b = new B1(); or B2(); or B3();
		A a = new A(b);
	}
}
```
의존성을 주입하는 것은 꼭 생성자를 통해 주입하는 것만은 아니다. 방법에 따라 의존성을 주입하는 방법은 다를 수 있다.

### 생성자를 통한 의존성 주입
```java
B b = new B1();
A a = new A(b);
```

### setter 메서드를 통한 의존성 주입
```java
B b = new B2();
A a = new A();
a.setB(b);
```

두 방법 모두 가능하며 상황에 맞게 사용하면 될 것 같다.

## 마무리 글
예제를 다루기 위해 main 메서드에서 테스트 하였는데, 실제로 스프링 프레임워크를 사용하게 되면 사용하고자 하는 의존성의 제어를 main 메서드가 아닌 IOC 컨테이너에서 처리하며, 또한 그곳에서 의존성을 주입받아 실제 작성하는 소스코드는 클래스간에 수정이 필요할 때 줄줄이 수정하는 지옥에서 해방될 수 있다고 한다.✨

다음 글에서 스프링 프레임워크를 활용하여 IOC와 DI를 활용하도록 하겠다.

<br>
<hr style="border:0px; border-bottom:2px dotted #D8D8D8">

*개인적인 공부 내용을 정리하는 것을 목적으로 하고 있습니다.*
*설명이 부족하거나 틀린 부분은 지적해 주시기 바랍니다.* 🐥