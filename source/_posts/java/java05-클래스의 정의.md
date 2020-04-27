---
title: JAVA - 05. 클래스의 정의
thumbnail: https://user-images.githubusercontent.com/62233873/78540149-aa58da80-782e-11ea-9754-33ae5e40ec43.jpg
date: 2020-04-26 14:45:00
tags: 
- java
- 클래스
- class
- 인스턴트
- 객체
- 생성자
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

## 클래스와 인스턴스
자바로 작성된 코드를 관찰해보면 종류에 상관 없이 모든 프로그램은 다음 두가지로 이뤄진다는 사실을 알 수 있다.

- 데이터 : 프로그램상에서 유지하고 관리해야 할 데이터
- 기능 : 데이터를 처리하고 조작하는 기능
 
이중에서 데이터는 '변수의 선언' 을 통해 유지 및 관리가 되고, 또 변수에 저장된 데이터는 '메소드의 호출'을 통해 처리가 된다. 이와 관련해서 다음 예제를 살펴보자.
<!-- more -->

```java
//BankAccountPO.java
public class BankAccountPO{

    static int balance = 0; // 예금 잔액

    public static void main(String[] args){
        deposit(10000); //입금 진행
        checkMyBalance();
        withdraw(3000);
        checkMyBalance();
    }

    public static int deposit(int amount){//입금을 담당하는 메소드
        balance += amount;
        return balance;
    }

    public static int withdraw(int amount){//출금을 담당하는 메소드
        balance -= amount;
        return balance;
    }

    public static void checkMyBalance(){//예금 조회를 담당하는 메소드
        System.out.println("잔액: " +balance);
    }
}
```
위의 클래스 BankAcountPO 를 보면 맴버변수 balance 와 메소드 deposit, withdraw, checkMyBalance 는 긴밀히 연관되어 있다. 긴밀히 연관되어있다는 것은 다음 내용을 뜻한다.

- 메소드 deposit, withdraw, checkMyBalance는 맴버변수 balance를 위한 메소드이다.

이렇듯 연관 잇는 변수와 메소드를 묶기 위해 '클래스'라는 것이 존재한다. 클래스를 이용하면 다음과 같이 변수 balance 그리고 이와 연관 있는 모든 메소드를 하나로 묶을 수 있다. 위의 코드를 가르켜 **'클래스 정의'**라 한다.

## 인스턴트 만들기
상단에 선언된 변수 balance는 '인스턴트 변수' 라고 한다. (또는 멤버변수, 필드 라고 불리기도 한다.) 인스턴트 변수 balance를 위해 존재하는 하위 메소드들은 '인스턴트 메소드'라고 한다.

인스턴트 변수는 앞서 변수의 스코프에서 다루었던 지역변수가 아니다.  인스턴트 변수가 선언된 위치는 메소드 내부가 아니므로 이 둘은 성격이 다르다. 이러한 인스턴스 변수의 중요한 특징 중 하나는 다음과 같다.

- 인스턴스 변수는 같은 클래스 내에 위치한 메소드 내에서 접근이 가능하다.

다음 예제를 살펴보자.

```java
class BankAccountPO{

    int balance = 0;

    public int deposit(int amount){
        balance += amount;
        return balance;
    }

    public int withdraw(int amount){
        balance -= amount;
        return balance;
    }

    public void checkMyBalance(){
        System.out.println("잔액: " +balance);
    }
}

public class 인스턴스만들기 {
    
    public static void main(String[] args){

        new BankAccountPO();
        /**
         * @인스턴스
         * 위의 문장을 실행하면 밑에 만들어둔 BankEx 에 정의된 변수와 메소드를 담고 있는 '인스턴스'라는 것이 
         * 만들어진다. 만들어져서 실제 메모리 공간에 존재하게 된다.
         * (인스턴스는 다른말로 객체라고도 한다. 인스턴스의 생성과 객체의 생성은 그 의미가 완전히 동일하다.)
         * 
         * 물론 다음과 같이 둘, 혹은 그 이상도 만들 수 있다.
         */
        new BankAccountPO();
        new BankAccountPO();

        /**
         * 이렇게 메모리상에 인스턴스를 만들기만 해서는 사용할 수가 없다. 
         * 만들어진 인스턴스를 참조할 수 있는 무언가가 필요하다. 
         * 그리고 이 무엇인가를 가리켜 '참조변수(Reference Variable)'이라고 한다.
         */
        BankAccountPO june; //참조변수 myAcnt1의 선언
        BankAccountPO james; //참조변수 myAcnt2의 선언
        
        /**
         * 즉 다음과 같이 참조변수를 선언하고 이를 통해서 새로 생성되는 인스턴스(객체)를 가리키게 할 수 있다.
         */

        june = new BankAccountPO02();//참조변수 june 이 새로 생성되는 인스턴스를 가리킴
        james = new BankAccountPO02();//참조변수 james 가 새로 생성되는 인스턴스를 가리킴

         /**
          * @new
          * 키워드 new 를 통해서 인스턴스를 생성하면 생성된 인스턴스의 주솟값이 반환된다.
            즉 참조변수에는 생성된 인스턴스의 주솟값이 저장되는 셈이다. 
            하지만 다음과 같이 표현하고 인식하자. 이것보다 일반적인 표현이다.
            (주솟값은 참조변수에 저장된 값이기에 본서에서는 이 값을 '참조 값' 이라고 한다.)
            - 참조변수는 인스턴스를 참조한다.
            - 참조변수는 인스턴스를 가리킨다.
            그리고 참조변수를 통해서 해당 인스턴스의 메소드를 호출하는것은 다음과 같다.
          */

          //각 인스턴스를 대상으로 예금을 진행
          june.deposit(10000);
          james.deposit(5000);

          //각 인스턴스를 대상으로 잔액을 조회
          System.out.println("myAcnt1의 잔액 :");
          june.checkMyBalance();

          System.out.println("myAcnt2의 잔액 :");
          james.checkMyBalance();

          /**
           * 코드와 실행 결과를 보면, 참조변수 준과 제임스가 가리키는 인스턴스가 
           * 서로 다른 인스턴스인 것을 알 수 있다.
           */

           /**
            * @참조변수에 null 대입
              때로는 참조변소가 참조하는 인스턴스와의 관계를 끊고 아무런 인스턴스도 참조하지 않도록
              할 필요가 있다. 그리고 이때에는 다음과 같이 참조변수에 null을 대입하면 된다.
            */

            james = null;
            june = null;
    }
}
```
<br>

## 인스턴스의 구분
앞서 정의한 BankAccount클래스를 다시 관찰해보자. 은행에서는 고객이 계좌를 개설할 때마다 이 클래스의 인스턴스를 생성해야 한다.

그런데 문제는 인스턴스를 구분할 수 있는 정보가 빠졌다는 것이다. 즉 이전 예제에 최소한 다음 두가지 정도는 추가가 되어야 한다. 그래야 누구의 계좌인지 구분할 수 있다.

- 계좌번호 
- 주민번호 

이것을 반영하여 새로운 클래스를 만들어보자
```java
class 인스턴트만들기{
    
	public static void main(String[] args) {

		BankAccount jaebeom = new BankAccount();
		
		jaebeom.initAccount("123-456-789", "950621", 10000);
		jaebeom.deposit(5000);
		jaebeom.checkMyBalance();
		
		BankAccount jongwon = new BankAccount();
		
		jongwon.initAccount("321-654-987", "960113", 10000);
		jongwon.withdraw(3000);
		jongwon.checkMyBalance();
	}

}

class BankAccount{
	String accNumber;//계좌번호
	String ssNumber;//주민번호
	int balance = 0;//예금 잔액
	
	//초기화를 위한 메소드
	public void initAccount(String acc, String ss, int bal) {
		accNumber = acc;
		ssNumber = ss;
		balance = bal; //계좌 개설 시 예금액으로 초기화
	}
	
	public int deposit(int amount) {
		balance +=amount;
		return balance;
	}
	
	public int withdraw(int amount) {
		balance -=amount;
		return balance;
	}
	
	public void checkMyBalance() {
		System.out.println("계좌번호:"+accNumber);
		System.out.println("주민번호:"+ssNumber);
		System.out.println("잔액:"+balance+"\n");
	}
}
```
<br>

이번 예제에서는 새로운 메소드 initAccount가 추가되었다. 이 메소드는 다음과 같은 부분에서 다른 메소드들과 성격상 구분이 된다. 

-인스턴스의 초기화를 위한 메소드이다.
-때문에 인스턴스 생성 시 반드시 한번 호출해서 초기화를 진행해야한다.

그러나 위와 같이 메소드를 정의하지 않고 **'생성자(Constructor)'**라는 것을 정의해서 인스턴스의 초기화를 진행할 수도 있다. 생성자는 인스턴스 생성 과정에서 초기화를 위해 자동으로 호출되는 일종의 메소드이다. 

## 생성자의 정의
생성자는 메소드와 모습이 같다. 따라서 생성자를 '생성자 메소드' 로 표현하는 경우도 있다. 그러나 생성자는 다음과 같은 부분에서 메소드와 차이가 있다. 달리 말하면 이는 생성자가 되기 위한 조건이기도 하다.

- 생성자의 이름은 클래스의 이름과 동일해야 한다.
- 생성자는 값을 반환하지 않고 반환형도 표시하지 않는다. 

위의 조건을 모두 만족하면 이는 자바 컴파일러에 의해서 생성자로 인식된다. 따라서 인스턴스 생성 시 자동으로 호출되어 인스턴스를 초기화 하게 된다. 그럼 앞서 예제에서 인스턴스 초기화를 위해 생성자를 만들어보자

```java
class Person{

    String name;
    int age;

    //생성자
    public Person(String name, int age){
        this.name = name; //this키워드는 class의 인스턴스 변수 자신을 가리킨다. 나중에 더 자세히 다루어보자.
        this.age = age;
    }

    public void myInfo(){
        System.out.println("저의 이름은 " +name+" 입니다.");
        System.out.println("나이는 "+ age +" 입니다.");
    }
}
```
위의 예제에 생성자를 보면 클래스와 이름이 동일하다. 그리고 반환하지 않으며 , 반환형도 선언하지 않았다. 따라서 생성자의 조건을 모두 갖췄다. 그리고 인스턴스를 메소드 main에서 생성할때 매개변수로 이름과 나이가 전달이 된다.

즉 위와같이 문장을 구성하면 '인스턴스 생성 마지막 단계' 에서 다음의 생성자가 호출되면서 값들이 전달된다. 그리고 이 값들로 인스턴스 변수가 초기화 된다.

생성자와 관련하여 다음 사실을 반드시 기억해야 한다.

- 인스턴스 생성의 마지막 단계는 생성자 호출이다.
- 어떠한 이유로든 생성자 호출이 생략된 인스턴스는 인스턴스가 아니다.

### 디폴트 생성자(Default Constructor)
인스턴스 생성의 마지막 단계는 생성자 호출이라 하였다. 그리고 생성자 호출이생략된 인스턴스는 인스턴스가 아니라고 하였다. 하지만 앞서 생성자가 없는 클래스를 수차례 정의하였고 이들을 대상으로 인스턴스를 생성한 바 있다. 그렇다면 이렇게 생성된 인스턴스는 인스턴스가 아니란 뜻인가?
사실 다음과 같이 생성자를 생략한 상태의 클래스를 정의하면 자바 컴파일러가 '디폴트 생성자' 라는 것을 클래스의 정의에 넣어준다.

```java
class Person{
     
      //디폴트 생성자
      public Person(){
        //empty
      }
}
```
위에서 보이듯이, 디폴트 생성자는 인자를 전달받지 않는 형태로 정의되어 삽입된다. 물론 내부적으로 하는 일도 없다. 하지만 이로 인해서 인스턴스의 생성 규칙인 '생성자의 호출' 은 유지가 된다. 생성자를 정의하지 않더라도 말이다. 그런데 컴파일러에 의해서 디폴트 생성자가 삽입이 되더라도 생성자는 직접 정의해주는것이 좋다.    아주 예외적인 상황이 아니라면, 생성자가 필요 없는 클래스는 잘 정의된 클래스가 아닐 확률이 높기 때문이다.

> 본 문서는 책의 일부 내용을 발췌한 것으로서 온오프라인 상의 무단 배포를 금합니다.
