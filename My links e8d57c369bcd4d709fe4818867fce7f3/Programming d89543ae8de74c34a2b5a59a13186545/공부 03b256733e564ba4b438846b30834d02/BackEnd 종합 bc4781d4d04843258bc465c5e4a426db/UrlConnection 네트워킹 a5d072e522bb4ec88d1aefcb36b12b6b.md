# UrlConnection 네트워킹

HttpURLConnection은 URLConnection의 하위 클래스로, HTTP 프로토콜을 사용하여 특정 웹 서버와 통신하기 위한 클래스이며 HttpURLConnection은 HTTP메서드 (예: GET, POST, PUT, DELETE 등)를 지원하며, HTTP 요청과 응답을 처리할 수 있는 메서드들을 제공한다.

HttpURLConnection을 사용하여 웹 서버에서 정보를 가져오는 절차

1. URL 생성
2. HttpURLConnection 초기화
3. HTTP 메서드 설정
4. 요청 헤더 설정(선택) 키 값 같은거 넘겨줄 때
5. 요청 본문 작성(선택)
6. 응답 코드 확인
7. 응답 헤더 읽기 (선택)
8. 응답 본문 읽기: InputStream을 사용하여 응답 본문을 읽고 처리한다.
9. 연결 종료

### HttpURLConnection API로 Open API를 접속해서 날씨 정보를 가져오기

[https://openweathermap.org/](https://openweathermap.org/)

들어가서 회원가입

키 발급 받으삼.

```java
package course2;

import com.google.gson.JsonObject;
import com.google.gson.JsonParser;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URL;

public class WeatherExample {
    public static void main(String[] args) {
        String apiKey = "8a557fb0f04d8cd6fd97f6acbffe38e2";
        String city = "Seoul";
        String urlString = "https://api.openweathermap.org/data/2.5/weather?q="+city+"&appid="+apiKey+"&units=metric";

        try {
            URL url = new URL(urlString);
            HttpURLConnection connection =(HttpURLConnection) url.openConnection();
            connection.setRequestMethod("GET");
            connection.setRequestProperty("Accept", "application/json"); // json 정보로 받겠다.

            int responseCode = connection.getResponseCode();
            System.out.println("Response Code: " + responseCode); //Response Code: 200

            if(responseCode == 200){
                //getInputStream() 은 바이트 단위의 스트림, InputStreamReader() 를 하면 문자 단위로 받기 떄문에 한글이 인코딩 된다
                //BufferedReader() 는 buffer 공간에 모으는 것
                BufferedReader in = new BufferedReader(new InputStreamReader(connection.getInputStream()));
                String inputLine;
                StringBuilder content = new StringBuilder(); //StringBuffer 에다 담는 것임
                while((inputLine = in.readLine()) != null){
                    content.append(inputLine);
                }
                in.close();

                JsonObject weatherData = JsonParser.parseString(content.toString()).getAsJsonObject();
                JsonObject mainData = weatherData.getAsJsonObject("main");
                double temp = mainData.get("temp").getAsDouble();

                System.out.println("Seoul's Temperature: " + temp + "°C"); //Seoul's Temperature: 23.52°C

                connection.disconnect();
            }
        } catch(IOException e) {
            e.printStackTrace();
        }
    }
}

```