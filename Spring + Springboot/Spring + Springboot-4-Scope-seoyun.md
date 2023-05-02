# Bean Scope와 종류에 대해 아는 만큼 설명해주세요.

## 1)Bean Scope란?
스프링은 빈이라는 개념으로 자바객체를 만들고 싱글톤화 시켜 관리해줍니다.<br>
이 객체들은 스프링 IoC 컨테이너의 의해 생성되고 소멸되는 등의 관리가 이루어지는데<br>
이때 bean이 관리되는 범위를 Bean scope라고 합니다.<br>
bean이 싱글턴화 되서 관리되는 이유는 spring bean의 기본 scope 전략이 Singleton 이기 때문입니다.<br>

## 2)Bean Scope 종류
- 싱글톤: 스프링은 기본적으로 bean 등록시 따로 설정을 하지 않았다면 싱글톤으로 등록
  - 애플리케이션 구동시 JVM 안에서 스프링이 bean마다 하나의 객체를 생성하는 것을 의미 <br>(그래서 개발자는 스프링을 통해서 제공받은 bean은 언제나 동일한 객체라는 가정하에 개발하는 것)
  - 기본 스코프, 스프링 컨테이너의 시작과 종료까지 유지되는 가장 넓은 범위의 스코프이다. <br>(싱글톤 bean은 spring 컨테이너에서 한 번 생성된다 컨테이너가 사라질 때 bean도 제거된다.)
  - @Component, @Configuration + @bean의 조합으로 등록된 bean들의 기본 scope이다.
  - <img width="765" alt="image" src="https://user-images.githubusercontent.com/94329274/235645376-bacac495-cb32-44a6-8eb6-88e6d6d2affe.png">
- 프로토타입(prototype):
  - 스프링 컨테이너는 프로토타입 빈의 생성과 의존관계 주입까지만 관여하고 더는 관리하지 않는 매우 짧은 범위의 스코프이다.
  - 프로토타입을 받은 클라이언트가 객체를 관리하여 준다.
  - <img width="766" alt="image" src="https://user-images.githubusercontent.com/94329274/235645732-13444e7b-a740-4200-a2e7-069b486aca60.png">
- 웹 관련 스코프: request, session, global session의 Scope는 일반 spring 어플리케이션이 아닌 SpringMVC Web Application에서만 사용된다.(웹환경에서만 동작하는 스코프)
  - request : 웹 요청이 들어오고 나갈 때까지 유지되는 스코프
  - session : 웹 세션이 생성되고 종료될 때까지 유지되는 스코프
  - application : 웹의 서블릿 컨텍스트와 같은 범위로 유지되는 스코프
  
---
자세한 내용은 [블로그 링크](https://velog.io/@may_yun/Spring-Bean-Scope%EC%99%80-%EC%A2%85%EB%A5%98)를 참고해 주세요

