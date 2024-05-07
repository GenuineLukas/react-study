# Gson API 활용하기

자바에서 JSON 데이터를 다루는 방법은 여러 가지가 있지만, 일반적으로 라이브러리를 사용해서 JSON을 쉽게 다룰 수 있다. 대표적인 라이브러리로는 Gson과 Jackson이 있다. 

[https://mvnrepository.com/](https://mvnrepository.com/)  로 가서 gson 치고 jar 파일 다운로드.

file > project structue > Libraries > ‘+’ sign >  다운로드 받은 jar 파일 추가.

객체에서 JSON

```java
package course2.part3;

import com.google.gson.Gson;
import course2.Module.Member;

public class GsonToJson {
    public static void main(String[] args) {
        Member member = new Member("홍길동", 30, "hong@example.com");

        Gson gson = new Gson();
        String json = gson.toJson(member);

        System.out.println("Member 객체를 JSON으로 변환:" + json);
    }
}

```

JSON에서 객체

```java
package course2.part3;

import com.google.gson.Gson;
import course2.Module.Member;

public class JsonToGson {
    public static void main(String[] args) {
        String json = "{\"name\":\"홍길동\",\"age\":30,\"email\":\"hong@example.com\"}";

        Gson gson = new Gson();
        Member hong = gson.fromJson(json, Member.class);

        System.out.println("JSON을 Member 객체로 변환: " + hong);
    }
}
```

중첩된 객체도 처리할 수 있다.

객체에서 JSON

```java
package course2.part3;

import com.google.gson.Gson;
import course2.Module.Address;
import course2.Module.Member;

public class GsonToJson {
    public static void main(String[] args) {
        Address address = new Address("서울", "대한민국");
        Member member = new Member("홍길동", 30, "hong@example.com", address);

        Gson gson = new Gson();
        String json = gson.toJson(member);

        System.out.println("Member 객체를 JSON으로 변환:" + json);
        //Member 객체를 JSON으로 변환:{"name":"홍길동","age":30,"email":"hong@example.com","address":{"city":"서울","country":"대한민국"}}
    }
}

```

JSON에서 객체

```java
package course2.part3;

import com.google.gson.Gson;
import course2.Module.Member;

public class JsonToGson {
    public static void main(String[] args) {
        String json = "{\"name\":\"홍길동\",\"age\":30,\"email\":\"hong@example.com\",\"address\":{\"city\":\"서울\",\"country\":\"대한민국\"}}";

        Gson gson = new Gson();
        Member hong = gson.fromJson(json, Member.class);

        System.out.println("JSON을 Member 객체로 변환: " + hong);
        //JSON을 Member 객체로 변환: Member{name='홍길동', age=30, email='hong@example.com', address=Address{city='서울', country='대한민국'}}
    }
}

```