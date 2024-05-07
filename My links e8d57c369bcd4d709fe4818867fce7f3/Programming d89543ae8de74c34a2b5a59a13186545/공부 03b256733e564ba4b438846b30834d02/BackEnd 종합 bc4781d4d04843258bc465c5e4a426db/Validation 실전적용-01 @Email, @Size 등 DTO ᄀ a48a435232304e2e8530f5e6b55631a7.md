# Validation 실전적용-01: @Email, @Size 등 DTO 객체의 변수 validate하기

이런식으로 DTO의 멤버변수들에 올바른 어노테이션을 달아준다

```java
package com.example.validation.model;

import com.fasterxml.jackson.databind.PropertyNamingStrategies;
import com.fasterxml.jackson.databind.annotation.JsonNaming;
import jakarta.validation.constraints.*;
import lombok.AllArgsConstructor;
import lombok.Builder;
import lombok.Data;
import lombok.NoArgsConstructor;

import java.time.LocalDateTime;

@JsonNaming(PropertyNamingStrategies.SnakeCaseStrategy.class)
@Data
@NoArgsConstructor
@AllArgsConstructor
@Builder
public class UserRegisterRequest {
    @NotBlank
    private String name;

    @NotBlank
    @Size(min = 1, max = 12)
    private String password;

    @NotNull
    @Min(1)
    @Max(100)
    private Integer age;

    @Email
    private String email;

    @Pattern(regexp = "^[2-9]\\d{2}-\\d{3}-\\d{4}$")
    private String phoneNumber;

    @FutureOrPresent
    private LocalDateTime registerAt;
}

```

UserApiController

```java
package com.example.validation.controller;

import com.example.validation.model.UserRegisterRequest;
import jakarta.validation.Valid;
import lombok.extern.slf4j.Slf4j;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

@Slf4j
@RestController
@RequestMapping("/api/user")
public class UserApiController {
    @PostMapping("")
    public UserRegisterRequest register(
            @Valid
            @RequestBody
            UserRegisterRequest userRegisterRequest
    ){
        log.info("init: {}", userRegisterRequest);

        return userRegisterRequest;
    }
}

```