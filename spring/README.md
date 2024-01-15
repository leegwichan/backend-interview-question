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
  - Filter는 Servlet의 스펙이고, Interceptor는 Spring MVC의 스펙입니다. Spring Application에서 Filter와 Interceptor를 통해 예외를 처리할 경우 어떻게
    해야 할까요?

- JPA
  - JPA 영속성 컨텍스트의 이점(5가지)을 설명해주세요.
  - JPA Propagation 전파단계를 설명해주세요.
  - JPA를 쓴다면 그 이유에 대해서 설명해주세요.
  - N + 1 문제는 무엇이고 이것이 발생하는 이유와 이를 해결하는 방법을 설명해주세요.


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

#### DI 컨테이너(IoC 컨테이너)의 역할

- 각 객체들을 (대체적으로) 싱글톤으로 객체를 관리한다
  - 런타임에서 빈 객체들이 클래스 별로 단 하나만 존재하도록 관리한다
- 의존관계가 필요할 경우, 설정 정보를 바탕으로 런타임 환경에서 필요한 객체를 주입시킨다

### Spring Bean

#### Spring Bean의 생성 과정

- Spring의 크게 두가지 라이프사이클
  - '빈을 생성하는 단계'와 '의존관계를 주입하는 단계'

#### Spring Bean의 Scope

#### `@Bean`, `@Component`
