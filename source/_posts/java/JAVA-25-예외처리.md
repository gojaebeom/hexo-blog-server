---
title: JAVA - 25. 예외 처리
thumbnail: https://user-images.githubusercontent.com/62233873/78540149-aa58da80-782e-11ea-9754-33ae5e40ec43.jpg
date: 2020-05-16 21:20:00
tags: 
- java
- 예외처리
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

## 오류, 에러(error)란 무엇인가?
프로그램을 실했할 때 오작동이나 비정상적으로 종료되는 원인을 오류나 에러라고 한다. 에러는 컴파일 에러와 런타임 에러로 나뉜다.<!-- more -->
- 컴파일 오류: 프로그램 코드 작성 중 발생하는 문법적 오류
- 런타임 오류: 실행 중인 프로그램이 의도 하지 않은 동작을 하거나(bug) 프로그램이 중지되는 오류 

## 예외처리
자바에서는 실행 시 발생할 수 있는 오류를 '에러(error)'와 '예외(Exception)'으로 구분한다. 에러는 메모리의 부족, stack over flow와 같이 발생하게 되면 복구할 수 없는 심각한 오류이고, 예외는 발생하더라도 수습할 수 있을 정도의 프로그래머가 예외처리를 통해 막을 수 있는 오류이다.
- 시스템 오류(error)
  - 가상 머신에서 발생, 프로그래머가 처리할 수 없음
  - 동적 메모리를 다 사용한 경우, stack over flow 등
- 예외(Exception)
  - 프로그램에서 제어할 수 있는 오류
  - 읽으려는 파일이 없는 경우, 네트웍이나 소켓 연결 오류 등

## 예외 클래스(Exception)
예외에 대한 최상위 클래스로 Exception이 있다. 그리고 입출력, 런타임 예외 등 각각 해당하는 예외를 담당하는 클래스들이 이를 상속하는 모습이다.  
![이미지](https://github.com/gojaebeom/hexo-blog-server/blob/master/themes/icarus/source/images/%EC%9E%90%EB%B0%94/exception/example1.png?raw=true)


## try-catch
자바에서 예외에 대한 처리는 다음과 같이 `try-catch` 구문으로 정의할 수 있다.
```java
try{
  //예외가 발생 할 수 있는 코드 부분
}catch(처리할 예외 타입 e){
  //try블록 안에서 예외가 발생했을 때 수행되는 부분
}finally{
  //예외 발생 여부와 상관 없이 항상 수행 되는 부분
  //리소스를 정리하는 코드를 주로 씀
}
```
기본적인 `try catch` 구문은 위와 같이 이루어 진다. `try`문에서 `Exception` 예외가 발생할 경우 `catch` 구문을 실행하게 된다. 
- 발생한 예외와 일치하는 catch 문이 있는지 확인
- 일치하는 catch문이 있다면 catch 블럭 내의 문장을 실행하고 try catch문을 빠져 나감
- finally는 예외 발생 여부와 상관 없이 항상 수행됨

### try-catch 활용
```java
public static void main(String[] args){
  int[] arr = new int[3];
  for(int i=0; i<4; i++){
    System.out.println(arr[i]);
  }
  System.out.println("hi");
}
```
위의 코드에서는 에러가 난다. 배열 arr의 크기는 0~2까지 총 3인데 for문은 4번 반복하면서 arr의 4번째 공간의 값을 출력하려고하는 부분에서 나는 오류이다. 그리고 이후의 hi문자를 출력하지 않고 에러가나는 부분에서 프로그램이 멈추는 것을 볼 수 있다. 다음 예제를 보자.

```java
public static void main(String[] args){
  int[] arr = new int[3];
  try{
    for(int i=0; i<4; i++){
      System.out.println(arr[i]);
    }
  }catch(ArrayIndexOutOfBoundsException e){
    System.out.println(e);
  }
  System.out.println("hi");
}
```
에러가 날것 같은 부분을 `try`구문으로 감쌌다. 그리고 에러가 나면 `catch` 구문에서 에러원인을 출력하는 것을 볼 수 있다. 여기서 중요한 점은 에러가 났음에도 그에 대한 원인만 출력하고 프로그램은 계속 실행되고 있다. 이처럼 예외에 대한 오류는 예외처리를 통해 프로그래머가 프로그램의 비정상적인 종료를 막을 수 있다.

## 예외의 종류
- **NullPointException** : null 레퍼런스를 참조할 때 발생
- **ClassCastExeption** : 변환할 수 없는 타입으로 객체를 변환할 때 발생
- **OutOfMemoryException** : 메모리가 부족한 경우 발생
- **IOException** : 입출력 동작 중 인터럽트 발생. 자바에서 입출력 함수를 사용하는 경우 반드시 이 예외처리를 해주도록 되어있다.
  - 인터럽트(interrupt) : 마이크로프로세서(CPU)가 프로그램을 실행하고 있을 때, 입출력 하드웨어 등의 장치나 또는 예외상황이 발생하여 처리가 필요할 경우 마이크로프로세서에게 알려 처리할 수 있도록 하는 것
- **NumberFormatException** : 문자열이 나타내는 숫자와 일치하지 않는 타입의 숫자로 변환하는 경우 발생한다.
- **IllegalArgumentException** : 잘못된 인자를 전달하는 경우 발생한다.
- **ArrayIndexOutOfBoundsException** : 배열의 범위를 벗어나서 접근을 하는 경우 발생한다.