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