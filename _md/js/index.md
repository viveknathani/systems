
[meta]: # (CSS_URL=../theme.css)
[meta]: # (DOCUMENT_TITLE=systems - viveknathani)

# javascript

JS is pretty cool. It is fundamental for websites that go beyond basic usecases. But, most people don't take the time to understand it fully. This document, hopefully covers the basic ground needed to be good at JS, along with some historical info.

## specification, engines
The original specification of JavaScript is called ECMAScript. The component that executes JS code is called as the engine. Engines can be interpreter-based or just-in-time compilation based. Most are latter these days. Some popular engines:

1. V8 (runs in chrome, edge)
2. SpiderMonkey (runs in firefox)

Most modern day browsers provide support for widely used and latest ECMAScript standards. In addition, the browser provides a ton of [APIs](https://developer.mozilla.org/en-US/docs/Web/API) that make JS more powerful.


## char set, variables

- JS has Unicode character set.
- three kinds of variable declarations: var, let, const
- const means don't change but the properties of objects assigned to constants are not protected.
- a variable declared using the var or let statement with no assigned value specified has the value of undefined.
- the undefined value behaves as false when used in a boolean context.
- the undefined value converts to NaN when used in numeric context.
- when you evaluate a null variable, the null value behaves as 0 in numeric contexts and as false in boolean contexts.
- data types as per ECMAScript2015: Boolean, null, undefined, Number, BigInt, String, Symbol, Object.

## hoisting
- another unusual thing about variables in JavaScript is that you can refer to a variable declared later, without getting an exception. this is called hositing. variables are lifted to the top of the function/statement but they return a value of undefined. 
- because of hoisting, all var statements in a function should be placed as near to the top of the function as possiblle.
- In ECMAScript 2015, let and const are hoisted but not initialized. Referencing the variable in the block before the variable declaration results in a ReferenceError, because the variable is in a "temporal dead zone" from the start of the block until the declaration is processed.
- Functions are hoisted if they're defined using function declarations — but functions are not hoisted if they're defined using function expressions.


