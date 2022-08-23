## 접근 지시자

- 접근 지시자 사용 이유
  - '은닉성': 외부로부터의 접근을 제한하여 데이터를 보호하기 위함
  - '캡슐화': 외부에는 불필요하고 내부적으로만 사용되는 부분을 감추기 위함
    <br>
- 종류 4가지
  - private : private이 붙은 변수, 메소드는 해당 클래스에서만 접근이 가능
  - default : 접근제어자를 별도로 설정하지 않는다면 접근제어자가 없으면 default로 설정 / 동일 패키지 내에서만 접근이 가능하다.
  - protected : 동일 패키지내의 클래스 또는 해당 클래스를 상속받은 외부 패키지의 클래스에서 접근이 가능하다.
  - public : 어떤 클래스에서라도 접근이 가능

![https://github.com/whdms705/cs-memo/raw/master/contents/imgs/access_md.png](https://github.com/whdms705/cs-memo/raw/master/contents/imgs/access_md.png)

> ※ private -> default -> protected -> public 순으로 보다 많은 접근을 허용한다

<hr>

## 메서드 템플릿 패턴(추상클래스) vs 전략패턴(인터페이스)

- 추상클래스 목적 : 재사용

  - 추상클래스를 상속받아서 다른 클래스에서 이용
    -> 추상클래스의 메서드를 재사용하는 것이 목적

- 인터페이스 목적 : 확장

  - 함수의 껍데기를 먼저 선언

    -> 다른 클래스에서 해당 함수 구현을 강제

    -> 해당 함수를 확장하는 것이 목적

<hr>

## new vs 상수풀

- string 선언 방식 2가지

```java
  String str1 = new String("aaa");
  String str2 = "aaa";
```

- new 생성자 방식

  - String 생성자의 매개변수로 문자열 작성
  - 힙 메모리에 저장
  - String 클래스는 final로 선언

    -> 결과적으로, 한번 생성된 문자열은 변경되지 않음

    -> 문자열 연결/ 변경시, 매번 새로운 메모리 공간 필요

    -> 메모리 낭비

- 상수풀에 저장
  - 문자열 상수를 가리키는 방식
  - 상수풀에 저장되며, 다음에 같은 변수값으로 초기화 할시 같은 상수 메모리 주소를 가리킴
  - String 생성자 방식보다 메모리를 아낄 수 있음

<hr>

## 불변객체(어떤 것들이 있고 , 왜 필요한가)

- 객체 생성 이후 내부의 상태가 변하지 않는 객체
- 불변 객체는 read-only 메소드만을 제공하며, 객체의 내부 상태를 제공하는 메소드를 제공하지 않거나 방어적 복사(defensive-copy)를 통해 제공
- Java의 불변 객체로는 String, Boolean, Integer, Float, Long, Double 등..

- 불변 객체(Immutable Object) 및 final을 사용해야 하는 이유 ]

  - Thread-Safe하여 병렬 프로그래밍에 유용하며, 동기화를 고려하지 않아도 된다.
    실패 원자적인(Failure Atomic) 메소드를 만들 수 있다.
  - Cache나 Map 또는 Set 등의 요소로 활용하기에 더욱 적합하다.
  - 부수 효과(Side Effect)를 피해 오류가능성을 최소화할 수 있다.
  - 다른 사람이 작성한 함수를 예측가능하며 안전하게 사용할 수 있다.
  - 가비지 컬렉션의 성능을 높일 수 있다.

출처: https://mangkyu.tistory.com/131 [MangKyu's Diary:티스토리]

<hr>

- String vs SpringBuilder vs StringBuffer
  - 동기화
  - thread safe
