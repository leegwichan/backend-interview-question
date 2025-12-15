# Spring

- Spring Core
  - IoC / DI
    - Spring DI/IoC는 어떻게 동작하나요?
    - DI 종류에는 어떤 것이 있고, 이들의 차이는 무엇인가요?
    - 의존성과 설정 값을 생성자 인자로 주입해야 하는 이유에 대해 설명해주세요
    - `@Autowired` 과정에 대해 설명해주세요
    - DI 컨테이너(IoC 컨테이너)의 역할은 무엇인가요?
  - Spring Bean
    - Spring Bean이 무엇인가요?
    - Spring Bean의 생성 과정을 설명해주세요
    - Spring Bean의 Scope에 대해서 설명해주세요
    - Bean/Component 어노테이션에 대해 설명해주시고, 둘의 차이점에 대해 설명해주세요

- Spring MVC
  - Spring Web MVC에서 요청 마다 Thread가 생성되어 Controller를 통해 요청을 수행할텐데, 어떻게 1개의 Controller만 생성될 수 있을까요?
  - Spring Web MVC의 Dispatcher Servlet의 동작 원리에 대해서 간단히 설명해주세요
  - Spring Web MVC의 근간에는 Java Servlet 이 있는데요. Spring 은 Servlet을 어떻게 구성해서 이를 구현했을까요?

- Spring Filter
  - Servlet Filter와 Spring Interceptor의 차이는 무엇인가요?
  - Filter는 Servlet의 스펙이고, Interceptor는 Spring MVC의 스펙입니다. Spring Application에서 Filter와 Interceptor를 통해 예외를 처리할 경우 어떻게 해야 할까요?

- JPA
  - JPA를 쓴다면 그 이유에 대해서 설명해주세요.
  - JPA 영속성 컨텍스트의 이점(5가지)을 설명해주세요.
  - JPA Propagation 전파단계를 설명해주세요.
  - N+1 문제는 무엇이고 이것이 발생하는 이유와 이를 해결하는 방법을 설명해주세요.

- 기타
  - POJO란 무엇인가요? Spring Framework에서 POOJO는 무엇이 될 수 있을까요?
  - Spring Application을 구동할 때, 메서드를 실행시키는 방법에 대해 설명해주세요
  - Spring에서 CORS 에러를 해결하기 위한 방법을 설명해주세요
  - 프론트 컨트롤러 패턴이란 무엇인가요?

### Spring Bean

- [DI/IoC](./spring_di_ioc.md)
  - DI 컨테이너(IoC 컨테이너)의 역할
  - DI의 주요 주입 방식 3가지
- [Spring Bean]
  - 생명 주기, Scope
  - `@Bean` vs `@Component`

### Spring MVC
- [Servlet Container(Tomcat) 스레드 풀](./servlet_container_thread_pool.md)
  - 스레드 풀 설정, 포화 정책
- [Spring MVC](./spring_mvc.md)
  - Spring MVC 구조, `HandlerAdapter` - `Handler` 간 동작
- [Controller](./spring_mvc_controller.md)
  - `@Controller` vs `@RestController`
- [Filter vs Interceptor](./spring_mvc_filter_interceptor.md)
  - 체인 형식의 관리
  - AOP vs 인터셉터

### Spring JPA

- [N+1 문제](./spring_jpa_n+1_problem.md)

#### JPA를 사용하는 이유

- SQL 중심의 개발에서 객체 중심적인 개발이 가능해진다
  - 상황에 맞는 SQL을 매번 작성하지 않아도 된다
- 유지 보수가 용이해진다
  - 기존에는 필드를 바꾸면 모든 SQL을 수정해야 했지만, JPA는 엔티티만 바꿔주면 자동으로 SQL을 바꾸어 요청함
- Spring이 시작될 때 잘못된 부분을 쉽게 파악할 수 있다
  - 기존에는 SQL이 실행이 되는 런타임 환경에서 오류를 파악할 수 있었다
  - JPA를 사용하게 되면서, Entity와 테이블 정보가 맞지 않을 경우, Spring Data JPA의 메서드 명이 잘못되어 있는 경우 Spring이 실행되지 않고 중단된다
- DB를 교체할 때 변경할 코드의 양이 적다
  - 페이징의 경우, 각 데이터베이스 마다 사용하는 SQL이 다르다
  - JPA는 `Dialect`라는 인터페이스를 사용하고 각 DB마다 구현체가 존재하므로, 내가 작성한 코드를 변경하지 않아도 사용하는 SQL을 변경하여 실행한다
- 영속성 컨텍스트가 1차 캐시의 역할을 하여, 필요하지 않은 SQL을 실행하지 않는다

#### 영속성 컨텍스트

- 장점 5가지
  - 영속성 컨텍스트가 1차 캐시의 역할을 하여, 필요하지 않은 SQL을 실행하지 않는다

#### JPA Propagation 전파단계

### 기타

#### POJO

- POJO (Plain Old Java Object)
  - 객체지향에 집중하고, 특정 클래스나 라이브러리에 종속되지 않는 객체
  - 객체 지향적인 원리에 충실하면서 환경과 기술에 종속되지 않고, 필요에 따라 재활용될 수 있는 방식으로 설계된 오브젝트

- POJO의 장점
  - 각종 프레임워크나 라이브러리에 종속적이지 않게 됨 -> 필요한 라이브러리를 쉽게 교체할 수 있다
  - 간편하게 테스트를 할 수 있다
    - 코드가 간결해져 디버깅이 상대적으로 쉬워진다
    - 특정 기술이나 환경에 종속적이지 않기 때문에 테스트가 쉬워진다
  - 객체지향적인 설계를 자유롭게 적용할 수 있다