# 렉시컬 환경 lexical environment

According to the ECMAScript specification 262 (8.1), a Lexical Environment is like a home for variables and functions while the code is running. It's defined based on how the code is written.

The Lexical Environment independent of the Execution Context, which is a data structure that contains information about variables and functions. It keeps track of the identifier (name of the variable or function), the value bound to the identifier, and the reference to the upper scope.

The Lexical Environment is responsible for managing scopes and identifiers, while the Execution Context stack manages the order in which the code is executed.

Lexical Environment is composed of the two components: Environment Record & Outer Lexical Environment Reference. Take a look a the code below.

```jsx
var x = 1;
const y = 2;

function foo (a) {
  var x = 3;
  const y = 4;
  
  function bar (b) {
      const z = 5;
      console.log(a + b + x  + y + z);
  }
  bar(10);
}

foo(20);
	
```

![Untitled](%E1%84%85%E1%85%A6%E1%86%A8%E1%84%89%E1%85%B5%E1%84%8F%E1%85%A5%E1%86%AF%20%E1%84%92%E1%85%AA%E1%86%AB%E1%84%80%E1%85%A7%E1%86%BC%20lexical%20environment%2000e5f620494149b493e1cc7cdc5165cb/Untitled.png)

code evaluation  code execution  code termination

1. Global object created 전역 객체 생성
    
    The global object is created before the code starts running. At this point, the built-in global properties, functions, and objects are added to it. In a web environment, this object is referred to as window. Depending on the operating system, window includes the client-side API (DOM, BOM, Canvas, XMLHttpRequest, fetch, etc.) and the host objects for certain environments.
    
2. Global code evaluation
    1. Global Execution Context created 전역 실행 컨텍스트 생성
        
        JavaScript creates an empty execution context and push it to the [execution context stack](%E1%84%89%E1%85%B5%E1%86%AF%E1%84%92%E1%85%A2%E1%86%BC%20%E1%84%8F%E1%85%A5%E1%86%AB%E1%84%90%E1%85%A6%E1%86%A8%E1%84%89%E1%85%B3%E1%84%90%E1%85%B3%20%E1%84%89%E1%85%B3%E1%84%90%E1%85%A2%E1%86%A8%20execution%20context%20stack%20bd41e97eec98459e8174cc75ac99c57d.md)  as the running execution context (means it’s at the top of the stack).
        
    2. Global Lexical Environment created 전역 렉시컬 환경 생성
        
        creates the global lexical environment and bind it to the global execution context.
        
        1. Global Environment Record created
            
            The global environment record is a component of the global lexical environment. The global environment record is composed of the **object environment record** and **declarative environment record.** 
            
            1. Object Environment Record created
                
                What does Object ER contain? → global object declared with `var`, global function declared with the function declaration, built-in global properties, built-in global functions, and the standard built-in objects.
                
                Object environment record bind itself(actually, the identifier BindingObject inside it) to the binding object (here, window). During the evaluation of the code, the global variables declared with `var` and the function declared by “function declaration” become the global object’s properties and methods through the binding object bound to the object environment record.
                
            2. Declarative Environment Record created 
                
                What does Declarative ER contain? → global variables declared with `let/const` .
                
    3. This binding
        
        “this” is bound to the **global environment record’s internal slot [[GlobalThisValue]]** which then binds to the global object (window). when you refer to “this” in the global scope, the object bound to the internal slot [[GlobalThisValue]] of the global environment record will be returned.
        
    4. Deciding Outer Lexical Environment Reference
        
        The Outer Environment Reference refers to the upper scope(outer Lexical Environment). The currently evaluating code === global code → the “null”  is bound to the Outer Lexical Environment Reference. 
        
3. Global code execution
    
    Now the global code gets executed sequentially from top to bottom (since JavaScript is an interpreted language). the variable assignment happens to allocate values to the global variable x and y. And the global function foo() gets called.
    
4. foo() function code evaluation
    
    **status quo: right before the foo(20) is called.
    
    1. Function Execution context created
        
        When you call the foo() function, the code outside of the function stops for a moment and the code inside the function runs. Firstly, JavaScript engine creates foo() function execution context. After the function Lexical Environment is completed, the function execution context is pushed to Execution Context Stack as the running execution context(means it’s at the top of the stack, physically above the previously running EC).
        
    2. Function Lexical Environment created
        
        JavaScript engine creates foo() function Lexical environment which then bound to the function execution context. 
        
        1. Function Environment Record created
            
            Function Environment Record, one of the components that compose function Lexical Environment, registers and manages the parameters, arguments objects, local variables, and nested functions declared inside the function.
            
        2. this binding
            
            The function environment record’s (here, the identifier in the lexical environment) internal slot [[ThisValue]] has its allocated value of this. What to bind to the internal slot [[ThisValue]] is dependent on how you call the method (함수 호출 방식). Since the method is called normally, this  === window here.
            
        3. Deciding the OuterLexicalEnvironment Reference
            
            At the moment when the foo function declaration is evaluated, the currently being executed execution context’s Lexical environment( Global Lexical Environment in this case) is referenced by the OuterLexicalEvnrionment. 렉시컬 환경의 외부 렉시컬 환경에 대한 참조에 할당되는 것은 함수의 상위 스코프를 가리키는 함수 객체의 내부슬롯 [[Environment]]에 저장된 렉시컬 환경의 참조이다.
            
    
    5.  foo function code execution
    
    The runtime starts and the foo function’s code gets executed sequentially. the parameters gets the arguments and the local variables x and y gets are assigned their value as well. Then, the bar() function gets called.
    
    1. bar function code evaluation
        
        **status quo: right before the bar() function is called. 
        
        the rest of the evaluation process is similar with that of foo() function.
        
    2. bar function code execution
        1. identifier “console” searched
            
            Firstly, JavaScript engine searches “console” identifier in the scope chain.
            
            - it fails to search it in the bar() function Lexical Environment. Move to foo() LE
            - it fails to search it in the foo() function Lexical Environment. Move to global LE
            - it can find the “console” identifier in the window(global object) through Object Environment Record’s BindingObject.
        2. “log” method searched
            
            log method is console’s own property(method). it’s not an inherited one.
            
        3. expression “a + b + x + y + z” evaluation.
            
            current LE → until the engine finds every value needed to complete the expression.
            
            | found in foo() LE | found in bar() LE |
            | --- | --- |
            | a, x, y | b, z |
        4. the result of the expression is passed to the console.log() method.
    3. bar function code termination
        
        JavaScript engine has no more code to execute inside the bar function so the bar function execution context is popped from the ECS(execution context stack). → also means the foo EC stack becomes the running execution stack. Although the bar execution context is popped from the stack, it doesn’t mean that the bar() Lexical Environment which used to be referred to by the bar EC is gone. it’s not gone until it’s removed from the memory by the garbage collector. 
        
    4. foo function code termination
        
        Once the bar function is terminated, there is no code to be executed. Then the foo function EC is popped from the ECS, making the global EC the running EC.
        
    5. global code termination
        
        Once the foo function is terminated, there is no code to be executed. Then the global function EC is popped from the ECS, leaving vacancy on the stack.