---
title: JAVA - 04. 메소드와 변수의 스코프
thumbnail: https://user-images.githubusercontent.com/62233873/78540149-aa58da80-782e-11ea-9754-33ae5e40ec43.jpg
date: 2020-04-22 18:00:00
tags: 
- java
- 메소드
- 스코프
- 변수의 스코프
- scope
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

## 메소드의 정의
앞서 예제를 작성하고 호출하기 위해 main메소드 안에서 작업한것을 알 수 있다. main메서드는 클래스의 내부에 존재해야한다.

지금까지 만들어온 메서드의 이름이 항상 main인 이유는 다음 약속에 근거한다. <!-- more --> 자바 프로그램은 main이라는 이름의 메소드에서부터 시작을 한다. 따라서 추가로 만들게 될 메소드의 이름은 다음과 같이 직접 결정하면 된다.

```java
public static void hiEveryone(int age) {
    System.out.println("좋은 아침입니다.");
    System.out.println("제 나이는 " + age+" 입니다.");
}
```
위의 코드 내용을 가리켜 '메소드 정의'라 한다. 즉 위의 코드는 '메소드 hiEveryone의 정의'이다. hiEveryone의 오른편 소괄호에는 정수형 변수 age가 있다. 이 변수가 어떻게 활용되는지 보자. 

```java
public static void main(String[] args) {
    hiEveryone(26);	
}
```
위의 결과를 보면 

'좋은 아침입니다. 제 나이는 26입니다.'

가 출력되는 것을 볼 수 있다.

즉 main 메서드에서 hiEveryone메서드를 호출하고 파라미터로 26을 전달하는 것 이다. 일단 public 과 static은 무시하고  여기서 알 수 있는건 메서드를 정의 할때는
```java
 자료형(리턴타입) | 메서드명 | (매개변수를 받으면 소괄호안에 해당하는 타입의 변수를 작성){
 	//중괄호 안에 로직 작성
 }
```
으로 만들 수 있고, 메서드 사용시에는 
```java
메서드명(매개변수를 만들었다면, 전달할 인자값 작성);
```
으로 사용할 수 있다. 물론 매개변수는 하나 이상 사용이 가능하다. 밑의 예제를 보자.
```java
public static void myInfo(String name, int age) {
    System.out.println("제 이름은 "+ name+" 이고, 나이는 " + age+" 입니다.");
}

public static void main(String[] args){
    myInfo("고재범", 26);
}
```
이처럼 매개변수를 두개, 혹은 그이상도 사용할 수 있다.

## 메소드의 반환값
이전에 다루었던 method는 매개변수를 사용하는 정도까지 알아보았다. 하지만 method의 실제 사용되는 모습이랑은 많이 다르다. 이번엔 method를 정의할 때 값을 반환 하는 방법을 알아보자.
```java
public static int add(int a, int b) {

    return a+b;
}
```
위의 메소드를 보면 void였던 부분에 int 가 들어가있다. 저 부분은 반환형을 지정하는 곳 인데, 지금까지 값을 반환하지 않았기 때문에 void를 사용하였다. 

void는 값을 return 하지 않는다고 선언하는 방법이다. 하지만 위의 예제는 정수타입의 값을 return하고 있기때문에 반환형으로 int를 사용하였다. 그럼 return의 정확한 의미는 무엇일까? 다음과 같다.
- 메소드를 호출한 영역으로 값을 반환.
- 메소드의 종료

메소드의 종료는 알겠는데, 메소드를 호출한 영역으로 값을 반환한다는건 무슨 소리일까? 다음 예제를 보자.
```java
public static void main(String[] args) {

    int num = add(1,2);
    System.out.println(num);
}
```
정수형 변수 num을 선언하고 add()메소드로 초기화하고있다. 메소드 add는 반환 타입이 정수였다. 그렇기때문에 정수형 변수의 값으로 담을 수 있게 되는 것 이다. 이때는 정확히 메소드 add의 반환 값이 담긴다고 생각하면 되겠다.

이것은 위에서 설명한 메소드를 호출한 영역으로 값을 반환한다는 것과 같은 맥락이다. 위의 목적은 메소드 add에게 값을 전달해 연산을 하도록하여 연산된 값을 이부분에서 출력해보기 위한 것 같다. 그렇다면 저렇게 변수에 담지 않고 바로 출력하는 것도 가능하다.
```java
public static void main(String[] args){
    System.out.println(add(10,10));
}
```

## 메소드의 재귀적호출(맛보기)
자바는 메소드의 '재귀적 호출'을 지원한다.따라서 이에 대해 설명할 텐데, 메소드의 재귀적 호출은 자료구조와 알고리즘의 구현에 유용한 문법이므로 조금 내용이 어렵다.

### 수학적 측면에서의 재귀적인 사고
고등학교 수학에서 접하는 팩토리얼(Factorial)은 기호 !으로 표현하며 계산 방식은 다음과 같다.

5! = 5 x 4 x 3 x 2 x 1
4! = 4 x 3 x 2 x 1
3! = 3 x 2 x 1
2! = 2 x 1
1! = 1
 
때문에 위의 팩토리얼의 계산식은 다음과 같이 쓸 수 있다.
5! = 5 x 4!
4! = 4 x 3!
3! = 3 x 2!
2! = 2 x 1!
1! = 1
(뭐하는 건지 모르겟다;; 수학공부좀 열심히할껄..)

위의 식에서 재귀(순환)를 발견할 수 있다. 팩토리얼의 계산식에 다시 팩토리얼이 등장한 이 상황이 바로 '재귀'이기 때문이다.
```java

public static void main(String[] args) {
    System.out.println("3 factorial : " + factorial(3));
}

public static int factorial(int n) {

    if(n == 1) //if문 다음으로 오는 내용이 한줄만있다면 {중괄호}를 생략 가능하다.
        return 1;

    return n * factorial(n-1);
}
```
본인도 아직 완벽히 이해하지 못했음으로 설명은 생략하겠다..ㅎ

## 변수의 스코프
지금까지 중괄호 {...}가 사용되었던 때를 정리해 보면 다음과 같다.
- if문 또는 switch문 같은 조건문에 사용되었다
- for , while등의 반복문에 사용되었다.
- 메소드의 몸체 부분을 감싸는 용도로 사용되었다. 

이처럼 중괄호는 다양한 경우에 사용된다. 그런데 이렇듯 중괄호로 특정 영역을 감싸면, 해당 영역은 변수에 관한 별도의 스코프를 형성하게 된다. 예를 들어서 다음과 같이 if문 안에 변수가 선언되게 되면
```java
public static void main(String[] args) {
    if(true) {
        int num = 0;
    }
    //System.out.println(num); 주석을 처리하면 에러가 난다.
}
```
if문 밖에서는 변수 num을 사용할 수 없다. 이 변수 num은 중괄호 내에서만 접근이 가능하며,중괄호를 벗어나는 순간 소멸되어 접근이 불가능한 변수가 된다. 좋은 예는 아니지만 이말은 즉 똑같은 변수명으로 괄호 밖에서 다시 선언할 수 있다.
```java
public static void main(String[] args) {
    if(true) {
        int num = 0;
    }
    //System.out.println(num); 주석을 처리하면 에러가 난다.

    int num = 0;
    System.out.println(num);
}
```
지금까지 설명한 중괄호 내에 선언된 변수들을 가리켜 '지역변수(Local Variable)'라 한다. 그리고 for문의 초기화 부분에서 선언되는 변수화 매개변수까지도 지역변수의 범주에 포함된다. 그런데 이러한 지역변수들이 갖는 중요한 특징이 하나 있다.

- 지역변수는 선언된 지역을 벗어나면 메모리 공간에서 소멸된다.

즉 선언된 지역을 벗어나면 단순히 접근만 불가능해지는 것이 아니라 메모리상에서 삭제가 되는 것이다.

> 본 문서는 책의 일부 내용을 발췌한 것으로서 온오프라인 상의 무단 배포를 금합니다.
