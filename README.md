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

    - MemberService가 인터페이스인 MemberRepository의 save 메서드를 호출

    - MemberRepository의 구현체인 MemoryMemberRepository와, JdbcMemberRepository 모두 사용 가능

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

       - MemberService 클라이언트가 구현 클래스를 직접 선택
       - 구현 객체를 변경하려면 클라이언트 코드를 변경해야 함
       - 분명 다형성을 사용했지만, OCP 원칙을 지킬 수 없음
       - 이 문제를 어덯게 해결할까?
         - 객체를 생성하고, 연관관계를 맺어주는 별도의 조립, 설정자가 필요
         - 이것이 바로 스프링

  3. LSP (리스코프 치완 원칙)

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

     - 그런데 OCP에서 설명한 MemberService는 인터페이스에 의존하지만, 동시에 구현 클래스에도 의존함

       - MemberService 클라이언트가 구현 클래스를 직접 선택

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









