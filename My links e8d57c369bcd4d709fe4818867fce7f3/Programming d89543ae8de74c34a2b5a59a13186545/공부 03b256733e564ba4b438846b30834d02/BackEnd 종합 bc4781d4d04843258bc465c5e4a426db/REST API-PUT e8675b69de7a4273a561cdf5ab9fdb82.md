# REST API-PUT

PUT의 목적은 리소스의 갱신/생성이다.

해당 데이터가 존대한다면 갱신이고, 그렇지 않다면 생성이다.

```java
package com.example.restapi.controller;

import com.example.restapi.model.UserRequest;
import lombok.extern.slf4j.Slf4j;
import org.springframework.web.bind.annotation.PutMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

@Slf4j //이 어노테이션을 사용하면 클래스 내에서 log라는 이름의 로거(Logger)를 사용할 수 있다.
@RestController
@RequestMapping("/api")
public class PutApiController {

    @PutMapping("/put")
    public void put(
            @RequestBody
            UserRequest userRequest
    ){
        log.info("Request : {}", userRequest);
    }
}
```

```java
package com.example.restapi.model;

import com.fasterxml.jackson.databind.PropertyNamingStrategies;
import com.fasterxml.jackson.databind.annotation.JsonNaming;
import lombok.AllArgsConstructor;
import lombok.Data;
import lombok.NoArgsConstructor;
@JsonNaming(PropertyNamingStrategies.SnakeCaseStrategy.class) // post json 을 스네이크 형태로 받겠다

@AllArgsConstructor
@Data
@NoArgsConstructor
public class UserRequest {
    private String name;
    private String phoneNum;
    private String email;
    private Integer userAge;
    private Boolean isKorean;
}
```

boolean 대신에 Boolean을 써야되는 이유는 lombok 라이브러리에서 set 함수를 생성할 때 setIsKorean으로 생성 안하고 setKorean으로 생성해버려서 결국 isKorean이라는 변수를 못찾고 post나 put을 할 때  false값이 들어오게 된다.