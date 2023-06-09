# 1. Managed - Unmanaged 언어의 차이는 무엇이고 어떤 장, 단점이 있나요?

## 한 줄 정리.

> 특정 런타임 환경에 의해 관리되고, 머신들이 Heap 영역의 메모리를 관리해주는 언어를 Managed 언어라고 하고 대표적으로  Java, C# 등이 있다. 특정 런타임 환경에 관리를 받지 않는 모든 언어를 UnManged 언어라고 하고 대표적으로 C, C++ 등이 있다.

## Managed 언어

- 코드가 하드웨어에서 바로 구동되는 것이 아닌, 특정 런타임 환경에 의해 관리되고 의존하는 코드
    - 특정 런타임 환경 : JVM(Java), CLR(C#), V8(JavaScript)
- 가상머신, 인터프리터, 엔진 등이 코드의 메모리를 관리한다
    - 메모리의 Heap 영역을 머신이 관리하면 Managed 언어이다
- Java, C#, JavaScript 등이 해당

### Managed 언어 장점

- 메모리의 할당과 해제를 통해 메모리 관리 없이 언어 자체적으로 메모리를 관리한다
- 언어가 하드웨어나 OS에 종속되지 않는다

### Managed 언어 단점

- 메모리를 구체적으로 관리할 수 없기 때문에, 프로그래밍의 자유도가 낮다
- 비정기적인 메모리 정리가 이루어진다

## UnManaged 언어

- 특정 런타임 환경에 관리를 받지 않는 모든 언어
- C, C++ 이 해당

### UnManaged 언어 장점

- Managed 언어에 비해 속도가 빠르다
- 메모리를 구체적으로 관리할 수 있어서 프로그래밍의 자유도가 높다

### UnManaged 언어 단점

- 직접 메모리를 관리해 메모리의 누수가 없게 해야한다
- 프로그래머가 실수할 경우 메모리의 누수가 발생

***
# 2. Java 접근 제어자에는 무엇이 있는지 설명해주시고 Protect와 Private는 어느 시점에 어떻게 사용될 수 있는지 이야기 해주세요.

## 접근 제어자란?

- 클래스, 멤버변수, 메서드, 생성자에 사용되며 외부에서 접근하지 못하도록 제한하는 역할을 한다
- 생략했을 경우 `default` 로 설정된다

## Java의 접근 제어자의 종류

1) `private` : 같은 클래스 내에서만 접근 가능

2) `default` : 같은 패키지 내에서만 접근 가능

3) `protected` : 같은 패키지 내에서, 그리고 다른 패키지의 자손 클래스에서 접근 가능

4) `public` : 접근 제한이 전혀 없다.

| 제어자 | 같은 클래스 | 같은 패키지 | 자손 클래스 | 전체 |
| --- | --- | --- | --- | --- |
| public | O | O | O | O |
| protected | O | O | O |  |
| default | O | O |  |  |
| private | O |  |  |  |
