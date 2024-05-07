# REST API-POST

post 방식은 디폴트로 객체를 사용해서 받아야 한다.

```java
package com.example.restapi.model;

import com.fasterxml.jackson.databind.PropertyNamingStrategies;
import com.fasterxml.jackson.databind.annotation.JsonNaming;
import lombok.AllArgsConstructor;
import lombok.Data;
import lombok.NoArgsConstructor;
// post json 을 스네이크 형태로 받겠다
@JsonNaming(PropertyNamingStrategies.SnakeCaseStrategy.class)

@AllArgsConstructor
@Data
@NoArgsConstructor
public class UserRequest {
    private String name;
    private String phoneNum;
    private String email;
    private Integer userAge;
}

```

```java
package com.example.restapi.controller;

import com.example.restapi.model.BookRequest;
import com.example.restapi.model.UserRequest;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
@RequestMapping("/api")
public class PostApiController {

    // http://localhost:8080/api/post
    @PostMapping("/post")
    public String post(
            @RequestBody BookRequest bookRequest //바디는 디폴트로 JSON
            ){
        System.out.println("posted object: " + bookRequest);
        return bookRequest.toString();
    }

    @PostMapping("/post-user")
    public UserRequest postUser(
            @RequestBody UserRequest userRequest
    ){
        System.out.println("posted object: " + userRequest);
        return userRequest;
    }
}

```