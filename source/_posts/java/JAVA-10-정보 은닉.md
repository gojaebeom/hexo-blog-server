---
title: JAVA - 10. 정보 은닉
thumbnail: https://github.com/gojaebeom/hexo-blog-server/blob/master/themes/icarus/source/images/%EC%9E%90%EB%B0%94/java-thumbnail.jpg?raw=true
author: JaeBeom Go
date: 2020-04-28 19:20:00
tags:
  - 자바
  - 정보 은닉
  - 접근 제어자 
  - 접근 제한자
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

## 정보 은닉
자바에서 말하는 정보는 클래스의 인스턴스 변수를 의미한다. 따라서 정보를 은닉한다는 것은 인스턴스 변수를 숨긴다는 뜻이다. 자바에서는 '접근 제어자'(접근 제한자, 접근 제어 지시자 등 다양하게 불린다)를 통해  접근의 허용 수준을 결정할 때 선언하는 키워드를 제공한다.<!-- more -->

## 접근 제어자
접근 제어자의 종류는 다음과 같이 4가지 이다.
- public, protected, private, default

이중에서 default는 키워드가 아닌, 아무런 선언도 하지 않은 상황을 의미한다. 비록 이는 키워드가 아닌 일종의 상황이지만 이 역시 접근 제한자의 한 종류로 구분을 한다. 

그리고 이러한 선언을 할 수 있는 대상은 다음 두 가지이다.
- 클래스의 정의
- 클래스의 맴버 변수와 메소드
 
클래스의 정의를 대상으로는 다음 두 가지 선언이 가능하다.
- 클래스 정의대상 : public ,default

그리고 맴버 변수와 메소드를 대상으로는 다음 네 가지 선언이 모두 가능하다.
- public, protected, private, default

그럼 이제 각각의 기능을 알아보자. 

### 클래스 정의 대상의 public 과 default 선언이 갖는 의미
- public : 어디서든 객체(인스턴스) 생성이 가능하다. 
- default : 동일 패키지로 묶인 클래스 내에서만 인스턴스 생성을 허용한다.

### 인스턴스 멤버 대상의 public , protected, private, default 선언이 갖는 의미
 
|  접근제한자 |   클래스 내부  |  동일 패키지  |  상속 받은 클래스  |  이외의 영역|
|------------|:-------------- :|-------------:|:------------------:|-------------:|
|    private  |        o       |        x      |         x         |       x
|    default  |        o       |        o      |         x         |       x
|   protected |        o       |        o      |         o         |       x
|    public   |        o       |        o      |         o         |       o 
    
위의 표에서 말하는 이외의 영역은 다른 패키지에 속한 클래스를 뜻한다. 즉 서로 다른 패키지에 속한 두 클래스 사이의 접근을 의미한다. 그리고 위 표의 내용을 기준으로 접근 허용 범위에 대하여 다음과 같이 이해하고 있는 것도 도움이 된다. 

- public >  protected > default > private

## 정보 은닉이 필요한 이유
우리가 어떠한 클래스를 정의한다고 생각해보자. 만약 사용자 입장에서 잘못된 조작을 할 수 있는 예외상황으로 인해 우리가만든 프로그램이 잘못사용될 경우 그 프로그램은 잘 짜여진 프로그램이 아닐 것 이다.

다음 예제를 보자
```java
public class MyDate{
    int day;
    int month;
    int year;

    public void showDate() {	
		System.out.println( year + "년" + month + "월 " + day + "일."  );
	}
}

public class MyDateTest{
    public static void main(String[] args) {
		MyDate date = new MyDate();
		date.day = 100;
		date.month = 100;
		date.year = 2019;
		date.showDate(); //2019년 100월 100일. 출력
	}
}
```
위 예제는 날짜값을 받아서 날짜를 출력하는 프로그램이다. 사용자가 맴버변수에 바로 접근하여 값을 할당하고, 그에 맞는 값이 출력되는 것을 볼 수 있다. 여기서 문제는 `2019년 100월 100일` 과 같은 날짜가 출력되는것이 정상인가? 존재하지 않는 날짜가 출력되기때문에 이는 잘못된 프로그램이라고 할 수 있다.

이와같이 사용자가 직접 값을 조작하면 예외 상황이 일어날 수 있는 코드들은 외부에서 접근하지 못하게 막아놓고 메소드를 통해 값을 받아 잘못된 값이 들어오면 조취를 취할 수 있게 하는 것이 정보은닉의 대표적인 예 이다. 다음 예제를 보자.

```java
public class MyDate {
    private int day; 
    private int month;
    private int year;

    //조건이 유효한지 체크하는 변수
    private boolean isValid = true;

    public void setDay(int day) {
        if(day < 1 || day > 31)
            isValid = false;
        else
            this.day = day; 
    }

    public void setMonth(int month) {
        if( month < 1 || month > 12) 
            isValid = false;
        else 
            this.month = month;
    }

    public void setYear(int year) {
        if(year < 1900 || year > 2020)
            isValid = false;
        else
            this.year = year;
    }

    public void showDate() {
        if(isValid) 
            System.out.println( year + "년" + month + "월 " + day + "일."  );
        else 
            System.out.println("정상적인 값이 아닙니다.");  
    }
}
```
맴버변수에 `isValid` 라는 변수를 `true`로 선언과 동시에 초기화 하였다. 유효성 검사를 하기위한 변수이다. 그리고 모든 맴버변수들을 private로 외부로부터 숨기고 각 변수들에게 값을 담을 수 있는 public 메소드들을 정의하였다. 그리고 이 메소드는 내부적으로 잘못된 값이 들어오면 `isValid`의 값을 `false`로 바꾼다. 이후에 날짜를 출력하는 `showDate` 메소드는 `isValid`의 값이 참일때 시간을 보여주고 거짓이면 실패 문구를 출력한다. 결과적으로 값이 하나라도 잘못 입력되면 날짜를 띄울 수 없게 만든 코드이다.

```java
public class MyDateTest{
    public static void main(String[] args){
        MyDate date = new MyDate();
    	date.setDay(0);
    	date.setMonth(5);
    	date.setYear(2020);
    	date.showDate();//정상적인 값이 아닙니다.
    }
}
```

위의 클래스를 `MyDateTest` 클래스에서 테스트해보면 잘못된 값이 하나라도 존재하면 '정상적인 값이 아닙니다.'(살짝 불친절한..) 문구가 나오는 것을 알 수 있다. 물론 값이 제대로 입력되면 정상적으로 날짜를 출력한다. 

이와 같이 프로그램을 만들다보면 외부로부터의 접근을 숨겨야하는 정보들이 있다. 그러한 정보들은 외부로부터의 접근을 막고 만든이가 의도하는대로 사용자가 프로그램을 다루게 하는것이 정보 은닉이 필요한 이유라 생각한다.