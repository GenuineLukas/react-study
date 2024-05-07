# Common examples of closures

Closure is used when the state should be changed and maintained safely, preventing it from unintentionally being changed.

The following code has two main problems.

1. the value of the variable `num` should not be changed until the increase function is called.
2. the value of the variable `num` should be changed only by the increase function.

```jsx
let num = 0;

const increase = function() {
	return ++num;
}

console.log(increase()); // 1
console.log(increase()); // 2 
console.log(increase()); // 3
```

**The revised code is as below.**

the code below is assuring that the `num` variable is mutable only by the inner function. Since the outer function is expressed as the immediately invoked one, the Execution context of it would be popped from the stack, leaving the lexical environment that is referenced by the [[Environment]] internal slot of the inner function object. This means the outer function is called only once, but the `num` variable could be accessed and changed by the inner function.

```jsx
const increase = (function () {
	let num = 0;
	return function() {
		return ++num;
	};
}());

console.log(increase()); //1
console.log(increase()); //2
console.log(increase()); //3
```

**adding decreasing functionality**

```jsx
const counter = (function () {
	let num = 0;

	return {
		increase() {
			return ++num;
		},
		decrease() {
			return num > 0 ? --num : 0;
		},
	}
}());

console.log(counter.increase()); //1
console.log(counter.decrease()); //0
console.log(counter.decrease()); //0
```

**Doing the same thing using prototype**

```jsx
const CounterVar = (function () {
    let num = 0;
    function Counter(){};
    Counter.prototype.increase = function () {
        return ++num;
    }
    Counter.prototype.decrease = function () {
        return num > 0 ? --num : 0;
    }
    return Counter;
}());
```

the variable `num` is initialized inside the immediately invoked function, it’s not possible for the function Counter()’s instance to directly access it. Also, anything outside the immediately invoked function cannot access the variable, making the increase() and decrease() function added to the prototype the only ways to access the `num` variable.

**Using closure in the functional programming**

The functional programming encourages the immutability. Therefore, the closure comes in handy when functionally programming.

```jsx
const counter = (function () {
	let counter = 0;
	
	return function (aux) {
		counter = aux(counter);
		return counter;
	};
}());

function increase(n) {
	return ++n;
}

function decrease(n) {
	return --n;
}

console.log(counter(increase)); //1
console.log(counter(increase)); //2
 
console.log(counter(decrease)); //1
console.log(counter(decrease)); //0
```

my thoughts: 이러한 식의 counter 문제에서는 즉시 실행 함수의 nested function이 closure인 부분이고 결국 increase 혹은 decrease (필요하다면 더 많은) 같은 function 들을 통해서만 count variable 에 접근할 수 있게 만드는 것이 목적이기도 하지만, 그 counting variable에 접근 가능한 function들이 하나의 variable을 share함으로써 counting을 할 수 있는 것도 중요하다. 이를 보장해주기위해 outer function에 즉시 실행 함수를 사용해서 변수에 접근 가능한 함수들이 하나의 Lexical Environment를 참조하게 하였다. 그것이 핵심이다. 만약 즉시 실행 함수가 아니었다면 독립된 렉시컬 환경으로 인해 변수 상태가 연동이 안되었을 것이다. → when you use the immediately invoked function, it’s executed only once. Then what’s assigned to the variable given the IIFE is the return value of the IIFE.