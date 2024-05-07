# Spring Boot Web-예외처리

프로젝트 셋팅

![Untitled](Spring%20Boot%20Web-%E1%84%8B%E1%85%A8%E1%84%8B%E1%85%AC%E1%84%8E%E1%85%A5%E1%84%85%E1%85%B5%20d037dacea05543c0a2f7ebc877e2619f/Untitled.png)

build.gradle 을 as project로 열어줘야 한다.

임의로 에러 발생

```java
package com.example.exeption.controller;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
@RequestMapping("/api")
public class RestApiController {
    @GetMapping
    public void hello(){
        throw new RuntimeException("run time exception call.");
    }
}
```

이렇게 해놓고 [http://localhost:8080/api](http://localhost:8080/api) 에 리퀘를 보내보면  500에러가 발생.

![Untitled](Spring%20Boot%20Web-%E1%84%8B%E1%85%A8%E1%84%8B%E1%85%AC%E1%84%8E%E1%85%A5%E1%84%85%E1%85%B5%20d037dacea05543c0a2f7ebc877e2619f/Untitled%201.png)

인덱스아웃오브바운즈 임의로 발생

```java
package com.example.exeption.controller;

import lombok.extern.slf4j.Slf4j;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

import java.util.List;

@Slf4j
@RestController
@RequestMapping("/api")
public class RestApiController {
    @GetMapping
    public void hello(){
         var list = List.of("hello");
         var element = list.get(1);

        log.info("element: {}", element);
    }
}
```

이렇게 하면

Talend Api tester에서 동일하게 internal error에 500번 에러 메세지가 뜨고

terminal에는

```java
java.lang.IndexOutOfBoundsException: Index: 1 Size: 1
	at java.base/java.util.ImmutableCollections$AbstractImmutableList.outOfBounds(ImmutableCollections.java:333) ~[na:na]
	at java.base/java.util.ImmutableCollections$List12.get(ImmutableCollections.java:585) ~[na:na]
	at com.example.exeption.controller.RestApiController.hello(RestApiController.java:17) ~[main/:na]
	at java.base/jdk.internal.reflect.DirectMethodHandleAccessor.invoke(DirectMethodHandleAccessor.java:104) ~[na:na]
...
```

이런식으로 IndexOutOfBoundException 메세지가 뜬다.

### 예외처리 하는 방법 **@RestControllerAdvice**

```java
package com.example.exeption.exception;

import lombok.extern.slf4j.Slf4j;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.ExceptionHandler;
import org.springframework.web.bind.annotation.RestControllerAdvice;

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
}

```

이런식으로 해놓고 아까 IndexOutOfBounds 발생된던 라웃으로 겟 요청을 보내보면 Talend Api tester에서는 200으로 정상적으로 들어오고 

![Untitled](Spring%20Boot%20Web-%E1%84%8B%E1%85%A8%E1%84%8B%E1%85%AC%E1%84%8E%E1%85%A5%E1%84%85%E1%85%B5%20d037dacea05543c0a2f7ebc877e2619f/Untitled%202.png)

이런식으로 콘솔에서는 발생한 특정에러가 잘 뜬다. IndexOutOfBoundsException은 Exception을 상속받기 때문에 둘 다에 대한 예외처리를 해줬음에도 더 세부적인 IndexOutOfBoundsException이 발생하는 것.

### 전역이 아닌 같은 컨트롤러에서 예외 잡기

![Untitled](Spring%20Boot%20Web-%E1%84%8B%E1%85%A8%E1%84%8B%E1%85%AC%E1%84%8E%E1%85%A5%E1%84%85%E1%85%B5%20d037dacea05543c0a2f7ebc877e2619f/Untitled.jpeg)

그런데 이거는 코드가 길어질 경우 용이하지 않다.

### 예외처리 범위에 제한을 두기

**`@RestControllerAdvice`** 애노테이션은 주로 모든 컨트롤러에서 발생하는 예외를 처리하기 위해 사용됩니다. 하지만 특정 패키지나 클래스 내의 컨트롤러에서 발생하는 예외만을 처리하도록 제한하고 싶을 때가 있습니다. 이 때 **`basePackages`** 속성을 사용하여 원하는 패키지를 지정할 수 있습니다.

예를 들어, **`com.example.exception.controller`** 패키지에 있는 컨트롤러에서 발생하는 예외만 처리하고 싶을 때는 다음과 같이 **`@RestControllerAdvice`**를 사용합니다:

```java
import org.springframework.web.bind.annotation.RestControllerAdvice;

@RestControllerAdvice(basePackages = "com.example.exception.controller")
public class CustomExceptionHandler {
    // 예외 처리 메서드들을 정의합니다.
}
```

이 외에도 클래스나 어노테이션을 기준으로 하는 방법이 있다.