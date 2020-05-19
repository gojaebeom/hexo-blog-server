---
title: JAVA - 23. 제네릭 타입
thumbnail: https://github.com/gojaebeom/hexo-blog-server/blob/master/themes/icarus/source/images/%EC%9E%90%EB%B0%94/thumbnail.png?raw=true
date: 2020-05-12 21:20:00
tags: 
- java
- 제네릭
category:
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

## 제네릭(Generic)
제네릭은 자바 5 이후에 도입되었다. **제네릭(Generic)**은 클래스 내부에서 사용할 데이터 타입을 외부에서 지정하는 기법을 의미한다. 먼저 예제를 보자.<!-- more -->

```java
public class Example<T>{...}
```

위와 같이 클래스명 뒤의 <>에 타입 매개변수를 지정할 수 있다. T는 Type의 약자인데 사실 이름은 아무렇게나 정의할 수 있다. 하지만 일반적으로 이름은 다음과 같이 짓는다.

## 제네릭 기본문법
제네릭예제를 다루기 이전에 제네릭에대한 기본문법을 간략히 알아보자.

### 타입 파라미터 명명 규칙
- 한문자로 이름 짓기
- 대문자로 이름 짓기

보편적으로 자주 사용하는 타입 매개변수의 이름과 의미는 다음과 같다.
- E (Element)
- K (Key)
- N (Number)
- T (Type)
- V (Value)

### 다중 타입 파라미터
```java
class Example1<K, V>{...}
class Example2{...}
class Example3{...}

public class ExampleTest{
    public static void main(String[] args){
        Example<Example2,Example3> example;
    }
}
```
위와 같이 타입은 두개 이상도 가능하다. 그에 따라 사용시 매개변수의 수만큼 사용할 클래스를 정의해주면 된다.

### 기본 자료형 제한
제네릭 클래스에 대하여 타입 파라미터의 값을 받을때 기본 자료형의 이름은 타입 인자로 쓸 수 없다. 
```java
Example<int> example = new Example<int>(); //에러
```
하지만 기본 자료형에 대한 래퍼 클래스가 존재하고, 필요한 상황에서 박싱과 언박싱이 자동으로 이뤄지기 때문에 다음과 같은 코드를 작성할 수 있다.

```java
public static void main(String[] args){
    Example<Integer> example = new Example<Integer>();
    example.set(100); //오토박싱
    int num = example.get(); //오토 언박싱
}
```

### 타입 인자의 생략
컴파일러는 프로그래머가 작성하는 제네릭 관련 문장에서 자료형의 이름을 추론하는 능력을 갖고 있다. 따라서 다음과 같은 문법이 가능하다.
```java
Example<String> example = new Example<String>();

//위 문장을 아래와 같이 표현할 수 있다.
Example<String> example = new Example<>();
```

### 타입 파라미터를 타입 인자로 전달
```java
Example<Example<String>> example = new Example<>();
```
위와 같이 타입 인자로 타입 파라미터를 가진 클래스를 담을 수 있다.

### 타입 인자 제한하기
제네릭 클래스를 정의 시 담고 싶은 것을 용도에 따라 제한하는 일도 생긴다. 이때 타입을 제한하는 문법을 사용할 수 있다.
```java
class Example<T extends Number>{...}

public class ExampleTest{
    public static void main(String[] args){
        Example<String> example = new Example<>();//에러

        Example<Integer> example = new Example<>();
    }
}
```
위와 같이 제네릭 타입을 정의할 때 타입 파라미터 `T`가 `Number` 클래스를 상속하는 코드를 작성하므로, Example 타입 인자로 Number 또는 이를 상속하는 하위 클래스만 담을 수 있는 것을 알 수 있다.

## 제네릭 예제
### 제네릭 이전 코드
제네릭이 왜 필요한지 예제를 다루어보자. 먼저 제네릭 사용 이전의 코드이다.

```java
//GenericTest.java
class Apple{
    public String toString(){
        return "Apple";
    }
}
class Blueberry{
    public String toString(){
        return "BlueVerry";
    }
}
class AppleBox{
    private Apple apple;

    public void set(Apple apple){
        this.apple = apple;
    }
    public Apple get(){
        return apple;
    }
}
class BlueverryBox{
    private Blueverry blueverry;

    public void set(Blueverry blueverry){
        this.blueverry = appleblueverry;
    }
    public Blueverry get(){
        return blueverry;
    }
}
```

과일 박스를 추상화하여 만든 클래스이다. 사과와 블루베리 클래스를 각 사과박스와 블루베리박스가 담아서 사용하는 예제를 테스트해보자.

```java
public class GenericTest{
    public static void main(String[] args){
        AppleBox aBox = new AppleBox();
        BlueverryBox bBox = new BlueverryBox();

        aBox.set(new Apple);
        bBox.set(new Blueverry);

        Apple apple = aBox.get();
        Blueverry blueverry = aBox.get();
    }
}
```
하지만 위의 `AppleBox` 와  `BlueverryBox`는 비슷한 코드들이 많다. 즉 따로 만들지 않고 Box라는 클래스를 통해 서로다른 객체로써 과일을 담을 수 있으니 다음과 같이 바꿀 수 있다.
```java
class Box{
    private Object obj;

    public void set(Object obj){
        this.obj = obj;
    }
    public Object get(){
        return obj;
    }
}

public class GenericTest{
    public static void main(String[] args){
        Box aBox = new Box();
        Box bBox = new Box();

        aBox.set(new Apple);//업캐스팅
        bBox.set(new Blueverry);//업캐스팅

        Apple apple = (Apple)aBox.get(); //다운캐스팅
        Blueverry blueverry = (Blueverry)bBox.get(); //다운캐스팅
    }
}
```
사과박스와 블루베리 박스역할을 하던 클래스두개를 하나의 클래스로 재정의하였다. Box 클래스는 사과와 블루베리 뿐만아니라 다른것들도 담을 수 있으므로 확장성과 제사용성이 더 좋아졌다. 그리고 위의 예제에서 보이고자 하는 부분은 `set 메소드`의 매개변수로 `Apple`과 `Blueverry`가 들어갈땐 업캐스팅으로 자동형변환이되어 들어간다. 하지만 그 값이 사용되는 부분에서 다운캐스팅을하는데 이때 명식적으로 형변환을 해주어야한다. 이 과정은 번거롭고 또 사용자의 실수가 발생할 수 있다. 

### 제네릭 적용 코드
위의 코드를 제네릭을 적용하여 수정해보자.
```java
class Box<T>{
    private T obj;

    public void set(T obj){
        this.obj = obj;
    }
    public T get(){
        return obj;
    }
}
public class GenericTest{
    public static void main(String[] args){
        Box aBox<Apple> = new Box<Apple>();//선언시에 타입을 지정
        Box bBox<Blueverry> = new Box<Blueverry>();//선언시에 타입을 지정

        aBox.set(new Apple);//업캐스팅
        bBox.set(new Blueverry);//업캐스팅

        Apple apple = aBox.get(); //다운캐스팅
        Blueverry blueverry = bBox.get(); //다운캐스팅
    }
}
```

객체 생성시에 타입 파라미터를 지정함으로써 다운캐스팅시 명시적으로 형변환을 해주지 않아도 되는것을 알 수 있다.