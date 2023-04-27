# @Bean과 @Component은 각각 언제 사용되고 어떤 차이점을 가지나요?

## 한 줄 정리

`@Bean` 과 `@Component` 모두 스프링에서 IoC Bean을 생성하기 위해 사용된다

`@Bean` 의 경우 `@Configuration` 과 같이 사용되며, 사용자가 직접 제어하지 않는 Map, List, ObjectMapper와 같은 라이브러리를 IoC Bean으로 만들기 위해 사용한다.
메서드에만 사용할 수 있으며, Class에 사용할 경우 컴파일 에러가 발생한다.

`@Component` 의 경우 사용자가 생성한 임의의 클래스에 사용한다. 클래스에 `@Component` 선언 후 `@Autowired` 를 이용해 해당 클래스를 사용할 수 있다. 
`@Configuration` , `@Controller` , `@Service`  등의 어노테이션은 `@Component` 를 포함하고 있다. 
Class에서만 사용 가능하며, 메서드에서 사용 시 컴파일 에러가 발생한다.

***

## `@Bean` 과 `@Component` 의 공통점

- 두 어노테이션 모두 스프링에서 IoC Bean(객체)을 생성하기 위해 사용한다
    - 싱글톤 레지스트리로 Bean을 관리할 수 있게된다

## `@Bean` 과 `@Component` 의 차이점

### `@Bean` 의 특징

![image](https://user-images.githubusercontent.com/69177351/234864383-6cd78a04-ad50-4638-8d69-41ac41de0637.png)

- `@Bean` 은 `@Configuration` 과 같이 사용된다
    - `@Configuration` 내부에는 `@Component` 가 들어있기 때문에, `@Bean` 도 `@Component` 와 동일하게 싱글톤 레지스트리로 Bean을 생성한다.
    - `@Configuration` 내부의 메서드에 `@Bean` 어노테이션을 사용한다
- Map, List, ObjectMapper 등 사용자가 직접 제어하지 않는 내/외부 라이브러리를 IoC Bean으로 만들기 위해 사용한다
- 반드시 메서드에만 사용할 수 있다
    - Class 단위에 `@Bean` 을 작성하는 경우, 컴파일 에러가 발생한다

```java
// @Bean 예제 코드
@Configuration
public class DatasourceConfig {

    @Bean
    public DataSourceProperties dataSourceProperties() {
        return new DataSourceProperties();
    }
		...
}
```

### `@Component` 의 특징

![image](https://user-images.githubusercontent.com/69177351/234864551-257eb500-1587-4c13-91c7-3745793dec94.png)

- 사용자가 만든 임의의 클래스를 빈으로 등록시키기 위해서 사용된다.
- `@Component` 선언 후 `@Autowired` 어노테이션을 사용해 해당 클래스를 사용할 수 있다.
- `@Configuration`,`@Controller`,`@Service`,`@Repository` 등의 어노테이션들은 `@Component`어노테이션을 포함하고 있다.
- Target이 TYPE이므로 Class 위에서만 선언될 수 있다
    - 메서드에 `@Component` 를 사용하면 컴파일 에러가 난다

```java
// 예제 코드
@Component(value="Test")
public class TestClass {
	
	private String TestName = "Test";
	
}
```

```java
// @Component가 선언된 클래스를 @Autowired로 불러올 수 있다
@Autowired
TestClass testClass;

@RequestMapping("/home")
public String indexPage(HttpServletRequest request){	
	
		System.out.println(testClass.getTestName());	
	
		return "/home";
}
```

***

## 참고

[https://seeminglyjs.tistory.com/414](https://seeminglyjs.tistory.com/414)

[https://giron.tistory.com/91](https://giron.tistory.com/91)

[https://jojoldu.tistory.com/27](https://jojoldu.tistory.com/27)
