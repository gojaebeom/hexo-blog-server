---
title: JAVA - 18. 다형성
thumbnail: https://github.com/gojaebeom/hexo-blog-server/blob/master/themes/icarus/source/images/%EC%9E%90%EB%B0%94/java-thumbnail.jpg?raw=true
author: JaeBeom Go
date: 2020-05-03 21:20:00
tags:
  - 자바
  - 상속
  - 다형성
categories:
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

## 다형성(Polymorphism)
다형성은 상속과 깊은 관계가 있다. 객체지향개념에서 다형성이란 '여러 가지 형태를 가질 수 있는 능력'을 의미하며, 자바에서는 한 타입의 참조변수로 여러 타입의 객체를 참조할 수 있도록함으로써 다형성을 프로그램적으로 구현하였다.<!-- more -->

## 다형성의 장점
다양한 여러 클래스를 하나의 자료형(상위 클래스)로 선언하거나 형변환 하여 각 클래스가 동일한 메서드를 오버라이딩 한 경우, 하나의 코드가 다양한 구현을 실행할 수 있다.

## 다형성 예제
```java
class Animal{
    public void move(){
        System.out.println("동물이 움직인다.");
    }
}
class Human extends Animal{
    public void move(){
        System.out.println("사람이 두발로 움직인다.");
    }
}
class Dog extends Animal{
    public void move(){
        System.out.println("강아지가 네발로 움직인다.");
    }
}
class Eagle extends Animal{
    public void move(){
        System.out.println("독수리가 날개로 움직인다.");
    }
}
```
위 예제는 `Animal` 클래스를 각 사람 , 강아지, 독수리 클래스가 상속 받아 `move` 메소드를 제정의(Overriding)하는 코드이다.

```java
public class PolymorphismTest{
    public static void main(String[] args){
        Animal human = new Human();//업캐스팅
        Animal dog = new Dog();//업캐스팅
        Animal eagle = new Eagle();//업캐스팅
    }
}
```
`Human`, `Dog`, `Eagle` 클래스는 Animal 클래스를 상속받으므로 위와 같이 Animal 참조변수로 형변환하여 참조할 수 있다. 이를 업캐스팅(Up-casting)이라고 한다.

만약 위와 같은 상황에서 각 객체의 `move` 메소드를 한번식 호출하는 코드를 작성하라고 한다면 어떻게 할 수 있을까?

```java
public class PolymorphismTest{
    public static void main(String[] args){
        Animal human = new Human();//업캐스팅
        Animal dog = new Dog();//업캐스팅
        Animal eagle = new Eagle();//업캐스팅

        ArrayList<Animal> animalList = new ArrayList<Animal>();
        animalList.add(human);
        animalList.add(dog);
        animalList.add(eagle);

        for(Animal animal : animalList){
            animal.move();
        }   
    }
}
```
`human`, `dog`, `eagle` 은 서로 다른 클래스에서 생성된 객체이다. 하지만 같은 부모클래스형으로 참조되어, 세 객체 모두 `ArrayList`의 `Animal` 타입으로 추가될 수 있었다. 이 후 for each 문으로 `animal.move()` 메소드를 한번 호출한 것으로 세 객체의 move 메소드를 호출하는 것을 볼 수 있다. 이것이 다형성의 장점이다.

## 다형성을 사용하지 않은 예제
```java
public class AnimalTest {
    public static void main(String[] args) {
        Human human = new Human();
        Dog dog = new Dog();
        Eagle eagle = new Eagle();

        human.move();
        dog.move();
        eagle.move();
    }
}
```
위와 같은 경우 코드의 양으로 보면 더 간단해 보일 수 있다. 하지만 Animal 클래스를 상속받는 다른 클래스가 더 많아진다고 가정해보자. 사람, 개, 독수리 뿐만아니라 동물의 범주에 모두 해당되는 10개체가 넘는 클래스만 정의하면 반복되는 코드량이 더 많아 질 것이다. 프로그램은 코드의 반복적인 작업을 줄이는것이 바람직하다. 이와 같은 관점에서 보면 다형성을 이용하여 작업하는 것이 이후의 코드 관리면에서도 큰 장점을 보인다.

## 하위 클래스로 형변환
[상속](http://localhost:4000/2020/05/01/java/JAVA-16.%EC%83%81%EC%86%8D/#more) 편에서 다루었던 업캐스팅은 묵시적인 형변환이다. 위의 예제에서도 알 수 있듯이 자동적으로 형변환이 된다. 만약 다시 자신의 참조변수에 참조하려고 할 때 우리는 `다운캐스팅`을 하여야 한다.
```java
Animal a = new Human(); // 업캐스팅
Human h = (Human)a; // 다운캐스팅
```
## 다운캐스팅(Down Casting)
묵시적으로 상위 클래스 형변환된 인스턴스가 원래 자료형(하위클래스)로 변환되어야 할 때 다운캐스팅이라 한다.
- 하위클래스로의 형 변환은 명시적으로 되어야 한다.