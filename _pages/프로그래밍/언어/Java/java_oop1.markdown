---
title: "[Java객체지향] 클래스와 객체, 인스턴스, 메서드와 패키지, 접근제어자"
tags:
    - Java객체지향
date: "2025-03-13"
thumbnail: "/assets/img/thumbnail/book.jpg"
---
# **자바 클래스와 객체, 인스턴스**


<br>
<br>
<br>



<br>
<br>
<br>


# **자바 접근 제어자**

(1) 접근제어자란(acess modifier)?

> 클래스와 클래스의 멤버(필드, 메소드, 생성자)를 사용할 때, 접근 가능한 범위를 지정해주는 것

(2) 접근제어자의 종류
클래스 접근제어자
`public`: 모든 클래스에서 해당 클래스에 접근 가능(패키지에 상관없이)

```java
public class car{

}
```

`default(생략)`: 같은 패이지 안의 클래스에서만 접근 간ㅇ

```java
class car{

}
```

클래스 멤버의 접근제어자

`public`: 패키지와 상관없이 모든 클래스에서 접근 가능
`private`: 같은 클래스 안에 있는 멤버들만 접근 가능
`protected`: 같은 패키지 안의 모든 클래스와, 다른 패키지의 자식 클래스에서 접근 가능
`default(생략)`: 같은 패키지 않의 클래스에서만 접근 가능

> public, protected, default, private 순으로 범위가 좁아짐


요약

|구분|public|protected|default|private|
|:---:|:---:|:---:|:---:|:---:|
|같은 패키지의 내 클래스|O|O|O|O|
|같은 패키지의 다른 클래스|O|O|O|X|
|다른 패키지의 자식 클래스|O|O|X|X|
|다른 패키지의 다른 클래스|O|X|X|X|
