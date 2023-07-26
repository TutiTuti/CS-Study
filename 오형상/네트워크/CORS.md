# CORS (Cross-Origin Resource Sharing)

> *****추가 HTTP 헤더를 사용하여, 한 출처에서 실행 중인 웹 애플리케이션이 다른 출처의 선택한 자원에 접근할 수 있는 권한을 부여하도록 브라우저에 알려주는 체제*****
> 

### Orgin

**Protolcol 과 Host 그리고 Port 까지 모두 합친 URL**

![image](https://github.com/kj-cs-study/CS-Study/assets/110380812/81c6f569-7028-48ec-a696-f91e68f8f837)

### 동일 출처 정책 (SOP (Same-Orgin Policy))

- 동일한 출처에서만 리소스를 공유할 수 있다
- 동일 출처(Same-Origin) 서버에 있는 리소스는 자유로이 가져올수 있지만, 다른 출처(Cross-Origin) 서버에 있는 이미지나 유튜브 영상 같은 리소스는 상호작용이 불가능

### ****작동 방식 3가지****

**1️⃣ 예비 요청 (Preflight Request)**

![image](https://github.com/kj-cs-study/CS-Study/assets/110380812/a74c14a3-cb74-4a15-843f-b6a0a0621deb)

- 예비 요청을 보내 서버와 잘 통신되는지 확인한 후 본 요청을 보낸다.
- 브라우저가 예비요청을 보내는 것을 **Preflight**라고 부르며, 이 예비요청의 HTTP 메소드를 GET이나 POST가 아닌 **OPTIONS**라는 요청이 사용된다는 것이 특징이다.

**2️⃣ 단순 요청 (Simple Request)**

![image](https://github.com/kj-cs-study/CS-Study/assets/110380812/4618e425-3db8-4fa6-86f7-df6bcaa33c68)

- **예비 요청(Prefilght)을 생략하고 바로 서버에 직행으로 본 요청을 보낸** 후, 서버가 이에 대한 응답의 헤더에 Access-Control-Allow-Origin 헤더를 보내주면 **브라우저가 CORS정책 위반 여부를 검사**하는 방식

💡 **단순 요청 3가지 조건**

1️⃣ 요청의 메소드는 GET, HEAD, POST 중 하나여야 한다.

2️⃣ Accept, Accept-Language, Content-Language, Content-Type, DPR, Downlink, Save-Data, Viewport-Width, Width 헤더일 경우 에만 적용된다.

3️⃣ Content-Type 헤더가 application/x-www-form-urlencoded, multipart/form-data, text/plain중 하나여야한다. 아닐 경우 예비 요청으로 동작된다.

대부분 HTTP API 요청은 text/xml 이나 application/json 으로 통신하기 때문에 3번째 Content-Type이 위반 → **대부분의 API 요청은 그냥 예비 요청(preflight)으로 이루어진다** 

**3️⃣인증된 요청 (Credentialed Request)**

![image](https://github.com/kj-cs-study/CS-Study/assets/110380812/9c26bcc5-5944-461a-8299-d8a7670219f9)

- 클라이언트에서 서버에게 **자격 인증 정보(Credential)** 를 실어 요청할때 사용되는 요청이다.
- 클라이언트에서 일반적인 JSON 데이터 외에도 쿠키 같은 인증 정보를 포함해서 다른 출처의 서버로 전달할때 CORS의 세가지 요청중 하나인 인증된 요청으로 동작된다는 말이며, 이는 기존의 단순 요청이나 예비 요청과는 살짝 다른 인증 형태로 통신하게 된다.
