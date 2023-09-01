# Boxing, UnBoxing, Auto Boxing, Auto UnBoxing

[wrapper](https://github.com/strangehoon/Today-I-learned/blob/main/Java/Wrapper%20%ED%81%B4%EB%9E%98%EC%8A%A4%EC%99%80%20Wrapper%20%ED%81%B4%EB%9E%98%EC%8A%A4%20%EC%82%AC%EC%9A%A9%20%EC%9D%B4%EC%9C%A0.md) 클래스는 산술 연산을 위해 정의된 클래스가 아니다. 따라서 연산 과정에서 기본 타입과 래퍼 타입을 변환하는 과정이 필요한데 boxing과 unboxing이 여기서 사용된다. 

* Boxing : 기본 타입의 데이터 → 래퍼 클래스의 인스턴스로 변환
```java
Integer num = new Integer(10); // Integer 래퍼 클래스 num 에 10의 값을 저장
```

* UnBoxing : 래퍼 클래스의 인스턴스에 저장된 값 → 기본 타입의 데이터로 변환
```java
int n = num.intValue(); // 래퍼 클래스 num 의 값을 꺼내 가져온다.
```
JDK 1.5 부터는 boxing과 unboxing이 필요한 상황에 자바 컴파일러가 자동으로 처리해주기 시작했다. 이러한 자동화된 boxing과 unboxing을 auto boxing과 auto unboxing이라고 부른다. 기본타입 값을 직접 boxing, unboxing 하지 않아도 래퍼 클래스 변수에 대입만 하면 자동으로 boxing과 unboxing이 된다.

* Auto Boxing : 기본 타입의 데이터 -> 래퍼 클래스의 인스턴스로 **자동** 변환
```java
Integer num = 17; // new Integer() 생략
```
* Auto UnBoxing : 래퍼 클래스의 인스턴스에 저장된 값 -> 기본 타입의 데이터로 **자동** 변환
```java
int n = num; // intValue() 생략
```

> 💡 기능적 편의성을 위하여 auto boxing, auto unboxing을 제공하지만, 다른 타입 간의 형 변환은 애플리케이션의 성능에 영향을 미치게 된다. 비록 사소한 차이 일지라도 애플리케이션의 성능 측면에서 봤을 때 꼭 필요한 상황이 아니라면 지양하는 것이 좋다.

> [자바 Wrapper 클래스와 Boxing & UnBoxing 총정리](https://inpa.tistory.com/entry/JAVA-%E2%98%95-wrapper-class-Boxing-UnBoxing)
