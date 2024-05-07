# 예외처리 실전적용-01: response 통일

![Untitled](%E1%84%8B%E1%85%A8%E1%84%8B%E1%85%AC%E1%84%8E%E1%85%A5%E1%84%85%E1%85%B5%20%E1%84%89%E1%85%B5%E1%86%AF%E1%84%8C%E1%85%A5%E1%86%AB%E1%84%8C%E1%85%A5%E1%86%A8%E1%84%8B%E1%85%AD%E1%86%BC-01%20response%20%E1%84%90%E1%85%A9%E1%86%BC%E1%84%8B%E1%85%B5%E1%86%AF%20e1c162d58f0149bba6e1cfca8cfcc50c/Untitled.jpeg)

### Builder에 대해 알아보자

**`@Builder`** 어노테이션은 롬복(Lombok) 라이브러리에서 제공하는 기능 중 하나로, 빌더 패턴(Builder Pattern)을 자동으로 생성해줍니다. 이를 통해 객체를 생성할 때의 가독성과 편의성을 높일 수 있습니다.

아래는 **`@Builder`** 어노테이션을 사용한 예시입니다.

```java
javaCopy code
import lombok.Builder;
import lombok.Getter;

@Getter
@Builder
public class Person {
    private String name;
    private int age;
    private String address;
}

// 사용 예시
public class Main {
    public static void main(String[] args) {
        Person person = Person.builder()
                              .name("John")
                              .age(30)
                              .address("123 Street")
                              .build();
    }
}

```

위의 코드에서 **`Person`** 클래스에 **`@Builder`** 어노테이션이 붙으면 롬복이 컴파일 시간에 **`PersonBuilder`** 클래스를 생성하여 빌더 패턴을 구현합니다. 그러면 **`Person`** 객체를 생성할 때 체인 형태로 속성을 설정할 수 있습니다.

**`@Builder`** 어노테이션은 클래스의 모든 필드에 대해 빌더를 생성하며, 선택적인 필드를 설정하지 않아도 됩니다. 또한 필수 필드와 선택적인 필드를 지정하려면 **`@Builder`** 어노테이션에 **`@NonNull`** 어노테이션을 사용하여 필수적인 필드를 지정할 수 있습니다.

코드 이해

```java
package com.example.exeption.controller;

import com.example.exeption.model.Api;
import com.example.exeption.model.UserResponse;
import org.springframework.http.HttpStatus;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

import java.util.List;

@RestController
@RequestMapping("/api/user")
public class UserApiController {

    //DB가 없기 떄문에 일단 주먹구구
    private static List<UserResponse> userList = List.of(
            UserResponse.builder()
                    .id("1")
                    .age(10)
                    .name("홍길동")
                    .build(),
            UserResponse.builder()
                    .id("2")
                    .age(10)
                    .name("유관순")
                    .build()
    );

    @GetMapping("id/{userId}")
    public Api<UserResponse> getUser(
            @PathVariable String userId
    ){
        var user = userList.stream().filter(
                        it -> it.getId().equals(userId)
                )
                .findFirst()
                .get();

        Api<UserResponse> response = Api.<UserResponse>builder()
                .resultCode(String.valueOf(HttpStatus.OK.value()))
                .resultMessage(HttpStatus.OK.name())
                .data(user)
                .build();

        return response;
    }
}

-----
package com.example.exeption.model;

import com.fasterxml.jackson.databind.PropertyNamingStrategies;
import com.fasterxml.jackson.databind.annotation.JsonNaming;
import lombok.AllArgsConstructor;
import lombok.Builder;
import lombok.Data;
import lombok.NoArgsConstructor;

@Data
@NoArgsConstructor
@AllArgsConstructor
@Builder
@JsonNaming(PropertyNamingStrategies.SnakeCaseStrategy.class)
public class UserResponse {
    private String id;
    private String name;
    private Integer age;
}
-----
package com.example.exeption.model;

import com.fasterxml.jackson.databind.PropertyNamingStrategies;
import com.fasterxml.jackson.databind.annotation.JsonNaming;
import lombok.AllArgsConstructor;
import lombok.Builder;
import lombok.Data;
import lombok.NoArgsConstructor;

@Data
@NoArgsConstructor
@AllArgsConstructor
@Builder
@JsonNaming(PropertyNamingStrategies.SnakeCaseStrategy.class)
public class Api<T> {
    private String resultCode;
    private String resultMessage;
    private T data;
}

```

이 상황에서 [http://localhost:8080/api/user/id/90](http://localhost:8080/api/user/id/90), 즉, 없는 유저를 요청하게 되면

response body에 No Content가 들어오게 되는데(전역적으로 예외처리를 안해줬으면 사실 그냥 500에러 뜸) 이를 방지하기 위해 예외 처리 하는 법을 알아보자.

![Untitled](%E1%84%8B%E1%85%A8%E1%84%8B%E1%85%AC%E1%84%8E%E1%85%A5%E1%84%85%E1%85%B5%20%E1%84%89%E1%85%B5%E1%86%AF%E1%84%8C%E1%85%A5%E1%86%AB%E1%84%8C%E1%85%A5%E1%86%A8%E1%84%8B%E1%85%AD%E1%86%BC-01%20response%20%E1%84%90%E1%85%A9%E1%86%BC%E1%84%8B%E1%85%B5%E1%86%AF%20e1c162d58f0149bba6e1cfca8cfcc50c/Untitled.png)

noSuchElement 함수를 보라.

```java
package com.example.exeption.exception;

import com.example.exeption.model.Api;
import lombok.extern.slf4j.Slf4j;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.ExceptionHandler;
import org.springframework.web.bind.annotation.RestControllerAdvice;

import java.util.NoSuchElementException;

@Slf4j
@RestControllerAdvice
/*
@RestControllerAdvice는 스프링 프레임워크에서 제공하는 애노테이션으로,
전역적으로 REST 컨트롤러에 대한 예외 처리를 담당하는 클래스에 붙입니다.
이를 통해 애플리케이션 내에서 발생하는 예외를 일관된 방식으로 처리할 수 있습니다.
 */
public class RestExceptionApiHandler {
    @ExceptionHandler(value = {Exception.class})
    public ResponseEntity exception(
            Exception e
    ){
        log.error("RestApiExceptionHandler", e);
        return ResponseEntity.status(200).build();
    }

    @ExceptionHandler(value = {IndexOutOfBoundsException.class})
    public ResponseEntity outOfBounds(
            IndexOutOfBoundsException e
    ){
        log.error("IndexOutOfBoundsException", e);
        return ResponseEntity.status(200).build();
    }

    @ExceptionHandler(value = {NoSuchElementException.class})
    public ResponseEntity<Api> noSuchElement(
            NoSuchElementException e
    ){
        log.error(" ", e);

        var response =  Api.builder()
                .resultCode(String.valueOf(HttpStatus.NOT_FOUND.value()))
                .resultMessage(HttpStatus.NOT_FOUND.getReasonPhrase())
                .build();
        
        return ResponseEntity
                .status(HttpStatus.NOT_FOUND)
                .body(response);
    }
}

```

이제 response body에 content가 넘어온다.

없는 유저 get할 때

![Untitled](%E1%84%8B%E1%85%A8%E1%84%8B%E1%85%AC%E1%84%8E%E1%85%A5%E1%84%85%E1%85%B5%20%E1%84%89%E1%85%B5%E1%86%AF%E1%84%8C%E1%85%A5%E1%86%AB%E1%84%8C%E1%85%A5%E1%86%A8%E1%84%8B%E1%85%AD%E1%86%BC-01%20response%20%E1%84%90%E1%85%A9%E1%86%BC%E1%84%8B%E1%85%B5%E1%86%AF%20e1c162d58f0149bba6e1cfca8cfcc50c/Untitled%201.png)

있는 유저 get할 때

![Untitled](%E1%84%8B%E1%85%A8%E1%84%8B%E1%85%AC%E1%84%8E%E1%85%A5%E1%84%85%E1%85%B5%20%E1%84%89%E1%85%B5%E1%86%AF%E1%84%8C%E1%85%A5%E1%86%AB%E1%84%8C%E1%85%A5%E1%86%A8%E1%84%8B%E1%85%AD%E1%86%BC-01%20response%20%E1%84%90%E1%85%A9%E1%86%BC%E1%84%8B%E1%85%B5%E1%86%AF%20e1c162d58f0149bba6e1cfca8cfcc50c/Untitled%202.png)

이렇게 되면 우리 서버는 예외상황에 관계없이 항상 동일한 스펙을  response로 제공하게 된다.