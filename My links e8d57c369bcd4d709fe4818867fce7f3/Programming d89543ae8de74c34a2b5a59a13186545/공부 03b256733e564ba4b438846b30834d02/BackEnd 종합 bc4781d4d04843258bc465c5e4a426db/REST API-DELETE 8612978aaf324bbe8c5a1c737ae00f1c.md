# REST API-DELETE

```java
package com.example.restapi.controller;

import com.example.restapi.model.BookQueryParam;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.web.bind.annotation.*;

@RestController //해당 컨트롤러가 Restful 웹 서비스의 컨트롤러임을 알려줌.
@RequestMapping("/api") //api 로 시작하는 주소로 들어오면 이 컨트롤러가 처리해줄 것임.
public class RestApiController {
    private static final Logger log = LoggerFactory.getLogger(RestApiController.class);

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
    public void queryParam(
            BookQueryParam bookQueryParam
    ) {
        System.out.println(bookQueryParam);
    }

    @DeleteMapping(path =
            {
             "/user/{userName}/delete",
            "/user/{userName}/del"
            })
    public void delete(
            @PathVariable String userName
    ){
        log.info("user-name: {}", userName);
    }
}

```

@Deletemapping 어노테이션 아래 있는게 delete하는 방법이다.