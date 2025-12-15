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

#### Spring Bean

- Spring Bean
  - 스프링 컨테이너에 의해 관리되는 재사용 가능한 소프트웨어 컴포넌트
  - 스프링 컨테이너가 관리하는 자바 객체를 뜻하며, 스프링 컨테이너는 하나 이상의 빈(Bean)을 관리한다.
  - 스프링 빈을 등록하는 방법은 XML, 자바 어노테이션 등이 있다
  - 스프링 빈이 등록될 때는 [빈 이름, 빈 객체] 쌍으로 등록되며, 빈 이름이나 빈 타입으로 조회할 수 있다

- Spring Bean의 생성 과정
  - 크게는 '빈을 생성하는 단계'와 '의존관계를 주입하는 단계'로 나눌 수 있다
  1. 스프링 컨테이너가 초기화될 때 먼저 빈 객체를 설정에 맞춰 생성
  2. 의존 관계를 설정
  3. 해당 프로세스가 완료되면 빈 객체가 지정한 메소드를 호출해서 초기화를 진행

- Spring Bean의 생명 주기
  - Bean은 스프링 컨테이너에 의해 생명주기를 관리한다.
  - 생명 주기 : 객체 생성 -> 의존 설정 -> 초기화 -> 사용 -> 소멸 과정
  - 객체를 사용해 컨테이너가 종료될 때 빈이 지정한 메서드를 호출해 소멸 단계를 거친다.
  - 생명 주기 관련 인터페이스
    - `InitializingBean` : 빈 초기화 시에 정의된 메서드를 호출함
    - `DisposableBean` : 빈 소멸 시에 정의된 메서드를 호출함
  - 생명 주기 관련된 어노테이션
    - `@PostConstruct` : 빈 초기화 시 실행
    - `@PreDestory` : 빈 소멸 시에 실행

#### Spring Bean의 Scope

|    Scope    | Description                        |
|:-----------:|------------------------------------|
|  singleton  | (기본값) 스프링 IoC 컨테이너당 하나의 인스턴스만 사용   |
|  prototype  | 매번 새로운 빈을 정의해서 사용                  |
|   request   | HTTP 라이프 사이클 마다 한개의 빈을 사용          |
| application | ServletContext 라이프사이클 동안 한개의 빈만 사용 |
|  websocket  | 라이프사이클 안에서 한개의 빈만 사용               |

- singleton, prototype을 제외하고는 전부 웹 환경(web-aware 컨택스트)에서만 사용할 수 있다
- prototype Scope의 경우 `@PostDestroy`가 있는 메서드를 실행하지 않는다

#### `@Bean`, `@Component`

- `@Bean`
  - 메소드 레벨에서 선언하며, 반환되는 객체(인스턴스)를 개발자가 수동으로 빈으로 등록하는 애노테이션
  - 주로 `@Configuration`과 같이 사용되며, `@Configuration`을 사용할 경우, 이미 등록된 빈을 주입받을 수 있다
  - 빈에 등록될 때 이름 기본 값 : 메서드 이름
- `@Component`
  - 클래스 레벨에서 선언
  - 스프링이 런타임시에 컴포넌트스캔을 하여 자동으로 빈을 찾고(detect) 등록하는 애노테이션
  - 빈에 등록될 때 이름 기본 값 : 클래스 이름 (맨 앞글자 소문자)
- 적합한 상황에 사용하는 방법
  - 내가 만든 클래스를 등록할 때는 `@Component`를 추천한다
  - 외부 라이브러리 등 내가 수정할 수 없는 클래스를 등록할 때는 `@Configuration`, `@Bean`을 사용하는 것을 추천한다

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