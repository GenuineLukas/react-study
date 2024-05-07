# Execution Context and Block-level scope

Unlike variables declared with var keyword, the ones declared with the const/let keyword considers every code block(function, if, for, while, try/catch statements) as local scope.

```jsx
let x = 1;

if(true) {
	let x = 10; 
	console.log(x); //10
}

console.log(x); //1
```

when the if statement block is executed, the block-level scope for the if statement should be created. To do this, JavaScript engine creates the Lexical Environment that has the declarative environment record. At this time, the OuterLexicalEnvrionmentReference of the newly created Lexica Environment is referring to the Lexical Environment before the if statement’s execution.

![Untitled](Execution%20Context%20and%20Block-level%20scope%20ca51f7d99960403bb71c01052d7c25cc/Untitled.png)