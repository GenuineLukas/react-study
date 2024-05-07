# Closure & Lexical Environment

take a look at the following code.

```jsx
const x =1;

function outer() {
	const x = 10;
	const inner = function () { console.log(x) };
	return inner;
}

const innerFunc = outer();
innerFunc(); //10
```

When you call the `outer()` function, it returns the `inner()` function and ends its life cycle, which means its execution context is removed from the execution context stack. As you can see in the code above, however,  the `inner()` function accessed the variable `x` from the already-terminated `outer()` function as if the `outer()` function was still running. This nested function, in this specific case,  is called a ***closure*** when a nested function, in terms of the life cycle, lasts longer t han the outer function and can refer to its variables.

![Untitled](Closure%20&%20Lexical%20Environment%209ff4e3d64b3b443ebaaee2d9df984de9/Untitled.png)

 When you create the function object by evaluating the outer() function, the global lexical environment is saved in the [[Environment]] slot of the outer() function object. When you call the outer() function, it creates a new lexical environment and assigns the previously saved global lexical environment to the new environment's OuterLexicalEnvironmentReference.

The inner() function is evaluated and creates an object for the inner function. The inner() function's [[Environment]] slot is assigned the lexical environment of the outer() function.

When the outer() function finishes executing, its execution context is popped from the stack. The lexical environment of the outer() function still exists, however. This is because the [[Environment]] slot of the inner function object references it, so it won't be deleted **by the garbage collector**. This enables the closures to access&change the variables defined outside the scope.