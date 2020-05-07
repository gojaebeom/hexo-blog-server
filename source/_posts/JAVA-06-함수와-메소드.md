title: JAVA - 06. 함수와 메소드
author: JaeBeom Go
date: 2020-05-06 18:51:12
tags:
---
## 함수(Function)란?
프로그래밍에서 함수는 하나의 기능을 수행하는 코드의 단위이다.

이전의 객체지향 프로그래밍이 무엇인가 다루었을 때 객체의 속성은 변수, 기능은 메소드라고 하였다. 메소드와 함수는 무슨 차이일까? 

## 메소드(Method)란?
클래스 내부에서 클래스의 기능을 갖는 함수를 `메소드` 라 한다. 즉 함수가 좀더 포괄적인 개념이다. 하지만 서로 기능적인 차이는 거의 없다. 단지 자바 프로그래밍을 할 때 우리는 function 보다 method라는 단어를 더 많이 접하게 될 것이다.

### 메소드 정의하기
클래스

```java
public class FunctionTest {
	
	public static int addNum(int num1, int num2) {
		int result;
		result = num1 + num2;
		return result;
	}
	
	public static void sayHello(String greeting) {
		System.out.println(greeting);
	}
	
	public static int calcSum() {
		
		int sum = 0;
		int i;
		
		for(i = 0; i<=100; i++) {
			sum += i;
		}
		
		return sum;
	}

	public static void main(String[] args) {

		int n1 = 10;
		int n2 = 20;
		
		int total = addNum(n1, n2);
		
		sayHello("�ȳ��ϼ���");
		int num = calcSum();
		
		System.out.println(total);
		System.out.println(num);
	}

}
```