# Spring

## 스프링이란?

- 스프링 DI 컨테이너 기술
- 스프링 프레임 워크
- 스프링 프레임 워크, 스프링 부트, 스프링 데이터, 스프링 세션, 스프링 시큐리티 등을 모두 포함하는 스프링 생태계
  - [spring.io](https://spring.io/projects)에서 다양한 기술들을 찾아볼 수 있음

- 스프링 프레임워크
  - 핵심기술: 스프링 DI 컨테이너, AOP, 이벤트, 기타
- 스프링 부트
  - 스프링을 편리하게 사용할 수 있도록 지원, 최근에는 기본으로 사용
  - 단독으로 실행할 수 있는 스프링 애플리케이션을 쉽게 생성
    - Tomcat 같은 웹 서버를 기본적으로 내장해서 별도의 웹 서버를 설치할 필요가 없음
  - starter 종속성을 제공하여 빌드가 쉬움
    - 엮여있는 라이브러리들 자동으로 다 가져와줌
    - 라이브러리의 버젼도 다 맞춰줌
  - 메트릭, 상태 확인, 외부 구성 같은 프로덕션 준비 기능 제공
    - 모니터링 같은 것
  - 관례에 의한 간결한 설정



## 스프링의 핵심 개념

### 스프링의 진짜 핵심

- 스프링은 자바 언어 기반의 프레임 워크
  - 자바의 가장 큰 특징은 객체 지향 언어
- 스프링은 객체 지향 언어가 가진 강력한 특징을 살려, **좋은 객체 지향 애플리케이션**을 개발할 수 있게 도와주는 프레임워크



## 좋은 객체 지향 프로그래밍

### 객체 지향 프로그래밍

- 객체 지향 프로그래밍은 컴퓨터 프로그램을 명령어의 목록으로 보는 시각에서 벗어나 여러개의 독립된 단위, 즉 **객체**들의 모임으로 파악하고자 하는 것
- 각각의 객체는 메세지를 주고받고, 데이터를 처리할 수 있음
- 프로그램을 유연하고 변경 용이하게 만들기 때문에 대규모 소프트웨어 개발에 많이 사용됨
  - 레고 블럭을 조립하듯이 컴포넌트를 쉽고 유연하게 변경하면서 개발할 수 있는 방법 -> 다형성



### 다형성

- 객체 지향을 실세계에 비유

  - **역할**과 **구현**으로 세상을 구분
    - 운전자 역할과 자동차 역할
    - 자동차의 구현은 K3, 아반떼, 테슬라 등 다양할 수 있음
    - 자동차의 구현이 바뀌어도 운전자에는 영향이 없음. 즉, 운전자는 자동차를 운전할 줄 만 알면 됨
      - 운전자는 자동차의 구조를 몰라도, 자동차 인터페이스만 사용할 줄 알면됨
    - 로미오와 줄리엣
      - 로미오는 장동건 원빈, 줄리엣은 김태희, 송혜교가 배역을 맡을 수 있음
      - 배역은 언제든지 변경 가능함

- 역할과 구현으로 구분하면 세상이 단순해지고, 유연해지며 변경이 편리해짐

  - 클라이언트는 대상의 역할(인터페이스)만 알면 됨
  - 클라이언트는 구현 대상의 내부 구조를 몰라도 됨
  - 클라이언트는 구현 대상의 내부 구조가 변경되어도 영향을 받지 않음
  - 클라이언트는 구현 대상 자체를 변경해도 영향을 받지 않음

- 자바 언어의 다형성을 활용

  - 역할 -> 인터페이스

  - 구현 -> 인터페이스를 구현한 클래스, 구현 객체

  - 객체를 설계할 때 역할과 구현을 명확하게 분리

    - 역할(인터페이스)을 먼저 부여하고, 그 역할을 수행하는 객체 만들기

  - 다형성으로 인터페이스를 구현한 객체를 실행 시점에 유연하게 변경할 수 있음

    - ```MemberService```가 인터페이스인 ```MemberRepository```의 ```save``` 메서드를 호출

    - ```MemberRepository```의 구현체인 ```MemoryMemberRepository```와, ```JdbcMemberRepository``` 모두 사용 가능

      ```Java
      public class memberService {
        private MemberRepository memberRepository = new MemoryMemberRepository;
        //private MemberRepository memberRepository = new JdbcMemberRepository;
      }
      ```

    - 이는 마치 운전자가 차를 바꿔타는 것과 같음

- 다형성의 본질

  - 인터페이스를 구현한 객체 인스턴스를 실행 시점에 유연하게 변경할 수 있음
  - 다형성의 본질을 이해하려면 **협력**이라는 객체 사이의 관계에서 시작해야함
  - **클라이언트를 변경하지 않고, 서버의 구현 기능을 유연하게 변경할 수 있음**

- 정리

  - 실세계의 역할과 구현이라는 편리한 컨셉을 통해 객체 세상으로 가져올 수 있음
  - 유연하고, 변경 용이
  - 확장 가능한 설계
  - 클라이언트에 영향을 주지 않는 변경 가능
  - **인터페이스를 안정적으로 잘 설계하는 것이 중요**

- 한계

  - 역할(인터페이스) 자체가 변하면, 클라이언트, 서버 모두에 큰 변경이 발생
    - 자동차가 비행기로 변경된다면?
    - 연극의 대본이 변경된다면?



### 스프링과 객체 지향

- 다형성이 가장 중요함
- 스프링은 다형성을 극대화해서 이용할 수 있게 도와줌
- 스프링의 제어의 역전(IoC), 의존관계 주입(DI)은 다형성을 활용해서 역할과 구현을 편리하게 다룰 수 있도록 지원함
- 스프링을 사용하면 마치 레고 블럭 조립하듯이, 공연 무대의 배우를 선택하듯이, 구현을 편리하게 변경할 수 있음



### 좋은 객체 지향 설계의 5가지 원칙(SOLID)

- 클린 코드로 유명한 로버트 마틴이 좋은 객체 지향 설계의 5가지 원칙을 정리

  1. SRP (단일 책임 원칙)

     - 한 클래스는 하나의 책임만 가져야 함
     - 하나의 책임이라는 것은 모호한 개념
       - 책임은 클 수 있고, 작을 수 있음
       - 문맥과 상황에 따라 다름
       - 경험이 필요
     - 중요한 판단의 기준은 **변경**
       - 변경이 있을 때 파급 효과가 적으면 단일 책임 원칙을 잘 따른 것
         - UI 변경했을 때 SQL부터 싹 다 고쳐야 한다면 잘못된 설계
         - 객체의 생성과 사용을 분리해야 함

  2. OCP (개방-폐쇄 원칙)

     - 소프트웨어 요소는 **확장**에는 열려 있으나, **변경**에는 닫혀 있어야 함

     - 다형성을 활용

       - 인터페이스를 구현한 새로운 클래스(확장)를 하나 만들어서 새로운 기능을 구현

       - 인터페이스는 변경되지 않음

         ```java
         public class memberService {
           private MemberRepository memberRepository = new MemoryMemberRepository;
           //private MemberRepository memberRepository = new JdbcMemberRepository;
         }
         ```

     - 문제점

       - ```MemberService``` 클라이언트가 구현 클래스를 직접 선택
       - 구현 객체를 변경하려면 클라이언트 코드를 변경해야 함
       - 분명 다형성을 사용했지만, OCP 원칙을 지킬 수 없음
       - 이 문제를 어덯게 해결할까?
         - 객체를 생성하고, 연관관계를 맺어주는 별도의 조립, 설정자가 필요
         - 이것이 바로 스프링

  3. LSP (리스코프 치환 원칙)

     - 프로그램의 객체는 프로그램의 정확성을 깨뜨리지 않으면서 하위 타입의 인스턴스로 바꿀 수 있어야 함
     - 다형성에서 하위 클래스는 인터페이스 규약을 다 지켜야 한다는 것, 다형성을 지원하기 위한 원칙
     - 인터페이스를 구현한 구현체를 믿고 사용하려면 이 원칙이 필요
     - 단순히 컴파일에 성공하는 것을 넘어서는 이야기
       - 자동차 인터페이스의 엑셀은 앞으로 전진하라는 기능
       - 뒤로 가게 구현하면 LSP 위반

  4. ISP (인터페이스 분리 원칙)

     - 특정 클라이언트를 위한 인터페이스 여러 개가 범용 인터페이스 하나보다 나음
     - 자동차 인터페이스를 운전 인터페이스와 정비 인터페이스로 분리
     - 사용자 클라이언트를 운전자 클라이언트와 정비사 클라이언트로 분리
     - 분리하면, 정비 인터페이스 자체가 변해도 운전자 클라이언트에 영향을 주지 않음
     - 인터페이스가 명확해지고, 대체 가능성이 높아짐

  5. DIP (의존관계 역전 원칙)

     - **추상화**에 의존해야지, **구체화**에 의존하면 안됨

       - 의존성 주입
       - 운전자는 자동차의 역할(인터페이스)에 대해 알아야하지, 테슬라에 대해 알면 안됨

     - 구현 클래스에 의존하지 말고, 인터페이스에 의존해야 함

     - 클라이언트가 인터페이스에 의존해야 유연하게 구현체를 변경할 수 있음

       - 구현체에 의존하면 변경이 아주 어려워 짐

     - 그런데 OCP에서 설명한 ```MemberService```는 인터페이스에 의존하지만, 동시에 구현 클래스에도 의존함

       - ```MemberService``` 클라이언트가 구현 클래스를 직접 선택

         ```java
         public class memberService {
           private MemberRepository memberRepository = new MemoryMemberRepository;
           //private MemberRepository memberRepository = new JdbcMemberRepository;
         }
         ```

       - DIP 위반

- 정리

  - 객체 지향의 핵심은 다형성
  - 다형성만으로는 쉽게 부품을 갈아 끼우듯이 개발할 수 없음
    - 구현 객체를 변경할 때 클라이언트 코드도 함께 변경됨
  - 다형성 만으로는 OCP, DIP를 지킬 수 없음
  - 뭔가 더필요함



## 객체 지향과 스프링

### 다시 스프링으로

- 스프링은 다음 기술로 다형성 + OCP, DIP를 가능하게 지원
  - DI(Dependency Injection): 의존관계, 의존성 주입
  - DI 컨테이너 제공
    - 자바 객체들을 컨테이너 안에 넣어놓고 의존 관계를 연결해주고 주입해주는 기능 제공
- 클라이언트 코드의 변경 없이 기능 확장
  - 쉽게 부품을 교체하듯이 개발

- 정리
  - 모든 설계에 역할과 구현을 분리
  - 애플리케이션 설계도 공연을 설계하듯이 배역만 만들어두고, 배우는 언제든지 유연하게 변경할 수 있도록 만드는 것이 좋은 객체 지향 설계
  - 이상적으로는 모든 설계에 인터페이스를 부여
    - 사용할 데이터 베이스가 정해지지 않은 상황에서 일단 개발해야할 때, 일단 데이터 베이스 인터페이스를 만들고, 간단한 구현체를 반들어 개발하다가 바꿔 끼우기
  - 실무적 관점
    - 인터페이스를 도입하면 추상화라는 비용이 발생
    - 기능을 확장할 가능성이 없다면, 구체 클래스를 직접 사용하고, 향후 꼭 필요할 때 리팩터링해서 인터페이스를 도입하는 것도 방법
      - 이 역시 경험





## 스프링 프로젝트 생성

- [springboot](https://start.spring.io)
  - Gradle Project/Java/안정적인 최신 버젼(SNAPSHOT이나 M2가 없는 것) 선택
  - Group, Artifact 입력하고, Packaging은 jar, Java는 11 선택
  - Dependency 추가하고 Generate 눌러 압축파일 다운
  - 압축 풀고 build.gradle을 IDE에서 프로젝트로 열기
  - build.gradle에서 설정 확인 가능
    - build.gradle에서 설정 변경시 코끼리 버튼 눌러줘야 적용됨
  - Preference에서 gradle 검색 후, Build and run과 Run tests using을 Gradle(Defalut)에서 IntelliJ로 바꾸기
    - Gradle로 돌리면 느림



## 스프링 프로젝트 실행

- src-main-java-{group}.{artifact}-{artifact}Application 실행



## IoC, DI, 그리고 컨테이너

### 제어의 역전 IoC (Inversion of Control)

- 기존 프로그램은 클라이언트 구현 객체가 스스로 필요한 서버 구현 객체를 생성하고, 연결하고, 실행했음.

  - 한마디로 구현 객체가 프로그램의 제어 흐름을 스스로 조종했으며 개발자 입장에서는 자연스러운 흐름

- 반면에 AppConfig가 등장한 이후에 구현 객체는 자신의 로직을 실행하는 역할만을 담당

  - 프로그램의 제어 흐름에 대한 권한은 모두 AppConfig가 가져감

    - ```OrderServiceImpl```은 필요한 인터페이스들을 호출하지만, 어떤 구현 객체들이 실행될지 모른채로, 자신의 로직만 실행

      ```java
      public class OrderServiceImpl implements OrderService{
      
          private final MemberRepository memberRepository;
          private DiscountPolicy discountPolicy;
      
          public OrderServiceImpl(MemberRepository memberRepository, DiscountPolicy discountPolicy) {
              this.memberRepository = memberRepository;
              this.discountPolicy = discountPolicy;
          }
      	...
      }
      ```

- 이렇게 프로그램의 제어 흐름을 직접 제어하는 것이 아니라 외부에서 관리하는 것을 제어의 역전(IoC)라고 함



### 프레임워크  vs  라이브러리

- 프레임워크가 내가 작성한 코드를 제어하고, 대신 실행하면 그것은 프레임워크가 맞다.
  - JUnit, Spring, ...
- 반면에 내가 작성한 코드가 직접 제어의 흐름을 담당한다면, 그것은 프레임워크가 아닌 라이브러리
  - 자바 객체를 json으로 바꾸는 라이브러리는 개발자가 직접 호출



### 의존관계 주입 DI (Dependency Injection)

- ```OrderServiceImple```은 ```MemberRepository```와 ```DiscountPolicy``` 인터페이스에 의존함

  - 그러나 어떤 구현 객체가 사용될지는 모름

- 의존관계는 **정적인 클래스 의존 관계**와 **실행 시점에 결졍되는 동적인 객체(인스턴스) 의존 관계**로 분리해서 생각해야 함

  - 정적인 클래스 의존 관계

    - 클래스가 사용하는 코드만 보고 의존관계를 쉽게 판단 가능

    - 애플리케이션을 실행하지 않아도 분석 가능

      ```java
      public class OrderServiceImpl implements OrderService{
      
          private final MemberRepository memberRepository;
          private DiscountPolicy discountPolicy;
      
          public OrderServiceImpl(MemberRepository memberRepository, DiscountPolicy discountPolicy) {
              this.memberRepository = memberRepository;
              this.discountPolicy = discountPolicy;
          }
      	...
      }
      ```

      - 그런데 이러한 클래스 의존관계 만으로는 실제 어떤 객체가 ```OrderServiceImpl```에 주입 될지 알 수 없음

    - 동적인 객체 인스턴스 의존 관계

      - 애플리케이션 실행 시점에 실제 생성된 객체 인스턴스의 참조가 연결된 의존 관계

        ```java
        public class AppConfig {
            public MemberService memberService() {
                return new MemberServiceImpl(memberRepository());
            }
        
            public DiscountPolicy discountPolicy() {
                return new RateDiscountPolicy();
            }
        
            private MemoryMemberRepository memberRepository() {
                return new MemoryMemberRepository();
            }
        
            public OrderService orderService() {
                return new OrderServiceImpl(memberRepository(), discountPolicy());
            }
        }
        ```

      - 애플리케이션 실행 시점(런타임)에 외부에서 실제 구현 객체를 생성하고, 클라이언트에 전달해서 클라이언트와 서버의 실제 의존 관계가 연결되는 것을 **의존 관계 주입**이라고 함
        - 객체 인스턴스를 생성하고, 그 참조값을 전달해서 연결됨
          - ```OrderServiceImpl```에 ```MemoryMemberRepository```와 ```RateDiscountPolicy```의 참조값을 연결
      - 의존 관계 주입을 사용하면, 클라이언트 코드를 변경하지 않고 클라이언트가 호출하는 대상의 타입 인스턴스를 변경할 수 있음
      - 의존 관계 주입을 사용하면, 정적인 클래스 의존 관계를 변경하지 않고, 동적인 객체 인스턴스 의존 관계를 쉽게 변경할 수 있음
        - 클라이언트 코드에 손대지 않고 ```FixDiscountPolicy```를 , ```RateDiscountPolicy```로 쉽게 바꿀 수 있음



## IoC 컨테이너, DI 컨테이너

- AppConfig처럼 객체를 생성하고, 관리하면서 의존관계를 연결해주는 것을 **IoC 컨테이너** 또는 **DI 컨테이너**라 함
- 의존 관계 주입에 초점을 맞추어 최근에는 주로 DI 컨테이너라고 부름
- 또는 어셈블러, 오브젝트 팩토리 등으로 부르기도 함



## 스프링 컨테이너

- ```ApplicationContext```를 스프링 컨테이너라 함

- 기존에는 개발자가 AppConfig를 통해 객체를 생성하고 DI를 했지만, 이제부터는 스프링 컨테이너를 사용함

- 스프링 컨테이너는 ```@Configuration```이 붙은 AppConfig를 설정(구성) 정보로 사용

  - 여기서 ```@Bean```이 붙은 메서드를 모두 호출해서 반환된 객체를 스프링 컨테이너에 등록

  - 이렇게 스프링 컨테이너에 등록된 객체를 스프링 빈이라고 함

  - 기본적으로 스프링 빈은 ```@Bean```이 붙은 메서드의 명을 스프링 빈의 이름으로 사용

    ```java
    @Configuration
    public class AppConfig {
        @Bean
        public MemberService memberService() {
            return new MemberServiceImpl(memberRepository());
        }
        @Bean
        public DiscountPolicy discountPolicy() {
            return new RateDiscountPolicy();
        }
        @Bean
        public MemoryMemberRepository memberRepository() {
            return new MemoryMemberRepository();
        }
        @Bean
        public OrderService orderService() {
            return new OrderServiceImpl(memberRepository(), discountPolicy());
        }
    }
    ```

       - 다음과 같이 스프링 빈의 이름 변경 가능하지만, 관례적으로 사용 자제

         ```java
         @Bean(name="memberService2")
         public MemberService memberService() {
             return new MemberServiceImpl(memberRepository());
         }
         ```

         

         

- 이전에는 개발자가 필요한 객체를 AppConfig를 통해 직접 조회했지만, 이제부터는 스프링 컨테이너를 통해 필요한 스프링 빈(객체)를 찾아야 함

  - 스프링 빈은 ```applicationContext.getBean()``` 메서드를 이용해서 찾을 수 있음

    ```java
    public class MemberApp {
        public static void main(String[] args) {
            ApplicationContext applicationContext = new AnnotationConfigApplicationContext(AppConfig.class);
            MemberService memberService = applicationContext.getBean("memberService", MemberService.class);
            
    		...
        }
    }
    ```

    

- 기존에는 개발자가 직접 자바코드로 모든 것을 했다면, 이제는 스프링 컨테이너에 객체를 스프링 빈으로 등록하고, 스프링 컨테이너에서 스프링 빈을 찾아서 사용하도록 변경됨



## 스프링 컨테이너 생성

```java
ApplicationContext applicationContext = new AnnotationConfigApplicationContext(AppConfig.class)
```

- ```ApplicationContext```는 인터페이스이며, 스프링 컨테이너라 함
  - XML 기반으로도 만들 수 있고, 어노테이션 기반의 자바 설정 클래스로도 만들 수 있음
  - 요즘엔 주로 어노테이션 기반을 사용

### 스프링 컨테이너의 생성 과정

1. 스프링 컨테이너 생성

   ```java
   ApplicationContext applicationContext = new AnnotationConfigApplicationContext(AppConfig.class)
   ```

   - 스프링 컨테이너를 생성할 때는 구성 정보(AppConfig.class)를 지정해주어야 함

2. 스프링 빈 등록

   - 스프링 컨테이너는 파라미터로 넘어온 설정 클래스 정보를 사용해서 스프링 빈을 등록
     - ```@Bean```이 붙은 메서드를 호출하고 반환된 객체를 스프링 빈 저장소에 넣음
     - 빈 저장소에는 빈 이름과 빈 객체가 저장됨
   - **주의: 빈 이름은 항상 다른 이름을 부여해야 함**

3. 스프링 빈 의존 관계 설정

   ```java
   @Configuration
   public class AppConfig {
       @Bean
       public MemberService memberService() {
           return new MemberServiceImpl(memberRepository());
       }
       @Bean
       public DiscountPolicy discountPolicy() {
           return new RateDiscountPolicy();
       }
       @Bean
       public MemoryMemberRepository memberRepository() {
           return new MemoryMemberRepository();
       }
       @Bean
       public OrderService orderService() {
           return new OrderServiceImpl(memberRepository(), discountPolicy());
       }
   }
   ```

   - 스프링 컨테이너는 설정 정보를 참고해서 의존 관계를 주입(DI) 함
   - 참고
     - 스프링은 빈을 생성하고, 의존관계를 주입하는 단계가 나누어져 있음
     - 그런데 위의 예시처럼 자바 코드로 스프링 빈을 등록하면, 생성자를 호출하면서 의존 관계 주입도 한 번에 처리됨
     - 여기서는 이해를 돕기 위해 개념적으로 나누어 설명한 것
     - 자세한 것은 의존 관계 자동 주입에서 다시 보기



## 스프링 빈 조회

- 실무에서는 빈을 조회할 일이 거의 없음

- 스프링 컨테이너에서 스프링 빈을 찾는 가장 기본적인 조회 방법

  - ```ac.getBean(빈이름, 타입)```

  - ```ac.getBean(타입)```

  - 조회 대상 스프링 빈이 없으면 예외 발생

    ```java
    public class ApplicationContextBasicFindTest {
    
        AnnotationConfigApplicationContext ac = new AnnotationConfigApplicationContext(AppConfig.class);
    
        @Test
        @DisplayName("빈 이름으로 조회")
        void findBeanByName() {
            MemberService memberService = ac.getBean("memberService", MemberService.class);
            assertThat(memberService).isInstanceOf(MemberServiceImpl.class);
        }
    
        @Test
        @DisplayName("이름 없이 타입으로 조회")
        void findBeanByType() {
            MemberService memberService = ac.getBean(MemberService.class);
            assertThat(memberService).isInstanceOf(MemberServiceImpl.class);
        }
    
        @Test
        @DisplayName("구체 타입으로 조회")
        // 구현에 의존하기 때문에 좋은 코드가 아님. 
        void findBeanByName2() {
            MemberService memberService = ac.getBean("memberService", MemberServiceImpl.class);
            assertThat(memberService).isInstanceOf(MemberServiceImpl.class);
        }
    
        @Test
        @DisplayName("빈 이름으로 조회X")
        void findBeanByNameX() {
            // 람다함수가 실행되면 왼쪽의 에러가 발생해야함
            assertThrows(NoSuchBeanDefinitionException.class, () -> ac.getBean("xxxxx", MemberService.class));
        }
    }
    ```

    - 타입으로 조회시 같은 타입의 스프링 빈이 둘 이상이면 오류가 발생함

      - 이 때는 빈 이름을 지정해줌

      - ```ac.getBeansOfType(타입)```으로 해당 타입의 모든 빈을 조회할 수 있음

        ```java
        public class ApplicationContextSameBeanFindTest {
        
            AnnotationConfigApplicationContext ac = new AnnotationConfigApplicationContext(SameBeanConfig.class);
        
            @Test
            @DisplayName("타입으로 조회시 같은 타입이 둘 이상 있으면, 중복 오류 발생")
            void findBeanByTypeDuplicate() {
                assertThrows(NoUniqueBeanDefinitionException.class, ()->ac.getBean(MemberRepository.class));
            }
            
            @Test
            @DisplayName("타입으로 조회시 같은 타입이 둘 이상 있으면, 빈 이름을 지정해주면 됨")
            void findBeanByName() {
                MemberRepository memberRepository = ac.getBean("memberRepository1", MemberRepository.class);
                assertThat(memberRepository).isInstanceOf(MemberRepository.class);
            }
        
            @Test
            @DisplayName("특정 타입을 모두 조회")
            void findAllBeanByType() {
                Map<String, MemberRepository> beansOfType = ac.getBeansOfType(MemberRepository.class);
                assertThat(beansOfType.size()).isEqualTo(2);
            }
        
            @Configuration
            static class SameBeanConfig {
                @Bean
                public MemberRepository memberRepository1() {
                    return new MemoryMemberRepository();
                }
        
                @Bean
                public MemberRepository memberRepository2() {
                    return new MemoryMemberRepository();
                }
            }
        }
        ```



- 상속 관계 조회

  - 부모 타입으로 조회하면, 자식 타입도 함께 조회됨

    - 모든 자바 객체의 최고 부모인 ```Object```로 조회하면, 모든 스프링 빈을 조회함

    ```java
    public class ApplicationContextExtendsFindTest {
        AnnotationConfigApplicationContext ac = new AnnotationConfigApplicationContext(TestConfig.class);
    
        @Test
        @DisplayName("부모 타입으로 조회시, 자식이 둘 이상 있으면, 중복 오류 발생")
        void findBeanByParentTypeDuplicate() {
            assertThrows(NoUniqueBeanDefinitionException.class, ()->ac.getBean(DiscountPolicy.class));
        }
    
        @Test
        @DisplayName("부모 타입으로 조회시, 자식이 둘 이상 있으면, 빈 이름을 지정하면 됨")
        void findBeanByParentTypeBeanName() {
            DiscountPolicy rateDiscountPolicy = ac.getBean("rateDiscountPolicy",DiscountPolicy.class);
            assertThat(rateDiscountPolicy).isInstanceOf(RateDiscountPolicy.class);
        }
    
        @Test
        @DisplayName("특정 하위 타입으로 조회")
        void findBeanBySubType() {
            RateDiscountPolicy bean = ac.getBean(RateDiscountPolicy.class);
            assertThat(bean).isInstanceOf(RateDiscountPolicy.class);
        }
    
        @Test
        @DisplayName("부모 타입으로 모두 조회")
        void findBeanByParentType() {
            Map<String, DiscountPolicy> beansOfType = ac.getBeansOfType(DiscountPolicy.class);
            assertThat(beansOfType.size()).isEqualTo(2);
        }
    
        @Configuration
        static class TestConfig {
            @Bean
            public DiscountPolicy rateDiscountPolicy() {
                return new RateDiscountPolicy();
            }
    
            @Bean
            public DiscountPolicy fixDiscountPolicy() {
                return new FixDiscountPolicy();
            }
        }
    }
    ```



## BeanFactory와 ApplicationContext

### BeanFactory

- 스프링 컨테이너의 최상위 인터페이스
- 스프링 빈을 관리하고 조회하는 역할 담당
  - ```getBean()```
- 지금까지 우리가 사용했던 대부분의 기능은 ```BeanFactory```가 제공



### ApplicationContext

- BeanFactory를 상속하는 인터페이스
- 빈을 관리하고 조회하는 기능을 ```BeanFactory```가 제공해주는데, 굳이 ```ApplicationContext```를 쓰는 이유
  - 애플리케이션을 개발할 때는 빈을 관리하고 조회하는 기능은 물론이고, 수 많은 부가 기능 필요
  - ```ApplicationContext```는 이 수 많은 부가기능과 관련된 인터페이스 또한 상속함
    - ```EnvironmentCapable, MessageSource, ApplicationEventPublisher, ResourceLoader, ...```



### 정리

- ```ApplicationContext```는 ```BeanFactory```의 기능을 상속받음
- ```ApplicationContext```는 빈 관리 기능 + 편리한 부가 기능을 제공
- ```BeanFactory```를 직접 사용할 일은 거의 없고, 대부분 ```ApplicationContext```를 사용
- ```BeanFactory```나 ```ApplicationContext```를 스프링 컨테이너라 함







 











