## 1주차 CS정리

### 메모리 저장구조

![](https://velog.velcdn.com/images/sebinyu1372/post/c827cdc7-556b-4b60-b7d2-218b1d41ecbd/image.png)

## 전역변수

- 클래스 영역 안에 있고, 전체 영역에서 사용가능한 변수
- 선언위치: 클래스 영역
- 라이프 타임: [프로그램 실행 ~ 프로그램이 종료]까지
- 메모리: 데이터 영역
- 다른 영역에서도 접근 할 수 있기 때문에, 보안성이 상대적으로 낮음

```java
public class Main {

    int a = 0; //전역변수.

    public static void main(String[] args) {

    }
}
```

<br>

## 클래스 변수 = static 변수

- 클래스 영역 안에 있고, 전체 영역에서 사용가능한 변수\_ 전역변수와 달리 static으로 선언 필요
- 선언위치: 클래스 영역
- 라이프타임: [프로그램 실행 ~ 프로그램이 종료]까지
- 메모리: 데이터 영역
- 변수의 초기화 지원(초기화 필요 없음)
- private가 아니라면, 참조변수로 다른클래스에서 사용 가능
- 메모리에 고정되기 때문에 남용시 메모리 혹은 프로그램 실행 속도에 악영향

```java
static int i = 500;
```

<br>

## 지역 변수

- 선언위치: 클래스영역 이외의 영역(메서드, 생성자, 초기화 블럭 내부)
- 매개변수/메소드등.. 구현 시 생성
- 선언위치: 스택 영역
- 초기화가 안되므로 초기화 후 사용가능
- 선언된 영억 내에서만 사용 가능하며, 영역 사용 종료시 스택에서 소멸
- ex) 매개변수 int x int y 는 메소드 실행 후 종료되면값이 소멸-> 하지만 globalIntger 는 전역변수이기 때문에 main메소드에서 값 확인가능

```java
	public void sum(int x , int y) {
		globalInteger = x + y;
		System.out.println("x = " + x); // 10 소멸
		System.out.println("y = " + y); // 20 소멸
		System.out.println("sum = "+ globalInteger); // 30 유지
	}
```

## 인스턴스 변수

- 선언위치: 클래스 영역
- 라이프타임: [인스턴스 생성 ~ 가비지컬렉터가 메메모리 수거 할때]까지
- 메모리: 힙 영역
- private가 아니라면, 참조변수로 다른클래스에서 사용 가능
- 인스턴스는 독립적인 저장공간을 가지므로 서로 다른 값을 가질 수 있다

<hr>
<br>

## 깊은 복사 vs 얇은 복사

- 깊은 복사(Deep Copy): '데이터 값'만을 새로운 메모리 공간에 복사하는 것을 의미
  -> 복사된 객체는 완전히 독립적인 메모리를 차지
- Cloneable로 구현 필요
  ![](https://velog.velcdn.com/images/sebinyu1372/post/ea910d7a-7b74-458e-976d-90621ff40bc1/image.png)

- 얕은 복사(Shallow Copy): '주소 값'을 복사
  -> 객체끼리 참조하고 있는 실제 값은 동일하고, 복사한 객체가 변경된다면 기존의 객체도 같이 변경
  - 배열경우 System.arraycopy로 구현가능
  - 객체 얕은 복사 예시)

```java
CopyObject original = new CopyObject("JuHyun", 20);
CopyObject copy = original;
```

![](https://velog.velcdn.com/images/sebinyu1372/post/cc7c3dce-8770-46ce-a951-1dba1ad4b652/image.png)

그림출처: https://zzang9ha.tistory.com/372

<hr>

<br>

## 싱글톤 패턴

유일하게 존재하는 인스턴스 접근 통제(private)
+) **공용** (static) 사용하고 싶을 때 사용

- 사용사례
  달력 만들기, 1개만 존재하는 스피커 제어 등...
  객체가 유일하게 1개 존재하는 것을 보증하고 싶을 시 사용

- 장단점

  - 장점
    - 고정된 메모리 영역을 얻으면서, **한번의 new**로 인스턴스를 계속 사용
      -> 메모리 낭비 방지
      -> 두번째 이용시 부터는, 객체 로딩시간이 줄어들어서 성능 향상
    - 싱글톤으로 만들어진 클래스의 인스턴스는 전역
      -> 데이터 공유 용이
  - 단점
    - 싱글톤 인스턴스가 너무 많은 일/많은 데이터 공유가 될 경우
      -> 다른 클래스 인스턴스들간의 결합도가 높아짐
      -> 이는 객체지향 설계 원칙에 어긋남
      -> 결과적으로 수정 어려워짐/ 유지보수 비용 증가로 이어질 수 있음
    - 싱글톤 인스턴스에 접근하는 모든 쓰레드가 거의 동시에 도착하고, 이로인해 동시성 문제 발생
      - 동시성 문제: 여러 요청이 동시에 동일한 자원(data)에 접근하고 수정하려는 것을 의미
    - 이러한 이유로 싱글톤 패턴은 꼭 필요한 경우가 아니라면 사용 지양하기

- 구현방법

1. Priavte static 인스턴스 변수
2. Private 생성자 ---> 외부에서는 직접 인스턴스를 생성할 수 없게됨
3. Public static getInstace() method 구현 ---> private으로 선언해서 getInstac메소드 필요

![](https://velog.velcdn.com/images/sebinyu1372/post/5358847b-bc4d-40dc-b50d-85a28d774ca6/image.png)

![](https://velog.velcdn.com/images/sebinyu1372/post/391e3b2e-2d0f-45ae-842c-2b0df3d6f3d7/image.png)

참조:
https://www.youtube.com/watch?v=Cs3g44R9seo
https://cjw-awdsd.tistory.com/42

<hr>
<br>

## 컴파일 과정

<br>

![](https://velog.velcdn.com/images/sebinyu1372/post/8b6f1506-295f-4829-8fb4-3cbab8d046fe/image.png)

1. 개발자가 .java파일을 생성
2. build를 한다.
3. java compliler의 javac의 명령어를 통해 바이트코드(.class)를 생성
4. class loader를 통해 jvm내로 로드
5. 실행엔진을 통해 컴퓨터가 읽을 수 있는 기계어로 해석되어(각 운영체제에 맞는 기계어)Runtime Data Area에 배치

`실행엔진`

- 실행 엔진은 바이트코드를 명령어 단위로 읽어서 실행하는데, 두 가지 방식을 **혼합**하여 사용한다.

## <Interpreter 방식>

바이트코드를 한 줄씩 해석, 실행하는 방식이다. 초기 방식으로, 속도가 느리다는 단점이 있다.

## <JIT(Just In Time) 컴파일 방식 = 동적 번역(Dynamic Translation)>

- Interpreter방식의 속도를 보완한 것이, JIT(Just In Time) 컴파일 방식
- 바이트코드를 JIT 컴파일러를 이용해, 프로그램을 실제 실행하는 시점(바이트코드를 실행하는 시점)에 각 OS에 맞는 Native Code로 변환하여 실행 속도를 개선하였다.
- 하지만 바이트코드를 Native Code로 변환하는 데 비용이 소요
  -> 비용절감을 위해, JVM은 모든 코드를 JIT 컴파일러 방식으로 실행하지 않고, 인터프리터 방식을 사용하다 일정 기준이 넘어가면 JIT 컴파일 방식으로 명령어를 실행한다.
- ** 또한, JIT 컴파일러는 같은 코드를 매번 해석하지 않고, 실행할 때 컴파일을 하면서 해당 코드를 캐싱해버린다. 이후에는 바뀐 부분만 컴파일하고, 나머지는 캐싱된 코드를 사용한다.**
  cf) 캐싱: 자주 사용하는 데이터들을 재사용목적으로 캐시 메모리에 저장하는 것

`출처` [https://blog.naver.com/software705/220645590756](https://blog.naver.com/software705/220645590756)

<hr>
<br>

## JVM

- 가상머신 = JRE (java runtime enviroment) = JVM(java virtual machine)
- 중간 기계어인 바이트코드 -> 플랫폼에 맞는 가상머신으로 실행파일 생성
- 자바의 [한번작성하면, 어디서든 돌아간다]라는 장점은 만든 수혜자
- OS환경이 바뀌면, 매번 프로그램을 해당 OS 컴파일러로 다시 컴파일 해주어야하는 번거로움을 없애줌

### **JVM 구조**

> JVM MEMORY영역에 Heap영역과 Native Memory영역에 jdk8에서 변화가 있다.

`jdk8이전`

![https://github.com/whdms705/cs-memo/raw/master/contents/imgs/java_compile.png](https://github.com/whdms705/cs-memo/raw/master/contents/imgs/java_compile.png)

`jdk7 vs jdk8 HEAP`

![https://github.com/whdms705/cs-memo/raw/master/contents/imgs/java_heap.png](https://github.com/whdms705/cs-memo/raw/master/contents/imgs/java_heap.png)

- JDK 8부터 Permanent Heap 영역이 제거
  -> 그 대신 Metaspace 영역이 추가되었다.
  - Perm은 JVM에 의해 크기가 강제되던 영역이다.(JVM이 관리하는 영역)
- Metaspace는 Native memory 영역(힙 영역X)으로, OS가 자동으로 크기를 조절한다.(OS 판단하여 메모리를 조절)
- 기존과 비교해 Perm영역에서 사용하던 메모리를 사용가능
  -> 메모리 부족에 대한 부담이 감소

`Perm영역의 역할은`

- Perm 영역은 보통
  Class의 Meta 정보
  Method의 Meta 정보,
  Static 변수와 상수 정보들이 저장되는 공간으로 흔히 메타데이터 저장 영역이라고도 한다.
- 이 영역은 Java 8 부터는 Native 영역으로 이동하여 Metaspace 영역으로 변경되었다.
- 기존 Perm 영역에 존재하던 Static Object는 Heap 영역으로 옮겨져서 GC의 대상이 최대한 될 수 있도록 하였다.

<hr>

## array vs ArrayList

<br>

8가지 차이점
![](https://velog.velcdn.com/images/sebinyu1372/post/f56eea44-9b28-4d85-b959-40e5a145a421/image.png)
차이점 설명

1. 배열 길이 관리 방식
   배열은 크기선언과 동시에 크기고정, arrayList는 사이즈가 동적으로 늘어 날 수 있는 배열
   cf) arrayList의 Default 저장용량은 10
2. 사이즈 변경
   1번이유로 인해 배열은 변경 불가
   arrayList는 추가, 삭제 가능

3. 담을 수 있는 자료
   배열은 primitive type(int, byte, char 등)과 object 모두를 담을 수 있지만, arrayList는 object element만 담을 수 있다.

4. 제네릭 사용가능여부
   Array: 동종(homogeneous) data structure이다.
   만약 명시된 타입이 아닌 다른 데이터 유형을 Array에 저장할 경우 ArrayStoreException이 발생한다.
   ArrayList : Generics(제네릭스)를 통해 Type-Safety를 보장한다.

```java
String temp[] = new String[2];    // creates a string array of size 2

temp[0] = new Integer(12);        // throws ArrayStoreException,
```

5. 인덱스 길이 불러오는 방식
   길이에 대해 배열은 length 변수를 쓰고, arrayList는 size() 메서드를 써야한다.

6. element들을 할당 방식
   배열은 element들을 할당하기 위해 assignment(할당) 연산자를 써야하고, arrayList는 add() 메서드를 통해 element를 삽입한다.

7. Multi-dimensional
   Array : 다차원이 가능하다.
   ArrayList : 항상 단일 차원이다.

```java
int addarrayobject[][] = new int[3][2];
```

8. Performance
   Array와 ArrayList의 성능은 수행되는 작업에 따라 달라진다.

- resize() operation : ArrayList의 자동 크기 조정은 임시 배열을 사용하여 이전 배열의 요소를 새 배열로 복사하기 때문에 성능이 저하된다.

- ArrayList의 자동 resize는 성능을 낮출 것이다(old array에서 new array로 요소들을 옮길 때 임시 array를 사용하기 때문에). ArrayList는 resizing하는 동안 내부적으로 Array의 지원을 받는다.(내부적으로 native method인 System.arrayCopy(...)를 사용하기 때문에)

- add() or get() operation : Array나 ArrayList로 부터 요소를 얻거나 추가할 때는 거의 비슷한 성능을 보인다.

출처:

- [QUORA] What is the difference between an array and an array list?
- https://velog.io/@humblechoi/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-Array-vs-ArrayList
