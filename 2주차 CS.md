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

    -> 함수를 확장하는 것이 목적

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
- 불변 객체는 read-only 메소드만을 제공하며, 객체의 내부 상태조작 불가능
- 복사 또한 방어적 복사(defensive-copy)를 통해 제공
- Java의 불변 객체로는 String, Boolean, Integer, Float, Long, Double 등..

- 불변 객체(Immutable Object) 및 final을 사용해야 하는 이유 ]

  - Thread-Safe하여 병렬 프로그래밍에 유용하며, 동기화를 고려하지 않아도 된다.
    실패 원자적인(Failure Atomic) 메소드를 만들 수 있다.
    - 불변 객체라면 어떠한 예외가 발생하여도 메소드 호출 전의 상태를 유지
    - 그리고 예외가 발생하여도 오류가 발생하지 않은 것 처럼 다음 로직을 처리
  - Cache나 Map 또는 Set 등의 요소로 활용하기에 더욱 적합하다.
    - 캐시나 Map, Set 등의 원소인 가변 객체가 불변객체로 선언된다면, 한 번 데이터가 저장된 이후에 다른 작업들을 고려하지 않아도 되므로 사용하는데 용이
  - 부수 효과(Side Effect)를 피해 오류가능성을 최소화할 수 있다.
    - 부수 효과란 변수의 값이나 상태 등의 변화가 발생하는 효과를 의미
    - 불변객체는 변경이 불가하므로, 객체의 수정자(Setter)를 통해 여러 객체들에서 값을 변경하는 경우로 인한 상태예측 어려움을 피할 수 있음
  - 다른 사람이 작성한 함수를 예측가능하며 안전하게 사용할 수 있다.
  - 가비지 컬렉션의 성능을 높일 수 있다.
    - 컨테이너(container) 클래스: List, Set, Queue, Map -가비지 컬렉터가 컨테이너 하위의 불변 객체들은 Skip할 수 있도록 도와줌
    - 왜냐하면 해당 컨테이너가 살아있다는 것은 하위의 불변 객체들 역시 처음에 할당된 그 상태로 참조되고 있다는 것을 의미
    - Skip하는 경우가 생기는 덕에, GC 수행 속도가 빨라짐

출처: https://mangkyu.tistory.com/120 [MangKyu's Diary:티스토리]

출처: https://mangkyu.tistory.com/131 [MangKyu's Diary:티스토리]

<hr>

- String vs StringBuilder vs StringBuffer

  - ## String
    String 클래스를 보면 final인 것을 볼 수 있습니다. final class는 더 이상 확장할 수 없다는 특징
  - 수정 시, 새로운 메모리가 필요
    - 이로인해 메모리 낭비가 생길 수 있으니 상황에 따라 구분해서 사용하기
  - 문자열 연산이 적고 자주 참조(조회)하는 경우에 사용하면 좋음
  - 멀티쓰레드 환경에서 동기화를 신경쓰지 않아도 됨 (final 클래스이면서 불변 클래스이기 때문)

  - ## StringBuffer vs StringBuilder

    - String과는 다르게 mutable(변경가능)
    - StringBuffer
      - 멀티스레드에 안전(thread safe)하도록 동기화
      - 동기화가 StringBuffer의 성능을 떨어뜨림
      - 그러므로 멀티쓰레드 환경에서는 StringBuffer를 사용하고, 그렇지 않다면 StringBuilder를 사용하는 것이 좋음
    - StringBuilder

      - StringBuffer에서 쓰레드의 동기화만 뺀 것
      - 즉, 동기화 제외 StringBuffer와 완전히 똑같은 기능으로 구현

    - 동기화
      - 멀티 스레드 환경에서, 사용하려는 스레드 하나를 제외한 나머지 스레드들은 리소스를 사용하지 못하도록 막는 것
      - 이것을 Thread-safe라고 함
      - 이를 통해 자료변질 오류를 막을 수 있음
      - Synchronized
        - Thread-safe를 위해 하나의 스레드만 일할 수 있도록 임계 영역(critical section)을 지정
        - 임계 영역(critical section): 둘 이상의 스레드가 동시에 접근해서는 안 되는 공유 리소스(자료 구조 또는 장치)를 접근하는 코드의 일부
        - 메서드 자체를 synchronized로 선언
        ```java
           public synchronized void plus(int value) {
             amount += value;
          }
        ```
        - 메서드 내의 특정 문장만 synchronized로 감싸는 synchronized 블록
        ```java
           public void minus(int value) {
             synchronized (this) {
                   amount -= value;
               }
           }
        ```
