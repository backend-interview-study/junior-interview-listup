# 1. 객체 지향의 클래스, 객체, 인스턴스 차이에 대해서 설명해 주세요.

## 클래스란

- 객체를 **정의**해 놓은 것. 객체의 설계도 / 틀
- 객체를 생성하는데 사용
- 연관되어 있는 변수와 메서드의 집합
- 메모리의 Method Area에 올라간다

## 객체란

- 클래스에 정의된 내용대로 메모리에 생성하는 것
- 일반적으로 객체는 다수의 속성과 다수의 기능을 갖는다
    
    → 객체는 속성과 기능의 집합
    

### 객체의 구성 요소

1. 속성 : 멤버변수, 특성, 필드, 상태
2. 기능 : 메서드, 행위, 함수

## 인스턴스란

- 어떤 클래스로 부터 만들어진 객체를 그 클래스의 인스턴스라 한다
    - ex. `Animal cat = new Animal()`
    - `cat` 은 객체이다
    - `cat` 이라는 객체는 `Animal` 의 인스턴스이다
- 클래스로부터 객체를 만드는 과정을 인스턴스화 라고 한다
- 메모리의 Heap 영역에 올라간다

## 객체 vs 인스턴스

- 클래스의 타입으로 선언되었을 때 객체라고 부르고, 그 객체가 메모리에 할당되어 실제 사용될 때 인스턴스라고 부른다.
- 객체는 현실 세계에 가깝고, 인스턴스는 소프트웨어 세계에 가깝다.
- 객체는 '실체', 인스턴스는 '관계'에 초점을 맞춘다.
    - 객체를 '클래스의 인스턴스'라고도 부른다.
- 방금 인스턴스 화하여 레퍼런스를 할당한 객체를 인스턴스라고 말하지만, 이는 원본(추상적인 개념)으로부터 생성되었다는 것에 의미를 부여하는 것일 뿐 엄격하게 인스턴스를 나누긴 어렵다.

***

# 2. 불변 객체는 무엇이고 Java에서 어떻게 구현할까요?

## 불변 객체란?

- 객체 생성 이후 내부 상태가 변하지 않고 변경할 수 없는 객체
- 객체의 내부 상태를 제공하는 메서드를 제공하지 않거나 방어적 복사를 통해 제공
- Java의 대표적 불변 객체 : `String`, `Integer`, `Long`, `Double` 등등

## 불변 객체의 장점

- Thread-Safe 해서 병렬 프로그래밍에 유용하고 동기화를 고려하지 않아도 된다
    - 항상 동일한 값을 보장하므로, 공유자원의 값이 덮어씌워지지 않는다
- 내부 상태의 변경이 없기 때문에 Cache, Map, Set 등의 요소로 활용하기에 적합하다
    - 한 번 데이터가 저장된 후 다른 작업(갱신)을 고려하지 안하오 된다
- 외부에서 객체에 대해 변경할 수 없으므로 안정성이 있다
    - 값의 수정이 불가능해 객체의 신뢰성이 높다
- GC의 성능을 높일 수 있다
    - 불변 객체를 이용하면 불변 객체 내부의 객체는 GC 스캔 대상에 제외된다
        
        → GC 의 스캔 빈도와 범위가 줄게 되어서 GC 의 성능에 도움이 된다
        
    - 객체를 많이 생성해도, 객체 생성에 대한 비용은 큰 부담이 되지 않는다

## 불변객체 생성 규칙

1. Setter Method 를 제공하지 않는다
2. 모든 필드를 `private`, `final` 로 선언한다
3. 클래스를 `final` 로 선언한다
4. 객체를 생성하기 위한 생성자 / 정적 팩토리를 추가한다
5. 불변 객체 사용 시 방어적 복사를 고려하지 않아도 된다

## 불변 객체 생성 방법

### 필드가 모두 primitive type인 경우

```java
public final class ImmutableObj {
    private final int num;

    public ImmutableObj(int num) {
        this.num = num;
    }

    public int getNum() {
        return num;
    }
}
```

### 필드에 reference type이 있는 경우

```java
public final class ImmutableReference {
    private final int num;
    private final Amount amount;

		// 전달받은 Amount 객체가 외부에서 변경될 수 있으므로 참조를 끊는다
    public ImmutableReference(int num, Amount amount) {
        this.num = num;
        this.amount = new Amount(amount.getValue());
    }

    public int getNum() {
        return num;
    }

		// 외부로 전달한 Amount 객체가 외부에서 변경될 수 있어서 참조를 끊는다
    public Amount getAmount() {
        return new Amount(amount.getValue());
    }
}
```

- 방어적 복사를 이용해 참조관계를 끊어야 한다
