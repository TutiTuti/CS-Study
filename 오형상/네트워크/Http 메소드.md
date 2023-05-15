## Http 메소드

### 1️⃣ Get


> 💡 Get은 보통 리소스를 조회할 때 사용하며, 서버에 전달하고 싶은 데이터는 query를 통해서 전달한다. 메시지 바디를 사용해서 데이터를 전달할 수 있지만, 지원하지 않는 곳이 많아서 권장하지 않는다.


### Get메서드의 속성

1️⃣ 안전

- 계속해서 호출해도 리소스를 변경하지 않는다.

2️⃣ 멱등

- 메소드를 계속 호출해도 결과가 똑같다.

3️⃣ 캐시가능

- 캐싱을 해서 데이터를 효율적으로 가져올 수 있다.

### Get 메서드 구현

> **@PathVariable**
중괄호 안에 전달할 값을 받습니다.
예시) http://localhost:8080/api/v1/get-api/variable2/값
> 

```java
@GetMapping("/variable2/{variable}")
    public String getVariable2(@PathVariable String variable) {
        return variable;
    }
```

> **@RequestParam**
?뒤로 전달할 값을 id=value 형태로 받습니다.
예시)
http://localhost:8080/api/v1/get-api/variable2?name=junha&email=okokok@mail&organization=test
> 

```java
@GetMapping("/request1")
    public String getVariable3(@RequestParam String name,
                               @RequestParam String email,
                               @RequestParam String organization) {
        return String.format("%s %s %s", name, email, organization);
    }
```

> **@PathVariable VS @RequestParam
@PathVariable**은 RESTful 방식이며 Rest 통신할 때 쓰입니다.
RESTful 방식에 맞게 좀 더 직관적입니다.

**@RequestParam**은 쿼리 스트링이라 부르며 Get방식의 통신을 할 때 주로 쓰입니다.
null값이 허용되며, 키:밸류 값으로 보낼 수 있습니다.
상황에 맞게 사용하면 됩니다.
> 

### DTO 객체를 활용한 Get 메서드 구현

> **DTO란?
Data Transfer Object**의 약자로, 다른 레이어 간의 데이터 교환에 활용됩니다. 각 클래스 및 인터페이스를 호출하면서 전달하는 매개변수로 사용되는 데이터 객체입니다.
> 

```java
public class MemberDto {
    private String name;
    private String email;
    private String organization;
		...
		//생성자, getter 생략
		...

		@Override
    public String toString(){
        return String.format("%s %s %s", this.name, this.email, this.organization);
    }
}
```

```java
@GetMapping("/request2")
    public String getVariable4(@RequestParam
                               Map<String, String> param) {
        param.entrySet().forEach(
                (map) -> {
                    System.out.printf("key:%s value:%s\n", map.getKey(), map.getValue());
                }
        );
        return "호출완료";
    }
```

### 2️⃣ Post

> POST 메소드는 주로 새로운 리소스를 생성(create)할 때 사용
> 

### @RequestBody

> HttpRequest의 RequestBody 내용을 자바 객체로 매핑하는 역할
> 

👀참고) 해당하는 어노테이션이 붙어있는 메서드로 클라이언트의 요청이 들어왔을 때, **DispatcherServlet**에서는 먼저 해당 HttpRequest의 미디어 타입을 확인하고, 타입에 맞는 MessageConverter를 통해 요청 본문인 requestBody를 통째로 변환해서 메서드로 전달

### @RequestBody를 활용한 POST 메서드 구현 (Map)

`Map` 객체는 `요청을 통해 어떤 값이 들어오게 될지 특정하기 어려울 때` 사용

```java
import org.springframework.web.bind.annotation.*;

import java.util.Map;

@RestController
@RequestMapping("/api/v1/post-api") // 공통 부분 분리
public class PostController {

    @PostMapping("/member")
    public String postMember(@RequestBody Map<String, Object> postData) {
		// Http body의 내용을 Map 객체에 매핑
        StringBuilder sb = new StringBuilder();
        postData.entrySet().forEach(map -> {
            sb.append(map.getKey() + " : " + sb.append(map.getValue()) + "\n");
        });
        return sb.toString();
    }
```

- Talend API Tester를 이용한 테스트
    
    ![Untitled](https://github.com/kj-cs-study/CS-Study/assets/110380812/f36dc725-83e5-4c55-8d83-adcf85f25d02)

    ![Untitled](https://github.com/kj-cs-study/CS-Study/assets/110380812/9d24d163-6711-4753-a5ed-6e88bc78d2e4)
    

### @RequestBody를 활용한 POST 메서드 구현 (DTO)

```java
import com.springboot.hello.domain.dto.MemberDto;
import org.springframework.web.bind.annotation.*;

@RestController
@RequestMapping("/api/v1/post-api")
public class PostController {
    
    @PostMapping("/member2")
    public String postMemberDto(@RequestBody MemberDto memberDto) {
		// Http body의 내용을 MemberDto 객체에 매핑
        return memberDto.toString();
    }
}
```

- Talend API Tester를 이용한 테스트 ( 정상 )

    ![Untitled](https://github.com/kj-cs-study/CS-Study/assets/110380812/649a120d-213c-4127-ad60-d2210c27c0b5)

    ![Untitled1](https://github.com/kj-cs-study/CS-Study/assets/110380812/3642d614-5d09-4d0b-ad74-c0ebf07a8a73)

    
- Talend API Tester를 이용한 테스트 ( MemberDto에 없는 값을 넣는다면 ❓)
    
    ![Untitled2](https://github.com/kj-cs-study/CS-Study/assets/110380812/773b02bf-91be-44e6-b5ef-54a7331138ef)

    ![Untitled3](https://github.com/kj-cs-study/CS-Study/assets/110380812/7adb0bae-4bcd-4210-ac26-5721b1f3824f)

    `name만 정상적으로 들어가고 나머지는 null로 들어간다.`
    

### 👀참고) @RestController 대신 @Controller를 사용하면 안되나 ❓


> 💡 @RestController는 @Controller에 @ResponseBody가 결합된 어노테이션


✔️ @ResponseBody `자바 객체를 HttpResponse의 responseBody 내용으로 매핑하는 역할`을 합니다.

✔️ @ResponseBody는 return Type에 맞는 MessageConverter를 통해 return 하는 객체를 해당 타입으로 변환해서 클라이언트로 전달

따라서 `@Controller를 사용하려면 아래와 같이 @ResponseBody를 붙여줘야한다.`

```java
import com.springboot.hello.domain.dto.MemberDto;
import org.springframework.web.bind.annotation.*;

@Controller
@RequestMapping("/api/v1/post-api")
public class PostController {
    
    @PostMapping("/member2")
	  public @ResponseBody String postMemberDto(@RequestBody MemberDto memberDto) {
		// Http body의 내용을 MemberDto 객체에 매핑
        return memberDto.toString();
    }
}
```

👀 [https://mangkyu.tistory.com/49](https://mangkyu.tistory.com/49) ( @Controller와 @RestController 차이 )

👀 [https://wildeveloperetrain.tistory.com/144](https://wildeveloperetrain.tistory.com/144) ( @RequestBody @ResponseBody )

---

### Get vs Post

![Untitled](https://github.com/kj-cs-study/CS-Study/assets/110380812/2edec85f-03fc-4046-8547-d43d88d4dcf7)


- **사용목적** : GET은 서버의 리소스에서 데이터를 요청할 때, POST는 서버의 리소스를 새로 생성하거나 업데이트할 때 사용한다.
- DB로 따지면 GET은 SELECT 에 가깝고, POST는 Create 에 가깝다고 보면 된다.
- **요청에 body 유무** : GET 은 URL 파라미터에 요청하는 데이터를 담아 보내기 때문에 HTTP 메시지에 body가 없다. POST 는 body 에 데이터를 담아 보내기 때문에 당연히 HTTP 메시지에 body가 존재한다.
- **멱등성 (idempotent)** : GET 요청은 멱등이며, POST는 멱등이 아니다.
- GET은 idempotent하기 때문에 캐시가 되고 POST는 idempotent하지 않기 때문에 캐시가 되지 않는다.

### 3️⃣ Put

> 웹 애플리케이션 서버를 통해 DB 등에 존재하는 리소스 값을 업데이트하는데 사용
> 

### PUT vs POST

| PUT | POST |
| --- | --- |
| 해당 리소스의 값 전체를 교체 | 해당 리소스의 값 일부만 교체 |
| 만약 전체가 아닌 일부만 전달할 경우, 전달한 필드외 모두 null or 초기값 처리된다 | 일부의 필드를 수정하는 용도로 쓰인다 |

```java
@RestController
@RequestMapping("/api/v1/put-api")
public class PutController {

// @RequestBody 와 Map 을 활용한 PUT 메서드 구현
    @PutMapping(value = "/member")
    public String putMember(@RequestBody Map<String, Object> putData) {
        StringBuilder sb = new StringBuilder();

        putData.entrySet().forEach(map -> {
            sb.append(map.getKey() + " : " + map.getValue() + "\n");
        });

        return sb.toString();
    }

    // DTO 객체를 활용한 PUT 메서드 구현
    @PutMapping(value = "/member1")
    public String postMemberDto1(@RequestBody MemberDto memberDto) {
        return memberDto.toString();
    }

    @PutMapping(value = "/member2")
    public MemberDto postMemberDto2(@RequestBody MemberDto memberDto) {
        return memberDto;
    }

    // ResponseEntity 를 활용한 PUT 메서드 구현
    @PutMapping(value = "/member3")
    public ResponseEntity<MemberDto> postMemberDto3(@RequestBody MemberDto memberDto) {
        return ResponseEntity
                .status(HttpStatus.ACCEPTED)
                .body(memberDto);
    }
}
```

### 4️⃣ Patch

> PUT과 유사하게 요청된 자원을 수정(UPDATE)할 때 사용
해당자원의 일부를 교체하는 의미로 사용
> 

```java
@RestController
@RequestMapping("/api/v1/patch-api")
public class PatchController {
	
	// DTO 객체를 활용한 PATCH 메서드 구현
    @PatchMapping("/{variable}")
    public String postMemberDto1(@PathVariable Long id, @RequestBody MemberDto memberDto) {
        return memberDto.toString();
	}
}
```

### Put vs Patch

| PUT | PATCH |
| --- | --- |
| 해당 리소스의 값 전체를 교체 | 해당 리소스의 값 일부만 교체 |
| 만약 전체가 아닌 일부만 전달할 경우, 전달한 필드외 모두 null or 초기값 처리된다 | 일부의 필드를 수정하는 용도로 쓰인다 |
| 멱등하다 | 멱등하지 않다. |

### 5️⃣Delete

> 웹 애플리케이션 서버를 통해 DB 등에 존재하는 리소스 값을 삭제하는데 사용
> 

```java
@RestController
@RequestMapping("/api/v1/delete-api")
public class DeleteController {

    // @PathVariable 과 @RequestParam 을 활용한 DELETE 메서드 구현
    @DeleteMapping(value = "/{variable}")
    public String DeleteVariable(@PathVariable String variable) {
        return variable;
    }

    // @RequestParam 을 활용한 DELETE 메서드 구현
    @DeleteMapping(value = "/request")
    public String getRequestParam1(@RequestParam String email) {
        return "e-mail : " + email;
    }
}
```

> 위 예제는 삭제 기능이 결여되어 있으며, 실제 메서드 코드는 데이터 삭제와 NULL 예외처리가 반드시 병행되어야 한다
>
