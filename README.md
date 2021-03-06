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



## 스프링의 다양한 설정 형식 지원

- 스프링 컨테이너는 다양한 형식의 설정 정보를 받아들일 수 있게 유연하게 설계됨

  - 어노테이션 기반 자바 코드 설정

    ```java	
    ApplicationContext applicationContext = new AnnotationConfigApplicationContext(AppConfig.class)
    ```

  - XML 설정

    - 최근에는 스프링 부트를 많이 사용하면서 XML 기반의 설정은 잘 사용하지 않음

    - 아직 많은 레거시 프로젝트들이 XML로 설정되어 있음

    - XML을 사용하면 컴파일 없이 빈 설정 정보를 변경할 수 있다는 장점이 있음

      ```xml
      <?xml version="1.0" encoding="UTF-8"?>
      <beans xmlns="http://www.springframework.org/schema/beans"
             xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
             xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
          <bean id="memberService" class="hello.core.member.MemberServiceImpl" >
              <constructor-arg name="memberRepository" ref="memberRepository" />
          </bean>
      
          <bean id="memberRepository" class="hello.core.member.MemoryMemberRepository" />
      
          <bean id="orderService" class="hello.core.order.OrderServiceImpl" >
              <constructor-arg name="memberRepository" ref="memberRepository" />
              <constructor-arg name="discountPolicy" ref="discountPolicy" />
          </bean>
      
          <bean id="discountPolicy" class="hello.core.discount.RateDiscountPolicy" />
      </beans>
      ```

      ```java
      public class XmlAppContext {
          @Test
          void xmlAppContext() {
              ApplicationContext ac = new GenericXmlApplicationContext("appConfig.xml");
              MemberService memberService = ac.getBean("memberService", MemberService.class);
              assertThat(memberService).isInstanceOf(MemberService.class);
          }
      }
      ```



## 스프링 빈 설정 메타 정보

- 스프링은 ```BeanDefinition```이라는 추상화를 통해 다양한 설정 형식을 지원
- 역할과 구현을 개념적으로 나눔
  - XML/자바 코드를 읽어서 ```BeanDefinition```을 만듦
  - 스프링 컨테이너는 XML인지, 자바 코드인지 몰라도 됨
- ```BeanDefinition```을 빈 설정 메타 정보라 함
- 스프링 컨테이너는 이 메타 정보를 기반으로 스프링 빈 생성
  - ```AnnotationConfigApplicationContext```는 ```AnnotatedBeanDefinitionReader```를 사용해서 ```AppConfig.class```를 읽고 ```BeanDefinition```을 만듦
  - ```GenerixXmlApplicationContext```는 ```XmlDefinitionReader```를 사용해서 ```appConfig.xml``` 설정 정보를 읽고 ```BeanDefinition```을 만듦



## 싱글톤 컨테이너

- 스프링 없는 순수한 DI 컨테이너인 ```AppConfig```는 요청을 할 때 마다 객체를 새로 생성함

  ```java
  public class SingletonTest {
      @Test
      @DisplayName("스프링 없는 순수한 DI 컨테이너")
      void pureContainer() {
          AppConfig appConfig = new AppConfig();
          //호출할 때 마다 객체를 생성
          MemberService memberService1 = appConfig.memberService();
          MemberService memberService2 = appConfig.memberService();
  
          //memberService1 != memberService2
          assertThat(memberService1).isNotSameAs(memberService2);
      }
  }
  ```

  - 고객 트래픽이 초당 100이 나오면, 초당 100개의 객체가 생성되고 소멸됨
    - 메모리 낭비
  - 이를 해결하기 위해서 객체를 1개만 생성하고 공유하도록 설계하는 방법이 싱글톤 패턴



## 싱글톤 패턴

- 클래스의 인스턴스가 딱 1개만 생성되는 것을 보장하는 디자인 패턴

- 인스턴스를 2개 이상 사용하지 못하도록 막아야 함

  - ```private``` 생성자를 사용해서 외부에서 임의로 ```new``` 키워드를 사용하지 못하도록 막음

    ```java
    public class SingletonService {
    
        private static final SingletonService instance = new SingletonService();
    
        public static SingletonService getInstance() {
            return instance;
        }
    
        private SingletonService() {
        }
    }
    ```

    - ```static``` 영역에 객체 ```instance```를 미리 하나 생성해서 올려둠
    - 이 객체 인스턴스가 필요할 때는 오직 ```getInstance``` 메서드를 통해서만 조회
      - 이 메서드를 호출하면 항상 같은 인스턴스 반환
    - 딱 1개의 객체 인스턴스만 존재해야하므로, 생성자를 ```private```으로 막아 외부에서 ```new``` 키워드로 객체 인스턴스가 생성되는 것을 막음
      - 외부에서 ```new SingletonService()```를 호출하면, ```private``` 때문에 컴파일 에러 발생
    - 싱글톤 패턴을 구현하는 방법은 여러가지가 있음
      - 여기서는 객체를 미리 생성해두는 가장 단순하고 안전한 방법 선택

- 싱글톤 패턴 적용 확인

  ```java
  @Test
  @DisplayName("싱글톤 패턴을 적용한 객체 사용")
  void singletonServiceTest() {
      SingletonService singletonService1 = SingletonService.getInstance();
      SingletonService singletonService2 = SingletonService.getInstance();
  
      assertThat(singletonService1).isSameAs(singletonService2);
  }
  ```

  		- 호출할 때 마다 같은 객체 인스턴스가 반환됨



### 싱글톤 패턴의 문제점

- 싱글톤 패턴을 구현하는 코드 자체가 많이 들어감
- 의존 관계상 클라이언트가 구체 클래스에 의존 -> DIP 위반
- OCP 위반 가능성 높음
- 테스트가 어려움
- 내부 속성 변경/초기화 어려움
- private 생성자로 자식 클래스 만들기 힘듦
- **결론적으로 유연성이 떨어짐 -> DI를 적용하기 어려움**
- 안티 패턴으로 불리기도 함



## 다시, 싱글톤 컨테이너

- 스프링 컨테이너는 싱글톤 패턴의 문제점을 해결하면서, 객체 인스턴스를 싱글톤으로 관리함

  - 스프링 빈이 바로 싱글톤으로 관리되는 빈임

- 싱글톤 객체를 생성하고 관리하는 기능을 싱글톤 레지스트리라 함

- 스프링 컨테이너의 이런 기능 덕분에 싱글톤 패턴의 모든 단점을 해결하면서 객체를 싱글톤으로 유지할 수 있음

  - 싱글톤 패턴을 위한 지저분한 코드가 필요 없음

  - DIP, OCP, 테스트, ```private``` 생성자로부터 자유로움

    ```java
    @Test
    @DisplayName("스프링 컨테이너와 싱글톤")
    void springContainer() {
        ApplicationContext ac = new AnnotationConfigApplicationContext(AppConfig.class);
    
        MemberService memberService1 = ac.getBean("memberService", MemberService.class);
        MemberService memberService2 = ac.getBean("memberService", MemberService.class);
    
        assertThat(memberService1).isSameAs(memberService2);
    }
    ```

- 스프링 컨테이너 덕분에 웹어플리케이션의 경우 고객의 요청이 올 때 마다 객체를 생성하는 것이 아니라, 이미 만들어진 객체를 공유해서 효율적으로 재사용할 수 있음

- 스프링의 기본 빈 등록 방식은 싱글톤이지만, 싱글톤 방식만 지원하는 것은 아님



## 싱글톤 방식의 주의점

- 객체 인스턴스를 하나만 생성해서 공유하는 싱글톤 방식은 여러 클라이언트가 하나의 같은 객체 인스턴스를 공유하기 때문에 싱글톤 객체의 상태가 유지(stateful)되도록 설계하면 안됨

- 무상태(stateless)로 설계해야 함

  - 특정 클라이언트에 의존적인 필드가 있으면 안됨
  - 특정 클라이언트가 값을 변경할 수 있는 필드가 있으면 안됨
  - 가급적 읽기만 가능해야 함
  - 필드 대신, 자바에서 공유되지 않는 지역변수, 파라미터, ThreadLocal 등을 사용해야 함

- 스프링 빈의 필드에 공유 값을 설정하면 매우 큰 장애가 발생할 수 있음

  ```java
  public class StatefulService {
  
      private int price; // 상태를 유지하는 필드
  
      public void order(String name, int price) {
          this.price = price; // 여기가 문제
      }
  
      public int getPrice() {
          return price;
      }
  }
  ```

  ```java
  class StatefulServiceTest {
  
      @Test
      void statefulServiceSingleton() {
          ApplicationContext ac = new AnnotationConfigApplicationContext(TestConfig.class);
          // 1이든 2든 같은 인스턴스임
          StatefulService statefulService1 = ac.getBean(StatefulService.class);
          StatefulService statefulService2 = ac.getBean(StatefulService.class);
          
          // Thread A: 사용자A 10,000원 주문
          statefulService1.order("userA", 10000);
          // Thread B: 사용자B 20,000원 주문
          statefulService2.order("userA", 20000);
  
          // Thread A: 사용자A 주문 금액 조회
          int price = statefulService1.getPrice();
  
          Assertions.assertThat(statefulService1.getPrice()).isEqualTo(20000);
  
      }
  
      static class TestConfig {
          @Bean
          public StatefulService statefulService() {
              return new StatefulService();
          }
      }
  }
  ```

  - Thread A가 사용자A의 코드를 호출하고, Thread B가 사용자B의 코드를 호출

  - ```StatefulService```의 ```price``` 필드는 공유되는 필드인데, 특정 클라이언트가 값을 변경함

  - 사용자A의 주문 금액은 10,000원이어야 정상이지만, 20,000원이 되어버림

  - 아래와 같이 무상태로 설계하는게 좋음

    ```java
    public class StatefulService {
        public void order(String name, int price) {
            this.price = price;
            return price;
        }
    }
    ```

  - 실제로는 훨씬 더 복잡한 코드에서 문제가 생기고 찾아내기 힘듦

    - 실무에서 이런 경우를 종종 보는데, 매우 해결하기 어려운 큰 문제들이 터짐
    - **스프링 빈은 항상 무상태로 설계해야 함**



## ```@Configuration과 싱글톤```

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

- ```memberService()```도 ```memberRepository()```를 호출하여 ```MemoryMemberRepository()``` 인스턴스를 생성하고, ```orderService()```도 ```memberRepository()```를 호출하여 ```MemoryMemberRepository()``` 인스턴스를 생성하는데, 이 둘은 사실 같은 인스턴스임

  ```java
  public class ConfigurationSingletonTest {
  
      @Test
      void configurationTest() {
          ApplicationContext ac = new AnnotationConfigApplicationContext(AppConfig.class);
  
          MemberServiceImpl memberService = ac.getBean("memberService", MemberServiceImpl.class);
          OrderServiceImpl orderService = ac.getBean("orderService", OrderServiceImpl.class);
          MemberRepository memberRepository = ac.getBean("memberRepository", MemberRepository.class);
  
          MemberRepository memberRepository1 = memberService.getMemberRepository();
          MemberRepository memberRepository2 = orderService.getMemberRepository();
  
          assertThat(memberRepository1).isSameAs(memberRepository2);
          assertThat(memberRepository).isSameAs(memberRepository1);
      }
  }
  ```



### @Configuration과 바이트 코드 조작의 마법(?)

- ```ApplicationContext ac = new AnnotationConfigApplicationContext(AppConfig.class)```를 통해 스프링 컨테이너를 만들면, ```MemoryMemberRepository()```객체가 여러개 생성되어야 할 것 같지만, 실제로는 한 개만 생성되어 공유됨

- 이는 ```@Configuration```이 적용된 ```AppConfig``` 때문임

  - 스프링 컨테이너에는 ```AppConfig``` 대신, CGLIB이라는 바이트 코드 조작 라이브러리를 통해 ```AppConfig```를 상속 받은 임의의 다른 클래스가 빈으로 등록됨

    ```java
    @Test
        void configurationDeep() {
            ApplicationContext ac = new AnnotationConfigApplicationContext(AppConfig.class);
            AppConfig bean = ac.getBean(AppConfig.class);
    
            System.out.println("bean = " + bean.getClass());
        }
    
    //출력
    //bean = class hello.core.AppConfig$$EnhancerBySpringCGLIB$$4ab6406e
    ```

  - 이 임의의 다른 클래스가 싱글톤을 보장

    - ```@Bean```이 붙은 메서드마다 이미 스프링 빈이 등록되어 있으면 찾아서 반환하고, 아니면 생성해서 빈으로 등록 후 반환하는 코드가 동적으로 만들어짐

    - 내부의 코드가 다음과 같이 작성되어 있을 것임(실제로는 훨씬 복잡)

      ```java
      ...
      @Bean
      public MemberRepository memberRepository() {
          if (MemoryMemberRepository가 스프링 컨테이너에 빈으로 등록되어 있다면) {
              return 스프링 컨테이너에서 찾아서 반환
          } else {
              빈으로 등록되어 있지 않다면, 기존 로직을 호출하여 MemoryMemberRepository 생성하고 스프링 컨테이너에 등록
              return 반환
          }
      }
      ```

- ```@Configuration```을 빼버리면, ```@Bean```이 붙은 메서드들이 빈으로 다 등록되지만, 싱글톤이 보장되지 않음

  - ```MemberService```와, ```OrderService```에서 같은 인스턴스를 사용하지 않고 ```MemoryMemberRepository()``` 인스턴스가 여러개 생성됨
  - 또한 그 인스턴스들은 순수한 자바 코드로 인스턴스를 만든 것일 뿐, 스프링 빈으로 등록되지 않음

- 스프링 설정 정보는 항상 ```@Configuration```을 사용하자



## 컴포넌트 스캔과 의존 관계 자동 주입

- 스프링은 설정 정보가 없어도 자동으로 스프링 빈을 등록하는 **컴포넌트 스캔 기능**과 **의존 관계 자동 주입 기능**을 제공

- ```@ComponentScan```을 붙여 컴포넌트를 스캔

  ```java
  @Configuration
  @ComponentScan(
          excludeFilters = @ComponentScan.Filter(type = FilterType.ANNOTATION, classes = Configuration.class)
  )
  public class AutoAppConfig {
  
  }
  ```

  - 이 때, ```@Configuration```이 붙은 설정 정보도 자동으로 등록되기 때문에, ```excludeFilter```를 이용하여 설정 정보를 컴포넌트 스캔 대상에서 제외해줌

  - 일반적으로 설정 정보를 스캔 대상에서 제외하지는 않지만, 기존 예제 코드를 활용하기 위함임

- 컴포넌트 스캔은 ```@Component``` 어노테이션이 붙은 클래스를 스캔해서 스프링 빈으로 등록

  ```java
  @Component
  public class MemoryMemberRepository implements MemberRepository {
  	...
  }
  ```

  - 스프링 빈의 기본 이름은 클래스명을 사용하되, 맨 앞글자만 소문자로 사용

    - ```MemberServiceImpl``` -> ```memberServiceImpl```

  - 빈 이름을 직접 지정할 때는, ```@Component("memberServiceImpl2")```와 같이 사용

  - 컴포넌트 스캔을 사용하면, 직접 의존 관계를 주입하는 것 대신 ```@Autowired```를 이용하여 의존 관계 주입

    - 생성자에 ```@Autowired```를 붙이면, 스프링 컨테이너가 자동으로 해당 스프링 빈을 찾아서 주입

    - 기본 조회 전략은 타입이 같은 빈을 찾아서 주입

      ```java
      @Component
      public class MemberServiceImpl implements MemberService{
      
          private final MemberRepository memberRepository;
      
          @Autowired
          public MemberServiceImpl(MemberRepository memberRepository) {
              this.memberRepository = memberRepository;
          }
      	...
      }
      ```

      

- 기존에 빈을 직접 등록했었던 ```AppConfig```처럼 잘 작동

  ```java
  public class AutoAppConfigTest {
  
      @Test
      void basicScan() {
          ApplicationContext ac = new AnnotationConfigApplicationContext(AutoAppConfig.class);
  
          MemberService memberService = ac.getBean(MemberService.class);
          assertThat(memberService).isInstanceOf(MemberService.class);
      }
  }
  ```





## 탐색  위치 와 기본 스캔 대상

### 탐색 위치 지정

- 모든 자바 클래스를 다 스캔하면 시간이 오래 걸리므로 꼭 필요한 위치부터 탐색하도록 시작 위치를 지정할 수 있음

  ```java
  @ComponentScan(
  	basePackages = "hello.core"
  )
  ```

  - ```basePackages```에 지정된 패키지와, 그 하위 패키지들을 모두 탐색
    - ```basePackages = {"hello.core", "hello.service"}```와 같이 탐색 시작 위치를 여러개 지정할 수 있음
  - ```basePackageClasses```를 지정하면, 지정한 클래스의 패키지를 탐색 시작 위치로 설정
  - 따로 설정하지 않으면 ```@ComponentScan```이 붙은 설정 정보 클래스의 패키지가 탐색 시작위치로 설정됨
  - **권장하는 방법**
    - 탐색 위치를 따로 지정하지 않고, 설정 정보 클래스의 위치를 프로젝트 최상단에 두는 것
      - 스프링 부트가 이 방법을 기본적으로 제공



### 컴포넌트 스캔 기본 대상

- 컴포넌트 스캔의 대상은 다음과 같음

  |      Annotation      |               use                |
  | :------------------: | :------------------------------: |
  |   ```@Component```   |      컴포넌트 스캔에서 사용      |
  |  ```@Contoroller```  |   스프링 MVC 컨트롤러에서 사용   |
  |    ```@Service```    |  스프링 비즈니스 로직에서 사용   |
  |  ```@Repository```   | 스프링 데이터 접근 계층에서 사용 |
  | ```@Configuration``` |    스프링 설정 정보에서 사용     |

  - ```@Component``` 외의 나머지 어노테이션의 정의를 보면, ```@Component```가 포함되어있음
  - 참고
    - 어노테이션에는 상속 관계가 없음
    - 어노테이션이 특정 어노테이션을 포함하고 있음을 인식할 수 있는 것은 자바 언어가 지원하는 기능이 아닌, 스프링이 지원하는 기능임



### 필터

```java
public class ComponentFilterAppConfigTest {

    @Test
    void filterScan() {
        ApplicationContext ac = new AnnotationConfigApplicationContext(ComponentFilterAppConfig.class);
        BeanA beanA = ac.getBean("beanA", BeanA.class);
        assertThat(beanA).isNotNull();

        org.junit.jupiter.api.Assertions.assertThrows(
                NoSuchBeanDefinitionException.class,
                () -> ac.getBean("beanB", BeanB.class)
        );

    }

    @Configuration
    @ComponentScan(
            includeFilters = @Filter(type = FilterType.ANNOTATION, classes = MyIncludeComponent.class),
            excludeFilters = @Filter(type = FilterType.ANNOTATION, classes = MyExcludeComponent.class)
    )
    static class ComponentFilterAppConfig {
    }
}
```

- ```includeFilters```에 ```MyIncludeComponent``` 어노테이션을 추가하여 ```BeanA```가 스프링 빈에 등록됨
- ```excludeFilters```에 ```MyExcludeComponent``` 어노테이션을 추가하여 ```BeanB```가 스프링 빈에 등록되지 않음



## 중복 등록과 충돌

### 자동 빈 등록 vs 자동 빈 등록

- 컴포넌트 스캔에 의해 자동으로 스프링 빈이 등록되었는데, 그 이름이 같은 경우 스프링은 ```ConflictingBeanDefinitionException``` 오류를 발생시킴



### 수동 빈 등록 vs 자동 빈 등록

- 이 경우, **스프링**에서는 수동 빈 등록이 우선권을 가짐
  - 수동 빈이 자동 빈을 오버라이딩 해버림
- 대부분 개발자가 의도적으로 설정해서 이런 결과가 만들어지기보다, 여러 설정들이 꼬여서 이런 결과가 만들어지는 게 대부분임
  - 이런 애매한 버그는 잡기 매우 힘듦
  - 따라서 **스프링 부트**는 최근 수동 빈 등록과 자동 빈 등록이 충돌나면 오류가 발생하도록 기본값을 바꿈



## 의존 관계 자동 주입

### 다양한 의존 관계 주입 방법

1. 생성자 주입

   - 생성자를 통해서 의존 관계를 주입 받는 방법

     ```java
     @Component
     public class OrderServiceImpl implements OrderService{
     
         private final MemberRepository memberRepository;
         private final DiscountPolicy discountPolicy;
     
         @Autowired
         public OrderServiceImpl(MemberRepository memberRepository, DiscountPolicy discountPolicy) {
             this.memberRepository = memberRepository;
             this.discountPolicy = discountPolicy;
         }
     
     	...
     }
     ```

   - 생성자 호출 시점에 딱 1번 호출되는 것이 보장됨

   - **불변, 필수** 의존 관계에 사용

   - 스프링 빈에서 오버로딩 없이 생성자가 하나인 경우, ```@Autowired``` 생략 가능

   - 대부분 생성자 주입 사용

2. 수정자 주입(```setter``` 주입)

   - ```setter```라 불리는 수정자 메서드를 통해서 의존 관계를 주입하는 방법

     ```java
     @Component
     public class OrderServiceImpl implements OrderService{
     
         private final MemberRepository memberRepository;
         private final DiscountPolicy discountPolicy;
       
         @Autowired
       	public setMemberRepository(MemberRepository memberRepository) {
           this.memberRepository = memberRepository
         }
       
         @Autowired
       	public setDiscountPolicy(DiscountPolicy discountPolicy) {
           this.discountPolicyy = discountPolicy
         }
       
     	...
     }
     ```

   - **선택, 변경** 가능성이 있는 의존 관계에 사용

3. 필드 주입

   - 이름 그대로 필드에 바로 주입하는 방법

     ```java
     @Component
     public class OrderServiceImpl implements OrderService{
     
         @Autowired private final MemberRepository memberRepository;
         @Autowired private final DiscountPolicy discountPolicy;
     
     	...
     }
     ```

   - 코드가 간결하지만, 외부에서 변경이 불가능하여 테스트하기 힘들다는 단점이 있음
   - 그래서 거의 사용하지 않음
     - 어플리케이션의 실제 코드와 관계 없는 테스트 코드나, 스프링 설정을 목적으로 하는 ```Configuration``` 같은 곳에서만 특별한 용도로 사용

4. 일반 메서드 주입

   - 일반 메서드를 통해서 주입 받을 수 있음

     ```java
     @Component
     public class OrderServiceImpl implements OrderService{
     
         private final MemberRepository memberRepository;
         private final DiscountPolicy discountPolicy;
       
         @Autowired
         public void init(MemberRepository memberRepository, DiscountPolicy discountPolicy) {
             this.memberRepository = memberRepository;
             this.discountPolicy = discountPolicy;
         }
     
     	...
     }
     ```

   - 한 번에 여러 필드를 주입 받을 수 있음

   - 일반적으로 잘 사용하지 않음



## 옵션 처리

- 주입할 스프링 빈이 없어도 동작해야 할 때가 있음

- ```@Autowired```만 사용할 경우, ```required``` 옵션의 기본값이 ```true```이기 때문에 오류가 발생할 수 있음

- 이를 다음의 세 가지 방법으로 처리 가능

  1. ```Autowired(required=false)```

     - 자동 주입할 대상이 없을 경우, 수정자 메서드 자체가 호출되지 않음

       ```java
       public class AutowiredTest {
       
           @Test
           void AutowiredOption() {
               ApplicationContext ac = new AnnotationConfigApplicationContext(TestBean.class);
           }
       
           static class TestBean {
               @Autowired(required=false)
               public void setNoBean1(Member noBean1) {
                   System.out.println("noBean1 = " + noBean1);
                 	// Member는 스프링 빈이 아니므로 아무것도 출력되지 않음
               }
           }
       }
       
       ```

  2. ```@Nullable```

     - 자동 주입할 대상이 없으면 null 주입

       ```java
       public class AutowiredTest {
       
           @Test
           void AutowiredOption() {
               ApplicationContext ac = new AnnotationConfigApplicationContext(TestBean.class);
           }
       
           static class TestBean {
               @Autowired
               public void setNoBean2(@Nullable Member noBean2) {
                   System.out.println("noBean2 = " + noBean2);
                 	// noBean2 = null
               }
           }
       }
       
       ```

  3. ```Optional<>```

     - 자동 주입할 대상이 없으면 ```Optional.empty``` 주입

       ```java
       public class AutowiredTest {
       
           @Test
           void AutowiredOption() {
               ApplicationContext ac = new AnnotationConfigApplicationContext(TestBean.class);
           }
       
           static class TestBean {
               @Autowired
               public void setNoBean3(Optional<Member> noBean3) {
                   System.out.println("noBean3 = " + noBean3);
                 	// noBean3 = Optional.empty
               }
           }
       }
       
       ```



## 생성자 주입을 선택하라

- 과거에는 수정자 주입과 필드 주입등의 방법을 많이 사용했지만, 최근에는 스프링을 포함한 DI 프레임워크 대부분이 **생성자 주입**을 권장함

### 생성자 주입을 권장하는 이유

- 불변

  - 대부분의 의존 관계 주입은 한 번 일어나면, 어플리케이션 종료 시점까지 의존 관계를 변경할 일이 없고 오히려 불변해야 하는 경우가 많음
  - 수정자 주입을 사용하면 ```setXxxx``` 메서드를 ```public```으로 열어둬야 함
    - 누군가 실수로 변경할 수도 있고, 변경하면 안되는 메서드를 열어두는 것은 좋은 설계가 아님

  - 생성자 주입은 객체를 생성할 때 딱 1번만 호출되므로, 이후에 호출되는 일이 없어 불변하게 설계할 수 있음

- 누락

  - 프레임워크 없이 순수한 자바 코드로만 단위 테스트를 수행할 때, 코드가 누락되면 컴파일 에러가 발생하므로 누락을 잡아내기 쉬움

- ```final``` 키워드

  - 생성자 주입을 사용하면, 필드에 ```final``` 키워드를 사용 가능
    - 수정자 주입을 포함한 나머지 주입 방식은 모두 생성자 이후에 호출되므로, 필드에 ```final``` 키워드 사용 불가능
  - 생성자에서 혹시라도 값이 설정되지 않으면, 컴파일 에러 발생



### 정리

- 생성자 주입 방식을 사용하면, 프레임 워크에 의존하지 않고, 순수한 자바 언어의 특징을 잘 살릴 수 있음
- 기본으로 생성자 주입을 사용하고, 필수 값이 아닌 경우에는 수정자 주입 방식을 옵션으로 부여
  - 생성자 주입과 수정자 주입을 동시에 사용 가능
  - 필드 주입은 사용하지 않는게 좋음



## 롬복(lombok)과 최신 트렌드

- 막상 개발을 해보면, 대부분이 다 불변이고, 따라서 생성자에 ```final``` 키워드를 사용하게 됨

  - 생성자도 만들어야 하고, 주입 받은 값을 대입하는 코드도 만들어야됨

    ```java
    @Component
    public class OrderServiceImpl implements OrderService{
    
        private final MemberRepository memberRepository;
        private final DiscountPolicy discountPolicy;
    
        @Autowired
        public OrderServiceImpl(MemberRepository memberRepository, DiscountPolicy discountPolicy) {
            this.memberRepository = memberRepository;
            this.discountPolicy = discountPolicy;
        }
    
    	...
    }
    
    ```

- lombok 라이브러리로 코드를 최적화할 수 있음

  - build.gradle 설정후 코끼리 클릭

    ```java
    ...
      
    //lombok 설정 추가
    configurations {
    	compileOnly {
    		extendsFrom annotationProcessor
    	}
    }
    //lombok 설정 끝
    
    ...
    
    dependencies {
    	implementation 'org.springframework.boot:spring-boot-starter'
    
    	//lombok 라이브러리 추가
    	compileOnly 'org.projectlombok:lombok'
    	annotationProcessor 'org.projectlombok:lombok'
    
    	testCompileOnly 'org.projectlombok:lombok'
    	testAnnotationProcessor 'org.projectlombok:lombok'
    	//lombok 라이브러리 추가 끝
    
    	testImplementation 'org.springframework.boot:spring-boot-starter-test'
    }
    
    ...
    ```

  - lombok 플러그인 설치하고, preference-annotation processor에서 enable annotation processing 활성화

  - lombok을 이용하여 다음과 같이 코드를 간단히 작성할 수 있음

    ```java
    @Component
    @RequiredArgsConstructor
    public class OrderServiceImpl implements OrderService{
    
        private final MemberRepository memberRepository;
        private final DiscountPolicy discountPolicy;
    
    	...
    }
    ```

    - ```@RequiredArgsConstructor```를 붙이면, ```final``` 키워드가 붙은 필드에 대해 컴파일 시점에 생성자에서 이를 대입하는 코드를 자동으로 생성해줌

- 정리
  - 최근에는 생성자를 딱 1개 두고, ```@Autowired```를 생략하는 방법을 주로 사용
  - 여기에 lombok의 ```@RequiredArgsConstructor```를 이용하면 더 간결한 코드 작성 가능



## 같은 타입의 빈이 2개 이상 조회되는 경우

- ```@Autowired```는 타입(Type)으로 조회함

  ```java
  @Autowired
  private DiscountPolicy discountpPolicy
  ```

  - 타입으로 조회하기 때문에 마치 ```ac.getBean(DiscountPolicy.class)```와 유사하게 동작(실제로는 더 많은 기능 제공)

  - 때문에 ```DiscountPolicy```의 하위 타입인 ```FixDiscountPolicy```와 ```RateDiscountPolicy```이 둘 다 스프링 빈으로 선언되면 ```NoUniqueBeanDefinition``` 에러 발생

    ```java
    @Component
    public class FixDiscountPolicy implements DiscountPolicy
    ```

    ```java
    @Component
    public class FixDiscountPolicy implements DiscountPolicy
    ```

- 이 때, 하위 타입으로 의존 관계를 주입할 수 있지만, 이는 DIP를 위배하고 코드의 유연성을 떨어뜨림

- 또한 이름만 다르고, 완전히 똑같은 타입의 스프링 빈이 2개 있을 때, 해결 불가

- 스프링 빈을 수동 등록해서 문제를 해결해도 되지만, 의존 관계 자동 주입에서 해결하는 여러 방법이 있음



### 해결법

- ```@Autowired``` 필드명 매칭

  - ```@Autowired```는 타입 매칭을 시도하고, 이 때 여러 빈이 조회되면 필드 이름, 파라미터 이름으로 빈 이름을 추가 매칭함

    ```java
    @Autowired
    private DiscountPolicy discountPolicy
    ```

    ```java
    @Autowired
    private DiscountPolicy rateDiscountPolicy
    ```

    - 필드명 매칭은 타입 매칭을 먼저시도하고, 그 결과 여러 빈이 있을 때 추가로 동작하는 기능



- ```@Qualifier``` 사용

  - ```Qualifier```는 추가 구분자를 붙여주는 방법

  - 추가적인 방법을 제공하는 것이지 빈 이름 자체를 변경하는 것은 아님

  - 주입할 때, ```@Qualifier```를 붙여주고 등록한 이름을 넣음

    ```java
    @Component
    @Qualifier("mainDiscountPolicy")
    public class RateDiscountPolicy implements DiscountPolicy
    ```

    ```java
    @Component
    @Qualifier("fixDiscountPolicy")
    public class FixDiscountPolicy implements DiscountPolicy
    ```

    ```java
    @Component
    public class OrderServiceImpl implements OrderService{
    
        private final MemberRepository memberRepository;
        private final DiscountPolicy discountPolicy;
    	
        @Autowired
        public OrderServiceImpl(MemberRepository memberRepository, @Qualifier("mainDiscountPolicy") DiscountPolicy discountPolicy) {
            this.memberRepository = memberRepository;
            this.discountPolicy = discountPolicy;
        }
        
        ...
    }
    ```

    			- ```@Qualifier```로 주입할 때, ```@Qualifier("mainDiscountPolicy")```를 못찾으면, ```"mainDiscountPolicy"```라는 이름의 스프링 빈을 추가로 찾음
       - 하지만, ```@Qualifier```는 ```@Qualifier```를 찾는 용도로만 사용하는게 좋음
         - 헷갈릴 요소를 만들지 말자



- ```@Primary``` 사용

  - ```@Primary```는 우선순위를 지정해줌

    ```java
    @Component
    @Primary
    public class RateDiscountPolicy implements DiscountPolicy
    ```

    ```java
    @Component
    public class FixDiscountPolicy implements DiscountPolicy
    ```



### ```@Primary```와 ```@Qualifier```의 활용

- 코드에서 자주 사용하는 메인 DB의 커넥션을 획득하는 스프링 빈A가 있고, 특별한 기능으로 가끔 사용하는 서브 DB의 커넥션을 획득하는 스프링 빈B가 있을 때, 빈A에는 ```@Primary```를 적용해서 조회하는 곳에서 ```@Qualifier``` 지정 없이 편하게 조회하고, 빈B에는 ```@Qualifier```를 지정해서 명시적으로 조회하면 코드가 깔끔해짐
  - 스프링 빈A에 ```@Qualifier```를 지정하는 것은 자유



### ```@Primary```와 ```@Qualifier```의 우선 순위

- ```@Primary```는 기본값처럼 동작하고, ```@Qualifier```는 매우 상세하게 동작함
- 스프링은 자동보다는 수동이, 넓은 범위의 선택권보다는 좁은 범위의 선택권이 우선 순위가 높음
- 따라서 ```@Primary``` 보다 ```@Qualifier```의 우선 순위가 높음



### Annotation 직접 만들기

- ```@Qualifier("mainDiscountPolicy")```와 같이 적으면, 컴파일시 타입 체크가 안됨

- 다음과 같이 직접 어노테이션을 만들 수 있음

  ```java
  @Target({ElementType.FIELD, ElementType.METHOD, ElementType.PARAMETER, ElementType.TYPE, ElementType.ANNOTATION_TYPE})
  @Retention(RetentionPolicy.RUNTIME)
  @Inherited
  @Documented
  @Qualifier("mainDiscountPolicy")
  public @interface MainDiscountPolicy {
  }
  ```

  ```java
  @Component
  @MainDiscountPolicy
  public class RateDiscountPolicy implements DiscountPolicy
  ```

  ```java
  @Component
  public class OrderServiceImpl implements OrderService{
  
      private final MemberRepository memberRepository;
      private final DiscountPolicy discountPolicy;
  
      @Autowired
      public OrderServiceImpl(MemberRepository memberRepository, @MainDiscountPolicy DiscountPolicy discountPolicy) {
          this.memberRepository = memberRepository;
          this.discountPolicy = discountPolicy;
      }
  
  	...
  }
  
  ```

- 자바에서 어노테이션에는 상속 개념이 없음
  - 어노테이션을 여러개 모아서 사용하는 기능은 스프링이 지원하는 기능



### 조회한 빈이 모두 필요할 때

- 의도적으로 해당 타입의 스프링 빈이 모두 필요한 경우도 있음

  - 할인 서비스를 제공하는데, 클라이언트가 할인의 종류(fix, rate)를 선택할 수 있는 경우

- 스프링을 사용하면 전략 패턴을 매우 쉽게 구현할 수 있음

  - Map 또는 List로 조회한 빈을 모두 받을 수 있음

    - 받은 빈들 중 동적으로 필요한 빈 선택 가능

    ```java
    public class AllBeanTest {
    
        @Test
        void findAllBean() {
            ApplicationContext ac = new AnnotationConfigApplicationContext(AutoAppConfig.class, DiscountService.class);
    
            DiscountService discountService = ac.getBean(DiscountService.class);
            Member member = new Member(1L, "userA", Grade.VIP);
            int discountPrice = discountService.discount(member, 10000, "fixDiscountPolicy");
    
            assertThat(discountService).isInstanceOf(DiscountService.class);
            assertThat(discountPrice).isEqualTo(1000);
    
            int rateDiscountPrice = discountService.discount(member, 20000, "rateDiscountPolicy");
            
            assertThat(discountService).isInstanceOf(DiscountService.class);
            assertThat(rateDiscountPrice).isEqualTo(2000);
        }
    
    
        static class DiscountService {
            private final Map<String, DiscountPolicy> policyMap;
            private final List<DiscountPolicy> policies;
    
            @Autowired
            public DiscountService(Map<String, DiscountPolicy> policyMap, List<DiscountPolicy> policies) {
                this.policyMap = policyMap;
                this.policies = policies;
                System.out.println("policyMap = " + policyMap);
                System.out.println("policies = " + policies);
            }
    
            public int discount(Member member, int price, String discountCode) {
                DiscountPolicy discountPolicy = policyMap.get(discountCode);
                return discountPolicy.discount(member, price);
            }
        }
    }
    ```

    - ```DiscountService```는 모든 ```DiscountPolicy```(fix, rate)를 주입 받음
    - ```discount()``` 메서드는 ```discountCode```로 넘어온 빈의 이름으로 ```policyMap```에서 해당 스프링 빈을 찾음



## 자동, 수동의 올바른 실무 운영 기준

- **편리한 자동 기능을 기본으로 사용하자**
  - 시간이 지날수록 점점 자동을 선호하는 추세
  - ```@Component```, ```@Controller```, ```@Service```, ```@Repository``` 등을 이용하여 일반적은 어플리케이션 로직을 자동으로 스캔할 수 있음
  - 스프링 부트는 컴포넌트 스캔을 기본으로 사용하며, 스프링 부트의 다양한 스프링 빈들도 조건이 맞으면 자동으로 등록되도록 설계됨
  - 설정 정보를 기반으로 어플리케이션을 구성하는 부분과, 실제 동작하는 부분을 명확하게 나누는 것이 이상적이지만, 개발자 입장에서 스프링 빈을 하나 등록할 때, ```@Component```만 넣어주면 끝나는 일을, ```@Configuration``` 설정 정보에 가서 ```@Bean```을 적고, 객체를 생성하고, 주입할 대상을 일일이 적는 과정은 번거로움
    - 관리할 빈이 많으면 설정 정보를 관리하는 것도 문제
  - 결정적으로 자동 빈 등록을 사용해도 OCP, DIP를 지킬 수 있음



- **수동 빈 등록을 사용하는 경우**

  - 어플리케이션은 크게 업무 로직과 기술 지원 로직으로 나눌 수 있음
    - 업무 로직 빈
      - 웹을 지원하는 컨트롤러, 핵심 비즈니스 로직이 있는 서비스, 데이터 계층의 로직을 처리하는 레포지토리
      - 보통 비즈니스 요구사항을 개발할 때 추가되거나 변경됨
      - 업무 로직은 숫자도 매우 많고, 한 번 개발하면, 컨트롤러, 서비스, 레포지토리처럼 어느정도 유사한 패턴이 있음
        - 이런 경우 자동 기능을 적극 사용하는 것이 편함
        - 문제가 발생해도 어떤 곳에서 문제가 발생했는지 명황하게 파악하기 쉬움
    - 기술 지원 빈
      - 기술적인 문제나 공통 관심사(AOP)를 처리할 때 주로 사용됨
      - 데이터 베이스 연결이나, 공통 로그 처리처럼 업무 로직을 지원하기 위한 하부 기술이나 공통 기술들
      - 기술 지원 로직은 업무 로직과 비교해서 수가 매우 적고, 보통 어플리케이션 전반에 걸쳐서 광범위하게 영향을 미침
        - 기술 지원 로직은 잘 적용되고 있는지 아닌지 조차 파악하기 힘듦
        - 이런 경우 가급적 수동 빈 등록을 사용해서 명확하게 드러내는 것이 좋음
        - 즉, 어플리케이션에 광범위하게 영향을 미치는 기술 지원 객체는 수동 빈으로 등록해서 설정 정보에 바로 나타나게 하는 것이 유지보수하기 편함

  - 비즈니스 로직 중에서 다형성을 적극 활용할 때

    - 앞서 살펴봤던, 조회한 빈이 모두 필요한 경우, 코드를 읽기 쉽게 하기 위해 수동으로 등록할 수 있음

      ```java
      public class AllBeanTest {
      
        	...
        
          static class DiscountService {
              private final Map<String, DiscountPolicy> policyMap;
              private final List<DiscountPolicy> policies;
      
              @Autowired
              public DiscountService(Map<String, DiscountPolicy> policyMap, List<DiscountPolicy> policies) {
                  this.policyMap = policyMap;
                  this.policies = policies;
                  System.out.println("policyMap = " + policyMap);
                  System.out.println("policies = " + policies);
              }
      
              ...
          }
      }
      ```

      - 위의 코드를 봤을 때, DiscountPolicy에 무엇이 들어올지 파악하기 쉽지 않음

      - 따라서 아래와 같이 설정 정보를 따로 관리하면, 한 눈에 파악하기 쉬움

        ```java
        @Configuration
        public class DiscountPolicyConfig {
          
        	@Bean
          public DiscountPolicy rateDiscountPolicy() {
            return new RateDiscountPolicy();
          }
          
          @Bean
          public DiscountPolicy fixDiscountPolicy() {
            return new FixDiscountPolicy();
          }
        }
        ```



- **스프링과 스프링 부트가 자동으로 등록하는 수 많은 빈들**
  - 이런 빈들은 스프링의 설계 의도대로 사용하는 것이 좋음
    - 스프링 부트의 경우 ```DataSource``` 같은 데이터 베이스 연결에 사용하는 기술 지원 로직까지 내부에서 자동으로 등록해주는데, 메뉴얼을 잘 참고해서 스프링 부트가 의도한대로 사용하면 됨
  - 반면, 스프링 부트가 아니라, 직접 기술 지원 객체를 스프링 빈으로 등록한다면 수동으로 등록해서 명확하게 드러내는 것이 좋음



### 정리

- 편리한 자동 기능을 기본으로 사용
- 직접 등록하는 기술 지원 객체는 수동 등록
- 다형성을 적극 활용하는 비즈니스 로직은 수동 등록을 고민



## 빈 생명주기 콜백

- 데이터 베이스 커넥션 풀이나, 네트워크 소켓처럼 어플리케이션 시작 시점에 필요한 연결을 미리 해두고 어플리케이션 종료 시점에 연결을 모두 종료하는 작업을 하려면, 객체의 초기화와 종료 작업이 필요함
- 스프링 빈은 간단하게 다음과 같은 라이프 사이클을 가짐
  - 생성자 주입을 제외하면, 객체 생성 -> 의존 관계 주입
- 스프링 빈은 객체를 생성하고 의존 관계 주입이 다 끝난 후에야 필요한 데이터를 사용할 수 잇는 준비가 완료됨
  - 따라서 초기화 작업은 의존 관계 주입이 모두 완료되고 난 다음에 호출해야 함
- 스프링은 의존 관계 주입이 완료되면, 스프링 빈에게 콜백 메서드를 통해서 초기화 시점을 알려주는 다양한 기능을 제공함
- 또한, 스프링 컨테이너가 종료되기 직전에 소멸 콜백을 줌



### 스프링 빈의 이벤트 라이프 사이클

1. 스프링 컨테이너 생성
2. 스프링 빈 생성 (생성자 주입의 경우 이 단계에서 의존 관계 주입이 일어남)
3. 의존 관계 주입
4. 초기화 콜백
   - 빈이 생성되고, 빈의 의존 관계 주입이 완료된 후 호출
5. 사용
6. 소멸전 콜백
   - 빈이 소멸되기 직전에 호출
7. 스프링 종료



### 참고: 객체의 생성과 초기화를 분리하자

- 생성자는 필수 정보를 파라미터로 받고, 메모리를 할당해서 객체를 생성하는 책임을 가짐
- 반면, 초기화는 이렇게 생성된 값들을 활용해서 외부 커넥션을 연결하는 등 무거운 동작을 수행함
- 따라서 생성자 안에서 무거운 초기화 작업을 한 번에 처리하는 것 보다, 객체를 생성하는 부분과 초기화 하는 부분을 명확하게 나누는 것이 유지 보수 관점에서 좋음



## 스프링의 빈 생명주기 콜백 방법

### 인터페이스 ```InitializingBean, DisposableBean```

- ```InitializingBean```은 ```afterPropertiesSet()``` 메서드로 초기화를 지원

- ```DisposableBean```은 ```destroy()``` 메서드로 소멸을 지원

  ```java
  public class NetworkClient implements InitializingBean, DisposableBean {
  
      private String url;
  
      public NetworkClient() {
          System.out.println("생성자 호출, url = " + url);
      }
  
      //서비스 시작시 호출
      public void connect() {
          System.out.println("connect: " + url);
      }
  
      public void call(String message) {
          System.out.println("call: "+url + " message = " + message);
      }
  
      //서비스 종료시 호출
      public void disconnect() {
          System.out.println("close: "+url);
      }
  
      public void setUrl(String url) {
          this.url = url;
      }
  
      @Override
      public void afterPropertiesSet() throws Exception {
          connect();
          call("초기화 연결 메세지");
      }
  
      @Override
      public void destroy() throws Exception {
          disconnect();
      }
  }
  
  ```

  

### 설정 정보에 초기화 메서드, 종료 메서드 지정

- 설정 정보에 다음과 같이 초기화, 종료 메서드를 지정할 수 있음

  ```java
  public class BeanLifeCycleTest {
  	...
      @Configuration
      static class LifeCycleConfig {
          
          @Bean(initMethod = "init", destroyMethod = "close")
          public NetworkClient networkClient() {
              NetworkClient networkClient =  new NetworkClient();
              networkClient.setUrl("http://hello-spring.dev");
              return networkClient;
          }
      }
  }
  ```

  ```java
  public class NetworkClient {
  	...
      public void init() {
          System.out.println("NetworkClient.init");
          connect();
          call("초기화 연결 메세지");
      }
  
      public void close() {
          System.out.println("NetworkClient.close");
          disconnect();
      }
  }
  ```

- 이 방식을 이용하면, 메서드 이름을 자유롭게 지을 수 있음

- 스프링 빈이 스프링 코드에 의존하지 않음

  - ```NetworkClient```에 스프링과 관련한 코드가 존재하지 않음

- 코드가 아니라, 설정 정보를 이용하므로 코드를 고칠 수 없는 외부 라이브러리에도 초기화, 종료 메서드 적용 가능

- 종료 메서드 추론

  - ```@Bean```의 ```destroyMethod``` 속성에는 아주 특별한 기능이 있음

  - 외부 라이브러리는 대부분 ```close, shutdown```이라는 이름의 종료 메서드 사용

  - ```@Bean```의 ```destroyMethod```는 기본값이 ```(inferred)```(추론)로 등록되어있음

    - 이 추론 기능은 ```close, shutdown```라는 이름의 메서드를 자동으로 호출

    - 따라서 직접 스프링 빈으로 등록하면, 종료 메서드를 따로 적어주지 않아도 잘 동작함
    - 추론 기능은 ```destoryMethod=""```와 같이 작성하면 제거됨



### ```@PostConstruct, @PreDestroy``` 어노테이션 지원

```java
public class BeanLifeCycleTest {
	...
    @Configuration
    static class LifeCycleConfig {
        @Bean
        public NetworkClient networkClient() {
            NetworkClient networkClient =  new NetworkClient();
            networkClient.setUrl("http://hello-spring.dev");
            return networkClient;
        }
    }
}
```

```java
import javax.annotation.PostConstruct;
import javax.annotation.PreDestroy;

public class NetworkClient {
	...
    @PostConstruct
    public void init() {
        System.out.println("NetworkClient.init");
        connect();
        call("초기화 연결 메세지");
    }

    @PreDestroy
    public void close() {
        System.out.println("NetworkClient.close");
        disconnect();
    }
}
```

- 권장되는 방법
  - 어노테이션 하나만 붙이면 되므로 편리
- 임포트한 패키지를 보면, ```javax.annotation```임
  - 스프링에 종속된 기술이 아니라, JSR-250이라는 자바 표준이기 때문에 스프링이 아닌 다른 컨테이너에서도 잘 동작
- 컴포넌트 스캔과 잘어울림
- 유일한 단점은 외부 라이브러리에는 적용할 수 없다는 점



### 정리

- ```@PostConstruct, @PreDestroy``` 어노테이션을 사용하자
- 코드를 고칠 수 없는 외부 라이브러리를 초기화, 종료해야 한다면, ```@Bean```의 ```initMethod, destroyMethod```를 사용하자



## 빈 스코프

- 빈이 존재할 수 있는 범위
- 다음과 같이 다양한 스코프를 지원
  - 싱글톤
    - 기본 스코프
    - 스프링 컨테이너의 시작과 종료까지 유지되는 가장 넓은 범위의 스코프
  - 프로토타입
    - 스프링 컨테이너는 프로토타입 빈의 생성과 의존 관계 주입까지만 관여하고 더는 관리하지 않는 매우 짧은  범위의 스코프
    - 종료 메서드 호출이 안됨
  - 웹 관련 스코프
    - request
      - 웹 요청이 들어오고, 나갈 때까지 유지되는 스코프
    - session
      - 웹 세션이 생성되고 종료될 때까지 유지되는 스코프
    - application
      - 웹의 서블릿 컨텍스와 같은 범위로 유지되는 스코프



### 프로토타입 스코프

- **싱글톤 스코프의 빈**을 조회하면, 스프링 컨테이너는 **항상 같은 인스턴스의 스프링 빈을 반환**

  ```java
  public class SingletonTest {
  
      @Test
      void singletonBeanFind() {
          AnnotationConfigApplicationContext ac = new AnnotationConfigApplicationContext(SingletonBean.class);
  
          SingletonBean singletonBean1 = ac.getBean(SingletonBean.class);
          SingletonBean singletonBean2 = ac.getBean(SingletonBean.class);
  
          assertThat(singletonBean1).isSameAs(singletonBean2);
          
          ac.close();
      }
  
      @Scope("singleton")
      static class SingletonBean {
          @PostConstruct
          public void init() {
              System.out.println("SingletonBean.init");
          }
  
          @PreDestroy
          public void destroy() {
              System.out.println("SingletonBean.destroy");
          }
      }
  }
  ```

- 반면, **프로토타입 스코프**를 조회하면, 스프링 컨테이너는 항상 **새로운 인스턴스를 생성해서 반환**

  ```java
  public class PrototypeTest {
  
      @Test
      void prototypeBeanFind() {
          AnnotationConfigApplicationContext ac = new AnnotationConfigApplicationContext(PrototypeBean.class);
  
          System.out.println("find prototypeBean1");
          PrototypeBean prototypeBean1 = ac.getBean(PrototypeBean.class);
          System.out.println("find prototypeBean2");
          PrototypeBean prototypeBean2 = ac.getBean(PrototypeBean.class);
          
          System.out.println("prototypeBean1 = " + prototypeBean1);
          System.out.println("prototypeBean2 = " + prototypeBean2);
  
          assertThat(prototypeBean1).isNotSameAs(prototypeBean2);
  
          ac.close();
      }
  
      @Scope("prototype")
      static class PrototypeBean {
          @PostConstruct
          public void init() {
              System.out.println("PrototypeBean.init");
          }
  
          @PreDestroy
          public void destroy() {
              System.out.println("PrototypeBean.destroy");
          }
      }
  }
  ```

  - 핵심은 스프링 컨테이너는 프로토타입 빈을 생성하고, 의존 관계 주입, 초기화까지만 처리
  - 클라이언트에 빈을 반환한 이후에 스프링 컨테이너는 프로토타입 빈을 관리하지 않음
  - 프로토타입 빈을 관리할 책임은 프로토타입을 주입받은 클라이언트에 있음
    - 따라서 ```@PreDestroy``` 같은 종료 메서드가 호출되지 않음
    - 종료 메서드에 대한 호출도 클라이언트가 직접 해야함



### 프로토타입 스코프 - 싱글톤 빈과 함께 사용할 때의 문제점

- 스프링 컨테이너에 프로토타입 스코프의 빈을 요청하면, 항상 새로운 객체 인스턴스를 생성해서 반환함

  ```java
  public class SingletonWithPrototypeTest1 {
  
      @Test
      void prototypeFind() {
          AnnotationConfigApplicationContext ac = new AnnotationConfigApplicationContext(PrototypeBean.class);
          PrototypeBean prototypeBean1 = ac.getBean(PrototypeBean.class);
          prototypeBean1.addCount();
          assertThat(prototypeBean1.getCount()).isEqualTo(1);
  
          PrototypeBean prototypeBean2 = ac.getBean(PrototypeBean.class);
          prototypeBean2.addCount();
          assertThat(prototypeBean2.getCount()).isEqualTo(1);
  
      }
  
      @Scope("prototype")
      static class PrototypeBean {
          private int count = 0;
  
          public void addCount() {
              count++;
          }
  
          public int getCount() {
              return count;
          }
  
          @PostConstruct
          public void init() {
              System.out.println("PrototypeBean.init" + this);
          }
  
          @PreDestroy
          public void destroy() {
              System.out.println("PrototypeBean.destroy");
          }
      }
  }
  ```

- 그러나 싱글톤 빈과 함께 사용할 때는 의도한대로 잘 동작하지 않으므로 주의해야 함

  ```java
  public class SingletonWithPrototypeTest1 {
  
      @Test
      void singletonClientUsePrototype() {
          AnnotationConfigApplicationContext ac = new AnnotationConfigApplicationContext(ClientBean.class, PrototypeBean.class);
  
          ClientBean clientBean1 = ac.getBean(ClientBean.class);
          int count1 = clientBean1.logic();
          assertThat(count1).isEqualTo(1);
  
          ClientBean clientBean2 = ac.getBean(ClientBean.class);
          int count2 = clientBean2.logic();
          assertThat(count2).isEqualTo(2);
      }
  
      @Scope("singleton")
      static class ClientBean {
          private final PrototypeBean prototypeBean; // 생성 시점에 주입되어 유지됨
  
          @Autowired
          public ClientBean(PrototypeBean prototypeBean) {
              this.prototypeBean = prototypeBean;
          }
  
          public int logic() {
              prototypeBean.addCount();
              int count = prototypeBean.getCount();
              return count;
          }
      }
  
  	...
  }
  ```

  - ```clientBean``` 내부의 ```prototypeBean```은 생성 시점에 주입된 빈임
    - 즉, 주입 시점에 스프링 컨테이너에 요청해서 프로토타입 빈이 새로 생성된 것이지, 사용할 때 마다 새로 생성되는 것이 아님
    - 따라서 ```clientBean2```에서 ```logic()```을 호출하면, 이미 생성되어있는 프로토타입 빈의 ```count```가 증가됨

- 스프링은 일반적으로 싱글톤 빈을 사용하므로, 싱글톤 빈이 프로토타입 빈을 사용하게 됨

  - 싱글톤 빈은 생성 시점에만 의존 관계 주입을 받기 때문에, 프로토타입 빈이 새로 생성되기는 하지만, 생성된 프로토타입 빈이 싱글톤 빈과 함께 계속 유지되는 것이 문제임
  - 프로토타입 빈의 사용 의도는 위와 같이 주입 시점에만 프로토타입 빈을 새로 생성하는 것이 아니라, 사용할 때마다 새로 생성하는 것임



### 프로토타입 스코프를 싱글톤 빈과 함께 사용할 때, ```Provider```를 사용하여 문제 해결

- 무식한 방법으로, 싱글톤 빈이 프로토타입 빈을 사용할 때 마다, 스프링 컨테이너에 새로 요청할 수 있음

  ```java
      static class ClientBean {
  
          @Autowired
          private ApplicationContext ac;
  
  
          public int logic() {
            	PrototypeBean prototypeBean = ac.getBean(PrototypeBean.class);
              prototypeBean.addCount();
              int count = prototypeBean.getCount();
              return count;
          }
      }
  ```

  - 위의 코드를 실행해보면, ```ac.getBean(PrototypeBean.class)```를 통해 항상 새로운 프로토타입 빈이 생성됨
  - 의존 관계를 외부에서 주입 받는게 아니라, 이렇게 직접 필요한 의존 관계를 찾는 것을 DL(Dependency Lookup, 의존 관계 조회)이라 함
  - 그런데, ```ApplicationContext``` 전체를 주입받으면, 스프링 컨테이너에 종속적인 코드가 되고 단위 테스트도 어려워짐
  - 스프링 컨테이너 대신, 딱 DL 정도의 기능만 제공하는 무언가가 필요함

- ```ObjectFactory, ObjectProvider```

  - ```ObjectProvider```는 ```ObjectFactory```에 기능이 추가된 것

  - 지정한 빈을 컨테이너 대신 찾아주는 DL 기능을 제공함

    ```java
    @Scope("singleton")
        static class ClientBean {
    
            @Autowired
            private ObjectProvider<PrototypeBean> prototypeBeanProvider;
    
            public int logic() {
                PrototypeBean prototypeBean = prototypeBeanProvider.getObject();
                prototypeBean.addCount();
                int count = prototypeBean.getCount();
                return count;
            }
        }
    ```

    - ```prototypeBeanProvider.getObject()```를 통해서 항상 새로운 프로토타입 빈이 생성됨
    - 스프링이 제공하는 기능을 사용하는 것이지만, 기능이 단순하여 단위 테스트를 만들어나 mock 코드를 만들기 쉬움
    - ```ObjectProvider```는 딱 필요한 DL 정도의 기능만 제공
    - ```ObjectProvider```는 스프링이 자동으로 만들어서 등록함

  - JSR-330 ```Provider```

    - ```java.inject.Provider```라는 JSR-330 자바 표준을 사용할 수도 있음

    - build.gradle에 라이브러리 추가

      ```gradle
      dependencies {
      	...
      	implementation 'javax.inject:javax.inject:1'
      	...
      }
      
      ```

    - ```ObjectProvider```와 마찬가지로 DL 기능 제공

      ```java
      @Scope("singleton")
          static class ClientBean {
      
              @Autowired
              private Provider<PrototypeBean> prototypeBeanProvider;
      
              public int logic() {
                  PrototypeBean prototypeBean = prototypeBeanProvider.get();
                  prototypeBean.addCount();
                  int count = prototypeBean.getCount();
                  return count;
              }
          }
      ```

      - ```prototypeBeanProvider.get()```를 통해 항상 새로운 프로토타입 빈 생성
      - 자바 표준이고, 기능이 단순하여 단위 테스트를 만들거나 mock 코드 만들기 쉬움
      - 딱 필요한 DL 정도의 기능만 제공
        - ```get()``` 메서드 하나로 기능이 매우 단순

    - 별도읭 라이브러리를 추가해야하므로 번거로움

    - 자바 표준이므로 스프링이 아닌 다른 컨테이너에서도 사용 가능



### 프로토타입 빈 정리

- 프로토타입 빈은 매번 사용할 때마다 의존 관계 주입이 완료된 새로운 객체가 필요하면 사용
- 그런데, 실무에서 웹 어플리케이션을 개발해보면, 싱글톤 빈으로 대부분의 문제를 해결할 수 있기 때문에 프로토타입 빈을 직접적으로 사용하는 경우는 매우 드묾
- ```ObjectProvider```, JSR303 ```Provider```는 프로토타입 뿐만 아니라 DL이 필요한 경우에 언제든지 사용 가능
- 스프링이 제공하는 ```@Lookup``` 어노테이션을 사용하는 방법도 있지만, 고려할 것이 많아 생략





## 웹 스코프

- 웹 스코프는 웹 환경에서만 동작함
- 프로토타입과는 다르게 스프링이 해당 스코프의 종료 시점까지 관리함
  - 따라서 종료 메서드가 호출됨
- 웹 스코프의 종류
  - request
    - HTTP 요청 하나가 들어오고, 나갈 때까지 유지되는 스코프
    - 각각의 HTTP 요청마다 별도의 빈 인스턴스가 생성되고 관리됨
  - session
    - HTTP Session과 동일한 생명주기를 가지는 스코프
  - application
    - 블릿 컨텍스트(```ServletContext```)와 동일한 생명주기를 가지는 스코프
  - websocket
    - 웹 소켓과 동일한 생명주기를 가지는 스코프



### request 스코프 예제

- 웹 스코프는 웹 환경에서만 동작하므로, build.gradle에 라이브러리 추가

  ```gradle
  dependencies {
  	...
  	implementation 'org.springframework.boot:spring-boot-starter-web'
  	...
  }
  ```

  - 참고
    - ```spring-boot-starter-web``` 라이브러리를 추가하면, 스프링 부트는 내장 톰켓 서버를 활용해서 웹 서버와 스프링을 함께 실행시킴
    - 스프링 부트는 웹 라이브러리가 없으면 ```AnnotationConfigApplicationContext```를 기반으로 어플리케이션을 구동
    - 웹 라이브러리가 추가되면, 웹과 관련된 추가 설정과 환경들이 필요하므로 ```AnnotationConfigServletWebServerApplicationContext```를 기반으로 어플리케이션을 구동

- 동시에 HTTP 요청이 오면, 정확히 어떤 요청이 남긴 로그인지 구분하기 어려움

  - 이럴때 request 스코프를 이용함

  - UUID를 사용해서 HTTP 요청을 구분하고, requestURL 정보도 추가로 넣어서 어떤 URL을 요청해서 남은 로그인지 확인해보자

    ```java
    @Component
    @Scope(value="request")
    public class MyLogger {
    
        private String uuid;
        private String requestURL;
    
        public void setRequestURL(String requestURL) {
            this.requestURL = requestURL;
        }
    
        public void log(String message) {
            System.out.println("[" + uuid + "] " + "[" + requestURL + "] " + message);
        }
    
        @PostConstruct
        public void init() {
            uuid = UUID.randomUUID().toString();
            System.out.println("[" + uuid + "] " + "[" + requestURL + "] request scope init: " + this);
        }
    
        @PreDestroy
        public void close() {
            System.out.println("[" + uuid + "] " + "[" + requestURL + "] request scope close: " + this);
        }
    }
    ```

    - request 빈은 HTTP 요청 당 하나씩 생성되고, HTTP 요청이 끝나는 시점에 소멸

    - 빈이 생성되는 시점에 ```@PostConstruct``` 초기화 메서드를 이용해서 uuid를 생성하고 저장

      - 이 빈은 HTTP 요청 당 하나씩 생성되므로, uuid를 저장해두면 다른 HTTP 요청과 구분 가능

    - 빈이 소멸되는 시점에 ```@PreDestroy```를 사용해서 종료 메세지 남김

    - ```requestURL```은 빈이 생성되는 시점에는 알 수 없으므로, 외부에서 ```setter```로 입력 받음

      

    ```java
    @Controller
    @RequiredArgsConstructor
    public class LogDemoController {
    
        private final LogDemoService logDemoService;
        private final MyLogger myLogger;
    
        @RequestMapping("log-demo")
        @ResponseBody
        public String logDemo(HttpServletRequest request) {
            String requestURL = request.getRequestURL().toString();
            myLogger.setRequestURL(requestURL);
    
            myLogger.log("controller test");
            logDemoService.logic("testId");
            return "OK";
        }
    }
    ```

    - 로거의 작동을 확인하는 컨트롤러

    - ```HttpServletRequest```를 통해 요청 URL을 받음

      - ```requestURL = http://localhost:8080/log-demo```
      - 이 값을 myLogger에 저장

    - 컨트롤러에서 ```controller test```라는 로그를 남김

      

    ```java
    @Service
    @RequiredArgsConstructor
    public class LogDemoService {
    
        private final MyLogger myLogger;
    
        public void logic(String id) {
            myLogger.log("service id = " + id);
        }
    }
    ```

    - 비즈니스 로직이 있는 서비스 계층
    - request 스코프를 사용하지 않고 파라미터로 모든 정보를 서비스 계층에 넘기면 지저분함
      - 또한, ```requestURL``` 처럼 웹과 관련된 정보가 웹과 관련없는 서비스 계층까지 넘어감
      - 웹과 관련된 부분은 컨트롤러까지만 사용해야 함
        - 서비스 계층은 웹 기술에 종속되지 않고, 가급적 순수하게 유지하는 것이 유지보수 관점에서 좋기 때문
    - ```MyLogger``` 덕분에 모든 정보를 파라미터로 넘기지 않고, ```MyLogger```의 멤버변수에 저장해서 코드와 계층을 깔끔하게 유지할 수 있음
    - 위와 같이 ```MyLogger, LogDemoController, LogDemoService```를 작성하고 스프링 어플리케이션을 실행시키면 오류 발생
      - 스프링 어플리케이션을 실행하는 시점에 싱글톤 빈은 생성해서 주입이 가능하지만, request 스코프 빈인 ```MyLogger```는 생성되지 않기 때문
      - ```MyLogger```는 HTTP 요청이 와야지 생성할 수 있음



### request 스코프와 Provider

```java
@Controller
@RequiredArgsConstructor
public class LogDemoController {

    private final LogDemoService logDemoService;
    private final ObjectProvider<MyLogger> myLoggerProvider;

    @RequestMapping("log-demo")
    @ResponseBody
    public String logDemo(HttpServletRequest request) {
        String requestURL = request.getRequestURL().toString();
        MyLogger myLogger = myLoggerProvider.getObject();
        myLogger.setRequestURL(requestURL);

        myLogger.log("controller test");
        logDemoService.logic("testId");
        return "OK";
    }
}
```

```java
@Service
@RequiredArgsConstructor
public class LogDemoService {

    private final ObjectProvider<MyLogger> myLoggerProvider;

    public void logic(String id) {
        MyLogger myLogger = myLoggerProvider.getObject();
        myLogger.log("service id = " + id);
    }
}
```

- ```ObjectProvider```를 통해 ```ObjectProvider.getObject()```를 호출하는 시점까지 request 스코프 빈의 생성을 지연할 수 있음
  - ```ObjectProvider.getObject()```를 호출하는 시점에는 HTTP 요청이 진행중이므로 request 스코프 빈의 생성이 정상 처리됨
  - ```ObjectProvider.getObject()```를 ```LogDemoController```와 ```LogDemoService```에서 각각 한 번씩 따로 호출해도 같은 HTTP 요청이면, 같은 스프링 빈이 반환됨



### request 스코프와 프록시

```java
@Component
@Scope(value="request", proxyMode = ScopedProxyMode.TARGET_CLASS)
public class MyLogger {
	...
}
```

- ```@Scope```에 ```proxyMode = ScopedProxyMode.TARGET_CLASS``` 옵션을 추가
  - 적용 대상이 인터페이스이면 ```TARGET_CLASS```
  - 적용 대상이 인터페이스이면 ```INTERFACES```
  - 이 옵션을 추가하면, ```MyLogger```의 가짜 프록시 클래스를 만들어두고, HTTP request와 상관 없이 가짜 프록시 클래스를 다른 빈에 미리 주입해둠
- 스프링 컨테이너는 CGLIB이라는 바이트 코드를 조작하는 라이브러리를 이용해서, ```MyLogger```를 상속받은 가짜 프록시 객체를 생성
  - 출력해보면, ```MyLogger$$EnhancerBySpringCGLIB```이라는 클래스로 만들어진 객체가 대신 등록되어 있음
  - ```ac.getBean("myLogger", MyLogger.class)```로 조회해도 프록시 객체가 조회됨
  - 의존 관계 주입도 이 가짜 프록시 객체가 주입됨
- 가짜 프록시 객체에는 요청이 들어오면 그때 내부에서 진짜 빈을 요청하는 위임 로직이 들어있음
  - 가짜 프록시 객체는 진짜 ```myLogger```를 찾는 방법을 알고 있음
  - 클라이언트가 ```myLogger.logic()```을 호출하면, 사실은 가짜 프록시 객체의 메서드를 호출
  - 가짜 프록시 객체는 request 스코프의 진짜 ```myLogger.logic()```을 호출
  - 가짜 프록시 객체는 원본 클래스를 상속 받았기 때문에, 이 객체를 사용하는 클라이언트 입장에서는 원본인지 아닌지 상관없이 동일하게 사용가능
    - 다형성
  - 가짜 프록시 객체는 실제 request 스코프와는 관계없음
    - 내부에 단순한 위임 로직만 존재
    - 싱글톤 처럼 동작
- 프록시 객체 덕분에 클라이언트는 마치 싱글톤 빈을 사용하듯이 편리하게 request 스코프를 사용할 수 있음
- Provider든, 프록시든 핵심 아이디어는 진짜 객체 조회를 꼭 필요한 시점까지 지연처리 한다는 점
- 어노테이션 설정 변경만드로 원본 객체를 프록시 객체로 대체할 수 있음
  - 다형성과 DI 컨테이너가 가진 큰 장점
    - 클라이언트 코드를 전혀 손댈필요 없음
  - 스프링의 AOP도 비슷한 원리
- 웹 스코프가 아니어도 프록시는 사용할 수 있음





​	
