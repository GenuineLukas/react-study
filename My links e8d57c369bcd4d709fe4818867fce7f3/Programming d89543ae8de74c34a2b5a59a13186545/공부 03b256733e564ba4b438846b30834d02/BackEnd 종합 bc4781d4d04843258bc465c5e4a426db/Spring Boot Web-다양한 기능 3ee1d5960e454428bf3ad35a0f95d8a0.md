# Spring Boot Web-다양한 기능

| String  | 일반 Text Type응답  |
| --- | --- |
| Object | 자동으로 Json변환되어 응답
상태값은 항상 200 OK |
| ResponseEntity | Body의 내용을 Object로 설정
상황에 따라서 HttpsStatus Code설정
- 예외 처리 해줄 때 주로 쓰인다. |
| @ResponseBody | RestController가 아닌곳(Controller)에서 Json 응답을 내릴 때 |

```java
package com.example.restapi.controller;

import com.example.restapi.model.UserRequest;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController //Rest API로 동작하겠다 == 응답값이 json으로 내려가겠다라는 선언
//@Controller -> html을 리턴 만약 json 객체를 내리고 싶으면 @GetMapping 위나 아래에 @ResponseBody를 해줘야 됌
@RequestMapping("/api/v1")
public class ResponseApiController {
    private static final Logger log = LoggerFactory.getLogger(ResponseApiController.class);

    @GetMapping("/method1")
    //RequestMapping(path  = "", method = RequestMethod.GET) 뒤에  메소드 없으면 모두에게 동작
    public UserRequest user(){
        var user = new UserRequest();
        user.setName("홍길동");
        user.setUserAge(21);

        return user;
    }

    @GetMapping("/method2")
     public String userStr(){
        var user = new UserRequest();
        user.setName("홍길동");
        user.setUserAge(32);

        log.info("user: {}", user);
        return user.toString();
    }

    @GetMapping("/method3")
    public ResponseEntity<UserRequest> userResponseEntity(){
        var user = new UserRequest();
        user.setName("홍길동");
        user.setUserAge(32);
        user.setEmail("nalkdjsf@gmail.com");

        return ResponseEntity
                .status(HttpStatus.CREATED)
                .header("x-custom", "hi") //optional
                .body(user);
    }
}

```

### Object Mapper

![Untitled](Spring%20Boot%20Web-%E1%84%83%E1%85%A1%E1%84%8B%E1%85%A3%E1%86%BC%E1%84%92%E1%85%A1%E1%86%AB%20%E1%84%80%E1%85%B5%E1%84%82%E1%85%B3%E1%86%BC%203ee1d5960e454428bf3ad35a0f95d8a0/Untitled.jpeg)

UserRequest에서 @Data 지우고 

테스트에서 

```java
var json = objectMapper.writeValueAsString(user);
		System.out.println(json);
```

이거 돌려보면 그저 {} 빈 비열이 나타나게 되는데 그 이유는 오브젝트 매퍼가 동작하는 방식은 변수에 매칭되는게 아닌 메소드에 매칭이 된다.

UserReqeust에 가서 어줍잖게

```java
public String name(){
	return this.name;
}
public int age(){
	return this.age;
}
```

이런식의 네이밍으로 해주면 당연히 계속 빈 배열이 직렬화 될것이다.

올바른 네이밍, 즉 get으로 시작하는 네이밍으로 코드를 작성해야 제대로 동작한다. 그런데 get뒤에 나오는 부분에 따라서 json으로 변환했을 때의 키값이 달라지기 때문에 이 부분도 조심해야 한다… 그냐 lombak 쓰자..^^

1. 만약 UserRequest 에 get으로 시작하는 메서드를 만들어 놓고 그 내용이 json으로 직렬화되길 원치 않는다면 @jsonIgnore 를 해주면 된다.

```java
@JsonIgnore
public Stirng getUser() {
	return userName;
}
```

1. 또한 json 객체로 직렬화 됐을 때의 이름을 지정해주고 싶으면 @JsonProperty를 해주면 된다.
    
    ```java
    @JsonProperty("user_email")
    private String email;
    ```
    

역직렬화의 경우 Json 객체를 자바 객체로 변환 하는데 이 과정에서는 변수 이름이 통일 되어 있다는 가정 하에 Setter 나 Getter 둘 중에 하나만 있으면 동작한다. (이건 역질렬화만의 예이고 set으로 시작하는 메서드를 기반으로 진행된다고 보는게 편하다). read value, 즉, json을 dto로 바꿀 때는 setter 메서드를 참고하는데 setter 메서드가 없다면 getter 메소드를 통해서도 세팅이 가능하다.

그런데 json 상에서 이름이 바꼈고 그 바뀐 이름으로 역직렬화에 동참하고 싶다면 

```java
public void setUserName(String name){
		this.userName = name;
}
```

이렇게 해주면 되긴 하는데 그냥 lombak 쓰고  @Data 붙이자.

1. 굳이 getter와 setter를 쓰고 싶지 않다면
    
    @JsonProperty 를 통해 직렬화와 역직렬화가 가능하다.
    
    ```java
    @JsonProperty
    private String userName;
    
    @JsonProperty
    private Integer userAge;
    
    @JsonProperty
    private String email;
    ...
    ```