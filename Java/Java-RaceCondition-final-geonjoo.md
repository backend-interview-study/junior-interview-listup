# 1. 스레드에서 Race condition에 대해서 설명해주세요.

## 한 줄 정리
- 공유 자원에 여러 스레드가 접근해서, 스레드의 실행 순서에 따라 연산의 결과값이 변할 수 있는 상태를 Race Condition이라 한다. RaceCondition을 해결하기 위해서는 세마포어 또는 뮤텍스를 이용한다.

***

## 경쟁 상태(Race Condition)란

- 공유 자원에 여러 프로세스 / 스레드가 동시에 접근할 때, 발생
- 실행 순서에 따라 연산의 결과값이 변할 수 있다.
- Java 는 멀티 스레드를 지원하는 언어이므로 경쟁 상태가 발생할 위험이 높다

## 경쟁 상태 해결 방법

### 1. 세마포어(Semaphore)

- 공유 자원의 데이터를 여러 프로세스가 접근하는 것을 막는 것
- 세마포어의 값을 확인하고 해당 자원이 사용중인지 확인
    - 자원을 사용하지 않는 상태가 되면, 대기중인 프로세스가 즉시 자원을 이용
    - 다른 프로세스에 의해 사용중인 경우, 재시도 전에 일정시간 대기
- 비교적 긴 시간을 확보하는 리소스에 이용

### 2. 뮤텍스(Mutex)

- 공유 자원을 가진 스레드들의 실행시간이 겹치지 않도록 하는 것
    - 상호 배제(Mutual Exclution) 되도록 하는 기술
- Locking 메커니즘으로 하나의 스레드가 뮤텍스를 얻어 공유 자원에 접근한다
- 뮤텍스를 얻은 스레드만이 공유 자원을 사용 완료했을 때 뮤텍스를 해제할 수 있다.

### 세마포어와 뮤텍스의 차이

- 뮤텍스
    - Locking 메커니즘으로 락을 걸은 쓰레드만이 임계 영역을 나갈때 락을 해제할 수 있다.
- 세마포어
    - Signaling 메커니즘으로 락을 걸지 않은 쓰레드도 signal을 사용해 락을 해제할 수 있다.

***

## 자바에서의 경쟁 상태

- 동일한 리소스를 여러 스레드가 동시에 접근 / 변경이 가능하므로 경쟁상태가 발생할 수 있다

### 해결 방법

- Java에서는 동기화 기법으로 상호배제를 구현한 Monitor를 Object내부에 구현하여 모든 인스턴스에 Thread동기화를 가능하게 한다.
- Monitor를 활용하기 위해 `synchronized` 키워드를 이용
    - lock, unlock을 걸어 처리
    - 현재 데이터를 사용하고 있는 스레드를 제외한 다른 스레드는 데이터에 접근할 수 없도록 막는다
    - `synchronized` 키워드를 너무 많이 사용하면 성능이 저하될 수 있다

***

## 참고. Spring에서의 경쟁상태 해결

### `@Transactional` 과 `synchronized` 을 사용한 메서드에서의 경쟁상태 해결

- `@Transactional` 어노테이션은 Spring AOP이고 새로운 프록시를 생성하게 된다
- 따라서 동기화 된 메서드가 종료되기 전에 트랜잭션 프록시가 진행될 수 있다

```
Thread1: |--Begin--|--increase--|--Commit-->

Thread2: |--------Begin--------|--decrease--|--Commit-->
```

- 이러한 문제를 피하기 위해서, `@Transactional` 을 필요한 경우에만 사용하는 것이 좋다

***

# 2. Java final 키워드에 대해서 설명해주세요. 각각의 쓰임에 따라 어떻게 동작하나요? (Class, Variable)

## final 키워드

- 변수(variable), 메서드(method), 또는 클래스(class)에 사용할 수 있다
- 어떤 곳에 사용되냐에 따라 다른 의미를 가진다

### 1. final 변수

- final이 붙은 변수는 값을 수정할 수 없다
    - 수정될 수 없기 때문에 초기화 값은 필수적이다
    - 초기화 전에 사용하면 컴파일 에러가 생긴다

```java
final int number = 2;
```

- 상수라고도 부른다
- `get` 만 가능하다
- 객체에 대한 참조인 경우, 최초 참조하는 객체 이외의 다른 객체를 참조할 수 없다
    - 참조된 객체의 메소드를 통해 객체 자체의 값은 바꿀 수 있다
    - 객체의 재할당을 막는다
        
        → 객체 자체가 불변은 아니다
        

```java
final Person person = new Person("아무개");
person = new Person("어배추고양이") // Compile Error

person.setName("어배추고양이"); // 객체의 값을 바꿀 수 있다
```


### 2. final 클래스

- final이 붙은 클래스는 상속(Inheritance)이 불가능한 클래스가 된다
    - 다른 클래스에서 상속해 재정의를 할 수 없다
    - ex. Integer와 같은 Wrapper 클래스
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e07704b7-bc34-44ae-a3a6-de0a00d3149f/Untitled.png)
    
- subclass를 만들 수 없다
- 라이브러리 형태의 프로젝트를 작성할 때 주로 사용

```java
final class Person {
  String name;
}

// 상속 불가능
class Doctor extends Person {

}
```

### 3. final 메서드

- final 이 붙은 메서드는 해당 메서드를 오버라이드하지 못한다
    
    → 재정의가 불가능하다
    
- 라이브러리 형태의 프로젝트를 작성할 때 주로 사용
