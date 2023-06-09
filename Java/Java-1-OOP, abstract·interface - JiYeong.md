### 1. OOP에 대해서 설명하세요( 5원칙과 4가지 특징 )
<h4>객체 지향 프로그래밍</h4> 객체 지향 프로그래밍은 컴퓨터 프로그래밍 패러다임 중 하나로, 컴퓨터 프로그래밍 패러다임 중 하나로, 여러 개의 독립된 단위인 객체들간의 상호작용을 통해서 프로그램을 만드는 방식이다.

<h4>장점</h4>

▶코드 재사용이 용이

▶유지보수가 쉬움

<h4>단점</h4>

▶처리 속도가 상대적으로 느림

▶설계시 많은 시간과 노력이 필요



<h3>4가지 특징</h3>

1. 추상화
  - 구체적인 사물들의 공통적인 특징을 파악해서 이를 하나의 개념(집합)으로 다루는 것
<br>

2. 캡슐화
  - 외부에 노출할 필요가 없는 정보들은 은닉 (정보은닉)
  - 정보 은닉(information hiding): 외부에서 접근하지 못하도록 제한하는 것
  - 높은 응집도, 낮은 결합도를 유지하여 유연함과 유지보수성 증가
<br>

3. 상속화
  - 부모 클래스가 자손 클래스에게 속성을 물려주는 것
  - 코드의 재사용
<br>

4. 다형화
  - 같은 형태이지만 다른 기능을 하는 것
  - 서로 다른 클래스의 객체가 같은 메시지를 받았을 때 각자의 방식으로 동작하는 능력
  - 오버라이딩(Overriding) 은 상위 클래스가 가지고 있는 메서드를 하위 클래스가 재정의해서 사용
  - 오버로딩(Overloading) 은 이름의 메서드 여러개를 가지면서 매개변수의 유형과 개수가 다르도록 하는 기술


<br>

### [5원칙](https://velog.io/@haero_kim/SOLID-%EC%9B%90%EC%B9%99-%EC%96%B4%EB%A0%B5%EC%A7%80-%EC%95%8A%EB%8B%A4)

|SOLID|설계|원칙|
|:-----:|:---------------------------:|:-----------------------------:|
| `S` | SRP, Single Responsibility Principle <br>단일 책임 원칙 | 한 클래스는 하나의 책임만 가져야 한다. |
| `O` | OCP, Open Close Prinicple <br>개방 폐쇄 원칙 | 확장에는 열려(Open) 있으나, 변경에는 닫혀(Closed)있어야 한다. |
| `L` | LSP, Liskov Substitution Principle <br>리스코프 치환 원칙 |  상위 타입은 항상 하위 타입으로 대체할 수 있어야 한다. |
| `I` | 	ISP, Interface Segregation Principle <br>인터페이스 분리 원칙 | 인터페이스를 클라이언트에 특화되도록 분리시키라는 설계 원칙 |
| `D` | DIP, Dependency Inversion Principle <br>의존 역전 원칙 | 추상화에 의존한다. 구체화에 의존하면 안된다. |


<hr>

### 2. 추상 클래스와 인터페이스를 설명해주시고, 차이에 대해 설명해주세요.

- 추상 클래스는 클래스 내 추상 메소드가 하나 이상 포함되거나 abstract로 정의된 경우를 말하고,
- 인터페이스는 모든 메소드가 추상 메소드로만 이루어져 있는 것을 말합니다.

#### 공통점
- new 연산자로 인스턴스 생성 불가능
- 사용하기 위해서는 하위 클래스에서 확장/구현 해야 한다.

#### 차이점
- 인터페이스는 그 인터페이스를 구현하는 모든 클래스에 대해 특정한 메소드가 반드시 존재하도록 강제함에 있고,
- 추상클래스는 상속받는 클래스들의 공통적인 로직을 추상화 시키고, 기능 확장을 위해 사용한다.
- 추상클래스는 다중상속이 불가능하지만, 인터페이스는 다중상속이 가능하다.
