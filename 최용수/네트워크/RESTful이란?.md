## REST ( Representational State Transfer ) 이란?
웹에서 데이터를 전송하고 처리하는 방법을 정의한 인터페이스를 말한다.   
모든 데이터 구조와 처리방식은 REST에서 URL을 통해 정의 된다.   

HTTP URL ( Uniform Resource Identifier )를 통해 자원(Resource)을 명시하고 ,HTTP Method(POST,GET,PUT,DELETE)를 통해     
자원에 대한 CRUD Operation을 적용하는 것을 의미한다.     
REST는 자원 기반의 구조(ROA, Resource, Oriented Architecture)설계의 중심에 Resource가 있고 HTTP Method를 통해    
Resource를 처리하도록 설계된 아키텍쳐를 의미한다. 웹사이트의 이미지,텍스트,DB 등 모든 자원에 고유한 ID인 HTTP URL를 부여한다.    
즉, 자원을 이름으로 구분하여 해당 자원의 상태를 주고 받는 모든것을 의미한다.  

### REST 특징
 - Uniform : HTTP표준에만 따른다면, 안드로이드/IOS 플랫폼이든, 특정언어나 기술에 종속되지 않고 모든 플랫폼에 사용할 수 있으며    
              URL로 지정한 리소스에 대한 조작이 가능한 아키텍쳐 스타일을 의미한다.
 - Stateless(무상태성) : 작업을 위한 상태정보를 따로 저장하고 관리하지 않는다.      
 - Cacheable(캐시가능) : HTTP라는 기존 웹 표준을 그대로 사용하기 때문에, 웹에서 사용하는 기존 인프라를 그대로 활용할 수 있다.    
 - Self-descriptiveness(자체표현구조) : REST API메시지만 보고도 이를 쉽게 이해할 수 있는 자체 표현 구조로 되어 있다.
 - Client-Server구조 :  REST서버는 API제공, 클라이언트는 사용자 인증이나 컨텍스트등을 직접 관리하는 구조로 각각    
              구분되기 때문에 클라이언트나 서버에서 개발해야할 내용이 명확해지고 서로 간 의존성이 줄어 들게 된다.    


### REST 장점
1. 쉬운사용 
  HTTP프로토콜의 인프라를 그대로 사용하므로 REST API사용을 위한 인프라 구축이 필요없다.
2. Client-Server역활의 명확한 분리 
  Client는 REST API를 통해 서버와 정보를 주고 받는다. REST의 특징인 Stateless에 따라 서버는 클라이언트의 Context를 유지할 필요가 없다.
3. 특정 데이터 표현을 사용가능
  REST API는 헤더 부분에 URI처리 메소드를 명시하고 필요한 실제 데이터를 "body"에 표현할 수 있도록 분리 시켰다.
4. 범용성
  HTTP 표준 프로토콜에 따르는 모든 플랫폼에서 사용이 가능하다.
  
### REST 단점
- 표준 자체가 존재하지 않아 정의가 필요하다.    
- 사용할 수 있는 메소드가 4가지 뿐이다.    
- 브라우저를 통해 테스트할 일이 많은 서비스라면 쉽게 고칠 수 있는 URL보다 Header 정보 값을 처리해야 하므로 전문성이 요구된다.    
- 구형 브라우저에서 호환이 되지 않아 지원해주지 못하는 동작이 많다.    

## RESTful 이란?
일반적으로 REST라는 아키텍처를 구현하는 웹 서비스를 나타내기 위해 사용되는 용어이다.    
REST API를 제공하는 웹 서비스를 RESTful 하다고 할 수 있다.    
### RESTful의 목적
- 이해하기 쉽고 사용하기 쉬운 REST API를 만드는 것   
- RESTful한 API를 구현하는 목적은 성능향상이 아니라 일관적인 컨벤션을 통한 API의 이해도 및 호환성을 높이는 것이 주동기이며    
성능이 중요한 상황에서는 굳이 RESTful한 API를 구현할 필요가 없다.
### RESTful하지 못한 경우
- CRUD 기능을 모드 POST로만 처리하는 API
- route에 resource, id외에 정보가 들어가는 경우

