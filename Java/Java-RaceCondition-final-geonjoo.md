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

#### 메서드에서 사용하는 경우

```java
public synchronized void method() {
		...
}
```

#### 객체 변수에 사용하는 경우(block문)

```java
private Object obj = new Object();

public void exampleMethod() { 
		// obj에 
		synchronized(obj) {
			...
		}
}

```

### 경쟁 상태 예시

- 스레드의 동기화 없이 변수 `c` 를 `+1` 후 `-1` 하는 경우

#### Counter class

```java
public class Counter implements Runnable {
    private int c = 0;

    public void increment() {
        try {
            Thread.sleep(10);
        } catch (InterruptedException e) {
            //Auto-generated catch block
            e.printStackTrace();
        }
        c++;
    }

    public void decrement() {
        c--;
    }

    public int getValue() {
        return c;
    }

    @Override
    public void run() {
        //incrementing
        this.increment();
        System.out.println("Value for Thread After increment " + Thread.currentThread().getName() + " " + this.getValue());
        //decrementing
        this.decrement();
        System.out.println("Value for Thread at last " + Thread.currentThread().getName() + " " + this.getValue());
    }
}
```

#### Main class

```java
public class Main {
    public static void main(String[] args) {
        Counter counter = new Counter();
        Thread t1 = new Thread(counter, "Thread-1");
        Thread t2 = new Thread(counter, "Thread-2");
        Thread t3 = new Thread(counter, "Thread-3");
        t1.start();
        t2.start();
        t3.start();
    }
}
```

#### 실행 결과

```
Value for Thread After increment Thread-1 2
Value for Thread After increment Thread-3 2
Value for Thread After increment Thread-2 2
Value for Thread at last Thread-3 0
Value for Thread at last Thread-2 -1
Value for Thread at last Thread-1 1
```

1, 0이 번갈아가며 나올것이라는 예상과는 다르게 값이 섞여서 나온다

### 경쟁 상태 해결 예시

#### Counter class

```java
public class Counter implements Runnable {
    private int c = 0;

    public void increment() {
        try {
            Thread.sleep(10);
        } catch (InterruptedException e) {
            //Auto-generated catch block
            e.printStackTrace();
        }
        c++;
    }

    public void decrement() {
        c--;
    }

    public int getValue() {
        return c;
    }

    @Override
    public void run() {
        synchronized (this){
            //incrementing
            this.increment();
            System.out.println("Value for Thread After increment " + Thread.currentThread().getName() + " " + this.getValue());
            //decrementing
            this.decrement();
            System.out.println("Value for Thread at last " + Thread.currentThread().getName() + " " + this.getValue());
        }
    }
}
```

#### 실행 결과

```
Value for Thread After increment Thread-1 1
Value for Thread at last Thread-1 0
Value for Thread After increment Thread-3 1
Value for Thread at last Thread-3 0
Value for Thread After increment Thread-2 1
Value for Thread at last Thread-2 0
```

- 원하는 결과가 나온것을 확인할 수 있다

[(10) 경쟁 상태 ( Race Condition )](https://korshika.tistory.com/150)

[Race Condition in Java](https://velog.io/@gjwjdghk123/RaceCondition)

[java - synchronized 란? 사용법?](https://coding-start.tistory.com/68)

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

