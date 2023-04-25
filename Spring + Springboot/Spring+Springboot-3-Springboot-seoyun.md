# 1. Spring, Spring Boot의 차이점에 대해 각각 설명해 주세요.

- Spring: 자바 EE 어플리케이션을 빌드할 수 있는 오픈소스 경량 프레임워크   
  - 자바 기반 애플리케이션을 만드는 데 사용
  - 의존성: 종속성 주입(dependency의 호횐되는 라이브러리 버전을 맞춰줘야 한다)
  - 서버 종속성: 서버를 명시적으로 설정해야 한다(Tomcat)
  - 배포: war 파일을 WAS에 담아 설정을 통해 배포

- SpringBoot: 스프링 프레임워크를 사용하기 위한 설정의 많은 부분을 자동화하여 개발자가 편하게 스프링을 활용할 수 있도록 돕는다.
  - 주로 REST API 개발을 위해 사용
  - 의존성: spring starter를 통한 dependency 라이브러리 버전 자동화(자동 구성)
  - 서버: springboot 내부에 Tomcat이 내장되어 있어서 (Embed Tomcat 사용) 따로 Tomcat을 설치하거나 매번 버전 관리를 하지 않아도 된다
  - AutoConfiguration을 통해 외부 라이브러리, 서버 등이 실행
  - 배포: 내장 WAS를 가지고 있기 때문에 jar file을 이용해 자바 옵션만으로 손쉽게 배포

Spring Framework는 기존에 EJB를 대신해 자바 애플리케이션을 더 쉽게 만들 수 있게 해 준다
스프링은 POJO 프로그래밍을 지향하는 특징을 가지며 그를 위해 IoC/DI, AOP, PSA를 지원한다.
Spring Boot Framework는 Spring Framework보다 개발자가 개발에만 집중할 수 있도록 도와주는 프레임워크이다.

---
자세한 내용을 [블로그 링크](https://velog.io/@may_yun/Spring-spring%EA%B3%BC-springboot%EC%9D%98-%EC%B0%A8%EC%9D%B4%EC%A0%90)를 참고해 주세요.
