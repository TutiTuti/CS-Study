# OAuth란 ? 
인터넷 사용자들이 비밀번호를 제공하지 않고 다른 웹사이트 상의 자신의 정보에 대해 웹사이트나 애플리케이션의 접근권한을   
부여할 수 있는 공통적인 수단으로서 사용되는, 접근 위임을 위한 개방형 표준이다.

## OAuth의 구성요소
|구분|설명|
|---|------|
|Resource Owner|웹 서비스를 사용하려는 유저|
|Client|자사 또는 개인이 만든 애플리케이션 서버|
|Authorization Server|권한을 부여해주는 서버|
|Resource Server|사용자의 개인정보를 가지고있는 애플리케이션 서버|
|Access Token|자원에 대한 접근 권한을 Resource Owner가 인가하였음을 나타내는 자격증명|
|Refresh Token|Client는 Authorization Server로 부터 accessToken과RefreshToken을 함께 부여받는다.|

![image](https://github.com/kj-cs-study/CS-Study/assets/37789623/a069c062-43fe-4f10-b048-11920b6ea4fb)
