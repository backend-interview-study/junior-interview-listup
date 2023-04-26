# Configuration은 어떻게 Bean을 등록하고 관리할까요? (Singleton을 지키는 매커니즘은?)

## 한 줄 정리

`@Configuration` 은 해당 클래스가 xml 설정을 대체하는 스프링 설정 클래스가 되도록 한다. 스프링 컨테이너는 `@Configuration` 가 있는 클래스를 Bean으로 등록하고 해당 클래스를 파싱해서 `@Bean` 이 있는 메서드를 찾아 Bean을 생성해준다.

이 때 스프링은 CGLIB이란 라이브러리를 이용해 프록시 패턴을 적용해서 `@Configuration` 내의 `@Bean` 메서드가 싱글톤으로 생성됨을 보장한다.

## Configuration 이란?

- `@Configuration` 이 붙은 클래스는 xml 설정을 대체하고, 빈 설정을 담당하는 클래스가 된다.
- 스프링에서는 클래스를 빈으로 등록할 때 `@Bean` 어노테이션을 사용
- 설정 클래스에 `@Configuration` 어노테이션이 있어야만 프록시 패턴을 적용해 Bean이 싱글톤으로 생성
    - `@Bean` 만 사용하는 경우 싱글톤을 보장하지 않는다
    - `@Configuration` 이 있으면 스프링이 CGLIB 라는 바이트코드 조작 라이브러리를 이용해 임의의 프록시 클래스를 생성한다
    - `proxyBeanMethods` 를 통해 싱글톤의 유지를 해제할 수 있다

### `@Configuration` 을 적용한 코드

```java
public class MyBean {
		
	public MyBean {
		System.out.println("MyBean instance created");
	}

}
```

```java
public class MyBeanConsumer {
		
	public MyBeanConsumer  {
		System.out.println("MyBeanConsumer created");
		System.out.println("myBean HashCode: " + myBean.hashCode());
	}

}
```

```java
@Configuration
public class AppConfig {
		
	@Bean
	public MyBean myBean() {
		return new MyBean();
		}

	@Bean
	public MyBeanConsumer myBeanComsumer() {
		return new myBeanConsumer(myBean());
	}

}
```

실행 결과

```
MyBean instance created
MyBeanConsumer created
myBean HashCode: 1647766367
```

→ 인스턴스가 한 번만 호출된 모습

### `@Configuration` 을 적용하지 않았을 때 결과

실행 결과

```
MyBean instance created
MyBean instance created
MyBeanConsumer created
myBean HashCode: 1647766367
```

→ `myBean()` 메서드가 호출될 때마다 new로 새로운 MyBean을 생성하기 때문에 `"MyBean instance created"` 가 두번 호출되게 된다

***

## 참고

[https://blogshine.tistory.com/551](https://blogshine.tistory.com/551)

[https://mangkyu.tistory.com/75](https://mangkyu.tistory.com/75)

[https://mangkyu.tistory.com/234](https://mangkyu.tistory.com/234)

[https://jaeano.tistory.com/76](https://jaeano.tistory.com/76)
