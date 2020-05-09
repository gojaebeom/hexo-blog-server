---
title: JAVA - 14. 배열
thumbnail: https://github.com/gojaebeom/hexo-blog-server/blob/master/themes/icarus/source/images/%EC%9E%90%EB%B0%94/java-thumbnail.jpg?raw=true
author: JaeBeom Go
date: 2020-04-30 20:20:00
tags:
  - 자바
  - 배열
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

## 배열이란?
배열은 자료형이 같은 둘 이상의 값을 저장할 수 있는 메모리 공간을 의미한다. 그리고 배열은 그 구조에 따라서 1차원 배열과 2차원 이상의 다차원 배열로 나뉜다. <!-- more -->

### 1차원 배열
1차원 배열은 다음과 같이 정의할 수 있다.
- 타입이 같은 둘 이상의 데이터를 저장할 수 있는 1차원 구조의 메모리 공간

그런데 자바는 배열도 인스턴스로 처리한다. 즉 자바에서는 배열도 인스턴스 이다. 다음 예제를 보자.

```java
public static void main(String[] args) {
	int[] ref = new int[5];//길이가 5인 int형 1차원 배열의 생성문
}
```
<br>

위 문장에서 등호를 기준으로 왼편, 오른편에 위치한 것은 각각 참조변수의 선언과 배열의 생성이다. 

물론 다음과 같이 참조변수의 선언과 배열 인스턴스의 생성을 구분할 수도 있다.

```java
public static void main(String[] args){
    int[] ref;
    ref = new int[5];

    //물론 int형 말고도 다양한 자료형으로 배열을 생성할 수 있다.
    double[] db = new double[5];
    float[] f = new float[3];
    String[] str = new String[10];
    
    //각 배열에 대한 길이 
    System.out.println(db.length);
    System.out.println(f.length);
    System.out.println(str.length);
}
```
<br>

위의 문장을 보면 각 배열의 인스턴스 변수 length에 접근하여 배열의 길이 정보를 출력하였다. 이렇듯 인스턴스 변수에 접근이 가능하다는 것은 배열이 인스턴스임을 보인는 결과이기도 하다.

## 배열 저장과 참조

```java
int[] arr = new int[3];
```
<br>

위 선언된 배열 arr에 첫 번째 공간에 값을 저장하는 방법은 다음과 같다.
```java
arr[0] = 7;
```
<br>

이렇듯 배열 요소의 위치를 지정하는 인덱스 값은 0에서부터 시작한다. 따라서 배열 arr의 두번째 , 새 번째 요소에 값을 저장하는 방법은 다음과 같다.

```java
arr[1] = 3; //2번째
arr[2] = 5; //3번째
```
<br>

배열에 저장된 값을 참조하는 방법도 이와 유사하다. 다음은 배열 arr의 모든 요소에 저장된 값을 더하는 방법을 보여준다. 
```java
int num = arr[0] + arr[1] + arr[2];
```
<br>

## 배열의 생성과 초기화
배열도 변수와 마찬가지로 생성과 동시에 초기화가 가능하다. 기본적인 배열의 생성 방식은 다음과 같다.
```java
int[] arr = new int[3];
```
<br>

이 배열을 생성과 동시에 초기화하려면 초기화할 값들을 다음과 같이 중괄호를 이용해서 나열하면 된다. 
```java
//int[] arr2 = new int[3] {1, 2, 3}; //컴파일 오류 발생
```
<br>
	
그런데 위의 문장에서는 초기화할 값들의 수를 통해 배열의 길이 정보를 계산할 수 있으므로, 이경우 배열의 길이 정보를 생략하도록 약속하였다. 즉 위의 문장은 다음과 같이 수정해야 한다.
```java
int[] arr2 = new int[] {1, 2 ,3};
```
<br>
	
위의 문장을 통해 생성되는 배열의 길이는 3이다. 그리고 위의 문장은 다음과 같이 줄여서 표현할 수 도있다.
```java
int[] arr3 = {1, 2, 3};
```
<br>
	
### 배열의 선언 두가지 방법
다음과 같이 배열을 생성하는 문장에서도 이 둘은 동일한 의미로 사용이 된다.
```java
int[] ar1 = new int[3]; //조금 더 선호하는 방법
int ar2[] = new int[3];
```
<br>
	
	
	
### 배열의 참조 값과 메소드
배열도 인스턴스이므로 메소드 호출 시 참조 값의 전달이 가능하다. 예를 들어 다음과 같이 배열의 참조 값을 인자로 전달할 수 있다.
```java
public static void main(String[] args) {
    int[] arr = {1, 2, 3};
    System.out.println(sumOfAry(arr));
}
	
//물론 아래 메소드처럼 메소드 생성시 배열의 참조변수를 매개변수로 선언해야 한다.
static int sumOfAry(int[] arr) {
    int sum = 0;
    for(int i = 0; i< arr.length; i++) {
        sum += arr[i];
    }
    return sum;
}
```
<br>

이 과정에서 배열이 새로 생성되는 것은 아니다. 그저 배열 인스턴스를 참조할 수 있는 참조 값만 인자로 전달이 되고, 이 값을 매개변수로 받을 뿐이다. 그리고 다음과 같이 배열의 참조 값을 반환하는 메소드를 정의하는 것도 가능하다.
```java
static int[] reIntArr(int x) {
    int[] arr = new int[x];
    return arr;//배열의 참조값을 반환
}
```

## main 메서드의 매개변수
지금까지 배열에 대해서 알아보았다. 그렇다면 main메소드의 매개변수 선언이 무엇을 의미하는지 알 수 있을 것이다.

매개변수로 String 배열의 참조변수가 선언되었다. 따라서 다음과 같이 main 메소드를 호출해야 한다. (main 메서드를 직접 호출한다는 가정하에 작성된 코드이다.)
```java
String[] arr = new String []{"Coffee", "Milk", "Orange"};
main(arr);
```
<br>

물론 코드상에서 main메소드를 위와 같이 직접 호출하지는 않는다. 게다가 우리가 main 메소드에 전달할 String 배열을 만들지도 않는다. 

그렇다면 어떻게 String 배열이 만들어지고 또 main 메소드의 인자로 전달되는 것일까?

String 배열을 구성하는 것도 main 메소드를 호출하는 것도 가상머신에 의해 이뤄지는 일이다. 다만 String 배열을 구성할 문자열은 프로그램 사용자가 전달해야 한다. 

예를 들어서 Simple.class 에 위치한 main 메소드를 다음과 같이 호출한다고 가정해보자. 
- C:\JavaStudy> java Simple

그러면 String 배열이 다음과 같이 구성이 되어 main 메소드에 전달이 된다. 
```java
String[] arr = new String[] {};
```
<br>

즉 빈 String 배열이 생성되어 main 메소드의 호출이 이뤄진다. 반면 다음과 같이 실행을 하면, 
- C:/JavaStudy> java Simple Coffee Mile Orange

즉 실행 명령문에 이어서 공백을 구분 기준으로 문자열을 입력하면, 이 내용을 대상으로 String 배열이 구성되고, 이 배열의 참조 값이 전달되면서 main 메소드가 호출이 된다. 그럼 이러한 내용의 확인을 위해 다음 예제를 실행해보자.
```java
public static void main(String[] args) {
    for(int i=0; i<args.length; i++) {
        System.out.println(args[i]);
    }
}
```
<br>

Coffee, Mile, Orange가 뜨는 것을 볼 수 있을 것이다.(참고로 이클립스에선 javac , java 명령어를 알아서 처리해주기때문에 cmd를 활용하여 명령어를 직접 입력해보는 것이 좋다)

이 밖에 다차원 배열등이 있지만 설명하는 것보단 직접 해보는 것이 더 효율적인 것 같다.

- 배열 관련 예제코드
    - [예제 01](https://github.com/gojaebeom/java_tutorial/blob/master/src/ch10_%EB%B0%B0%EC%97%B4/%EB%B0%B0%EC%97%B4_%EC%98%88%EC%A0%9C01.java)
    - [예제 02](https://github.com/gojaebeom/java_tutorial/blob/master/src/ch10_%EB%B0%B0%EC%97%B4/%EB%B0%B0%EC%97%B4_%EC%98%88%EC%A0%9C02.java)
