### 1.Wrapper Class란 무엇이며, Boxing과 UnBoxing란?
자바의 자료형은 크게 기본 타입(primitive type)과 참조타입(reference type)으로 나누어진다.

대표적으로 기본 타입은 char, int, float, double, boolean 등이 있고 참조 타입은 class, interface 등이 있다.

기본 자료타입(primitive type)을 객체로 다루기 위해서 사용하는 클래스들을 래퍼 클래스(wrapper class)라고 한다.

자바는 모든 기본타입(primitive type) 값을 갖는 객체를 생성할 수 있다.

이런 객체를 포장 객체라고 하는데 그 이유는 기본 타입의 값을 내부에 두고 포장하기 때문이다.

래퍼 클래스로 감싸고 있는 기본 타입 값은 외부에서 변경할 수 없다. 만약 값을 변경하고 싶다면 새로운 포장 객체를 만들어야 한다.
![wra](https://user-images.githubusercontent.com/81270199/231724531-e7efc84e-dde7-4d17-aa7b-fa4445b1bbd0.png)

![wraa](https://user-images.githubusercontent.com/81270199/231725100-693c415e-aeef-4aca-a52c-a4eb3aba85ba.png)


![ob](https://user-images.githubusercontent.com/81270199/231725320-048e84f7-b82b-4f87-8121-ba065a22b8ab.png)


```java
public class Wrapper_Ex {
    public static void main(String[] args)  {
        Integer num = new Integer(17); // 박싱
        int n = num.intValue(); //언박싱
        System.out.println(n);
    }
}
```

결론적으로

- 기본 자료형(Primitive data type)에 대한 객체 표현을 Wrapper class
- 기본 자료형 → Wrapper class로 변환하는 것을 Boxing이라 하며,
- Wrapper class → 기본 자료형으로 변환하는 것을 UnBoxing이라 한다.




<br>

<hr>

### 2.java의 main 메서드가 static인 이유?

메모리가 초기화 된 순간 객체는 하나도 존재하지 않기 때문에 객체 멤버 메서드는 바로 실행 할 수 없다.

따라서, 객체의 존재 여부에 관계없이 쓰기 위해 static이어야 한다. static 멤버는 JVM 구동시 스태틱 영역에 바로 배치되기 때문이다.

(main 메서드는 프로그램의 시작점. 프로그램이 실행되면 제일 먼저 호출되는 메서드이기 때문에 객체를 생성하지 않은 채로 바로 작업을 수행해야 하기 때문에 static이어야 함)
