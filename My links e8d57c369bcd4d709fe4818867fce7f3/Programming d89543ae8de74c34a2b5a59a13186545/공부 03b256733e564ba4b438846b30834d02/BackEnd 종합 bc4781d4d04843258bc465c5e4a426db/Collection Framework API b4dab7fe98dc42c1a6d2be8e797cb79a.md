# Collection Framework API

### List: 순서가 있는 객체의 모음을 다루는 인터페이스

### Set: 중복된 원소가 없는 객체의 모음을 다루는 인터페이스

### Map: 키-값 쌍의 객체를 다루는 인터페이스

** map에서 키-값 쌍을 빼내려면 Entry로 빼내야 한다.

```java
for(Map.Entry<String, Integer> entry : studentScordes.entrySet()){
	System.out.println(entry.getKey()+"'s score:"+entry.getValue());
}
```