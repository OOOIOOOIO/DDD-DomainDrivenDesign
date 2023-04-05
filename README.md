# DDD-DomainDrivenDesign
[Book]도메인 주도 개발 시작하기(DDD 핵심 개념 정리부터 구현까지), 최범균

<br>

# CH 01 : 도메인 모델 시작하기

## 1.2 : 도메인 전문가와 개발자 간 지식 공유
- 개발자는 요구사항을 분석하고 설계하여 코드를 작성하며 테스트 및 배포를 실행한다. 이 과정에서 요구사항은 첫 단추와 같다.
- 요구사항을 제대로 이해하지 않으면 쓸모없거나 유용함이 떨어지는 시스템을 만들기 때문이다.

<br>

## 1.3 : 도메인 모델
- 도메인 모델은 특정 도메인을 개념적으로 표현한 것이다.
- 도메인을 이해하려면 도메인이 제공하는 기능과 도메인의 주요 데이터 구성을 파악해야 한다. 이를 가장 잘 보여줄 수 있는 모델이 바로 객체 모델이다.
- 객체 모델 외에도 상태 다이어그램, 클래스 다이어그램 등 UML 표기법을 사용하여 표현할 수도 있다.

![UML 화살표](img.png)
![화살표 설명](img_1.png)

<br>

## 1.4 : 도메인 모델 패턴
- 일반적인 애플리케이션 아키텍쳐는 Presentation, Application, Domain, Infrastructure 이렇게 4가지 영역으로 구성된다.
  - Presentation(사용자 인터페이스 또는 표현) : 사용자의 요청을 처리하고 사용자에게 정보를 보여준다. 여기서 사용자는 소프트웨어를 사용하는 사람뿐만 아니라 외부 시스템일 수도 있다.
  - Application(응용) : 상용자가 요청한 기능을 실행한다. 업무 로직을 직접 구현하지 않으며 도메인 계층을 조합해서 기능을 실행한다.
  - Domain : 시스템이 제공할도메인 규칙을 구현한다.
  - Infrastructure : 데이터베이스나 메시징 시스템과 같은 외부 시스템과의 연동을 처리한다.<br>

- 마틴 파울러의 "엔터프라이즈 애플리케이션 아키텍처 패턴" 책의 도메인 모델 패턴
  - 이 책의 도메인 모델은 아키텍쳐 상의 도메인 계층을 객체 지향 기법으로 구현하는 패턴을 말한다.
  - 도메인 모델에서 중요한 점은 도메인과 관련된 중요 업무 규칙을 도메인 모델에서 구현한다는 점이다.
  - 핵심 규칙을 구현한 코드는 도메인 모델에만 위치하기 때문에 규칙이 바뀌거나 규칙을 확장해야 할 때 다른 코드에 영향을 덜 주고 변경 내역을 모델에 반영할 수 있게 된다.

<br>

## 1.5 : 도메인 모델 도출
- 아무리 뛰어난 개발자라도 도메인에 대한 이해 없이 코딩을 시작할 수 없다. 기획서, 유스케이스, 사용자 스토리와 같은 요구사항과 관련자와의 대호를 통해 도메인을 이해하고 이리ㅡㄹ 바탕으로 도메인 모델 초안을 만들어야 비로소 코드를 작성할 수 있다.
- 어떤 툴을 사용하든 도메인에 대한 초기 모델이 필요하다
- 도메인을 모델링할 때 기본이 되는 작업은 모델을 구성하는 핵심 구성요소, 규칙, 기능을 찾는 것이다. 이 과정은 요구사항에서 출발한다.
- 요구사항을 토대로 명명 규칙, 상태, 제약 규칙, 기능 등을 도출하여 코드에 반영한다.

> 문서화 <br>
문서화를 하는 주된 이유는 지식을 공유하기 위함이다. 실제 구현은 코드에 있으므로 코드를 보면 다 알 수 있지만 코드는 상세한 모든 내용을 다루고 있기 때문에 코드를 이용해서 전체 소프트웨어를 분석하려면 많은 시간을 투자해 야 한다.전반적인 기능 목록이나 모듈 구조, 빌드 과정은 코드를 보고 직접 이해하는 것보다 상위 수준에서 정리한 문서를 참조하는 것이 소프트웨어 전반을 빠르게 이해하는 데 도움이 된다. 전체 구조를 이해하고 더 깊게 이해할 필 요가 있는 부분을 코드로 분석해 나가면 된다.
코드를 보면서 도메인을 깊게 이해하게 되므로 코드 자체도 문서화의 대상이 된다. 도메인 지식이 잘 묻어나도록 코 드를 작성하지 않으면 코드의 동작 과정은 해석할 수 있어도 도메인 관점에서 왜 코드를 그렇게 작성했는지 이해하 는 데는 도움이 되지 않는다. 단순히 코드를 보기 좋게 작성하는 것뿐만 아니라 도메인 관점에서 코드가 도메인을 잘 표현해야 비로소 코드의 가독성이 높아지고 문서로서 코드가 의미를 갖는다.

<br>

## 1.6 : 엔티티와 밸류
- 도출한 모델은 크게 엔티티(Entity)와 밸류(Value)로 구분할 수 있다.
- 엔티티(Entity)
  - 엔티티의 가장 큰 특징은 식별자를 가진다는 것이다.
  - 엔티티의 식별자는 바뀌지 않는다. 엔티티를 생성하고 속성을 바꾸고 삭제할 때까지 식별자는 유지된다.
  - 엔티티의 식별자는 바뀌지 않고 고유하기 때문에 두 엔티티 객체의 식별자가 같으면 두 엔티티는 같다고 판단할 수 있다. 엔티티를 구현한 클래스는 식별자를 이용해서 equals(), hashCode() 메서드를 구현할 수 있다.
- 엔티티의 식별자 생성
  - 특정 규칙에 따라 생성
    - 주문번호, 운송자번호, 카드번호와 같은 식별자는 특정 규칙에 따라 생성한다. 흔히 현재 시간과 다른 값을 조합하여 사용한다. 
  - UUID나 Nano ID와 같은 고유 식별자 생성기 사용
  - 값을 직접 입력
    - 회원의 아이디나 이메일과 같은 식별자는 값을 직접 입력한다. 
  - 일련번호 사용(시퀀스나 DB의 자동 증가 컬럼 사용)
    - 자동증가 컬럼은 DB 테이블에 데이터를 삽입해야 비로소 값을 알 수 있기 때문에 테이블에 데이터를 추가하기 전까지 식별자를 알 수 없다.
    - 이는 엔티티 객체를 생성할 때 식별자를 전달할 수 없음을 의미한다.
    - 하지만 리포지터리(repository)에서 DB가 생성한 식별자를 구해서 엔티티 객체에 반영하기 때문에 크게 신경쓰지 않아도 된다.
- 밸류 타입
   - 밸류 타입은 개념적으로 완전한 하나를 표현할 때 사용한다. 밸류 타입을 사용하면 개념적으로 완전한 하나를 잘 표현할 수 있다.
   - 밸류 타입을 따로 사용하는 경우 밸류 타입을 위한 기능을 추가할 수도 있다.
   - 밸류 객체의 데이터를 변경할 때는 기존 데이터를 변경하기보다는 변경한 데이터를 갖는 새로운 밸류 객체를 생성하는 방식을 선호한다.
   - 데이터의 변경 기능을 제공하지 않는 타입을 불변(immutable)이라고 표현하는데 밸류 타입을 불변으로 구현하면 좋다. 가장 큰 이유는 안전한 코드를 작성할 수 있다는 것이다.
   - 두 밸류 객체를 비교할 때는 equals() 메소드를 이용해 모든 속성이 같은지 비교한다.
- 엔티티 식별자와 밸류 타입
  - 식별자는 단순한 문자열이 많은데, 단순한 문자열이 아니라 도메인에서 특별한 의미를 지니는 밸류 타입을 사용해 그 의미가 잘 드러나도록 할 수 있다.
- Setter 사용
  - Setter를 사용하게 되면 도메인 객체가 불완전한 상태로 사용된다. 
  - 이를 막기 위해 생성 시점에 필요한 것을 전달해 주어야 한다. 즉, 생성자를 통해 필요한 데이터를 모두 받자.
  - 불변 밸류 타입을 사용하면 자연스럽게 밸류 타입에 set 메서드를 구현하지 않게 된다.

<br>

## 1.7 : 도메인 용어와 유비쿼터스 언어
- 도메인 용어를 최대한 반영하면 코드를 도메인 용어로 해석하거나 도메인 용어를 코드로 해석하는 과정이 줄어든다.
- 코드의 가독성을 높여서 코드를 분석하고 이해하는 시간을 줄여준다.
- 최대한 도메인 용어를 사용해서 도메인 규칙을 코드로 ㅈ가성하게 되므로(의미를 변환하는 과정에서 발생하는) 버그도 줄어든다.
- 에릭 에반스는 도메인 주도 설ㄱ계에서 언어의 중요함을 강조하기 위해 유비쿼터스 언어(ubiquitous language)라는 용어를 사용했다.
  - 해당 도메인 개발과 관련된 공통의 언어를 만들어 소통 과정에서 발생하는 용어의 모호함을 줄일 수 있고 개발자는 도메인과 코드 사이에서 불필요한 해석 과정을 줄일 수 있다.
  - 도메인 용어는 좋은 코드를 만드는 데 매우 중요한 요소이지만 대부분 영어로 되어 있다. 
  - 각 단어의 뉘앙스나 미세한 차이를 이해하고 알맞은 단어를 사용하기 위해 영어 공부를 꼭 해야 할 것이다.

<br>
<hr>
<br>

# CH 02 : 아키텍처 개요

## 2.1 : 네 개의 영역
- 표현, 응용, 도메인, 인프라스트럭처는 아키텍처를 설계할 때 출현하는 전형적인 네 가지 영역이다.
  - 표현(UI 영역) 
    - 사용자의 요청을 받아 응용 영역에 전달하고 응용 영역의 처리 결과를 다시 사용자에게 보여주는 역할을 한다. 웹 애플리케이션의 스프링 MVC 프레임워크가 표현 영역을 위한 기술에 해당한다.
    - 웹 애플리켕션의 표현 영역은 HTTP 요청을 응용 영역이 필요로 하는 형식으로 변환해서 응용 영역에 전달하고 응용 영역의 응답을 HTTP 응답으로 변환하여 전송한다.
    - 표현 영역을 통해 사용자의 요청을 전달받는 응용 영역은 시스템이 사용자에게 제공해야 할 기능을 구현한다.
  - 응용 영역
    - 기능을 구현하기 위해 도메인 영역의 도메인 모델을 사용한다.
    - 응용 서비스는 로직을 직접 수행하기보다는 도메인 모델에 로직 수행을 위임한다.
  - 도메인 영역
    - 도메인 모델을 구현한다.
    - 도메인 모델은 도메인의 핵심 로직을 구현한다.
  - 인프라스트럭처
    - 구현 기술에 대한 것을 다룬다.
    - RDBMS 연동을 처리하고 메세징 큐에 메시지를 전송하거나 수신하는 기능을 구현한다.
    - 몽고DB나 레디스와 데이터의 연동을 처리한다.
    - SMTP를 이용한 메일 발송 기능을 구현하거나 HTTP 클라이언트를 이용해서 REST API를 호출하는 것도 처리한다.

<br>

## 2.2 : 계층 구조 아키텍처
- 네 영역을 구성할 때 많이 사용하는 아키텍쳐는 계층 구조이다.
- 계층구조는 그 특성상 상위계층(표현)에서 하위 계층(인프라스트럭처)으로의 의존만 존재하고 하위 계층은 상위 계층에 의존하지 않는다.
  - 표현 계층은 응용 계층에 의존하지만 응용 계층은 표현 계층에 의존하지 않는다.
- 계층 구조를 엄격하게 적용한다면 상위 계층은 바로 아래의 계층에만 의존을 가져야 하지만 구현의 편리함을 위해 계층 구조를 유연하게 적용하기도 한다. 예를 들면 응용계층에서 바로 인프라스트럭처를 의존하는 것이다. 
- 하지만 이렇게 표현, 응용, 도메인 계층이 상세한 구현 기술을 다루는 인프라스트럭처 계층에 종속된다는 문제가 있다.
- 이렇게 인프라스트럭처에 의존하게 되면 "테스트를 하기 어려움"과 "구현 방식을 변경(기능 확장)의 어려움"이라는 문제가 있다.
- 이에 대한 해답은 DIP에 있다.

<br>

## 2.3 : DIP
- 고수준 모듈은 의미 있는 단일 기능을 제공하는 모듈이다.
- 저수준 모듈은 고수준 모듈의 하위 기능을 실제로 구현한 것이다.
- 2.2에서의 문제점은 고수준 모듈이 저수준 모듈을 사용하면서 발생한 문제이다. 이를 해결하기 위해 DIP를 사용해 저수준 모듈이 고수준 모듈에 의존하도록 바꾼다
- 그렇다면 저수준 모듈이 고수준 모듈에 의존하도록 하려면 어떻게 해야할까? 비밀은 추상화한 인터페이스에 있다.
- 인터페이스(고수준 모듈)을 상속해 실제 구현한 클래스(저수준 모듈)을 사용하면 저수준 모듈이 고수준 모듈에 의존하게 된다.
- 이처럼 저수준 모듈이 고수준 모듈을 의존한다고 해서 DIP(Dependency Inversion Priciple), 의존 역전 원칙이라 한다.
- 스프링과 같은 의존 주입을 지원하는 프레임워크를 사용하면 설정 코드를 수정해서 쉽게 구현체를 변경할 수 있다. 인터페이스를 대역 객체를 사용해 테스트를 진행할 수 있게 된 것이다.
- 실제 구현 없이 테스트를 할 수 있는 이뉴는 DIP를 적용해서 고수준 모듈을 저수준 모듈에 의존하지 않도록 했기 때문이다.

### 주의사항
  - DIP를 잘못 생각하면 단순히 인터페이스와 구현 클래스를 분리하는 정도로 받아들일 수 있다.
  - DIP의 핵심은 고수준 모듈이 저수준 모듈에 의존하지 않도록 하기 위함이다.
- DIP와 아키텍처
  - 인프라스트럭처 영역은 구현 기술을 다루는 저수준 모듈이고 응용, 도메인 영역은 고수준 모듈이다. DIP를 적용하면 인프라스트럭처 영역이 응용 영역과 도메인 영역에 의존(상속)하는 구조가 된다.
  - 인프라스트럭처에 위치한 클래스가 도메인이나 응용 영역에 정의한 인터페이스를 상속받아 구현하는 구조가 되므로 도메인과 응용 영역에 대한 영향을 주지 않거나 최소화하면서 구현 기술을 변경하는 것이 가능하다.

<br>

## 2.4 : 도메인 영역의 주요 구성요소
- 도메인 영역의 모델은 도메인의 주요 개념을 표현하며 핵심 로직을 구현한다.
- 엔티티와 밸류 타입은 도메인 영역의 주요 구성요소이다.
- Entity
  - 고유의 식별자를 갖는 객체로 자신의 라이프 사이클을 갖는다.
- Value
  - 고유의 식별자를 갖지 않는 객체로 주로 개념적으로 하나의 값을 표현할 때 사용된다.
  - 엔티티의 속성으로 사용할 뿐만 아니라 다른 밸류 타입의 속성으로도 사용할 수 있다.
- Aggregate(애그리거트)
  - 애그리거트는 연관된 엔티티와 밸류 객체를 개념적으로 하나로 묶은 것이다.
  - 도메인 모델에서 전체 구조를 이해하는 데 도움이 되는 것이 바로 애그리거트이다.
  - 애그리거트는 관련 객체를 하나로 묶은 군집이다.
  - 애그리거트는 군집에 속한 객체를 관리하는 루트 엔티티를 닺는다. 루트 엔티티는 애그리거트에 속해 있는 엔티티와 밸류 객체를 이용해서 애그리거트가 구현해야 할 기능을 제공한다.
  - 애그리거트를 사용하는 코드는 항상 애그리거트 루트가 제공하는 기능을 실행하고 애그리거트 루트를 통해 간접적으로 애그리거트 내의 다른 엔티티나 밸류 객체에 접근한다.
    - 이를 통해 애그리거트의 내부 구현을 숨겨서 애그리거트 단위로 구현을 캡슐화할 수 있도록 돕는다.
- Repository
  - 도메인 모델의 영속성을 처리한다.
  - 애그리거트 단위로 도메인 객체를 저장하고 조회하는 기능을 정의한다.
- Domain Service
  - 특정 엔티티에 속하지 않은 도메인 로직을 제공한다.
  - 도메인 로직이 여러 엔티티와 밸류를 필요로 하면 도메인 서비스에서 로직을 구현한다.

### 주의사항
  - 실제 도메인 모델의 엔티티와 DB 관계형 모델의 엔티티는 같은 것이 아니다.
  - 두 모델의 가장 큰 차이점은 도메인 모델의 엔티티는 데이터와 함께 도메인 기능을 하메 제공한다는 점이다.
  - 도메인 모델의 엔티티는 간순히 데이터를 담고 있는 데이터 구조라기보다는 데이터와 함게 기능을 함께 제공하는 객체이다.
  - 도메인 모델의 엔티티는 두 개 이상의 데이터가 개념적으로 하나인 경우 밸류 타입을 이용해서 표현할 수 있다.
  - 밸류는 불변으로 구현할 것을 권장하며, 이는 엔티티의 밸류 타입 데이터를 변경할 때 객체 자체를 완전히 교체한다는 것을 의미한다.

<br>

## 2.5 : 요청의 흐름

![img_2.png](img_2.png)

<br>

## 2.6 : 인프라스트럭쳐 개요
- 인프라스트럭쳐는 표현, 응용, 도메인 영역을 지원한다.
- DIP를 무조건적으로 적용할 필요는 없다.
  - DIP가 주는 편리함과 변경의 유연함, 테스트하기 쉬움 등 장점만큼 구현의 편리함 또한 중요하기 때문에, DIP의 장점을 해치지 않는 범위에서 응용 영역과 도메인 영역에서 구현 기술에 대한 의존을 가져가는 것이 나쁘지 않다고 생각한다.
  - 좋은 예시가 바로 스프리으이 @Transactional, @Entity, @Table 등이 있다.

<br>

## 2.7 : 모듈 구성
- 도메인 모듈은 도메인에 속한 애그리거트를 기준으로 다시 패키지를 구성한다.
- 애그리거트, 모델, 리포지터리는 같은 패키지에 위치시킨다.
- 복잡하다면 도메인 별로 패키지를 구분할 수 있다.

<br>
<hr>
<br>

# CH 03 : 애그리거트

## 3.1 : 애그리거트
- 주요 도메인 요소 간의 관계를 파아하기 어렵다는 것은 코드를 변경하고 확장하는 것이 어려워진다는 것을 의미한다.
- 복잡한 도메인을 이해하고 관리하기 쉬운 단위로 만들려면 상위 수준에서 모델을 조망할 수 있는 방법이 필요하다. 그것이 바로 애그리거트이다.
- 애그리거트는 복잡한 도메인을 단순한 구조로 만들어준다.
- 애그리거트는 관련된 모델을 하나로 모았기 때문에 한 애그리거트에 속한 객체는 유사하거나 동일한 라이프 사이클을 갖는다.
  - 애그리거트에 속한 구성요소는 대부분 함께 생성하고 함께 제거한다.
- 애그리거트는 독립된 객체 군이며 각 애그리거트는 자기 자신을 관리할 뿐 다른 애그리거트를 관리하지 않는다.
- 경계를 설정할 때 기본이 되는 것은 도메인 규칙과 요구사항이다. 도메인 규칙에 따라 함께 생성되는 구성요소는 한 애그리거트에 속한 가능성이 높다. 또한 함꼐 변경되는 빈도가 높은 객체는 한 애그리거트에 속한 가능성이 높다.

### 주의사항
- 흔히 A가 B를 갖는다로 설계할 수 있는 요구사항이 있다면 A와 B를 한 애그리거트로 묶어서 생각하기 쉽다.
- 하지만 A가 B를 갖는다로 해석할 수 있는 요구사항이 있더라도 이것이 반드시 A와 B가 한 애그리거트에 속한다는 것을 의미하는 것이 아니다.
  - 좋은 예시가 바로 상품과 리뷰다.
  - 상품 상세 페이지에 들어가면 상품 상세 정보와 함께 리뷰 내용을 보여줘야하는 요구사항이 있다. 하지만 상품과 리뷰는 함께 생성되지도 않고 함께 변겨오디지도 않는다. 따라서 서로 다른 애그리거트에 속한다.
  
<br>

## 3.2 : 애그리거트 루트
- 도메인 규칙을 지키려면 애그리거트에 속한 모든 객체가 정상 상태를 가져야 한다.
- 애그리거트에 속한 모든 객체가 일관된 상태를 유지하려면 애그리거트 전체를 관리할 주체가 필요한데, 바로 애그리거트의 루트 엔티티이다.
- 애그리거트 루트
  - 애그리거트가 제공해야 할 도메인 기능을 구현한다.
  - 애그리거트 루트가 제공하는 메서드는 도메인 규칙에 따라 애그리거트에 속한 객체의 일관성이 깨지지 않도록 구현해야 한다.

### 트랜잭션 범위
- 트랜잭션 범위는 작을수록 좋다. 한 트랜잭션이 한 개 테이블을 수정하는 것과 세 개의 테이블을 수정하는 것을 비교하면 성능에서 차이가 발생한다.
  - 또한 한 개 테이블을 수정하면 트랜잭션 충돌을 막기 위해 잠그는 대상이 한 개 테이블의 행으로 한정되지만, 여러개일 경우 잠금 대상이 많아진다.
  - 잠금 대상이 많아진다는 것은 그만큼 동시에 처리할 수 있는 트랜잭션 개수가 줄어든다는 것을 의미하고 이것은 전체적인 성능(처리량)을 떨어뜨린다.
- 한 트랜잭션에서는 한 개의 애그리거트만 수정해야 한다.
  - 한 트랜잭션에서 두 개 이상의 애그리거트를 수정하면 트랜잭션 충돌이 발생할 가능서이 높아진다.
  - 애그리거트가 자신의 책임 범위를 넘어 다른 애그리거트의 상태까지 관리하는 꼴이 된다.
  - 애그리거트는 쵣한 서로 독립적이어야 한다. 만약 부득이하게 한 트랜잭션으로 두 개 이상의 애그리거트를 수정해야 한다면, 애그리거트에서 다른 애그리거트를 직접 수정하지 말고 응용 서비스(Application)에서 두 애그리거트를 수정하도록 구현해야 한다.

### 주의사항
- 애그리거트 외부에서 애그리거트에 속한 객체를 직접 변경하면 안 된다. 이것은 애그리거트 루트가 강제하는 규칙을 적용할 수 없어 모델의 일관성을 깨는 원인이 된다.
- 즉 논리적인 데이터 일관성이 깨지게 되는 것이다.
- 불필요한 중복을 피하고 애그리거트 루트를 통해서만 도메인 로직을 구현하게 만들려면 도메인 모델에 대해 두 가지를 습관적으로 적용해야 한다.
  - 단순히 필드를 변경하는 Set 메서드를 공개(Public) 범위로 만들지 않는다.
  - 밸류 타이븐 불변으로 구현한다.
- 보통 한 애그리거트에 속하는 모델은 한 패키지에 속하기 때문에 패키지나 protected 범위를 사용하면 애그리거트 외부에서 상태 변경 기능을 실행하는 것을 방지할 수 있다.

<br>

## 3.3 : 리포지터리와 애그리거트
- 애그리거트는 개념상 완전한 한 개의 도메인 모델을 표현하므로 객체의 영속성을 처리하는 리포지터리는 애그리거트 단위로 존재한다.
  - 하나의 애그리거트 안에서 서로 각기 다른 물리적으로 별도의 DB 테이블에 저장한다고 해서 각각을 위한 리포지터리를 만들지 않는다. 루트 애그리거트 리포지터리만 존재한다.
- ORM 기술 중 하나인 JPA를 사용하면 데이터베이스 관계형 모델에 객체 도메인 모델을 맞춰야 할 때도 있다.
- 특히 레거시 DB를 사용하거나 팀 내 DB 설계 표준을 따라야 한다면 DB 테이블 구조에 맞게 모델을 변경해야 한다.
- 애그리거트를 영속화할 저장소로 무엇을 사용하든지 간에 애그리거트의 태가 변경되면 모든 변경을 원자적으로 저장소에 반영해야 한다.
  - 애그리거트에서 두 개의 객체를 변경했는데 저장소에는 한 객체에 대상 변경만 반영되면 데이터 일관성이 깨지므로 문제가 된다.

<br>

## 3.4 : ID를 이용한 애그리거트 참조
- 한 객체가 다른 객체를 참조하는 것처럼 애그리거트도 다른 애그리거트를 참조한다.
  - 애그리거트 관리 주체는 애그리거트 루트이므로 애그리거트에서 다른 애그리거트를 참조한다는 것은 다른 애그리거트 루트를 참조한다는 것이다.
- 필드를 이용해서 다른 애그리거트를 직접 참조하는 것은 개발자에게 구현의 편리함을 제공한다.(객체) 하지만 필드를 이용한 애그리거트 참조는 다음 문제를 야기할 수 있다.
  - 편함 탐색 오용
    - 한 애그리거트 내부에서 다른 애그리거트 내부에서 다른 애그리거트 객체에 접근할 수 있으면 다른 애그리거트의 상태를 쉽게 변경할 수 있게 된다.
    - 한 애그리거트에서 다른 애그리거트의 상태를 변경하는 것은 애그리거트 간의 의존 결합도를 높여서 결과적으로 애그리거트의 변경을 어렵게 만든다.
  - 성능에 대한 고민
    - JPA를 사용하면 참조한 객체를 지연, 즉시 로딩 두 가지 방식으로 로딩할 수 있다. 이를 고려하여 연관 매핍과 JPQL/Creteria 쿼리의 로딩 전략을 결정해야 한다.
  - 확장 어려움
    - 사용자가 늘고 트래픽이 증가하면 자연스럽게 부하를 분산하기 위해 하위 도메인별로 시스템을 분리하기 시작한다. 하위 도메인 마다 다른 저장소를 사용하기도 한다. 이것은 더이상 JPA와 같은 단일 기술을 사용할 수 없음을 의미한다.

### 위 3가지 문제점을 완화하는 방법 : 간접 ID 참조
- ID 참조를 사용하면 모든 객체가 참조로 연결되지 않고 한 애그리거트에 속한 객체들만 참조로 연결된다.
  - 이는 애그리거트의 경계를 명확히 하고 애그리거트 간 물리적인 연결을 제거하기 때문에 모델의 복잡도를 낮춰준다. 또한 애그리거트 간의 의존을 제거하므로 응집도를 높여주는 효과가 있다.
  - 구현 복잡도가 낮아진다. 다른 애그리거트를 직접 참조하지 않기 때문에 어떤 방식으로 로딩할 지 고민하지 않아도 된다.
- ID 참조는 응용 서비스에서 필요한 애그리거트를 로딩하므로 애그리거트 수준에서 지연 로딩을 하는 것과 동일한 결과를 만든다
- 애그리거트 별로 다른 구현 기을 사용하는 것도 가능해진다.
- 애그리거트마다 서로 다른 저장소를 사용하면 한 번의 쿼리로 관련 애그리거트를 조회할 수 없다. 이떄는 조회 성능을 높이기 위해 캐시를 적용하거나 조회 전용 저장소를 따로 구성한다.

### ID를 이용한 참조와 조회 성능
- 다른 애그리거트를 ID로 참조하면 참조하는 여러 애그리거트를 읽을 때 조회 속도가 문제 될 수 있다.
- ID 참조는 지연 로딩을 하는 것과 동일한 결과를 만들기 때문에 N+1 문제가 발생한다.
  - N+1 문제를 해결하기 위해선 조인을 사용해야 한다. 조인을 사용하는 가장 쉬운 방법은 직접참조 방식으로 바꾸고 즉시 로딩을 사용하는 것이다.
  - 혹은 ID 참조 방식을 사용하면서 조회 전용 쿼리를 사용하면 된다. 

<br>

## 3.5 애그리거트 간 집합 연관
- 1-N
  - 애그리거트 간 1-N 관계는 Set과 같은 컬렉션을 이용해서 표현할 수 있다.
  - 개념적으로 애그리거트 간에 1-N 연관이 있더라도 이런 성능 문제 때문에 애그리거트 간의 1-N 연관을 실제 구현에 반영하지 않는다.
- M-N
  - M-N 연관은 개념적으로 양쪽 애그리거트에 컬렉션으로 연관을 만든다.
  - 개념적으로는양방향 M-N 연관이 존재하지만 실제 구현에서는 단반향 M-N 연관만 용하면 되는 것이다.(여러 Category를 갖는 여러 Product 관계)
  - RBMS를 이용해서 M-N 연관을 구현하려면 조인 테이블을 사용한다(중간에 테이블 하나 생성하여 이용)
  - JPQL의 member of 연산자를 이용해 특정 Category에 속한 Product 목록을 구하는 기능 등을 구현할 수 있다.

<br>

## 애그리거트를 팩토리로 사용하기
- 도메인을 생성하는 로직 등이 어플리케이션 레이어에 있다면 애그리거트에 팩토리 기능을 추가하자.
- 만약 A 애그리거트가 갖고 있는 데이터를 이용해서 다른 B 애기르거트를 생성해야 한다면 애그리거트에 팩토리 메서드를 구현하는 것을 고려하자.
  - B를 생성하기 위해 A의 식별자가 필요하며 A의 조건을 판단한 후 B를 생성해야 한다면 A에 B를 생성하는 팩토리 메서드를 추가하자.


<br>
<hr>
<br>

# CH 04 : 리포지터리와 모델 구현

## 4.1 JPA를 이용한 리포지터리 구현
- 리포지터리 인터페이스는 애그리거트와 같이 도메인 영역에 속하고, 리포지터리를 구현한 클래스는 인프라스트럭쳐 영역에 속한다.
- 인터페이스는 애그리거트 루트를 기준으로 작성한다. 
- 애그리거트를 조회하는 이름을 지을 떄 널리 사용되는 규칙은 findBy프로퍼티이름(프로퍼티 값) 형식을 사용한다.

<br>

## 4.2 Spring Data JPA를 이용한 리포지터리 구현

## 4.3 매핑 구현
- 애그리거트와 JPA 매핑을 위한 기본 규칙은 다음과 같다.
  - 애그리거트 루트는 엔티티이므로 @Entity로 매핑을 설정한다.
- 한 테이블에 엔티티와 밸류 데이터가 같이 있다면
  - 밸류는 @Embeddable로 매핑을 설정한다.
  - 엔티티 클래스의 밸류 타입 프로퍼티는 @Embedded로 매핑 설정한다.
- 엔티티와 밸류의 생성자는 객체를 생성할 때 필요한 것을 전달받는다. 하지만 JPA에서 엔티티와 밸류 타입 클래스를 매핑하려면 기본 생성자가 제공되어야 한다.
  - DB에서 데이터를 읽어와 매핑된 객체를 생성할 때 기본 생성자를 사용해서 객체를 생성하기 때문이다.(JPA 프로바이더가 객체를 생성할 때만 사용된다.)
  - 따라서 기본 생성자를 public or protected로 설정해준다. 하지만 기본 생성자를 다른 코드에서 사용하면 일관성이 깨지므로 protected로 선언한다.
- AttributeConverter를 사용해 밸류 매핑 처리
  - 두 개 이상의 프로퍼티를 가진 밸류 타입을 한 개의 컬럼에 매핑하려면 @Embeddable로 처리할 수 없다. 이럴 때 사용하는 것이 AttributeConverter이다.
  - AttributeConverter는 밸류 타입 -> DB 컬럼 값, DB 컬럼 값 -> 밸류 타입으로 변환하는 기능을 구현한다.
  - AttributeConverter를 적용하고 싶다면 @Converter 어노테이션을 적용해야 한다.
- @Converter 사용
  - 클래스 레벨에서 @Converter 어노테이션의 autoApply 속성을 true로 두면 모델(해당 클래스)에 출현하는 모든 밸류 타입의 프로퍼티에 컨버터가 자동으로 적용된다.
  - 필드 레벨에 직접 @Converter를 적용할 수도 있다. @Converter(converter = MoneyCoverter.class)

- ### 밸류 컬렉션, 별도 테이블 매핑
  - 밸류 컬렉션을 별도 테이블로 매핑할 때는 @ElementCollection과 @CollectionTable을 함께 사용한다.
  
### Entity
```java

@Entity
@Table(name = "purchase_order")
public class Order {
  @EmbededId
  private OrderNo number;

  /** ... */


  @ElementCollection(fetch = FetchType.Eager)
  @CollectionTable(name = "order_line",
          joinColumns = @JoinColumn(name = "order_number"))
  @OrderColum(name = "lin_idx")
  private List<OrderLine> orderLines;
}


```

### Value
```java

@Embeddable
public class OrderLine{
  @Embedded
  private ProductId productId;
  
  @Column(name = "price")
  private Money price;
  
  @Column(name = "quantity")
  private int quantity;
  
  @Column(name = "amounts")
  private Money amounts;
    
}
```

### Value
```java

@Embeddable
public class OrderNo implements Serializable {

  @Column(name = "order_number")
  private String number;

}
```
- JPA에서 식별자 타입은 Serializable 타입이어야 하므로 식별자로 사용할 밸류 타입은 Serializable 인터페이스를 상속받아야 한다.


- Order에 OrderLine의 매핑을 함께 표시했는데, OrderLine에는 List의 인덱스 값을 저장하기 위한 프로퍼티가 존재하지 않는다.
  - 그 이유는 List 타입 자체가 인덱스를 갖고 있기 때문이다. JPA는 @OrderColumn 어노테이션을 이용해서 지정한 컬럼에 리스트의 인덱스 값을 저장한다.
- @CollectionTable은 밸류를 저장할 테이블을 지정한다. name 속서은 테이블 이름을 지정하고 joinColumns 속성은 외부키로 사용할 컬럼을 지정한다.
- 예제 코드에서는 외부키가 한개인데, 두 개 이상인 경우 @JoinColumn의 배열을 이용해서 외부키 목록을 지정한다.

<br>

- ### 밸류 컬렉션, 한 개 컬럼 매핑
  - 밸류 컬렉션을 별로 테이블이 아닌 한 개 컬럼에 저장해야 할 때가 있다.
  - 예를 들어 도메인 모델에는 이메일 주소 목록을 Set으로 보관하고 DB에는 한 개 컬럼에 콤마로 구분해서 저장해야 할 때가 있다.
  - 이때 AttributeConverter를 사용하면 밸류 컬렉션을 한 개 컬럼에 쉽게 매핑할 수 있다. 
  - 단, AttrivuteConverter를 사용하려면 밸류 컬렉션을 표현하는 새로운 밸류 타입을 추가해야 한다.


### 이메일 집합을 위한 Value

````java

public class EmailSet {
  private Set<Email> emails = new HashSet<>();

  public EmailSet(Set<Email> emails) {
    this.emails = emails;
  }

  public Set<Email> getEmails() {
    return Collections.unmodifiableList(emails);
  }
}
````

### AttributeConverter 구현
````java

public class EmailSetConverter implements AttributeConverter<EmailSet, String>{

  @Override
  public String convertToDatabaseColumn(EmailSet attribute) {
      if(attribute == null) return null;
      
      return attribute.getEmail().stream()
              .map(email -> email.getAddress())
              .collect(Collectors.joining(","));
      
      
  }
  
  
  @Override
  public EmailSet convertToEntityAttribute(String dbData){
      if(dbData == null) return null;
      
      String[] emails = dbData.split(",");
      Set<Email> emailSet = Arrays.stream(emails)
              .map(value -> new Email(value))
              .collect(toSet());
      
      return new EmailSet(emilSet);
  }
}

````

### 사용
```java
  @Column(name = "emails")
  @Convert(converter = EmailSetConverter.class)
  private EmailSet emailSet;

```

<br> 

- ### 별도 테이블에 저장하는 밸류 매핑
- 애그리거트에서 루트 엔티티를 뺀 나머지 구성요소는 대부분 밸류이다. 루트 엔티티 외에도 또 다른 엔티티가 있다면 다른 애그리거트인지 의심해 보아야 한다.
- 애그리거트에 속한 객체가 밸류인지 엔티티인지 구분하는 방법은 고유 식별자를 갖는지 확인하는 것이다.
- 하지만 식별자를 찾을 때 매핑되는 테이블의 식별자를 애그리거트 구성요소의 식별자와 동일한 것으로 착각하면 안된다.
- 밸류를 매핑 한 테이블을 지정하기 위해 @SecondaryTable과 @AttributeOverride를 사용한다.

### Entity

```java


@Entity
@Table(name = "article")
@SecondaryTable(
        name = "article_content",
        pkJoinColumns = @PrimaryKeyJoinColumn(name = "id")
)
public class Article {
  @Id
  @GeneratedValue(staragy = GenerationType.IDENTIFY)
  private Long id;
  
  private String title;
  
  @AttributeOverrides({
          @AttributeOverride(
                  name = "content",
                  column = @Column(table = "article_content", name = "content")
          ),
          @AttributeOverride(
                  name = "contentType",
                  column = @Column(table = "article_content", name = "content_type")
          )
  })
  @Embedded
  private ArticleContent content;
}
```
- @SecondaryTable의 name 속성은 밸류를 저장할 테이블을 지정한다.
- pkJoinColumns 속성은 밸류 테이블에서 엔티티 테이블로 조인할 때 사용할 컬럼을 지정한다.
- content 필드에 @AttributeOverride를 적용했는데, 이 어노테이션을 사용해서 해당 밸류 데이터가 저장된 테이블 이름을 지정한다.
- @SecondaryTable을 이용하면 아래 코드를 실행할 때 두 테이블을 조인해서 데이터를 조회한다.

````java
// @SecondaryTable로 매핑된 article_content 테이블을 조인
Article article = entityManager.find(Article.class, 1L);
````
- 위 예시를 들어 게시글 목록을 보여주는 화면은 article 테이블의 데이터만 필요하지 article_content 테이블의 데이터는 필요하지 않다.
- 그런데 @SecondaryTable을 사용하면 Article을 조회할 때 article_content 테이블까지 조인해서 데이터를 읽어오는데, 이것은 원하는 결과가 아니다.
- 이 문제를 해소하고자 ArticleContent를 엔티티로 매핑하고 Article에서 지연 로딩 방식을 설정할 수도 있지만 밸류 모델을 엔티티로 만드는 것은 좋은 방법이 아니다.
- 대신 조회 전용 기능을 구현하는 방법을 사용하자(CH 05)

<br>

### - 밸류 컬렉션을 @Entity로 매핑하기
- JPA는 @Embeddable 타입의 클래스 상속 매핑을 지원하지 않는다. 상속 구조를 갖는 밸류타입을 사용하려면 @Embeddable 대신 @Entity를 이용해서 상속 매핑으로 처리해야 한다.
- 밸류 타입을 @Entity로 매핑하므로 식별자 매핑을 위한 필드도 추가해야 한다. 또한 구현 클래스를 구분하기 위한 식별(disciriminator) 컬럼을 추가해야 한다.
- 예를 들어 제품의 이미지 업로드 방식에 따라 이미지 경로와 섬네일 이미지 제공 여부가 달라진다고 하자.

### Entity
```java
@Entity
@Inheritance(strategy = InheritanceType.SINGLE_TABLE)
@DiscriminatorColumn (name = "image type")
@Table (name = "image")
public abstract class Image {
  @Id
  @GeneratedValue (Strategy = GenerationType.IDENTITY)
  @Column (name = "image id")
  private Long id;
  
  @Column (name = "image path")
  private String path;
  
  @Temporal (TemporalType.TIMESTAMP)
  @Column (name = "upload _time")
  private Date uploadTime;
  
  protected Image(){}
  
  public Image (String path) {
    this.path = path;
    this.uploadTime = new Date();
  
  }
  
  protected String getPath(){
     return path;
  }
  
  public Date getUploadTime(){
    return uploadTime;
  }
  
  public abstract String getURL;
  public abstract boolean hasThumbnail;
  public abstract String getThumbnailURL;
      
    
  }
```
- 밸류를 @Entity로 매핑했으므로 상태 변경 메서드를 제공하지 않는다.
- @Inheritance 어노테이션 적용, strategy 값으로 SINGLE_TABLE 사용
- @DiscriminatorColumn 어노테이션을 이용해 타입 구분용으로 사용할 컬럼 지정

### Value
```java

@Entity
@DiscriminatorValue("II")
public class InternalImage extends Image{
    
}


@Entity
@DiscriminatorValue("EI")
public class ExternalImage extends Image{

}
```
- Image를 상속받은 클래스는 @Entity와 @Discriminator를 사용해 매핑한다.

### Entity
````java

@Entity
@Table(name = "product")
public class Product {
  @EmbeddedId
  private ProductId id;
  
  private String name;
  
  @Convert(converter = MoneyConverter.class)
  private Money price;
  
  private String detail;
  
  @OneToMany(
          cascade = {CascadeType.PERSIST, CascadeType.REMOVE},
          orphanRemoval = true)
  @JoinColumn(name = "product_id")
  @OrderColumn(name = "list idx")
  private List <Image> images = new ArrayListo();
  
  public void changeImages(List<Image> newImages){
      images.clear();
      images.addAll(newImages);
  }
  
}
````
- Image가 엔티티이므로 Pruduct와 같이 @OneToMany를 이용해 매피을 처리한다. Image는 밸류이므로 독자적인 아피으 사이클을 갖지 않고 Product에 완전히 의존한다.
- 따라서 Product를 저장할 때 하메 저장되고 Product를 삭제할 때 함꼐 삭제되도록 cascade 속성을 지정한다.
- 리스트에서 Image 객체를 제거하면 DB에서 함께 삭제되도록 orphanRemoval도 true로 설정한다.
- @OneToMany 관게에서 컬렉션의 clear는 성능이 좋지 않다. 이를 해결하기 위해선 Value 타입으로 교체해야 한다.

<br>

### - ID 참조와 조인 테이블을 이용한 단방향 M-N 매핑
- 이 부분은 밸류 컬렉션 매핑과 동일한 방식으로 설정하지만 차이점이 있다면 Set 타입을 밸류 대신 식별자가 온다는 것이다.

<br>

## 4.4 애그리거트 로딩 전랴
- JPA 매핑을 설정할 때 항상 기억행 할 점은 애그리거트에 속한 객체가 모두 모여야 완전한 하나가 된다는 것이다.
- 애그리거트가 완전해야 하는 이유
  - 상태를 변경하는 기능을 실행할 때 애그리거트 상태가 완전해야 한다.
  - 표현 영역에서 애그리거트의 상태 정보를 보여줄 때 필요하다.
- 조회 시점에서 애그리거트를 완전한 상태가 되도록 하려면 애그리거트 루트에서 연관 매칭의 조회 방식을 즉시 로딩으로 설정하면 된다.(FetchType.EAGER)
  - 하지만 컬렉션에 대해 로딩 전략을 EAGER로 설정하면 오히려 즉시 로딩 방식이 문제가 될 수 있다.
  - 일반적으로 카타시안(Cartesian) 조인을 사용하면 쿼리 결과에 중복이 발생한다.
    - 카타시안 조인 : 조인 조건을 생략하고 A테이블의 모든 행이 B테이블의 모든 행과 조인되는 경우
  - 한 제품에 대한 이미지가 20개고 욥션이 15개라면 find() 메서드 실행 시 쿼리는 300행을 리턴한다.
- 애그리거트는 개념적으로 하나지만 루트 엔티티를 로딩하는 시점에 애그리거트에 속한 모든 객체를 모두 로딩해야 하는 것은 아니다.
- JPA는 트랜잭션 범위 내에서 지연 로딩을 허용하기 때문에 실제로 상태를 변경하는 시점에 필요한 구성요소만 로딩해도 문제가 되지 않는다.
- 또한 일반적인 애플리케이션은 상태 변경 기능을 실행하는 빈도보다 조회 기증을 실행하는 빈도가 훨신 높다. 그러므로 상태 변경을 위해 지연 로딩을 사용할 때 발생하는 추가 쿼리로 인한 실행 속도 저하는 보통 문제가 되지 않는다.
- 이러한 이유로 모든 연관을 즉시 로딩을 설정할 필요는 없다. 애그리거트에 맞게 즉시, 지연 로딩 전략을 선택해야 한다.

<br>

## 4.5 애그리거트의 영속성 전파
- 애그리거트가 완전한 상태여야 한다는 것은 애그리거트 루트를 조회할 때뿐만 아니라 저장하고 삭제할 때도 하나로 처리해야 함을 의미한다.
  - 저장 메서드는 애그리거트 루트만 저장하면 안되고 애그리거트에 속한 모든 객체를 저장해야 한다.
  - 삭제 메서드는 애그리거트 루트뿐만 아니라 애그리거트에 속한 모든 객체르 삭제해야 한다.
- @Embeddable 매핑 타입은 함께 저장되고 삭제되므로 cascade 속성을 추가로 설정하지 않아도 된다.
- @Entity 타입에 대한 매핑은 cascade, orphanRemoval 속성을 사용해 라이프 사이클을 함께 해야 한다.

<br>

## 4.6 식별자 생성 기능
- 사용자가 직접 생성
  - 이메일 주소처럼 사용자가 직접 식별자를 입력하는 경우는 딱히 도메인 영역이나 DB에서 식별자 생성 기능을 구현할 필요가 없다.
- 도메인 로직으로 생성
  - 식별자 생성 규칙이 있다면 엔티티를 생성할 때 식별자를 엔티티가 별도 서비스로 식별자 생성 기능을 분리해야 한다.
  - 식별자 생성 규칙은 도메인 규칙이므로 도메인 영역에 식별자 생성 기능을 위치시켜야 한다. 도메인 서비스를 도메인 영역에 위치시킬 수 있다.
    - 응용 서비스는 도메인 서비스를 이용해 식별자를 구하고 엔티티를 생성한다.
  - 식별자 생성 규칙을 구현하기에 또 다른 장소는 리포지터리다.
    - 리포지터리 인터페이스에 식별자를 생성하는 메서드를 추가하고 리포지터리 구현 클래스에 맞게 구혀한다.
- DB를 이용한 일련번호 사용
  - @GeneratedValue를 사용한다.
  - 자동 증가 컬럼은 DB의 insert 쿼리를 실해해야 식별자가 생성되므로 도메인 객체를 리포지터리에 저장할 때 식별자가 생성된다.
  - 이 말은 도메인 객체를 생성하는 시점에는 식별자를 알 수 없고 도메인 객체를 저장한 뒤에 식별자를 구할 수 있음을 의미한다.
  - JPA는 저장 시점에 생성한 식별자를 @Id로 매핑 한 프로퍼티/필드에 할당하므로 위 코드처럼 저장 이후에 엔티티의 식별자를 사용할 수 있다.
  - 자동 증가 컬럼 외에도 JPA 식별자 생성 기능을 사용하는 경우에는 저장 시점에 식별자를 생성한다.

<br>

## 4.7 도메인 구현과 DIP
- 구현의 편리함이 높다면 DIP를 고집하지 않아도 된다.

<br>
<hr>
<br>

# CH 05 : 스프링 데이터 JPA를 이용한 조회 기능

## 5.1 시작에 앞서
- CQRS는 명렁(Command) 모델과 조회(Query) 모델을 분리하는 패턴이다. 
  - 명령 모델은 상태를 변경하는 기능을 구현할 때 사용한다.(주문취소, 배송지 변경 등 상태 변경)
  - 조회 모델은 데이터를 조회하는 기능을 구현할 때 사용한다.(주문 목록, 상품 상세 등 조회 기능)
- 5장에서는 이름을 혼용해서 사용
  - Repository - 도메인 모델에 속한다는 의미
  - DAO - 데이터 접근을 의미

<br>

## 5.2 검색을 위한 스펙
- 검색 조건이 고정되어 있고 단순하면 특정 조건으로 조회하는 기능을 만들면 된다.
- 하지만 검색 조건을 다양하게 조합해야 할 때 사용할 수 있는 것이 스펙이다. 스펙은 애그리거트가 특정 조건을 충족하는지를 검사할 때 사용하는 인터페이스이다.
```java
public interface Speficiation<T>{
    public boolean isSatisfiedBy(T agg);
}
```
- isSatisfiedBy() 메서드의 agg 파라미터는 검사 대상이 되는 객체이다.
  - 검사 대상 객체가 조건을 충족하면 true를 리턴한다.
- 스펙을 리포지터리에 사용하면 agg는 애그리거트 루트가 되고 DAO에 사용하면 검색 결과로 리턴할 데이터 객체가 된다.

<br>

## 5.3 스프링 데이터 JPA를 이용한 스펙 구현
- 스펙 인터페이스에서 제네릭 타입 파라미터 T는 JPA 엔티티 타입을 의미한다.

<br>

## 5.4 리포지터리/DAO에서 스펙 사용하기
- findAll() 메서드는 검색 조건을 표현하는 스펙 인터페이스를 파라미터로 갖는다.

<br>

## 5.5 스펙 조합
- 스프링 데이터 JPA가 제공하는 스펙 인터페이스는 스펙을 조합할 수 있는 두 메서드를 제공한다.
  - and() : 두 스펙을 모두 충족하는 조건을 표현하는 스펙 생성
  - or() : 두 스펙 중 하나 이상 충족하는 조건을 표현하는 스펙 생성
  - not() : 정적 메서드로 조건을 반대로 적용할 때 사용
  - where() : 스펙 인터페이스의 정적 메서드로 null의 전달 유무에 따라 null이면 아무 조건이 없는 스펙을, 아니라면 받은 스펙 객체를 그대로 리턴한다.

<br>

## 5.6 정렬 지정하기
- 스프링 데이터 JPA는 두가지 방법을 사용해 정렬을 지정할 수 있다.
  - 메서드 이름에 OrderBy를 사용해서 정렬 기준 지정
    - 2개 이상의 프로퍼티레 대한 정렬 순서를 지정할 수도 있다. 하지만 너무 메서드명이 너무 길어질 수 있으므로 Sort 타입을 사용한다.
  - Sort를 인자로 전달
    - find 메서드의 파라미터로 제공된다.
    - Sort#and(Sort#)을 통해 연결할 수 있다.

<br>

## 5.7 페이징 처리하기
- 스프링 데이터 JPA는 페이징 처리를 위해 Pageable 타입을 이용한다.
- Sort 타입과 마찬가지로 find 메서드의 파라미터로 제공된다.
- Pageable 타입은 인터페이스로 실제 Pageable 타입 객체는 PageRequest 클래스를 이용해서 생성한다.
  - PageRequest.of(페이지 번호, 사이즈, Sort) 형식이다.(Sort를 통해 정렬 방식을 정할 수 있다.)
- Pageable을 사용하는 메서드의 리턴 타입이 Page일 경우 스프링 데이터 JPA는 목록 조회 쿼리와 함께 COUNT 쿼리도 실행해서 조건에 해당하는 총 데이터의 개수를 구한다.
- Pageable을 사용하더라도 리턴 타입이 List일 경우 COUNT 쿼리가 실행되지 않는다.

<br>

## 5.8 스펠 조합을 위한 스펙 빌더 클래스
- 조건을 표현하고 메서드 호출 체인으로 연속된 변수 할당을 줄여 코드 가독성을 높이고 구조를 단순히 가져갈 수 있다.
  - and()
  - ifHasText()
  - ifTrue()

<br>

## 5.9 동적 인스턴스 생성
- JPA는 쿼리 결과에서 임의의 객체를 동적으로 생성할 수 있는 기능을 제공하고 있다.
- new 키워드 뒤에 생성할 인스턴스의 완전한 클래스 이름을 지정하고 괄호 안에 생성자에 인자로 전달할 값을 지정한다.
- 생성할 인스턴스의 생정자는 필요한 인자를 할당받는다.

<br>

## 5.10 하이버네이트 @Subselect 사용
- @Immutable, @Subselect, @Synchronized는 하이버네이트 전용 어노테이션인데 이 태그를 사용하면 테이블이 아닌 쿼리 결과를 @Entity로 매핑할 있다.
- @Immutable
- @Subselect
- @Synchronize

<br>
<hr>
<br>

# CH 6 : 응용 서비스와 표현 영역

## 6.1 표현 영역과 응용 영역

<br>

## 6.2 응용 서비스의 역할
- 응용 서비스는 주로 도메인 객체 간의 흐름을 제어하기 때문에 단순한 형태를 갖는다.
- 응용 서비스는 트랜잭션 처리도 담당한다. 응용 서비스는 도메인의 상태 변경을 트랜잭션으로 처리한다. 이외에도 접근 제어 이벤트 처리 등을 수행한다.
- 도메인 로직을 도메인 영역과 응용 서비스에 분산해서 구현할 경우 코드 품질에 문제가 발생한다.
  - 코드의 응집성이 떨어진다.
  - 동일한 도메인 로직을 구현할 가능성이 높아진다.

<br>

## 6.3 응용 서비스의 구현
- 응용 서비스는 표현 영역과 도메인 영역을 연결하는 매개체 역할을 한다. 이는 디자인 패턴에서 파사드와 같은 역할을 한다.
- 응용 서비스를 구현할 때 논쟁이 될 만한 것이 인터페이스가 필요한 지이다. 인터페이스가 필요한 몇 가지 상황이 있다.
  - 구현 클래스가 여러가지인 경우
  - 런타임에 객체를 교체해야하는 경우
  - TDD를 통해 표현 영역부터 개발할 경우(응용 서비스를 구현할 수 없으므로)
    - 하지만 Mockito와 같은 테스트 도구를 통해 테스트용 대역 객체를 만들 수 있다.
- 표현 영역에 의존하지 않기
  - 표현 영역에 해당하는 HttpServletRequest나 HttpSession을 응용 서비스의 파라미터로 전달하면 안된다.

<br>

## 6.4 표현 영역
- 표현 영역의 책임은 크게 3가지가 있다.
  - 사용자가 시스템을 사용할 수 있는 흐름(호면)을 제공하고 제어한다.
  - 사용자의 요청을 알맞은 응용 서비스에 전달하고 결과를 사용자에게 제공한다.
  - 사용자의 세션과 쿠키 등을 관리한다.

<br>

## 6.5 값 검증
- 값 검증은 표현 영역과 응용 서비스 두 곳에서 모두 수행할 수 있다. 원칙적으로는 모든 값에 대한 검증은 응용 서비스에서 처리한다.
- Spring MVC는 폼에 입력한 값이 잘못된 경우 에러 메세지를 보여주기 위한 용도로 Errors나 BindingResult를 사용한다.
  - Service에서 예외를 모아 Controller에 넘겨준 후 Controller가 BindingResult에 담아 리턴하는 방식이 이상적
- ### 책 참고

<br>

## 6.6 권한 검사
- 보안 프레임워크의 복잡도를 떠나 보통 3곳에서 권한 검사를 수행할 수 있다.
  - 표현 영역
    - 표현 영역에서 할 수 있는 기본적인 검사는 인증된 사용자인지 아닌지 검사하는 것
    - URL을 처리하는 컨트롤러 웹 요청을 전달하기 전에 인증 여부를 검사해서 인증된 사용자의 웹 요청만 컨트롤러에 전달한다.(필터 사용)
    - 인증된 사용자가 아닐 경우 로그인 화면으로 리다이렉트 시킨다.
  - 응용 서비스
    - 메서드 단위로 권한 검사를 수행한다.
    - Spring Security의 AOP를 활용하여 권한 검사를 할 수 있다.
  - 도메인
    - 개별 도메인 객체 단위로 권한 검사를 할 경우 복잡해지기 때문에 직접 권한 검사 로직을 구현해야할 수도 있다.
    - 프레임워크에 대한 이해도가 높다면 Spring Security와 같은 프레임워크를 확장하는 것도 좋은 방법이다.

<br>

## 6.7 조회 전용 기능과 응용 서비스
- 조회 전용 기능은 트랜잭션이 필요하지 않다. 이 경우라면 굳이 서비스 계층 없이 표현 영역에서 바로 조회 전용 기능을 사용해도 좋다.

<br>
<hr>
<br>

# Ch 07 : 도메인 서비스

## 7.1 여러 애그리거트가 필요한 기능
- 도메인 영역의 코드를 작성하다 보면, 한 애그리거트로 기능을 구현할 수 없을 때가 있다. 대표적인 예가 결제 금액 계산 로직이다.
  - 상품 애그리거트 : 구매하는 상품의 가격이 필요하다. 또한 상품에 따라 배송비가 추가되기도 한다.
  - 주문 애그리거트 : 상품별로 구매 개수가 필요하다.
  - 할인 쿠폰 애그리거트 : 쿠폰별로 지정한 할인 금액이나 비율에 따라 주문 총 금액을 할인한다. 할인 쿠폰을 조건에 따라 중복 사용할수 있다거나 지정한 카테고리의 상품에만 적용할 수 있다는 제약 조건이 있다면 할인 계산이 복잡해진다.
  - 회원 애그리거트 : 회원 등급에 따라 추가 할인이 가능하다.
- 위와 상황에서 실제 결제 금액을 계산해야 하는 주체는 어떤 애그리거트일까? 총 주문 금액을 계산하는 것은 주문 애그리거트가 할 수 있지만 실제 결제 금액은 이야기가 다르다.
- 생각해 볼 수 있는 방법은 주문 애그리거트가 필요한 데이터를 모두 가지도록 한 뒤 할인 금액 계산 책임을 주문 애그리거트에 할당하는 것이다. 하지만 이렇게 한 애그리거트에 넣기 애매한 도메인 기능을 억지로 특정 애그리거트에 구현할 경우 코드가 길어지고 자신의 책임 범위를 벗어나는 기능을 구현하기 때문에 외부에 대한 의존도도 높아진다.
- 이를 해소하기 위해서 가장 쉬운 방법은 도메인 기능을 별도 서비스로 구현하는 것이다.

<br>

## 도메인 서비스
- 도메인 서비스는 도메인 영역에 위치한 도메인 로직을 표현할 때 사용한다. 주로 다음 상황에서 도메인 서비스를 이용한다.
  - 계산 로직 : 여러 애그리거트가 필요한 계산 로직이나, 한 애그리거트에 넣기에는 다속 복잡한 계산 로직
  - 외부 시스템 연동이 필요한 도메인 로직 : 구현하기 위해 타 시스템을 사용해야 하는 도메인 로직
- 애그리거트에 억지로 넣기 보다는 도메인 서비스를 이용하여 도메인 개념을 명시적으로 드러내면 된다.
- 도메인 서비스는 상태 없이 로직만 구현해야 한다.
- 애그리거트 객체에 도메인 서비스를 전달하는 것은 응용 서비스 책임이다.
  - 응용 서비스에서 도메인 서비스를 받아 도메인에 넘겨준다.
- 도메인 서비스 객체를 애그리거트에 주입하면 안된다.(@Autowired)
  - 도메인 객체는 필드(프로퍼티)로 구성된 데이터와 메서드를 이용해서 개념적으로 하나인 모델을 표현한다.
  - 그런데 도메인 서비스 필드는 데이터 자체와 관련이 없다. 또한 일부 기능만을 필요로하기 때문에 굳이 주입할 필요도 없다.
- 애그리거트 메서드를 실행할 때 도메인 서비스를 인자로 전달하지 않고 반대로 도메인 서비스의 기능을 실행할 때 애그리거트를 전달하기도 한다.
  - 계좌 이체 기능 : 계좌 이체는 두 계좌 애그리거트가 관여하는데, 한 애그리거트는 금액을 출금하고 한 애그리거트는 금액을 입금한다.
- 도메인 서비스는 도메인 로직을 수행할 뿐 응용 로직을 수행하지 않는다. 트랜잭션 처리와 같은 로직은 응용 로직이므로 도메인 서비스가 아닌 응용 서비스에서 처리해야 한다.

<br>
<hr>
<br>

# Ch 08 : 애그리거트 트랜잭션 관리

## 8.1 애그리거트와 트랜잭션
- 한 주문 애그리거트에 대해 운영자는 배송 상태를 변경하고 사용자는 배송지 주소를 변경하면 어떻게 될까
- 트랜잭션마다 리포지터리는 새로운 애그리거트 객체를 생성하므로 운영자 스레드와 고객 스레드는 같은 주문 애그리거트를 나타내는 다른 객체를 구하게 된다.
- 운영자 스레드와 고객 스레으는 개념적으로 동일한 애그리거트지만 물리적으로 서로 다른 애그리거트 객체를 사용한다.
- 이러한 상황에서 두 ㅅ스레드는 각각 트랜잭션을 커밋할 때 수정한 내용을 DB에 반영한다. 그러면 배송 상태도 바뀌고 배송지 정보도 바뀌면서 운영자는 기존 배송지 정보를 이용해 배송 상태를 변경하였는데 그 사이 고객은 배송지 정보를 변경했다는 점이다. 즉, 애그리거트의 일관성이 깨지는 것이다.
- 애그리거트의 일관성이 깨지는 문제를 해결하기 위한 방법으로 2가지가 있다.
  - 운영자가 정보를 조회하고 상태를 변경하는 동안 고객이 애그리거트를 수정하지 못하게 막는다.
  - 운영자가 정보를 조회한 이후 고객이 정보를 수정할 시 운영자가 다시 애그리거트를 조회하고 상태를 변경하도록 한다.
- 위 2가지는 애그리거트 자체의 트랜잭션과 관련이 있다. DBMS가 지원하는 트랜잭션과 함께 애그리거트를 위한 추가적인 트랜잭션 처리 기법이 필요하다.
- 대표적인 트랜잭션 처리 방식에는 선점(Pessimistic) 잠금과 비선점(Optimistic) 잠금 2가지 방식이 있다.

<br>

## 8.2 선점 잠금(Pessimistic Lock)
- 선점 잔금(Pessimistic Lock)은 먼저 애그리거트를 구한 스레드가 애그리거트 사용이 끝날 떄까지 다른 스레드가 해당 애그리거트를 수정하지 못하게 막는 방식이다.
  - 스레드 1이 선점 잠금 방식으로 애그리거트를 구한 뒤 이어서 스레드 2가 같은 애그리거트를 구하려고 하면 스레드 2는 스레드 1이 애그리거트에 대한 잠금을 해제할 때까지 블로킹(Blocking)된다.
  - 스레드 1이 애그리거트를 수정하고 트랜잭션을 커밋하면 잠금이 해제되어 대기하고 있던 스레드 2가 애그리거트에 접근하게 된다.
  - 스레드 2는 스레드 1이 수정한 애그리거트의 내용을 보게 된다.
- 선점 잠금 방식은 한 스레드가 애그리거트를 구하고 수정하는 동안 다른 스레드가 수정할 수 없으므로 동시에 애그리거트를 수정할 때 발생하는 데이터 충돌 문제를 해소할 수 있다.
- 선점 잠금은 보통 DBMS가 제공하는 행단위 잠금을 사용해서 구현한다.
  - 오라클을 비롯한 다수의 DBMS가 "for update"와 같은 쿼리를 사용해서 특정 레코드에 한 커넥션만 접근할 수 있는 잠금장치를 제공한다.
- JPA EntityManager는 LockModeType을 인자로 받는 find() 메서드를 제공한다.
  - LockModeType.PESSIMISTIC_WRITE을 값으로 전달하면 해당 엔티티와 매핑된 테이블을 이용해서 선점 장금 방식을 적용할 수 있다.
- Spring Data JPA는 @Lock 어너테이션을 사용해 잠금 모드를 지정한다.
  - @Lock(LockModeType.PESSIMISTIC_WRITE)

### 선점 잠금과 교착 상태
- 선점 잠금 기능을 사용할 때는 잠금 순서에 따른 교착 상태(deadlock)가 발생하지 않도록 주의해야 한다.
  1. 스레드1 : A 어그리게이트에 대한 선점 장금 구함
  2. 스레드2 : B 어그리게이트에 대한 선점 장금 구함
  3. 스레드1 : B 어그리게이트에 대한 선점 장금 시도
  4. 스레드2 : A 어그리게이트에 대한 선점 장금 시도
  - 위 순서에 따르면 스레드 1은 영원히 B 애그리거트에 대한 선점 잠금을 구할 수 없다. 스레드 2가 B 애그리거트에 대한 잠금을 이미 선점하고 있기 때문이다. 스레드 2도 마찬가지로 A 애그리거트에 대한 잠금을 구할 수 없다.
  - 즉, 스레드 1과 스레드 2는 교착 상태에 빠지게 된다.
- 이런 문제가 발생하지 않도록 하기 위해선 잠금을 구할 때 최대 대기 시간을 지정해야 한다.
- JPA에서 선점 잠금을 시도할 때 최대 대기 시간을 지정하려면 힌트를 사용한다.
```java
Map<String, Object> hints = new HashMap();
hits.put(javax.persistence.lock.timeout", 2000);

entiityManager.find(..., hints);
```

- Spring Data JPA는 @QueryHints 어노테이션을 사용해 쿼리 힌트를 지정할 수 있다.
```java
@QueryHints({
        @QueryHint(name = "javax.persistence.lock.timeout", value = "2000")
})
```

<br>

## 8.3 비선점 잠금(Optimistic Lock)
- 선점 잠금으로 모든 트랜잭션 충돌 문제가 해결되는 것은 아니다.
  1. 운영자는 배송을 위해 주문 정보를 조회한다. 시스템은 정보를 제공한다.
  2. 고객이 배송지 변경을 위해 변경 폼을 요청한다. 시스템은 변경 폼을 제공한다.
  3. 고객이 새로운 배송지를 입력하고 폼을 전송하여 배송지를 변경한다.
  4. 운영자가 1번에서 조회한 주문 정보를 기준으로 배송지를 정하고 배송 상태 변경을 요청한다.
  - 여기서 문제는 운영자가 배송지 정보를 조회하고 배송 상태로 변경하는 사이에 고객이 배송지를 변경한다는 것이다.
  - 이러한 문제는 선점 잠금 방식으로 해결할 수 없다. 
- 비선점 장금은 동시에 접근하는 것을 막는 대신 변경한 데이터를 실제 DBMS에 반영하는 시점에 변경 가능 여부를 확인하는 방식이다.
- 비선점 잠금을 구현하려면 애그리거트에 버전으로 사용할 숫자 타입 프로퍼티를 추가해야 한다.
  - 수정할 애그리거트와 매핑되는 테이블의 버전 값이 현재 애그리거트의 버전과 동일한 경우에만 데이터를 수정한다.
  - 수정에 성공하면 버전 값을 1 증가시킨다.
  - 다른 트랜잭션이 먼저 데이터를 수정해서 버전 값이 바뀌면 데이터 수정에 실패하게 된다.
- JPA는 버전을 이용한 비선점 잠근 기능을 지원한다.
```java
@Version
private Long version;
```
- JPA는 엔티티가 변경되어 UPDATE 쿼리를 실행할 때 @Version에 명시한 필드를 이용해서 비선점 쿼리를 실행한다. 
  - UPDATE order SET ..., version = version+1 WHERE number = ? and version = 10
- 응용 서비스는 버전에 대해 알 필요가 없다. 애그리거트 데이터가 변경되면 JPA는 트랜잭션 종료 시점에 비선점 잠금을 위한 쿼리를 실행한다.
- 비선점 잠금을 위한 쿼리를 실행할 때 쿼리 실행 결과로 수정된 행의 개수가 0이면 이미 누군가 앞서 데이터를 수정한 것이다.
  - 이는 트랜잭션이 충돌한 것이므로 트랜잭션 종료 시점에 익셉션이 발생한다. OptimisticLockingFailureException이 발생한다.
- 비선점 잠금 방식을 여러 트랜잭션으로 확장하려면 애그리거트 정보를 뷰로 보여줄 때 버전 정보도 함께 사용자 화면에 전달해야 한다.(hidden으로 숨김)
- 응용서비스에 전달할 요청 데이터는 사용자가 전송한 버전 값을 포함한다. 전달받은 버전 값을 이용해 애그리거트 버전과 일치하는지 확인하고, 일치하는 경우에만 기능을 수행한다.
  - VersionConflictException을 만들어 같지 않을 경우 예외를 던져주는 방법도 있다.
- VersionConflictException은 이미 누군가가 애그리거트를 수정했다는 것을 의미하고, OptimisticLockingFailureException은 누군가가 거의 동시에 애그리거트를 수정했다는 것을 의미한다.

### 강제 버전 증가
- 애그리거트에 애그리거트 루트 외에 다른 엔티티가 존재하는데 기능 실행 도중 루트가 아닌 다른 엔티티의 값만 변경할 때 JPA는 루트 엔티티의 버전 값을 증가시키지 않는다.
  - 이러한 JPA의 트깆ㅇ은 애그리거트 관점에서 보면 문제가 된다. 애그리거트의 구성요소 중 일부 값이 바뀌면 논리적으로 애그리거트는 바뀐 것이다. 
  - 따라서 애그리거트 내에 어떤 구성요소의 상태가 바뀌면 루트 애그리거트의 버전값이 증가해야 비선점 잠금이 올바르게 동작한다.
- JPA의 EntityManaver는 강제 버전 증가 잠금 모드를 지원한다.
  - entityManager.find(..., LockModeType(OPTIMISTIC_FORCE_INCREMENT))
- Spring Data JPA
  - @Lock(LockModeType.OPTIMISTIC_FORCE_INCREMENT)
- 강제 버전 증가를 사용하면 해당 엔티티의 상태가 변경되었는지에 상관없이 트랜잭션 종료 시점에 버전 값 증가를 처리한다.
- 이 잠금 모드를 사용하면 애그리거트 루트 엔티티가 아닌 다른 엔티티나 밸류가 변경되더라도 버전 값을 증가시킬 수 있으므로 비선점 잠금 기능을 안전하게 적용할 수 있다.

<br>

## 8.4 오프라인 선점 잠금(Offline Pessimistic Lock)
- 한 트랜잭션 범위에서만 적용되는 선점 잠금이나 나중에 버전 충동을 확인하는 비선점 잠금방식과 다르다.
- 오프라인 선점 잠금 방식은 여러 트랜잭션에 걸쳐 동시 변경을 막는다. 첫 번째 트랜잭션을 시작할 때 오프라인 잠금을 선점하고 마지막 트랜잭션에서 잠금을 해체한다.
- 오프라인 선점 방식은 잠금 유효 시간을 가져야 한다. 유효 시간이 지나면 자동으로 잠금을 해제해서 다른 사용자가 잠금을 일정 시간 후에 다시 구할 수 있도록 해야한다.
- 오르라인 선점 방식은 일정 주기로 유효 시간을 증가시키는 방식이 필요하다.(수정 폼에서 Ajax 호출을 통해 유효 시간을 1분씩 증가시키는 방법이 있다.)

## 오프라인 선점 잠금을 위한 LockManager 인터페이스와 관련 클래스
- 오프라인 선점 잠금은 크게 잠금 선점 시도, 잠금 확인, 잠금 해제, 잠금 유효시간 연장의 네 가지 기능이 필요하다.
- 책의 코드 참고

## DB를 이용한 LockManager 구현
- 책 코드 참고

<br>
<hr>
<br>

# Ch 09 : 도메인 모델과 바운디드 컨텍스트









