---
title: JAVA - 13. static 응용 - Singleton
thumbnail: https://github.com/gojaebeom/hexo-blog-server/blob/master/themes/icarus/source/images/%EC%9E%90%EB%B0%94/java-thumbnail.jpg?raw=true
author: JaeBeom Go
date: 2020-04-29 21:20:00
tags:
  - 자바
  - static
  - singleton
  - 싱글톤
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

## 싱글톤 패턴(Singleton Pattern)이란?
싱글톤이란 어떤 클래스가 최초 한번만 메모리를 할당하고 그 메모리에 객체를 만들어 사용하는 디자인 패턴을 말한다.<!-- more -->


## 싱글톤이 사용되는 이유
한번의 객체 생성으로 재 사용이 가능하기 때문에 메모리 낭비를 방지할 수 있다. 또한 싱글톤으로 생성된 객체는 무조건 한번 생성으로 전역성을 띄기에 다른 객체와 공유가 용이하다.


## 싱글톤 예제
우리가 프로그램을 만들다보면 단 하나만 존재해야 하는 인스턴스들이 존재할 수 있다. 예를 들어 특정 학교와 학생이라는 객체를 만든다고 할 때 학생은 다수 존재하기 때문에 생성자를 계속 만들어 사용해왔다. 하지만 학생들을 대상으로 학교는 1이상 생성하는 것은 비효율적 이므로 한번만 생성할 수 있게 만들어야 한다. 그렇다면 우리는 기술적으로 어떻게 객체를 최초 한번만 생성하게 할 수 있을까?

객체를 새로 생성할 때 우리는 생성자를 호출하여 만들 수 있다. 그렇다면 생성자를 외부에서 호출하지 못하게 막는다면 어떨까?

```java
public class School{
    private School(){...}
}
```
위와 같이 생성자를 private로 정의하면 직접 생성자를 정의하였기 때문에 자바가상머신이 디폴트 생성자를 만들어주지도 않는다. 즉 외부에서 생성자를 호출 할 수 없게 되는 것 이다. 하지만 위와 같은 상황에선 School 의 객체를 아예 생성할 수 없기 때문에 몇가지 코드를 더 추가해 주어야 한다.

```java
public class School{
    private static School instance = new School();
    private School(){...}

    public static School getInstance(){
        return instance;
    }
} 
```
private 는 클래스 내부에선 접근할 수 있기 때문에 내부에서 생성자를 호출하여 새로운 객체를 만들고 `School타입`의 참조변수에 할당된 것을 볼 수 있다. 그리고 `getInstance` 메소드를 통해 참조변수(생성된 객체의 주솟값을 참조) `instance`를 반환함으로써 외부에서 이 값을 통해 `School 객체`를 사용할 수 있을 것 이다.

여기서 중요한 것은 참조변수 instance가 static 변수라는 점 인데, 만약 instance가 non-static한 변수였다면 생성자를 통해 객체가 생성될 때 존재하게 될 것이다. 하지만 static 변수는 자바가상머신이 클래스를 읽어올때 생성되는 변수이다. 그렇기때문에 생성자를 호출하지 않아도 외부에서 클래스를 통해 사용되어질 수 있는 것 이다. 물론 정보은닉적인 관점에서 instance 변수 자체는 private 키워드를 통해 외부에서 조작하지 못하게 하고 getInstance 메소드를 통해서만 사용될 수 있게 하였다.

그렇다면 자연스럽게 getInstance 메소드가 static 메소드인 이유도 알 수 있다. 일반 인스턴스 메소드 역시 객체가 생성될때 사용할 수 있다. 때문에 static 메소드로 정의 함으로써 외부에서 클래스를 통해 바로 호출이 가능하게 해야하는 것 이다.

```java
public class SchoolTest {
    public static void main(String[] args) {
        School s1 = School.getInstance();
        School s2 = School.getInstance();
        System.out.println(s1);
        System.out.println(s2);
    }
}
```
SchoolTest 클래스를 테스트한 결과 School 클래스를 객체 생성없이 바로 `getInstance()` 를 호출하고 있다. `getInstance`가 반환하는 `참조변수 instance`는 클래스를 로딩하는 시점에서 객체가 생성되어 주솟값을 담고 있기때문에 참조변수의 값으로써 사용되어질 수 있다. 위의 참조변수 s1와 s2의 값을 출력해보면

test.School@79698539
test.School@79698539

위와 같이 같은 인스턴스를 참조하고 있는 것을 알 수 있다.

## 싱글톤의 문제점
전역성을 띄면서 다른 객체와 공통으로 사용하는 경우와 같은 몇 가지 케이스에서만 사용할 때 효율적이며 그 외에는 문제점이 생길 수 있다.
일단 싱글톤으로 만든 객체의 역할이 간단한 것이 아닌 역할이 복잡한 경우라면 해당 싱글톤 객체를 사용하는 다른 객체간의 결함도가 높아져서 객체 지향 설계 원칙에 어긋나게 된다. (개방-폐쇄)