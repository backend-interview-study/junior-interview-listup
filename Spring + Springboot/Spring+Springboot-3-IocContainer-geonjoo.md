# Spring IoC Container란 무엇인가요?

## 한 줄 정리

Spring IoC Container란 Spring Framework에서 제어 역전을 위해 자바 객체의 생성부터 소멸까지의 생명주기를 Container가 관리하도록 하는 것이다. 대표적으로 BeanFactory와 ApplicationContext 인터페이스가 있다.

***

## IoC란?

제어 역전(Inversion of Control)으로, 스프링 애플리케이션에서 자바 객체(Bean)의 생성과 의존 관계 설정, 사용, 제거 등의 작업을 애플리케이션 코드 대신 스프링 컨테이너가 담당한다.

컴포넌트 의존관계 설정 및 생명주기를 해결하기 위한 디자인 패턴(Design Pattern)

## IoC Container란?

- 스프링에서 객체의 생명주기를 관리, 생성된 인스턴스들에게 추가적인 기능을 제공하도록 하는 것
- 스프링에서 IoC Container를 **빈 팩토리**, **DI Container**, **Application Context**라고 부른다.

## IoC Container의 장점

- IoC 컨테이너는 자바 객체(POJO)의 생명 주기를 책임지고, 의존성을 관리
    
    → 개발자는 비즈니스 로직에 집중할 수 있다.
    
- 객체 생성 코드가 없으므로 TDD가 용이

## IoC Container의 종류

![image](https://user-images.githubusercontent.com/69177351/234356057-884c82ec-ea8c-4f27-aca7-7fc24a71c9e7.png)

### 1. BeanFactory

- Bean 이란 Spring Container가 관리하는 객체를 의미
- Spring Container의 최상위 인터페이스이다.
- Spring Bean을 등록, 생성, 조회, 반환하는 역할을 담당한다.
    - Bean을 조회할 수 있는 `getBean()` 메소드를 제공
- BeanFactory 계열의 인터페이스만 구현한 클래스는 단순히 컨테이너에서 객체를 생성하고 DI를 처리하는 기능만 제공한다.
- 팩토리 디자인 패턴을 구현한 것으로 BeanFactory는 빈을 생성하고 분배하는 책임을 지는 클래스
- 보통은 BeanFactory를 바로 사용하지 않고, 이를 확장한 ApplicationContext를 사용

### 2. ApplicationContext

- Bean을 등록, 생성, 조회, 반환 관리하는 기능은 BeanFactory와 동일
- 애플리케이션 컨텍스트는 빈 팩토리 기능을 모두 상속 받아서 제공한다.
- 스프링의 각종 부가 기능을 추가로 제공한다.
    - 메시지 소스를 활용한 국제화 기능
        - 한국에서 들어오면 한국어로, 영어권에서 들어오면 영어로 출력
    - 환경 변수
        - 로컬, 개발, 운영 등을 구분해서 처리
    - 애플리케이션 이벤트
        - 이벤트를 발행하고 구독하는 모델을 편리하게 지원
    - 편리한 리소스 조회
        - 파일, 클래스 패스, 외부 등에서 리소스를 편리하게 조회
