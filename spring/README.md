# Spring

- Spring Core
  - [IoC / DI](#ioc--di)
    - Spring DI/IoC는 어떻게 동작하나요?
    - DI 종류에는 어떤 것이 있고, 이들의 차이는 무엇인가요?
    - 의존성과 설정 값을 생성자 인자로 주입해야 하는 이유에 대해 설명해주세요
    - `@Autowired` 과정에 대해 설명해주세요
    - DI 컨테이너(IoC 컨테이너)의 역할은 무엇인가요?
  - [Spring Bean](#spring-bean)
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
  - Filter는 Servlet의 스펙이고, Interceptor는 Spring MVC의 스펙입니다. Spring Application에서 Filter와 Interceptor를 통해 예외를 처리할 경우 어떻게
    해야 할까요?

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

### IoC / DI

- IoC(Inversion of Control) : 프로그램의 제어 흐름을 직접 제어하는 것이 아니라 외부(프레임워크)에서 관리하는 것
- DI(Dependency Injection) : 의존관계는 정적인 클래스 의존 관계와, 실행 시점에 결정되는 동적인 객체(인스턴스) 의존 관계 둘을 분리해서 생각해야 한다.
  - 스프링 프레임워크에서 클래스 사이 의존관계를 빈 설정 정보를 바탕으로 컨테이너가 자동으로 연결해준다
- Spring DI/IoC 동작
  - 빈 등록 단계 : 설정 정보를 통해 스프링 컨테이너 (`ApplicationContext`)에 빈 객체를 등록한다
  - 객체 생성 단계 : 이미 등록된 빈 객체들을 의존 관계를 필요로 하는 객체에게 주입하며 (대체적으로) 싱글톤을 유지한다

#### DI (Dependency Injection)의 종류

- 생성자 주입
  - 생성자 호출시점에 딱 1번만 호출되는 것이 보장
  - **불변, 필수** 의존관계에 사용
  - 생성자가 딱 1개만 있다면 `@Autowired`를 생략해도 자동 주입 된다

- 필드 주입
  - 필드에 바로 주입하는 방법
  - 코드가 간결해지지만, DI 프레임워크에 종속적인 코드가 된다
  - Spring에 종속적인 테스트 코드에서만 사용하는 것을 추천한다

- 수정자 주입 (일반 메서드 주입)
  - `setter`라 불리는 필드의 값을 변경하는 수정자 메서드를 통해서 의존관계를 주입하는 방법
  - **선택, 변경** 가능성이 있는 의존관계에 사용
  - `@Autowired(required = false)`로 지정하면 주입할 대상 없이도 동작하게 할 수 있다

- **생성자 주입을 해야 하는 이유**
  - 대부분의 의존 관계는 애플리케이션 종료 전까지 변할 일이 없다
    - '수정자 주입'을 이용하게 되면, 클래스(객체) 외부에서 의존 관계를 변경할 수 있다
    - 그래서 주로 `final`을 이용하여 필드를 불변으로 설정해준다
  - 프레임워크 없이 순수한 자바 코드로 단위 테스트를 할 수 있다
    - '필드 주입'을 사용하게 될 경우, 프레임워크 없이 의존 관계를 설정할 수 없다

#### `@Autowired` 의 과정

- 과정
  - 우선 해당 클래스가 스프링 빈으로 등록될 때, `@Autowired` 어노테이션이 달린 방법으로 주입한다
  - @Autowired 를 지정하면, 스프링 컨테이너가 자동으로 해당 스프링 빈을 찾아서 주입한다
    - 이때 기본 조회 전략은 타입이 같은 빈을 찾아서 주입한다
    - 경우에 따라 에러를 발생시키거나 그냥 진행한다

- 주의 사항
  - 타입으로 조회하면 선택된 빈이 2개 이상일 때 문제가 발생한다.
    - 같은 타입의 여러 개의 빈이 등록되어 있다면, `@Qualifier`, `@Primary` 등으로 해결할 수 있다
  - 아래와 같은 상황에서는 해당 타입으로 등록된 스프링 빈이 없어도 실행될 수 있다

```java
class IfNotEnrolledCase {
    //호출 안됨
    @Autowired(required = false)
    public void setNoBean1(Member member) {
        System.out.println("setNoBean1 = " + member);
    }

    //null 호출
    @Autowired
    public void setNoBean2(@Nullable Member member) {
        System.out.println("setNoBean2 = " + member);
    }

    //Optional.empty 호출
    @Autowired(required = false)
    public void setNoBean3(Optional<Member> member) {
        System.out.println("setNoBean3 = " + member);
    }
}
```

#### DI 컨테이너(IoC 컨테이너)의 역할

- 각 객체들을 (대체적으로) 싱글톤으로 객체를 관리한다
  - 런타임에서 빈 객체들이 클래스 별로 단 하나만 존재하도록 관리한다
- 의존관계가 필요할 경우, 설정 정보를 바탕으로 런타임 환경에서 필요한 객체를 주입시킨다

### Spring Bean

- Spring Bean
  - 스프링 컨테이너에 의해 관리되는 재사용 가능한 소프트웨어 컴포넌트
  - 스프링 컨테이너가 관리하는 자바 객체를 뜻하며, 스프링 컨테이너는 하나 이상의 빈(Bean)을 관리한다.
  - 스프링 빈을 등록하는 방법은 XML, 자바 어노테이션 등이 있다
  - 스프링 빈이 등록될 때는 [빈 이름, 빈 객체] 쌍으로 등록되며, 빈 이름이나 빈 타입으로 조회할 수 있다

#### Spring Bean의 생성 과정

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