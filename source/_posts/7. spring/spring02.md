---
title: Dependency Injection

thumbnail: images/spring/thumbnail.png
date: 2020-06-23 23:27:00

tags: 
- maven

category:
- 자바 튜토리얼
- 4. spring

#카탈로그 생성 및 위치
toc: true
widgets:
  - type: toc
    position: right
  - type: category
    position: right
sidebar:
  right:
    sticky: true
---

스프링에 대하여 알아보자.
<!-- more -->

```java
public class Program1 
{
	public static void main(String[] args) 
	{
		Exam exam = new StudyExam();
		//ExamConsole console = new InlineExamConsole(exam); //DI
		ExamConsole console = new GridExamConsole(exam); //DI
		console.print();
	}
}
```
