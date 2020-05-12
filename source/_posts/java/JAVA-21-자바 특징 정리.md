---
title: JAVA - 21. 객체지향의 특징
thumbnail: https://user-images.githubusercontent.com/62233873/78540149-aa58da80-782e-11ea-9754-33ae5e40ec43.jpg
date: 2020-05-06 21:20:00
tags: 
- java
- 자바 객체지향
- 객체지향
- 자바의 특징
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

## 객체지향 프로그래밍(Object Oriented Programming )이란?
객체지향은 프로그램 설계방법론중 하나 이다. 프로그램을 수많은 '객체'라는 기본 단위로 나누고 이 객체들의 상호작용으로 서술하는 방식이다. 객체란 하나의 역할을 수행하는 '메소드와 변수(데이터)'의 묶음으로 봐야 한다.<!-- more -->


어느 유튜버의 강의을 보다가 가장 마음에 와닿았던 맨트가 있었다. 철학자 **플라톤**의 **이데아 론**을 객체지향(OOP)과 빗대어 설명한 부분이다.

"*목수의 머릿속엔 가장 이상적이고 완벽한 책상이 하나 존재한다. 목수가 현실에 책상을 만들때는 그 이상적인 세계에 존재하는 책상을 본따서 만든다고 한다. 즉 현실의 책상은 목수의 머릿속에 있는 책상의 이상적인 설계도를 본따서 만든다고 생각할 수 있다. 플라톤은 이 이상적인 세계를 **이데아**라고 불렀다. 그리고 현실에 존재하는 물건은 그 이상적인 세계에 있는 물건을 가져와 복제한 **레플리카**라고 했다.*"

갑자기 철학적인 이야기가 나와 이상하다고 생각할 수 있지만, 우리가 프로그래밍에 사용하는 class, object 들은 실제로 고대 그리스 **플라톤의 이데아론**에서 왔다.

```java
class Dog{...}
```

우리는 위와 같이 클래스를 정의하고 사용해왔다. 하지만 위의 클래스는 단지 정의 되어져 있을 뿐 사용된 것은 아니다. 이것은 우리가 머릿속에서 생각하는 이상적인 설계도일 뿐이다.
```java
public static void main(String[] args){
  Dog backgoo = new Dog();

  Dog rudy = new Dog();

  Dog jack = new Dog();
}
```
위와같이 머릿속의 개라는 이미지를 현실에 만들었을때(인스턴스화), 비로소 이것은 객체로써 존재하게 되는 것 이다. 우리는 이것을 머리에 암기하는 것이 아니라, 자연스러운 흐름대로 이해할 필요가 있다.

이제 객체지향의 특징들에 대해서 알아보자.

### 객체지향의 특징
- *추상화*
- *캡슐화*
- *상속*
- *다형성*

## 추상화
추상화에 사전적 정의는 다음과 같다.
> 추상(抽象)은 사물을 정확하게 이해하기 위해서는 사물이 지니고 있는 여러 가지 측면 가운데서 특정한 측면만을 가려내어 포착하는 것이다. 어떤 일면만을 추상하는 것은 다른 측면을 버린다는 것과 같다. 이것을 '사상(捨象)'이라 한다.

추상화에 대한내용은 생각하기에 따라 다르기도하고 설명이 너무 난잡해질 수 도 있는 것 같다. 정말 간단하게 생각하자면, **자바에서 추상화란 공통된 속성(변수)과 행위(메소드)를 모아서 클래스를 만드는 것이다.**


## 캡슐화
객체지향에서 캡슐화란 두가지 특징이 있다.
- *객체의 속성(맴버변수, data fields)과 행위(메서드, methods)를 하나로 묶는다.*
- *실제 구현 내용 일부를 외부에 감추어 은닉한다.*

외부에 감추는 방법으로는 언어적 측면으로 접근제한자를 두어 은닉의 정도를 기술하여 구현한다. 이것이 캡슐화에서 중요한 **정보은닉**이다.

### 정보은닉 개념
정보은닉이란 캡슐화된 객체의 내부구현을 외부로부터 숨기는 것이다. 이전 포스트에서도 다루었는데, 자바에서 정보란 클래스의 인스턴스변수(맴버변수, 필드, 속성 등)를 말한다. 보통 이러한 정보들은 접근제한자를 두어 외부에서 직접 접근하지 못하게 하고 메소드를 통해서만 변수에 접근할 수 있게 하는 방식을 많이 사용한다.

```java
class Person{
  String name;

  void setName(String name){
    this.name = name;
  }
    
  String getName(){
    return name;
  }
}
```
위의 클래스 Person은 사람의 기본적인 특징 '이름을 가지고있다' 를 반영한 클래스이다. 이를 인스턴스화하여 다음과 같이 사용할 수 있다.
```java
public static void main(String[] args){
  Person jaebeom = new Person();
  jaebeom.setName("고재범");
  System.out.println(jaebeom.getName());
}
```

위의 예제는 작성자인 본인이 만든 클래스이다. 이것을 만든 의도는 본인이 가장 잘 이해하고있다.(잘 만들었던 못 만들었던 만든사람의 의도가 명확하다) 그리고 작성자는 맴버변수인 name에 값을 바로 대입하지 않고 메소드를 통해서 값을 할당하고 사용되길 원한다. 하지만 위의 예제의 경우에 접근지시자(접근제한자)를 사용하지 않았다. 그로 인하여 다른 사용자가 잘못 사용하게되는 예를 보자.
```java
public static void main(String[] args){
  Person jade = new Person();
  jade.name = "고재범";
  System.out.println(jade.name);
}
```

Person 클래스의 맴버변수에 바로 접근하여 값을 할당하고 출력하는 모습을 볼 수 있다. 이는 작성자의 의도와 다르게 잘못된 방향으로 사용이 되고있다. 위의 경우 치명적인 문제가 생길 일은 없지만, 맴버변수 name을 위해 정의한 setName, getName 메소드가 불필요하게 되어버렸다. 이렇게 작성자의 의도와는 반대로 사용이 되어지는 것을 막기위해 우리는 정보를 은닉할 필요가 있다. 사실 위의 예제로는 정보은닉의 필요성을 못 느낄 수 도 있다. 그렇다면 내용을 추가해보자.

```java
class Person{
  String name;
  double weight;
  
  void setWeight(double weight){
    if(weight <= 0){
      System.out.println("몸무게는 0보다 작거나 같을 수 없습니다! 다시 입력해주세요");
      return;
    }
    this.weight = weight;
  }

  double getWeight(){
    return weight;
  }
}
```
Person 클래스에 몸무게라는 속성을 추가하였다. 그리고 setWeight 메소드를 보면 몸무게는 0키로그램보다 작거나 같을 수 없기 때문에 예외적인 부분을 처리하고 있다. 하지만 사용자가 이외의 방법으로 접근하여 -999 같은 값을 입력할 수 있다면 이는 프로그램 실행의 문제로도 이어질 수 있는 부분이다. 위의 예제를 다음과 같이 수정해보자.
```java
class Person{
  private String name;
  private double weight;
  
  public void setWeight(double weight){
    if(weight <= 0){
      System.out.println("몸무게는 0보다 작거나 같을 수 없습니다! 다시 입력해주세요");
      return;
    }
    this.weight = weight;
  }

  public double getWeight(){
    return weight;
  }
}
```

접근 제한자 private 을 속성에 지정하여 외부에서의 접근을 막는다. 그리고 이 속성들은 오직 메소드(행동)을 통해서만 통제할 수 있도록 할 수 있다. (public 은 외부의 모든 곳에서 사용이 가능하지만 따로 접근 제한자를 명시하지 않으면 default 제한자와 같다. 이는 외부 패키지와 상속받은 클래스등에서는 사용할 수 없게 된다)

## 상속
상속은 자식 클래스가 부모 클래스의 특성과 기능을 그대로 물려받는 것을 말한다. 기능의 일부분을 변경해야 할 경우 자식 클래스에서 상속받은 그 기능만을 수정해서 다시 정의하게 되는데, 이러한 작업을 **'오버라이딩(Overriding)'**이라고 한다. 상속은 캡슐화를 유지하면서도 클래스의 재사용이 용이하도록 해 준다.

```java
class Phone{

  private int IMEI;//고유번호
  private String model;//폰의 기종 이름

  //객체를 생성시 기본정보를 기입받는 생성자
  public Phone(int IMEI, String model){
    this.IMEI = IMEI;
    this.model = model;
  }

  public void call(){
    //전화
  }

  public void messege(){
    //메세지
  }
}

public class Test{
  public static void main(String[] args){
    Phone myPhone = new Phone(000000, "모토로라");
  }
}
```

위의 예제는 Phone에 대한 클래스의 정의이다. 이 클래스는 외부에서 잘 사용되어 지고 있다. 하지만 시대가 변함에 따라 스마트 폰이 나오고 Phone 클래스에도 새로운 기능들을 넣으려고 한다. 만약 Phone의 클래스 내부의 값이나 메소드들의 로직을 직접 수정하게 되면 지금까지 Phone 클래스와 의존성이 있는 모든 클래스들을 다시 수정해야 한다. 예를 들어보자.

```java
class Phone{
  private int IMEI;
  private String model;
  private String OS; //새로 추가된 속성, 안드로이드 또는 ios 의 OS 탑재 가능

  //객체 생성시 기본정보를 입력받는 생성자 
  public Phone(int IMEI, String model, String OS){
    this.IMEI = IMEI;
    this.model = model;
    this.OS = OS; 
  }

  //새로 추가된 메소드, 웹 검색을 할 수 있다.
  public void webSearch(){ 
    //하지만 기존의 phone에서는 불가능하기때문에 스마트폰이아니면 불필요한 메소드가 된다.
  }
}

public class Test {
  public static void main(String[] args) {
      //Phone myPhone = new Phone(000000, "모토로라"); //에러
      /*
      * 기존에 사용하던 생성자는 매개변수를 2개만 받았는데
      * OS의 종류까지 초기에 입력받는 것으로 수정되었다.
      * 물론 메소드 오버로딩으로 기존의 생성자는 유지하고 새로운 생성자를 만들 수 도 있지만, 
      * 이 밖에도 추가되고 수정되어야 할것이 많다고 가정해보자.
      */
      //결국 다음과 같이 수정해야 한다.
      Phone myPhone = new Phone(000000, "모토로라", "OS 없음");
  }
}
```
이렇듯 내부적인 코드의 변화로 인해 Phone과 의존성이 있는 클래스들은 모두 수정해야 한다. 하지만 기존의 Phone 클래스는 수정하지 않고 Phone의 기능을 상속받아 새로 SmartPhone이라는 클래스를 정의한다면 어떻게 될까. 예제를 통해 알아보자.

```java
class Phone{
  private int IMEI;
  private String model;

  public Phone(int IMEI, String model){
    this.IMEI = IMEI;
    this.model = model;
  }
  ...
}

class SmartPhone extends Phone{

  private String OS;

  public SmartPhone(int IMEI, String model, String OS){
    super(IMEI, model);//부모 클래스 생성자에게 필요한 매개변수 전달
    this.OS = OS;//추가적으로 OS 종류 전달
  }

  public void bluetooth() {
    //블루투스
  }

  public void wiFi() {
    //와이파이
  }
}

public class Test {
  public static void main(String[] args) {
    Phone myPhone = new Phone(000000, "모토로라");//기존 사용자는 손대지 않는다.

    SmartPhone yourPhone = new SmartPhone(000001, "A90", "안드로이드");// 새로 스마트폰을 사용하는 사용자만 바꾸어주면 된다.
    yourPhone.wiFi();
  }
}
```
위의 예제와 같이 기존의 폰을 사용 사용하는 사람은 따로 변화를 주지 않아도 되고, 새로 스마트폰을 쓰는 사람들만 SmartPhone 객체로 생성해주면 되는 것 이다. 이건 어디까지나 글쓴이가 생각하는 예제이다. 본인한테 맞는 방법으로 생각하는 것이 좋을 것 같다.

## 다형성
[다형성](https://gojaebeom.github.io/2020/05/03/java/JAVA-18-%EB%8B%A4%ED%98%95%EC%84%B1)에 대한 정리 글을 참고해보자. 다형성은 여러 가지 형태를 가질 수 있는 기능을 말한다.

```java
abstract class LolChampions{
  public abstract void champName();
  public abstract void qSkill();
  public abstract void wSkill();
  public abstract void eSkill();
  public abstract void rSkill();
  public final void champInfo() {
  System.out.println("챔피언 정보");
    champName();
    qSkill();
    wSkill();
    eSkill();
    rSkill();
  }
}
class Heimerdinger extends LolChampions{
  @Override
    public void champName() {
    System.out.println("하이머딩거");
  }
  @Override
    public void qSkill() {
    System.out.println("Q스킬 : H-28G 진화형 포탑");
  }
  @Override
    public void wSkill() {
    System.out.println("W스킬 : 마법공학 초소형 로켓");
  }
  @Override
    public void eSkill() {
    System.out.println("E스킬 : CH-2 전자폭풍 수류탄");
  }
  @Override
    public void rSkill() {
    System.out.println("궁극기 : 업그레이드!!!");
  }
}
class Lux extends LolChampions{
  @Override
    public void champName() {
    System.out.println("럭스");
  }
  @Override
    public void qSkill() {
    System.out.println("Q스킬 : 빛의 속박");
  }
  @Override
    public void wSkill() {
    System.out.println("W스킬 : 프리즘 보호막");
  }
  @Override
    public void eSkill() {
    System.out.println("E스킬 : 광휘의 특이점");
  }
  @Override
    public void rSkill() {
    System.out.println("궁극기 : 최후의 섬광");
  }
}
```
다형성을 설명하기위해 두개의 클래스가 하나의 추상클래스를 상속받는 예제를 보였다. 아래 예제를 보자.
```java
public class PolymorphismTest {
    public static void main(String[] args) {
    LolChampions lolChamp = null;

    Scanner sc = new Scanner(System.in);
    System.out.println("챔피언을 고르시오.");
    System.out.println("1. 하이머딩거 / 2. 럭스");

    switch(sc.nextInt()) {
    case 1:
      lolChamp = new Heimerdinger();
      break;
    case 2:
      lolChamp = new Lux();
      break;
    default:
      System.out.println("잘못된 입력입니다!");
    }

    if(lolChamp != null) {
      lolChamp.champInfo();
    }
  }
}
```
`LolChampions` 타입의 참조변수를 선언하고 `null` 값을 받고 있다. 그리고 스캐너를 통해 콘솔값 1을 입력받으면 참조변수 `lolChamp`에 `Heimerdinger` 인스턴스를 참조하고 2를 입력 받으면 `Lux` 인스턴스를 참조한다. 이것이 다형성이다. 하나의 참조변수에 타입이 다른 객체들이 참조되어 하나의 코드가 상황에 따라 다른 결과를 보여주게된다. 

## 오버라이딩(Overriding)
상위 클래스에 정의된 메소드를 하위 클래스에서 다시 정의하는 행위를 가리켜 '메소드 오버라이딩' 이라 하는데, 여기서 말하는 오버라이딩은 '무효화 시키다'의 뜻으로 해석이 된다.

```java
class A{
  public void hello() {
    System.out.println("hello A");
  }
}

class B extends A{
  public void hello() {
    System.out.println("hello B");
  }
}

public class Test{
  public static void main(String[] args) {
    A a = new A();
    a.hello();

    A b = new B();//B는 A를 상속받기 때문에 B객체를 A타입의 참조변수가 참조할 수 있다.
    //B b = new B(); // 물론 이 방법도 가능하다.
    b.hello();
  }
}
```
위와 같이 A클래스를 B클래스가 상속 받으면서 기존의 A클래스에 있는 Hello 메소드를 B클래스에서 재정의 하였다. 메소드명을 바꾼다거나, 매개변수를 바꾼다거나, 반환형을 바꾼다는 개념이 아니다. 메소드 내부 로직을 바꾸는 것을 의미한다. 위의 상속의 개념에서 사용되는 overriding은 상속을 보다 편리하게 해주는 장점이 있다.


## 오버로딩(Overloading)
한 클래스 내에 동일한 이름의 메소드를 둘 이상 정의한느 것은 허용되지 않는다. 그러나 매개변수의 선언이 다르면 가능하다. 그리고 이것을 메소드 오버로딩이라 한다.

**메소드 오버로딩의 조건**
- *메소드의 이름*
- *메소드의 매개변수 정보*

실제로 우리가 자주 사용하는 println 메소드를 예로 들어보자.
```java
void println()
void println(boolean x)
void println(char x)
void println(String x)
void println(double x)
```
우리가 println을 쓰면서 String 값, int 값, double 값 등등의 값을 줄 수 있엇던 이유 역시 오버로딩이 있었기 때문에 가능하다. 만약 오버로딩이라는 것이 없었다면 아마 우리는 다음과 같은 메소드를 사용했을 것이다..
```java
void println()
void printlnBoolean(boolean x)
void printlnChar(char x)
void printlnString(String x)
void printlnDouble(double x)
```

원래 자바 포스트를 작성하기 이전에 다룰려고 했던 객체지향 특징이였다. 하지만 자바 문법에 어느정도 익숙해지고 예제를 이해하면서 넘어가면 더 자연스러울 거라고 생각하고 이 시점에 글을 작성하게 되었다.

*이번 포스팅은 글쓴이의 주관적인 생각이 많이 들어가있는 글이기 때문에 틀리거나 추가 설명이 필요하다고 생각되는 부분은 지적해주시면 감사하겠습니다.(오타는 어디에나 존재합니다..)*









