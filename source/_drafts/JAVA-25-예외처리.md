---
title: JAVA - 24. 컬랙션 프레임워크
thumbnail: https://user-images.githubusercontent.com/62233873/78540149-aa58da80-782e-11ea-9754-33ae5e40ec43.jpg
date: 2020-05-13 21:20:00
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

## 오류란 무엇인가?
우리는 지금까지 프로그래밍을 하면서 여러 오류들을 보았다. 대표적으로 컴파일 오류와 런타임오류로 구분지어보자.
- 컴파일 오류: 프로그램 코드 작성 중 발생하는 문법적 오류
- 런타임 오류: 실행 중인 프로그램이 의도 하지 않은 동작을 하거나(bug) 프로그램이 중지되는 오류 

## 예외처리
- 시스템 오류(error)
  - 가상 머신에서 발생, 프로그래머가 처리할 수 없음
  - 동적 메모리를 다 사용한 경우, stack over flow 등
- 예외(Exception)
  - 프로그램에서 제어할 수 있는 오류
  - 읽으려는 파일이 없는 경우, 네트웍이나 소켓 연결 오류 등

## 예외 클래스(Exception)
예외에 대한 최상위 클래스로 Exception이 있다.
![이미지]()


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

### console.log
```java

```

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
에러가 날것 같은 부분을 `try`구문으로 감쌌다. 그리고 에러가 나면 `catch` 구문에서 에러원인을 출력하는 것을 볼 수 있다. 여기서 중요한 점은 에러가 났음에도 그에 대한 원인만 출력하고 프로그램은 계속 실행되고 있다.
