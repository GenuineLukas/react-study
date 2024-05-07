# REST API - GET

spring initializr → Gradle-Groovy, Java,  2.7.7, Artifact: rest-api, Jar, 17

ADD DEPNDENCIES → Lombok, Spring Web

intelliJ → open build.gradle (open as project)

```java
package com.example.restapi.controller;

import org.springframework.web.bind.annotation.*;

@RestController //해당 컨트롤러가 Restful 웹 서비스의 컨트롤러임을 알려줌.
@RequestMapping("/api") //api 로 시작하는 주소로 들어오면 이 컨트롤러가 처리해줄 것임.
public class RestApiController {
    //@GetMapping(path="/hello")은 "/api/hello" 경로로의 GET 요청을 처리하는 메소드. "Hello Spring Boot" 문자열을 반환.
    @GetMapping(path="/hello")
    public String hello(){
        return "<html><body><h1> Hello Spring Boot </h1></body></html>";
    }

    @GetMapping(path = "/echo/{message}/age/{age}/is-man/{isMan}") //PATH VARIABLE goes inside the curly bracket.
    public String echo(
            @PathVariable String message,
            @PathVariable int age, //Integer 보다는 int. None이 들어올 수 있기 때문에 -> 404 not found
            @PathVariable boolean isMan
    ){

        System.out.println("echo message: " + message);
        System.out.println("echo age: " + age);
        System.out.println("echo isMan: " + isMan);

        return message.toUpperCase();
    }
    // example combination: http://localhost:8080/api/echo/steve/age/20/is-man/true
    /*
    echo message: steve
    echo age: 20
    echo isMan: true
     */

    // query param example: http://localhost:8080/book?category=IT&issuedYear=2023&issued-month=01&issued_day=31
    @GetMapping(path = "/book")
    public String queryParam(
            @RequestParam String category,
            @RequestParam String issuedYear,
            @RequestParam(name="issued-month") String issuedMonth, //naming convention
            @RequestParam(name="issued_day") String issuedDay //naming convention
    ){
        System.out.println(category +" : "+ issuedYear+", " + issuedMonth+", " + issuedDay);
        return category +" : "+ issuedYear+", " + issuedMonth+", " + issuedDay;
    }
}
```

public String queryParam을 보면 이것이 쿼리 파라미터를 받는 첫번째 방법이다.

## 쿼리 파라미터를 객체로 받는 방법

현재 파일 구조

![Untitled](REST%20API%20-%20GET%209a48bda57cba486c84ad2adc304b1b3b/Untitled.png)

```java
package com.example.restapi.controller;

import com.example.restapi.model.BookQueryParam;
import org.springframework.web.bind.annotation.*;
.
.
.
@GetMapping(path = "/book")
    public void queryParam(
            BookQueryParam bookQueryParam
    ) {
        System.out.println(bookQueryParam);
    }
}
```

```java
package com.example.restapi.model;

import lombok.AllArgsConstructor;
import lombok.Data;
import lombok.NoArgsConstructor;

@Data
@AllArgsConstructor
@NoArgsConstructor
public class BookQueryParam {
    private String category;
    private String issuedMonth;
    private String issuedYear;
    private String issuedDay;
}

```