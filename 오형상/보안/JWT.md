
## JWT(JSON Web Token)

### 개념

✔️ **인증에 필요한 정보들을 암호화시킨 JSON 토큰**

✔️ JWT는 JSON 데이터를 **Base64 URL-safe Encode** 를 통해 인코딩하여 직렬화한 것이며, 토큰 내부에는 위변조 방지를 위해 개인키를 통한 **전자서명**도 들어있다.

### 구조

✔️ JWT는 **.** 을 구분자로 나누어지는 세 가지 문자열의 조합이다.

✔️ **.**을 기준으로 좌측부터 **Header**, **Payload**, **Signature**를 의미한다.

![image](https://user-images.githubusercontent.com/110380812/236996253-3c37d69d-c6d9-40b2-82c9-a1d72fccfdc6.png)

**Header**

✔️ JWT 에서 사용할 타입과 해시 알고리즘의 종류가 담겨있다.

```json
{
	"alg":"HS256", // 서명 암호화 알고리즘
	"typ":"JWT" // 토큰 유형
}
```

**Payload**

✔️ 서버와 클라이언트가 주고받는 시스템에서 실제로 **사용될 정보에 대한 내용**을 담고 있는 섹션

```json
{
	"sub":"1234"
	"name":"konger",
}
```

**Signature**

✔️ Header, Payload 를 Base64 URL-safe Encode 를 한 이후 Header 에 명시된 해시함수를 적용하고, 개인키(Private Key)로 서명한 전자서명이 담겨있다.
