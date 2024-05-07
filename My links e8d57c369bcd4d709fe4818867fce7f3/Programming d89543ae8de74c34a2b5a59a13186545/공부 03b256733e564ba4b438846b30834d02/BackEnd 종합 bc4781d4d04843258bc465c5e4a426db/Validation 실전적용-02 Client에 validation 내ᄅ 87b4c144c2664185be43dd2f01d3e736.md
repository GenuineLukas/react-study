# Validation 실전적용-02: Client에 validation 내려주기

DTO를 감싸줄 Api 모습

```java
package com.example.validation.model;

import com.fasterxml.jackson.databind.PropertyNamingStrategies;
import com.fasterxml.jackson.databind.annotation.JsonNaming;
import jakarta.validation.Valid;
import lombok.AllArgsConstructor;
import lombok.Builder;
import lombok.Data;
import lombok.NoArgsConstructor;

import java.util.List;

@Data
@NoArgsConstructor
@AllArgsConstructor
@Builder
@JsonNaming(PropertyNamingStrategies.SnakeCaseStrategy.class)
public class Api<T> {
    private String resultCode;

    private String resultMessage;

    @Valid //이걸 붙여줘야 해당 제네릭 타입에 대해서도 validation check 을 해준다.
    private T data;

    private Error erorr;

    @Data
    @NoArgsConstructor
    @AllArgsConstructor
    @Builder
    @JsonNaming(PropertyNamingStrategies.SnakeCaseStrategy.class)
    public static class Error{
        private List<String> errorMessage;
    }
}

```

DTO 기본적인 모습

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

PostRequest 오는 곳 모습

```java
package com.example.validation.controller;

import com.example.validation.model.Api;
import com.example.validation.model.UserRegisterRequest;
import jakarta.validation.Valid;
import lombok.extern.slf4j.Slf4j;
import org.springframework.http.HttpStatus;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

@Slf4j
@RestController
@RequestMapping("/api/user")
public class UserApiController {
    @PostMapping("")

    public Api<UserRegisterRequest> register(
            @Valid
            @RequestBody
            Api<UserRegisterRequest> userRegisterRequest

            // Exception Handler 로 validation 로직을 빼게 되면
            // 자연스래 이 클래스로 요청이 들어왔다라는 거는 해당 안에 있는 값들은
            // 유효하다는 말이 되고 이제 비지니스 로직만 처리를 하고
            // 해당 값을 리턴시켜주면 된다.
    ){
        log.info("init: {}", userRegisterRequest);

        var body = userRegisterRequest.getData();
        Api<UserRegisterRequest> response = Api.<UserRegisterRequest>builder()
                .resultCode(String.valueOf(HttpStatus.OK.value()))
                .resultMessage(HttpStatus.OK.getReasonPhrase())
                .data(body)
                .build();

        return response;
    }
}

```

예외처리 + client에 뭔가 잘못됏다고 알려주기

```java
package com.example.validation.exception;

import com.example.validation.model.Api;
import lombok.extern.slf4j.Slf4j;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.MethodArgumentNotValidException;
import org.springframework.web.bind.annotation.ExceptionHandler;
import org.springframework.web.bind.annotation.RestControllerAdvice;

import java.util.stream.Collectors;

@Slf4j
@RestControllerAdvice
public class ValidationExceptionHandler{
    @ExceptionHandler(MethodArgumentNotValidException.class)
    public ResponseEntity<Api> validateException(
            MethodArgumentNotValidException e
    ){
        log.error(e.getMessage());

        var errorMessageList = e.getFieldErrors().stream()
                .map(it -> {
                    var format = "%s : { %s } %s";
                    var message = String.format(format, it.getField(), it.getRejectedValue() , it.getDefaultMessage());
                    return message;
                }).collect(Collectors.toList());

        var error = Api.Error
                .builder()
                .errorMessage(errorMessageList)
                .build();

        var errorResponse = Api
                .builder()
                .resultCode(String.valueOf(HttpStatus.BAD_REQUEST.value()))
                .resultMessage(HttpStatus.BAD_REQUEST.getReasonPhrase())
                .erorr(error)
                .build()
                ;

        return ResponseEntity.status(HttpStatus.BAD_REQUEST).body(errorResponse);
    }
}

```