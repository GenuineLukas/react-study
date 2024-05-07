# Lexical Environments of the for loop

just a code example

```jsx
const funcs = [];
for(let i =0; i < 3; i++) {
	funcs[i] = function () { return i; };
}

for(let i = 0; i < funcs.length; i++) {
	console.log(funcs[i]()); // 0 1 2
}
```

![Untitled](Lexical%20Environments%20of%20the%20for%20loop%203fd7e2b033ba46a6baaa291b9e379d38/Untitled.png)

for 문의 변수 선언문에서 let 이나 const 키워드로 선언한 변수를 사용하면 for 문의 코드 블록이 반복 실행될 때마다 for 문 코드 블록의 새로운 렉시컬 환경이 생성된다. 만약 for 문의 코드 블록 내에서 정의한 함수가 있다면 이 함수의 상위 스코프는 for 문의 코드 블록이 반복 실행될 때마다 생성된 for 문 코드 블록의 새로운 렉시컬 환경이다.

이때 함수의 상위 스코프는 for문의 코드 블록이 반복 실행될 때마다 식별자(for 문의 변수 선언문에서 선언한 초기화 변수 및 for 문의 코드 블록 내에서 선언한 지역 변수 등)의 값을 유지해야 한다. 이를 위해 for 문이 반복될 때마다 독립적인 렉시컬 환경을 생성하여 식별자의 값을 유지한다.

이처럼 let이나 const 키워드를 사용하는 반복문(for문, for…in문, for…of문, while문 등)은 코드블록을 반복 실행할 때마다 새로운 렉시컬 환경을 생성하여 반복할 당시 상태를 마치 스냅샷 찍는 것처럼 저장한다. 단, 니느 반복문의 코드 블록 내에서 함수를 정의할 때 의미가 있다. 반복문의 코드 블록 내부에 함수 정의가 없는 반복문이 생성하는 새로운 렉시컬 환경은 반복 직후, 아무도 참조하지 않기 떄문에 가비지 컬렉션의 대상이 된다.