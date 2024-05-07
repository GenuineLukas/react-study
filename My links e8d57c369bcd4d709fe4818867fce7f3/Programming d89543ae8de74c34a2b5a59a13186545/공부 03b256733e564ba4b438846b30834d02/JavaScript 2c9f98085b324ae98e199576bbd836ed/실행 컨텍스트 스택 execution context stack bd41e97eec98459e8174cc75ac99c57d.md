# 실행 컨텍스트 스택 execution context stack

Take a look at the following example.

```jsx
const x = 1;

function foo () {
    const y = 2;

    function bar () {
        const z = 3;
        console.log(x + y + z);
    }
    bar();
}

foo(); // 6
```

if you break down the code above into to src codes(more by src code type), it will be broken down into the global code and function code. JavaScript evaluates the global code first to make the execution context of it. Then, when the function (here, foo()) is called, it evaluates the function piece of the code to make another execution context of it as well.

The execution contexts created will be managed inside the “stack” data structure. This is what we call **execution context stack.** here is what the execution stack would look like during the execution of the code above.

![Untitled](%E1%84%89%E1%85%B5%E1%86%AF%E1%84%92%E1%85%A2%E1%86%BC%20%E1%84%8F%E1%85%A5%E1%86%AB%E1%84%90%E1%85%A6%E1%86%A8%E1%84%89%E1%85%B3%E1%84%90%E1%85%B3%20%E1%84%89%E1%85%B3%E1%84%90%E1%85%A2%E1%86%A8%20execution%20context%20stack%20bd41e97eec98459e8174cc75ac99c57d/Untitled.png)

1. **전역코드의 평가와 실행**
    
    JavaScript engine  firstly evaluates the global code and create the global context. Then, it starts to push to the stack, registering the global variable x and the global function foo() to the execution context. After this, the global code gets executed value is allocated to the global variable x and the global function foo() is called.
    
2. **foo함수 코드의 평가와 실행**
    
    Once the global function foo() is called, the execution of the global code intermittently paused and the authority to control the code is granted to the inside of the foo() function. The JavaScript engine evaluates inside of the function and push it to the foo() function’s execution context, registering foo() function’s local variable y and the nested function bar() to the execution context of the foo() function.
    
3. **bar 함수 코드의 평가와 실행**
    
    Once the nested function bar() is called, the execution of the foo() function is intermittently paused and the authority to control the code is granted to the inside of the bar() function. The JavaScript engine evaluates inside of the function and push it to the bar() function’s execution context, registering the bar()’s local variable z to the bar() function’s execution context. After this, the console.log() inside the bar() function function gets called, terminating the execution process of the bar() function.
    
4. **foo 함수 코드로 복귀**
    
    Once the execution of the bar() function gets terminated, the control of the code flow gets back to the foo() function, removing( popping ) the bar() function’s execution context from the execution context stack. Then, the execution of the foo() function gets terminated as well.
    
5. **전역 코드로 복귀**
    
    Once the execution of the foo() function gets terminated, the control of the code flow gets back to the global code, removing( popping ) the foo() function’s execution context from the execution context stack. Then the execution context of the global code is also popped after all this.
    
     *** **running execution context:** the execution context staying at the top of the stack ***