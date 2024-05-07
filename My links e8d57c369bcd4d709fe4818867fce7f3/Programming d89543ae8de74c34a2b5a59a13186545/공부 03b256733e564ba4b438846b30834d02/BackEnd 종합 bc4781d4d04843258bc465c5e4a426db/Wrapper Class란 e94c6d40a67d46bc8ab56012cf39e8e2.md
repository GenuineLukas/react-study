# Wrapper Class란

자바에서 collection framework를 사용할 때 collection framework의 element로 primitive type을 넣을 수가 없다. 그렇다면 int나 double 같은거를 담고 싶을 때 어떻게 해야 하나? Wrapper 객체로 변환 시켜야 한다.

Wrapper class: 기본 데이터 타입을 객체로 다룰 수 있도록 만들어진 클래스이다. wrapper 클래스를 사용하면 자동으로 박싱(Boxing)과 언박싱(unboxing)이 이루어진다.

- Auto-Boxing:

```java
Integer aa = 10;
//이렇게 쓰면 new Integer(10)을 자동으로 하고 aa에 할당해준다.
```

- Auto-Unboxing:

```java
int a = aa
//이렇게 쓰면 aa.intValue()로 포장을 풀고 a에 할당해준다.
```