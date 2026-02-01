
# Core JavaScript Concepts

  

## Scope and Closures

### Global Scope
Visible everywhere in your app (inside & outside functions/blocks).
```javascript
let globalVar = "I'm global";
function test() {
	console.log(globalVar);
}
test(); // I'm global
console.log(globalVar); // I'm global
```

- Declared outside all functions/blocks

### Function Scope
Variables declared **inside a function** stay inside that function.
```javascript
function test() {
  let functionVar = "I'm inside function";
  console.log(functionVar);
}
test(); // works
console.log(functionVar); // ❌ ReferenceError
```

**Applies to:**
- let 
- var
- const

Outside the function = **no access**

### Block Scope
Variables declared inside `{}` blocks like:
-   `if`
-   `for`
-   `while`
-   `{}`

```javascript
if (true) {
  let blockVar = "I'm block scoped";
  const blockConst = "Me too";
}
console.log(blockVar); // ❌ ReferenceError
```

- Only `let` and `const` are block scoped
- `var` is not block scoped

## Lexical Scoping
Lexical scoping means a function’s scope is determined by where it is defined in the source code, and inner functions have access to outer scopes.

> Inner functions can access variables from their outer functions.  
> Outer functions can’t access inner variables.

**Example:**
```javascript
let a = 10;

function outer() {
  let b = 20;
  function inner() {
    let c = 30;
    console.log(a, b, c);
  }
  inner();
}
outer(); // Output: 10 20 30
```
- `inner()` can access:
	- it's own scope `c`
	- parent scope `b`
	- global scope `a`
- This process is called **scope chaining**

### An example for lexical + closures
```javascript
function outer() {
	let x = 100;
	function inner() {
		console.log(x);
	}
	return inner;
}
const fn = outer();
fn(); // 100
```

## Closures: Functions that remember their lexical scope
A closure is a function that retains access to its lexical scope even after the outer function has finished execution.

**Downsides :**
- can cause memore leaks if overused
- be careful with closures in leaks and event listeners

```javascript
function outer() {
  let count = 0;
  function inner() {
    count++;
    console.log(count);
  }
  return inner;
}
const counter = outer();

counter(); // 1
counter(); // 2
counter(); // 3
```


