# JWT 란 ?
Json Web Token의 약자로 JSON 포캣을 이용하여 사용자에 대한 속성을 저장하는  Claim 기반의 Web Token이다.    
JWT는 토큰 자체로 사용하는 Self-Contained 방식으로 정보를 안전하게 전달한다. 주로 회원 인증이나 정보 전달에 사용되는   
JWT는 아래의 로직을 따라서 처리된다.

![image](https://github.com/kj-cs-study/CS-Study/assets/37789623/4de7558e-cffd-480e-a42b-87f2a054a758)

## JWT의 구조
JWT는  Header, Payload, Signature 3부분으로 이루어지며, JSON 형태인 Base64Url로 인코딩되어 표현된다.   
각각의 부분을 . 구분자를 이용하여 이어준다.

### Header
헤더는 typ과 alg 두 가지 정보로 구성된다.   
alg는 Signature를 해싱하기 위한 알고리즘을 지정하는 것이다.
typ은 토큰의 타입을 지정한다. ex) JWT

### Payload
토큰의 페이로드에는 토큰에서 사용할 정보의 조각들인 클레임(Claim)이 담겨있다.
클레임은 3가지로 나누어지며, JSON(Key,Value)형태로 다수의 정보를 넣을 수 있다.
#### 등록된 클레임 ( Registered Claim )
토큰 정보를 표현하기 위해 이미 정해진 종류의 데이터들로 선택적 작성이 가능하며 사용할 것을 권장한다.   
간결하게 하기 위해 Key는 모두 길이3 String이며 subject로는 unique한 값을 사용하는데 사용자 메일을 주로 사용한다.   
iss : 토큰발급자(issuer)   
sub : 토큰 제목(subject)   
aud : 토큰 대상자(audience)   
exp : 토큰 만료 시간(expiration), NumericDate형식으로 되야함( 1480849147370 )   
nbf : 토큰 활성 날자(not before), 이 날이 지나기 전의 토큰은 활성화되지 않음
iat : 토큰 발급 시간(issued at), 토큰 발급 이후의 경과 시간을 알 수있음.
jti : JWT 토큰 식별자(JWT ID), 중복 방지를 위해 사용하며, 일회용 토큰(Access Token)등에 사용

#### 공개 클레임 ( Public Claim )
사용자 정의 클레임으로, 공개용 정보를 위해 사용된다. 충돌 방지를 위해 URL 포맷을 이용한다.
```
{ 
    "https://mangkyu.tistory.com": true
}
```

#### 비공개 클레임 ( Private Claim )
사용자 정의 클레임으로, 서버와 클라이언트 사이에 임의로 지정한 정보를 저장한다.
```
{ 
    "token_type": access 
}
```

### Signature
토큰을 인코딩하거나 유효성 검증을 할 때 사용하는 고유한 암호화 코드이다.   
서명은 위에서 만든 Header, Payload의 값을 각각 BASE64Url로 인코딩하고, 인코딩 값을 비밀 키를 이용해 Header에서 정의한 알고리즘으로   
해싱을 하고, 이 값을 다시 BASE64Url로 인코딩하여 생성한다.


생성된 토큰은 HTTP통신을 할 때 Authorization이라는 key의 value로 사용된다.    
일반적으로 value이는 Bearer이 앞에 붙여진다.
```
{ 
    "Authorization": "Bearer {생성된 토큰 값}",
 }
```
## JWT 단점 및 고려할 점
Self-contained : 토큰 자체에 정보를 담고 있으므로 양날의 검이 될 수 있다.   
토큰 길이 : 토큰의 페이로드에 3종류의 클레임을 저장하기 때문에, 정보가 많아질수록 토큰의 길이가 늘어나 네트워크에 부하를 줄 수 있다.   
Payload 인코딩 : Payload자체는 암호화가 아니라 인코딩 된 것이므로 중간에 탈취하여 디코딩하면 정보를 볼 수 있으므로   
                 JWE로 암호화하거나 Payload에 중요 데이터를 넣지 않아야 한다.    
Stateless : JWT상태를 저장하지 않기 때문에 한번 만들어지면 제어가 불가능하다 임의로 삭제가 안되므로 토큰 만료시간을 꼭 넣어야 한다.   
Store Token : 토큰은 클라이언트 측에서 관리해야 하기 때문에, 토큰을 저장해야 한다.
