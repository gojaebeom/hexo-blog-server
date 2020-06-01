---
title: JAVA - 05. 제어문
thumbnail: https://github.com/gojaebeom/hexo-blog-server/blob/master/themes/icarus/source/images/%EC%9E%90%EB%B0%94/thumbnail.png?raw=true
date: 2020-04-22 17:16:00
tags: 
- java
- 제어문
- if문
- for문
- while문
- do while문
- 조건문
- 반복문
category:
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
## 조건문이란?
조건식을 만족하느냐 아니냐에 따라 프로그램의 실행을 제어할 수 있는 문법이다. 이 때 조건식은 true나 false 같은 boolean형 타입을 반환할 수 있는 식을 말한다. 자바 문법 중에서 조건문은 if, switch, 조건연산자등이 있다. <!-- more -->

### if문
특정 조건이 만족될 때에만 실행하고픈 문장이 있다면 키워드 if를 사용하면 된다. 그리고 두개의 문장 중 조건에 따라 하나만 실행하고 싶다면 거기에 else를 더 추가하면 된다. else는 if문 소괄호의 조건이 참이 아니라면 실행되는 곳이다.
```java
//if문 예제
int num1 = 1;
int num2 = 2;

if(num1 < num2) {
    //조건 true 시 실행되는 영역
    System.out.println("참입니다");
}else {
    //조건 false 시 실행되는 영역
    System.out.println("거짓입니다");
}
```

if ~ else if 문은 2개 이상의 조건을 주고싶을 때 사용할 수 있는 방법이다. 밑의 예제를 보자.
```java
//if ~ else if문 예제
if(num1 < num2) {
    System.out.println("num1보다 num2가 큽니다.");
}else if(num1 > num2) {
    System.out.println("num2보다 num1이 큽니다.");
}else if(num1 == num2) {
    System.out.println("num1과 num2는 같습니다.");
}else {
    System.out.println("셋다 해당되지 않습니다.");
}
```

### 조건 연산자(삼항 연산자)
조건 연산자는 피연산자가 세 개인 연산자이다. 이러한 조건 연산자는 간단한 if~else문을 대체하는 용도로 주로 사용된다. 밑의 예제를 보자.
```java
//조건 연산자 예제
int num1 = 10;
int num2 = 20;
int result = (false) ? num1 : num2;
System.out.println("결과 : "+ result);
```
변수 num5 는 선언과 동시에 조건연산자에 의한 값을 할당한다. ()안의 조건이 참이면 num3이 저장될 것이고 , 거짓이라면 num4가 저장될 것 이다. 하지만 임의적으로 false라는 값을 줌으로써 변수 num5에는 num4의 값, 즉 20이 저장되는것을 알 수 있다.

### switch문
조건에 따라 실행할 문장을 구분한다는 측면에서 if문과 유사하다. else if가 많이 들어가는 상황에서는 switch문이 더 좋은 선택이 될 수 있다. 밑의 예제를 보자.
```java
public static void main(String[] args) {

    int num1 = 10;
    String animal = "고양이";

    switch(animal) {
    case "강아지":
        System.out.println("강아지가 맞습니다");
    case "고양이":
        System.out.println("고양이가 맞습니다.");
    case "고라니":
        System.out.println("고라니가 맞습니다.");
    default :
        System.out.println("해당하는 동물이 없습니다.");
}
```
**레이블(Label)**

위의 switch 내부에 존재하는 키워드 case와 default를 가리켜 레이블이라고 한다. 레이블 case와 default는 코드상에서 위치를 표시하기 위해 사용된다. case는 switch 의 조건과 같은 타입을 가져야하고 같은 결과 값일 경우 그 case 이후의 값들이 출력이된다. 이것은 이후에 나오는 break문으로 제어할 수 있다. 

default는 case에서 switch와 같은 조건의 값이 없다면 실행되는 구문이다. 그리고 case와 default를 보면 들여쓰기가 되어있지 않다. 이는 책에 위치를 표시하는 레이블과 그 성격이 같다. 그리고 레이블은 책을 펼치기 전에 보여야 한다. 이와 마찬가지로 case와 default도 조금이라도 잘 보이도록 들여쓰기 대상에서 제외하는 것이 일반적이다.
 
일단 위의 결과를 보게되면 switch의 참거짓을 판단하는 매개변수로 animal이라는 변수를 주었다. 이 변수에 할당된 값은 '고양이' 이다. 당연히 콘솔에 고양이가 맞습니다. 라고 찍힐 것이라고 예상할 수 있지만 결과는 고양이가 맞습니다. 이후에 나오는 모든 조건의 결과

고양이가 맞습니다.
고라니가 맞습니다.
해당하는 동물이 없습니다.

가 찍힌다.

이는 break 라는 키워드로 case의 실행구문이 끝난 이후 사용해 주어야 하위 case들이 실행 되는 것을 막을 수 있다. 밑의 예제를 보자.
```java
switch(animal) {
case "고양이":
    System.out.println("고양이가 맞습니다.");
    break;
case "강아지":
    System.out.println("강아지가 맞습니다.");
    break;
case "고라니":
    System.out.println("고라니가 맞습니다.");
    break;
default :
    System.out.println("해당하는 동물이 없습니다.");
}
```
위의 switch문과는 다르게 각 case가 끝나는 부분에 break가 추가 되었다. 그리고 결과로는 고양이가 맞습니다. 이후의 출력은 사라졌다. 즉 if, else처럼 해당하는 조건에 맞는 결과값만이 출력이 되는 것을 확인 할 수 있다. 이는 switch문의 일반적인 사용 모델이다.

---- 

## 반복문이란?
반복문은 어떤 작업이 반복적으로 수행되도록 할 때 사용된다. while, do~while, for문등을 예로 들 수 있다.

### while문
먼저 while 문 예제를 살펴보자.
```java
public static void main(String[] args) {

    int num = 0;

    
    //While문
    while(num < 5) {
        System.out.println("I Like Java");
        num++;
    }
}
```
위의 결과는 I Like Java가 5번 출력되는 것을 알 수 있다.
- while문의 소괄호에는 반복의 조건을 명시한다. 
- true 또는 false가 와야 하므로 이를 반환하는 연산이 오게 된다. 
- 그리고 그 조건이 true를 반환하는 동안에는 횟수에 상관없이 while문의 중괄호가 반복 실행되는데 , 다음의 패턴으로 반복이 된다.
   1. 먼저 조건검사
   2. 그리고 결과가 true이면 중괄호 영역 실행
   
반면에 밑에 예제에서 다루는 do ~ while문은 다음의 패턴으로 진행한다.
1. 먼저 중괄호 영역 실행
2. 그리고 조건 검사 후 결과가 true이면 반복 결정
밑의 예제를 확인해 보자.

```java
int num2 = 0;

//do_while문
do {
    System.out.println("I Like Java " + num2);
    num2++;
}while(num2 < 5);

```
<br>

위 예제는 이전의 while문을 do-while로 바꾼것 뿐이다. 따라서 실행결과는 동일하다. 보는것처럼 while문으로 작성된 문장은 do-while로도 작성가능한 경우가 대부분다. 

따라서 "조건에 따른 반복이 필요하다. 그런데 반드시 한 번은 실행을 해야 한다." 라는 경우에는 do~while문을 사용하는 것이 괜찮다. 이 이외의 경우에는 while문 또는 이어서 소개하는 for문을 사용하는 것이 바람직하다. 그래야 선택하는 반복문에 더 많은 의미를 부여할 수 있다. 

### for문 
이전에 다루었던 while문에서 했던 예제들은 거의 반복하는 값이 정해져있었다. 이처럼 '반복의 횟수가 정해져 있는 상황' 에서는 for문을 이용해서 다음과 같이 작성하는 것이 더 간결하고 뜻도 더 잘 통한다. 밑의 예제를 보자.
```java
//for문 예제
public static void main(String[] args) {

    for(int i=0; i<5; i++) {
        System.out.println("I Love Java");
    }
}
```
위 예제에서 실행 흐름을 보자면 
1. 변수의 선언및 초기화
2. 반복 조건이 true인지 확인
3. 반복 영역을 실행 (반복 조건이 true이면)
4. 변수의 값 증가

그리고 그 이후 두번째 반복부터는 첫번째 조건인 변수의 선언및 초기화 부분은 지나치게 된다. 

### break 와 continue
break 문은 앞서 switch문을 빠져나가는 용도로 다루었었는데, 마찬가지로 반복문을 빠져나가는 용도로도 사용된다. 
보통 if문과 함께 사용되어 특정 조건이 만족될 때, 이를 감싸는 반복문을 빠져나가도록 구성이 된다. break는 이전에 다루던 것과 별 차이가 없기 때문에 따로 예제를 다루지 않는다.

continue문은 break문과 혼동하기 쉬워서 주의가 필요하다. 우선 continue는 반복문의 탈출과 거리가 멀다. 실행하던 반복문의 나머지 부분을 생략하고 프로그램의 흐름을 조건 검사 부분으로 이동시킨다. 밑의 예제를 보자.

```java
public static void main(String[] args){
    int n = 0;

    while((n++)<5) {//while 하단부에서 증가시켜줬던 구문을 이런식으로 작성할 수 있다.

        if(n == 1)
        continue;

        System.out.println("I Like Java");
    }
}
```
위의 구문을 실행시켜보면 총 4번 실행 되는 것을 알 수 있다. 0~4까지 총 5번 출력되는 것이 맞는 것 이라고 생각 할 수 있는데, 이유는 조건에 따른 continue 구문이 실행하게 되면 그 이후의 문장은 무시하고 다시 반복문의 조건 검사로 이동하게 되기때문이다.
