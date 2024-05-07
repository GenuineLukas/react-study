# 예외처리 실전적용-2:@Order를 이용하여 Global한 플로우 처리

새로운 GlobalExceptionHandler를 만들어서 다음과 같이 구현

```java
package com.example.exeption.exception;

import com.example.exeption.model.Api;
import lombok.extern.slf4j.Slf4j;
import org.springframework.core.annotation.Order;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.ExceptionHandler;
import org.springframework.web.bind.annotation.RestControllerAdvice;

@Slf4j
@RestControllerAdvice
@Order(value = Integer.MAX_VALUE)
/*
* exception 핸들링을 해주는 클래스가 2개 이상 존재할 때
* 순서를 정해줄 수 있다.
* */
/*
RestExceptionApiHandler 에서 세부적인 exception 핸들링을 해주고 나서
남은 exception 에 대해서 이 클래스로 들어와서 핸들링 해준다.
 */

public class GlobalExceptionHandler {
    @ExceptionHandler(value = {Exception.class})
    public ResponseEntity<Api> exception(
            Exception e
    ){
        log.error(", e");
        //이 해당 익셉션에 대해 아무것도 모르므로 internal server error 로 해준다 (500대)
        var response = Api.builder()
                .resultCode(String.valueOf(HttpStatus.INTERNAL_SERVER_ERROR.value())) //500
                .resultMessage(HttpStatus.INTERNAL_SERVER_ERROR.getReasonPhrase()) //Internal Server Error
                .build();

        return ResponseEntity
                .status(HttpStatus.INTERNAL_SERVER_ERROR)
                .body(response);
    }
}

```

@Order 어노테이션을 보면 Integer의 최댓값으로 value가 설정된 것을 볼 수 있는데 이 숫자가 크면 클수록 늦게 우선순위가 뒤로 밀린다.

이렇게 서버에 어떠한 일이 생기더라도 가장 default가 되는 글로벌 리셉션 핸들러를 두고 해당 예외를 처리할 수 있도록 적용하는 것이 중요하다.