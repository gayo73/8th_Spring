## DI
    
DI (Dependency Injection : 의존성 주입)은 spring 프레임워크가 제공하는 3가지 핵심 프로그래밍 모델 중 하나이다. 외부에서 두 객체 간의 관계를 결정해주는 디자인 패턴으로, 인터페이스를 사이에 둬서 클래스 레벨에서는 의존관계가 고정되지 않도록 하고 런타임 시에 관계를 동적으로 주입하여 유연성을 확보하고 결합도를 낮출 수 있게 해준다는 특징을 갖고 있다.
    
- 의존성 : 한 객체가 다른 객체를 사용할 때 의존성이 있다고 말함
        
![의존성 주입 : 두 객체 간의 관계를 맺어줌](%EC%9D%98%EC%A1%B4%EC%84%B1%EC%A3%BC%EC%9E%85.png)
        
의존성 주입 : 두 객체 간의 관계를 맺어줌
        
- 의존성 주입이 필요한 이유?
    - 강하게 결합 되어있을 때
            
        ```cpp
        public class Store {
            
            private Pencil pencil;
            
            public Store() {
                    this.pencil = new Pencil();
            }
            
        }
        ```
            
        두 클래스가 강하게 결합되어 있어서 만약 Store에서 Pencil이 아닌 Food와 같은 다른 상품을 판매하고자 한다면 Store 클래스의 생성자에 변경이 필요하다. 
            
    - 객체들 관의 관계가 아닌, 클래스 간의 관계가 맺어지게 됨
            
        올바른 객체지향적 설계라면 객체들 간에 관계가 맺어져야 한다. 객체들 간에 관계가 맺어졌다면 다른 객체의 구체 클래스(Pencil인지 Food 인지 등)를 전혀 알지 못하더라도, (해당 클래스가 인터페이스를 구현했다면) 인터페이스의 타입(Product)으로 사용할 수 있다.
            
        
    ```cpp
    public interface Product {}
    public class Pencil implements Product {} // pencil에서 product 인터페이스 구현
        
    public class Store {
        private Product product;
        public Store(Product product) {
                this.product = product;
        }
    }
        
    public class BeanFactory {
        public void store() {
            // Bean의 생성
            Product pencil = new Pencil();
            // 의존성 주입
            Store store = new Store(pencil);
        }
    }
    ```
        
    
특징
    
- 두 객체 간의 관계라는 관심사의 분리
- 두 객체 간의 결합도를 낮춤
- 객체의 유연성을 높임
- 테스트 작성을 용이하게 함

## IoC
    
IoC(Inversion of Control : 제어의 역전)은 말 그대로 개발자가 제어해야할 요소들을 Spring Framework 에서 대신 제어해주는 것을 뜻한다.
    
- IoC 컨테이너 (=spring 컨테이너)
    : 스프링 프레임워크에서 객체 생성 및 소멸 (생명주기)관리, 의존성을 관리를 해주는 컨테이너
        
    - 빈(Bean) : 스프링 컨테이너가 관리하는 객체
    - 빈 팩토리(BeanFactory) : 이 빈들을 관리한다는 의미로 컨테이너
- 특징
    - IoC 컨테이너가 객체의 생성을 책임지고, 의존성을 관리
    - POJO의 생성, 초기화, 서비스, 소멸에 대한 권한을 가짐
        - POJO(Plain Old Java Object)
        : 주로 특정 자바 모델이나 기능, 프레임워크를 따르지 않는 Java Object를 지칭
    - 개발자들이 직접 POJO를 생성할 수 있지만 컨테이너에게 맡김
    - 개발자는 비즈니스 로직에 집중할 수 있음
    
DI는 IoC의 구현 방법 중 하나로, 제어의 역전 원칙을 따라 객체의 의존성을 외부에서 주입받는 패턴이다. IoC가 코드 흐름의 주체를 외부에 두는 것을 의미한다면, DI는 이 원칙을 구체적으로 구현한 것이다.
    
## 프레임워크와 API의 차이
    
프레임워크와 API는 모두 개발자가 애플리케이션을 쉽게 구축하도록 돕는 도구지만, 사용 방식과 개념이 다르다.
    
- 프레임워크는 애플리케이션의 전체 구조를 정의하며, 프로그램의 흐름을 제어하는 방식으로 동작한다.
        
    즉, 특정 문제 해결을 위한 상호작용하는 클래스와 인터페이스의 집합으로, 개발자는 프레임워크의 구조에 따라 코드를 작성하게 된다. 
        
    ex) Spring Framework와 같은 서버 개발용 프레임워크
        
- API는 소프트웨어 컴포넌트 간에 기능을 제공하기 위한 정의와 프로토콜의 집합이다.
        
    프레임워크와는 달리, API는 특정 기능에 대한 인터페이스를 제공할 뿐 프로그램의 구조나 흐름에는 영향을 주지 않는다. 
        
    ex) Google Maps API는 지도 데이터를 요청하고, 요청에 따른 위치 정보를 반환하는 특정 기능을 제공
        
    
프레임워크는 프로그램의 흐름과 구조를 제어하며 개발자가 그 안에서 필요한 코드를 작성한다. API는 개별적인 기능에 대한 인터페이스를 제공하여 특정 작업을 수행할 수 있게 하되 프로그램의 흐름을 제어하지는 않는다.
    
## AOP
    
AOP (Aspect-Oriented Programming : 관점 지향 프로그래밍)는 특정 기능이 여러 모듈에서 공통적으로 요구될 때 이를 모듈화하여 필요할 때마다 쉽게 사용할 수 있도록 하는 방식을 말한다. 
    
어떤 로직을 기준으로 핵심적인 관점, 부가적인 관점으로 나누어서 보고 그 관점을 기준으로 나눌 수 있다.
    
ex) 핵심적인 관점 - 핵심 비즈니스 로직 / 부가적인 관점 - 핵심 로직을 실행하기 위해 행해지는 DB 연결, 로깅, 파일 입출력 등
    
- AOP의 주요 개념
    - Aspect : 공통적인 관심사를 모듈화한 구성 요소로, 예를 들어 보안 검증이나 로그 기록을 Aspect로 구현하여 코드 곳곳에서 재사용할 수 있다.
    - Join Point : Aspect가 적용될 수 있는 구체적인 실행 시점으로, 메서드 실행 전후, 생성자 호출 시점 등이 여기에 해당한다.
    - Advice : Join Point에서 실제로 수행될 동작을 정의한 구현체로, 메서드 실행 전후에 실행할 로직이 여기에 포함된다.
    - Pointcut : Join Point를 세밀하게 지정하는 조건으로, 특정 메서드 진입 시점에 Advice가 실행될 수 있도록 구체적으로 설정할 수 있다.
    - Weaving : AOP 기능을 실제 코드에 적용하는 과정으로, 프록시 객체를 생성하거나 컴파일 시점에 적용할 수 있다.
- 스프링 AOP 특징
    - 프록시 객체를 사용해 원래 객체를 감싸는 방식으로 적용
    - 프록시 객체는 실제 객체와 동일한 타입을 가지며, 메서드 호출이 발생할 때 원래 객체가 아닌 프록시 객체가 이를 처리하여 부가 기능을 수행
    - 스프링 IoC 컨테이너와 결합해 엔터프라이즈 애플리케이션의 관점 지향 요구사항을 효과적으로 처리

## 서블릿
    
서블릿(Servlet)은 웹 애플리케이션에서 클라이언트 요청을 받아 처리하고, 그 결과를 반환하는 자바 기반 기술이다. JSP와 같은 웹 기술과 함께 서버 사이드 애플리케이션을 구축하는 데 자주 사용된다. 클라이언트의 요청을 처리하는 작은 프로그램으로, HTML에 자바 코드를 삽입하는 방식으로 동적 웹 페이지를 생성할 수 있다.
    
- 특징
    - 웹 서버 상에서 실행 : 클라이언트 요청을 웹 서버(WAS)가 서블릿으로 전달하고, 서블릿은 이를 처리하여 결과를 반환
    - 멀티스레드 기반 : 서버는 각 클라이언트 요청을 개별 스레드로 처리하여 성능을 향상 시킴
    - MVC 패턴에서 Controller 역할 수행 : 사용자 요청을 받아 로직을 처리하고, 그 결과를 View에 전달
    
서블릿은 웹 서버와 클라이언트 간의 동적인 데이터를 처리할 때 (ex. 로그인 과정에서 유저의 정보 검증 후 응답 처리) 필수적이며, 주로 컨트롤러 역할을 수행하여 비즈니스 로직과 응답 처리를 담당한다.

## 실습인증
![실습인증.png](%EC%8B%A4%EC%8A%B5%EC%9D%B8%EC%A6%9D.png)