<!-- Professional JavaScript for web developers, third edition, NCZ -->
# **CONTENTS**
- ## [Variables](#var)
    - ### [Hoisting](#hst)
- ## [Operators](#opr)
    - ### [Bitwise operations](#bo)
    - ### [Relational operators and equality operators](#roeo)
- ## [Data types](#dttp)
    - ### [Primitive wrapper types](#pwt)
    - ### [Numbers](#nu)
        - #### [Number methods](#nmd)
    - ### [Strings](#str)
        - #### [String methods](#smd)
    - ### [Boolean](#bln)
    - ### [Arrays](#arrs)
        - #### [Array methods](#amd)
        - #### [Array sort](#ast)
    - ### [Type conversion](#tc)

<a id="cnt2"></a>

- ## [Flow control](#fc)
- ## [Reference types, objects](#ob)
    - ### [Types of properties](#top)
    - ### [Creating objects](#cob)
        - #### [Constructor/prototype pattern](#ccpp)
    - ### [prototype](#pro)
    - ### [Inheritance](#inher)
        - #### [Combination inheritance](#cinh)
        - #### [Parasitic combination pattern](#pcp)
    - ### [Date](#dat)
    - ### [RegExp](#Reg)
    - ### [Singleton built-in objects](#sbio)
        - #### [The Global object](#tgo)
        - #### [The Math object](#mth)
    - ### [Tamper-proof objects](#tpo)
- ## [Execution context and scope](#scp)
    - ### [Garbage collection](#gcll)

<a id="fun"></a>

- ## [Functions](#fu)
    - ### [Recursion](#rec)
    - ### [Closure](#clo)
    - ### [Private variables](#pvar)
    - ### [**this**](#thi)
    - ### [Function properties and methods](#fpm)
    - ### [Advanced functions](#advf)
        - #### [Safe type detection](#std)
        - #### [Scope-safe constructors](#ssc)
        - #### [Lazy loading functions](#llf)
        - #### [Function binding](#fbd)
        - #### [Function currying](#fcur)

- ## [The Browser Object Model](#bom)

<a id="fcl"></a>

- ## [Errors](#err)
- ## [Debugging](#dbg)
- ## [Strict mode](#strm)
- ## [Best practices](#bp)
<br /><br /><br /><br />
# Basics
- A complete JavaScript implementation is made up of:
    - The Core (European Computer Manufacturers Association, ECMAScript "ek-ma-script")
        - ECMAScript has no methods for input or output. ECMA-262 defines this language as a base upon which more-robust scripting languages may be built. Web browsers are just one host environment in which an ECMAScript implementation may exist. A host environment provides the base implementation of ECMAScript and implementation extensions designed to interface with the environment itself. 

        - Extensions, such as the Document Object Model (DOM), use ECMAScript's core types and syntax to provide additional functionality that's more specific to the environment. 
        - Other host environments include NodeJS, a server-side JavaScript platform, and Adobe Flash.
        - ECMAScript is simply a description of a language implementing all of the facets described in the specification. JavaScript implements ECMAScript, but so does Adobe ActionScript.
    - The Document Object Model (DOM)
        - It's an application programming interface (API) for XML that was extended for use in HTML. The DOM maps out an entire page as a hierarchy of nodes. Each part of an HTML or XML page is a type of a node containing different kinds of data. DOM provides methods and interfaces for working with the content of a web page.

        - DOM is not JavaScript-specific and indeed has been implemented in numerous other languages.
    - The Browser Object Model (BOM)

        - BOM deals with the browser window and frames, but generally any browser-specific extension to JavaScript is considered to be a part of the BOM. Using the BOM, developers can interact with the browser outside of the context of its displayed page. It was the only part of a JavaScript implementation that had no related standard. This changed with the introduction of HTML5, which sought to codify much of the BOM as part of a formal specification.
- **Case Sensitive**.
## Terms
- The computation is called an **evaluation**.
## Where & How
1. Scripts (including external scripts) can be placed in the `<body>`, or in the `<head>` section of an HTML page, or in both.
2. The script will behave as if it was located exactly where the `<script>` tag is located.  
3. It's OK to add several script files to one page. Just use several script tags.  
## External JavaScript Advantages
- It separates HTML and code
- It makes HTML and JavaScript easier to read and maintain
- Cached JavaScript files can speed up page loads  
## 4 ways of displaying data
1. Writing into an HTML element, using **innerHTML**.
2. Writing into the HTML output using **document.write()**.
    > Only for test purposes.  
    > Using document.write() after an HTML document is fully loaded, will delete all existing HTML. 
3. Writing into an alert box, using **window.alert()**.
4. Writing into the browser console, using **console.log()**.
    > For debugging purposes.  
## Identifiers
1. The first character must be ~~a digit~~, a letter, or an underscore (`_`), or a dollar sign (`$)`.
2. Subsequent characters may be digits, letters, underscores, or dollar signs.  

- Tend to use camel case that starts with a lowercase letter (lower camel case). 

    ```javascript
    var firstName, lastName, masterCard, interCity; 
    ```

- The reserved word list does not include some words that should have been reserved but were not, such as *`undefined`*, `NaN`, and `Infinity`.
## Statements
- Ending statements with semicolon is not required, but highly recommended.
## Comments
- It is most common to use single line comments.  
- Block comments are often used for formal documentation.  
    > The `/* */` form of block comments can also occur in regular expression literals, so block comments are not safe for commenting out blocks of code. So, it is recommended that `/* */` comments be avoided and `//` comments be used instead.

    ```javascript
    /*
    var rm_a = /a*/.match(s);
    */
    ```

<a id="var"></s>

# [Variables](#)

```javascript
var person = "John Doe", carName = "Volvo", price = 200;

var person = "John Doe",
    carName = "Volvo",
    price = 200;
```
- A variable without a value has the value *undefined*. Any variable can be emptied, by setting the value to *undefined*. 
- Redeclare a JavaScript variable, and it will not lose its value.  

<a id="hst"></a>

## [Hoisting](#)
- Hoisting is JavaScript's default behavior of moving all declarations to the top of the current scope (to the top of the current script or the current function). As a result of hoisting, a variable can be used before it has been declared. But initializations are not hoisted.
- JavaScript in strict mode does not allow variables to be used if they are not declared.
- **Function declarations** are read and added to the execution context before the code begins running through a process called ***function declaration hoisting***. As the code is being evaluated, the JavaScript engine does a first pass for function declarations and pulls them to the top of the source tree. So even though the function declaration appears after its usage in the actual source code, the engine changes this to *hoist* the function declarations to the top. **Function expressions** aren't complete until the execution reaches that line of code. The function is part of an initialization statement, not part of a function declaration. So no hoist in function expressions.

    ```javascript
    alert(typeof sum);      // undefined
    alert(sum(10,10));      // error
    var sum = function(num1, num2){
        return num1 + num2;
    };
    ```

- Any variables or functions created inside of `eval()` will not be hoisted, as they are contained within a string when the code is being parsed. They are created only at the time of `eval()` execution. 

<a id="opr"></a>

# [Operators](#)
- Operators are unique in ECMAScript in that they can be used on a wide range of values, including strings, numbers, Booleans, and even objects.
- Operations that have the same precedence are computed from left to right.

Operator|Description
--|---
. [] ( )| Refinement and invocation
delete new typeof + - !| Unary operators
* / %| Multiplication, division, modulo
+ -| Addition/concatenation, subtraction
>= <= > <| Inequality
=== !== | Equality
&& | Logical and
`||` | Logical or
?:| Ternary

## Unary operators
- When using either a prefix increment or a prefix decrement, the variable's value is changed before the statement is evaluated. Postfix increment and decrement differ from the prefix versions in one important way: the increment or decrement doesn't occur until after the containing statement has been evaluated.
    - When used on a string that is a valid representation of a number, convert to a number and apply the change. The variable is changed from a string to a number.

    - When used on a string that is not a valid number, the variable's value is set to `NaN`. The variable is changed from a string to a number.
    - When used on a Boolean value that is false, convert to 0 and apply the change. The
    variable is changed from a Boolean to a number.
    - When used on a Boolean value that is true, convert to 1 and apply the change. The variable is changed from a Boolean to a number.
    - When used on a floating-point value, apply the change by adding or subtracting 1.
    - When used on an object, call its `valueOf()` method to get a value to work with. Apply the other rules. If the result is `NaN`, then call `toString()` and apply the other rules again. The variable is changed from an object to a number.

        ```javascript
        var f = 1.1;
        --f;        // 0.10000000000000009
        var o = {
            valueOf: function() {
                return -1;
            }
        }
        --o;        // -2
        ```

- Unary plus does nothing to a numeric value. When the unary plus is applied to a nonnumeric value, it performs the same conversion as the `Number()` casting function. Unary minus negates a numeric value. When used on nonnumeric values, unary minus applies all of the same rules as unary plus and then negates the result. 

<a id="bo"></a>

## [Bitwise operations](#)
- The bitwise operators work with **integers**. JavaScript doesn't have integers. JavaScript stores numbers as 64 bits floating point numbers, but all bitwise operations are performed on 32 bits binary numbers.
- Before a bitwise operation is performed, JavaScript converts numbers to 32 bits signed integers. After the bitwise operation is performed, the result is converted back to 64 bits JavaScript numbers. A curious side effect of this conversion is that the special values `NaN` and Infinity both are treated as equivalent to 0 when used in bitwise operations.
- By default, all integers are represented as signed in ECMAScript.
- If a bitwise operator is applied to a nonnumeric value, the value is first converted into a number using the `Number()` function (this is done automatically) and then the bitwise operation is applied. The resulting value is a number.
- **The first bit is bit 0**. There is no access to bit 31 when dealing with signed integers.
- Signed integers use the first 31 of the 32 bits to represent the numeric value of the integer. The 32nd bit (sign bit) represents the sign of the number: 0 for positive or 1 for negative. If any bits are unused, they are filled with 0 and essentially ignored.
- Negative numbers are in a format called `two's complement`. It's is calculated in three step:
    1. determine the binary representation of the absolute value
    1. bitwise NOT every digit
    1. add 1 to the result
### Bitwise NOT
- The end effect of the bitwise NOT (tilde `~`) is that it negates the number and subtracts 1.
### Bitwise AND
- ampersand `&`.
### Bitwise OR
- pipe `|`.
### Bitwise XOR
- caret `^`.
### Left shift
- The left shift (two less-than signs`<<`) and shifts all bits in a number to the left by the number of positions given and fill the the empty bits on the right side with 0. It preserves the sign of the number it's operating on.
### Signed sight shift
- The signed right shift (two greater-than signs `>>`) shifts all bits in a 32-bit number to the right while preserving the sign (positive or negative). The empty bits occurring at the left of the number but **after the sign bit** were **filled with the value in the sign bit** to create a complete number.
### Unsigned right shift
- The unsigned right shift (three greater-than signs `>>>`) shifts **all bits** in a 32-bit number to the right. The empty bits get filled with zeros regardless of the sign of the number.
## Boolean operators
### Logical NOT
- The logical NOT operator (exclamation point `!`) can be applied to any value. This operator always returns a `Boolean` value, regardless of the data type it's used on. The logical NOT operator first converts the operand to a `Boolean` value and then negates it.
- Using two NOT (`!!`) operators in a row simulates the behavior of the `Boolean()` casting function. The first NOT returns a `Boolean` value no matter what operand it is given. The second NOT negates that `Boolean` value and so gives the true `Boolean` value of a variable.
### Logical AND
- Logical AND can be used with any type of operand. The logical AND operator is a **short-circuited** operation, meaning that if the first operand determines the result, the second operand is never evaluated.
- The `&&` operator produces the value of its first operand if the first operand is falsy. Otherwise, it produces the value of the second operand.  
### Logical OR
- The logical OR operator is **short-circuited**. In this case, if the first operand evaluates to true, the second operand is not evaluated.
- The `||` operator produces the value of its first operand if the first operand is truthy. Otherwise, it produces the value of the second operand.

    ```javascript
    var myObject = preferredObject || backupObject;
    ```

## Multiplicative operators and additive operators
- There are three multiplicative operators in ECMAScript: multiply, divide, and modulus. If either of the operands for a multiplication operation isn't a number, it is converted to a number behind the scenes using the `Number()` casting function (automatic type conversion). This means that an empty string is treated as 0, and the Boolean value of true is treated as 1.
    - If `Infinity` is multiplied by 0, the result is `NaN`.
    - If `Infinity` is divided by `Infinity`, the result is `NaN`.
    - If zero is divided by zero, the result is `NaN`.
    - If `Infinity` is divided by any number, the result is either `Infinity` or `–Infinity`, depending on the sign of the second operand.
    - The `/` operator can produce a noninteger result even if both operands are integers.
    - If the dividend is an infinite number and the divisor is a finite number, the result is `NaN`.
    - If the dividend is a finite number and the divisor is 0, the result is `NaN`.
    - If the dividend is a finite number and the divisor is an infinite number, then the result is the dividend. 
- For add operator:
    - If either operand is an object, number, or Boolean, its `toString()` method is called to get a string value and then the previous rules regarding strings are applied. For *undefined* and *null*, the `String()` function is called to retrieve the values "undefined" and "null", respectively.
    - If –0 is added to +0, the result is +0.
    - If –0 is added to –0, the result is –0.
- For subtract operator:
    - If +0 is subtracted from +0, the result is +0.
    - If –0 is subtracted from +0, the result is –0.
    - If –0 is subtracted from –0, the result is +0.
    - If either operand is a string, a Boolean, *null*, or *undefined*, it is converted to a number (using `Number()` behind the scenes) and the arithmetic is calculated using the previous rules.
    - If either operand is an object, its `valueOf()` method is called to retrieve a numeric value to represent it. If that value is `NaN`, then the result of the subtraction is `NaN`. If the object doesn't have `valueOf()` defined, then `toString()` is called and the resulting string is converted into a number.

        ```javascript
        5 - true;           // 4
        5- "";              // 5
        5- null;            // 5
        ```

- JavaScript will try to convert strings to numbers in all numeric operations except for `+` operator.

<a id="roeo"></a>

## [Relational operators and equality operators](#)
- 4 relational operators: less-than (`<`), greater-than (`>`), less-than-or-equal-to (`<=`), greater-than-or-equal-to (`>=`). Each of them returns a Boolean value.
    - The result of any relational operation with `NaN` is false.
    - If the operands are strings, compare the character codes of each corresponding character in the string. The character codes of uppercase letters are all lower than the character codes of lowercase letters.

    - If one operand is a number, convert the other operand to a number and perform a numeric comparison. 
    - If an operand is an object, call `valueOf()` and use its result to perform the comparison according to the previous rules. If `valueOf()` is not available, call `toString()` and use that value according to the previous rules. 
    - If an operand is a Boolean, convert it to a number and perform the comparison.
- Equal and not equal to perform conversion before comparison (type coercion), and identically equal and not identically equal to perform comparison without conversion.
    - If an operand is a `Boolean` value, convert it into a numeric value before checking for equality. A value of false converts to 0, whereas a value of true converts to 1.
    - If one operand is a string and the other is a number, attempt to convert the string into a number before checking for equality.
    - If one of the operands is an object and the other is not, the `valueOf()` method is called on the object to retrieve a primitive value to compare according to the previous rules.
    - **Values of *null* and *undefined* are equal**.
    - Values of *null* and *undefined* cannot be converted into any other values for equality checking.
    - If either operand is `NaN`, the equal operator returns false and the not-equal operator returns true.
    - If both operands are objects, then they are compared to see if they are **the same object**.

    ```javascript
    null == undefined;      // true
    undefined == 0;         // false
    null == 0;              // false
    null === undefined;     // false
    ```

## Conditional operators, assignment operators, and comma operator
- Compound-assignment operators are designed specifically as shorthand ways of achieving operations in ECMAScript. They do not represent any performance improvement.
- The comma operator allows execution of more than one operation in a single statement. When used in assigning values, it always returns the **last item** in the expression.


    ```javascript
    variable = boolean_expression ? true_value : false_value;

    var num = (5, 1, 4, 8, 0);      
    num;                        // 0
    ```

<a id="dttp"></a>

# [Data types](#)
- The values produced by `typeof` are "number", "string", "boolean", "*undefined*", "function", and "object". If the operand is an array or null, then the result is 'object', which is wrong. The **primitive types** of JavaScript are numbers, strings, booleans (true and false), null, and *undefined*. All other values are objects. 
    > ECMA-262 specifies that any object implementing the internal `[[Call]]` method should return "function" from `typeof`.

    ```javascript
    typeof undefined    //--> type is also undefined
    typeof ""           //--> value is "", type is string
    typeof null         //--> type is object
    ```

    1. *null* is considered to be an empty object reference, an empty object pointer. When defining a variable that is meant to later hold an object, it is advisable to initialize the variable to *null* as opposed to anything else. That way, you can explicitly check for the value *null* to determine if the variable has been filled with an object reference at a later time.

    1. A variable containing the value of *undefined* is different from a variable that hasn't been declared at all. Though the `typeof` operator returns *undefined* when called on an undeclared variable, which can be a bit confusing. 

        ```javascript
        var a;
        typeof a;           // undefined
        typeof b;           // undefined

        console.log(a);     // undefined
        console.log(b);     // ReferenceError
        ```

    - **The value *undefined* is a derivative of *null***, so ECMA-262 defines them to be superficially equal (==). *undefined* and *null* are equal in value but different in type.
- Primitive variables are of a **fixed size** and accessed by value. They are stored in memory **on the stack**, hard coded and immutable. Reference values are objects and are stored in memory **on the heap**. JavaScript does not permit direct access of memory locations. Manipulating an object means working on a reference to that object rather than the actual object itself.
- When a primitive value is assigned from one variable to another, the value stored on the variable is copied into the location for the new variable. Each of these variables can now be used separately with no side effects. When a reference value is assigned from one variable to another, the value copied into the location for the new variable is is actually **a pointer** to an object stored on the heap. Once the operation is complete, two variables point to exactly the same object, so changes to one are reflected on the other.
 
- The `instanceof` operator returns `true` if the variable is an instance of the given reference type (identified by its *prototype* chain). All reference values, by definition, are instances of `Object`. If `instanceof` is used with a **primitive value**, it will always return `false`, because primitives aren't objects.

    > The `valueOf()` method is used internally in JavaScript to convert `Number` objects to primitive values.
- All JavaScript data types have a `valueOf()` and a `toString()` method.

<a id="pwt"></a>

## [Primitive wrapper types](#)
- 3 special **reference** types are designed to ease interaction with primitive values: the `Boolean` type, the `Number` type, and the `String` type. Every time a primitive value is read, an object of the corresponding primitive wrapper type is created behind the scenes, allowing access to any number of methods for manipulating the data. Each of the wrapper types maps to the primitive type of the same name. For example, any time a string value is accessed in read mode (which is to say its value is being read from memory), the following three steps occur:
    1. Create an instance of the `String` type.
    2. Call the specified method on the instance.
    3. Destroy the instance.

    ```javascript
    var s1 = "some text";
    var s2 = s1.substring(2);

    // as if
    var s1 = new String("some text");
    var s2 = s1.substring(2);
    s1 = null;
    ```

- The major difference between reference types and primitive wrapper types is the lifetime of the object. When you instantiate a reference type using the `new` operator, it stays in memory until it goes out of scope, whereas **automatically** created primitive wrapper objects exist for only **one line of code** before they are destroyed. This means that properties and methods cannot be added at runtime even though attempting to do so won't cause an error.

    ```javascript
    var name = "SB";
    name.age = 26;
    name.age;       // undefined
    ```

- It is possible to create the primitive wrapper objects explicitly using the `Boolean`, `Number`, and `String` constructors. This should be done only when absolutely necessary because it is often confusing for developers as to whether they are dealing with a primitive or reference value. Calling `typeof` on an instance of a primitive wrapper type returns "object", and all primitive wrapper objects convert to the `Boolean` value true.
- The `Object` constructor also acts as a factory method and is capable of returning an instance of a primitive wrapper based on the type of value passed into the constructor. Calling a primitive wrapper constructor using `new` is not the same as calling the casting function of the same name.

    ```javascript
    var obj = new Object("text");
    obj instanceof String;          // true

    var value = "4";
    var number = Number(value);     // casting function
    typeof number;                  // "number"
    var obj = new Number(value);    // constructor
    typeof obj;                     // "object"
    ```


<a id="nu"></a>

## [Numbers](#) 
Value(aka fraction/mantissa) | Exponent | Sign
---|---|---
52 bits (0 - 51) | 11 bits (52 - 62)  | 1 bit (63)

- JavaScript has a single number type internally represented as 64-bit floating point (IEEE-754 format) to represent both integers and floating-point values. There is no separate integer type. Including a decimal point and at least one number after the decimal point defines a floating-point value. Storing floating-point values uses twice as much memory as storing integer values. ECMAScript always looks for ways to convert floating-point values into integers.
    - When there is no digit after the
    decimal point, the number becomes an integer. 

    - If the number being represented is a whole number (such as 1.0), it will be converted into an integer.

        ```javascript
        var floatN1 = 1.;   // interpreted as integer 1
        var floatN2 = 1.0;  // interpreted as integer 1
        ```

- Integers are accurate to **15** digits. Floating-point values are accurate up to **17** decimal places but are far less accurate in arithmetic computations than whole numbers. To solve the problem, it helps to multiply and divide. Never test for specific floating-point values.

    ```javascript
    var x = 999999999999999;   // x will be 999999999999999
    var y = 9999999999999999;  // y will be 10000000000000000


    var x = 0.2 + 0.1;         // x will be 0.30000000000000004

    var y = (0.2 * 10 + 0.1 * 10) / 10;       // y will be 0.3
    ```

- The smallest and largest number that can be represented in ECMAScript is stored in `Number.MIN_VALUE` (5e-324) and `Number.MAX_VALUE` (1.7976931348623157e+308). If a calculation results in a number that cannot be represented by JavaScript's numeric range, the number automatically gets the special value of `Infinity` or `-Infinity`. If a calculation returns either positive or negative `Infinity`, that value cannot be used in any further calculations, because Infinity has no numeric representation with which to calculate. `isFinite()` function determines if a value is finite.

    ```javascript
    isFinite(Number.MAX_VALUE * 2);     // false
    isFinite(-Infinity + Infinity);     // false 
    ```

- The value `NaN` is a number value that is the result of an operation that cannot produce a normal result. In ECMAScript, dividing a number by  a non-number returns `NaN`, which allows other processing to continue. Any operation involving `NaN` always returns `NaN`. `NaN` is not equal to any value, including itself. ECMAScript provides the `isNaN()` function. This function accepts a single argument, which can be of any data type. When a value is passed into `isNaN()`, an attempt is made to convert it into a number. Any value that cannot be converted into a number causes the function to return true. `isNaN()` returns true when a variable without initialization is passed in.

    ```javascript
    isNaN(NaN);         // true
    isNaN("abc");       // true
    isNaN("1");         // false (converted to 1)    
    isNaN(false);       // false (converted to 0)

    var a;
    isNaN(a);           // true
    ```

    > `isNaN()` can be applied to objects. In that case, the object's `valueOf()` method is first called to determine if the returned value can be converted into a number. If not, the `toString()` method is called and its returned value is tested as well. This is the general way that built-in functions and operators work in ECMAScript.

- `NaN` is of number type. Each of `Infinity` and `-Infinity` is a number. Positive zero (`+0`) and negative zero (`–0`) are considered equivalent in all cases.

    ```javascript
    typeof(NaN);
    typeof(Infinity);
    typeof(-Infinity);
    // --> all 3 are "number"
    ```

- JavaScript interprets numeric constants preceded by `0x` (case insensitive) as hexadecimal. Some JavaScript versions interpret numbers with a leading `0` as octal. Octal literals are invalid when running in strict mode and will cause the JavaScript engine to throw a syntax error. **Numbers created using octal or hexadecimal format are treated as decimal numbers in all arithmetic operations**.

    ```javascript
    var octalNum1 = 070;     
    octalNum1;                  // 56
    var octalNum2 = 079;        
    octalNum2;                  // invalid octal, interpreted as 79
    var octalNum3 = 08;         
    octalNum3;                  // invalid octal, interpreted as 8 
    ```

- Instances of `Number` object overrides `valueOf()`, `toLocaleString()`, and `toString()`. The `valueOf()` method returns the primitive numeric value represented by the object, whereas the other two methods return the number as a string.

<a id="nmd"></a>

### [Number methods](#)
#### [**`toString()`**](#cts)
#### **`toFixed()`, `toExponential()`, `toPrecision()`**
- The `toFixed()` method returns a **string** representation of a number with a specified number of decimal points. If the number has more than the given number of decimal places, the result is rounded to the nearest decimal place. The `toFixed()` method can represent numbers with 0 through 20 decimal places.
- The By default, `toExponential()` method returns a **string** with the number formatted in exponential notation. It accepts one argument, which is the number of decimal places to output. ECMAScript converts any floating-point value with at least **six** zeros after the decimal point into e-notation. 100 and `1e2` are the same number.
- The `toPrecision()` method returns either the fixed or the exponential representation of a number, depending on which makes the most sense. This method takes one argument, which is the total number of digits to use to represent the number (not including exponents). The `toPrecision()` method can represent numbers with 1 through 21 decimal places.

    ```javascript
    var x = 9.656;

    x.toFixed();            // "10" (rounded)
    x.toFixed(0);           // "10"
    x.toFixed(2);           // "9.66"
    x.toFixed(4);           // "9.6560"


    x.toExponential();      // "9.656e+0"
    x.toExponential(2);     // "9.66e+0"
    x.toExponential(4);     // "9.6560e+0"


    x.toPrecision();        // "9.656"
    x.toPrecision(2);       // "9.7"
    x.toPrecision(4);       // "9.656"
    x.toPrecision(6);       // "9.65600"
    var y = 99;
    y.toPrecision(1);       // "1e+2"
    ```

#### **`Number()`**
- The `Number()` casting function can be used on any data type.
    - When applied to Boolean values, true and false get converted into 1 and 0, respectively.
    - When applied to numbers, the value is simply passed through and returned.
    - When applied to *null*, `Number()` returns 0.
    - When applied to *undefined*, `Number()` returns `NaN`.
    - When applied to strings:
        - If the string contains only numbers, optionally preceded by a plus or minus sign, it is always converted to a decimal number leading zeros are ignored.

        - If the string contains a valid floating-point format,  it is converted into the appropriate floating-point numeric value (leading zeros are ignored).
        - If the string contains a valid hexadecimal format, it is converted into an integer that matches the hexadecimal value.
        - If the string is empty, it is converted to 0.
        - If the string contains anything other than these previous formats, it is converted into `NaN`.
    - When applied to objects, the `valueOf()` method is called and the returned value is converted based on the previously described rules. If that conversion results in `NaN`, the `toString()` method is called and the rules for converting strings are applied.

    ```javascript
    Number(070);            // 56
    Number("070");          // 70
    Number(0xf);            // 15
    Number("0xf");          // 15
    Number(true);           // 1
    Number(undefined);      // NaN
    Number(null);           // 0
    Number("");             // 0
    Number("10 20");        // NaN
    Number(new Date());     // 1509610811019
    ```

#### **`parseInt()`, `parseFloat()`**
- `parseInt()` parses a **string** and **returns a whole number**. It examines the string much more closely to see if it matches a number pattern. Leading white space in the string is ignored until the first non–white space character is found. If this first character isn't a number, the minus sign, or the plus sign, `parseInt()` always returns `NaN`, which means the ***empty string*** returns `NaN`. If the first character is a number, plus, or minus, then the conversion goes on to the second character and continues on until either the end of the string is reached or a **nonnumeric character** is found. It also recognizes the various integer formats (decimal, hexadecimal; the ability to parse octal values has been removed from `parseInt()` in ECMAScript 5). `parseInt()` provides a second argument: the radix (number of digits) to use. The prefix can be left off when a radix is provided. It's advisable to always include a radix to avoid errors.
- The `parseFloat()` function works in a similar way. A decimal point is valid the first time it appears. Initial zeros are always ignored, so hexadecimal numbers always become 0. `parseFloat()` parses **only decimal values**, there is **no radix mode**. If a  string represents a whole number, `parseFloat()` returns an integer.

    ```javascript
    parseInt("");           // NaN
    parseInt("10");         // 10
    parseInt("10.33");      // 10
    parseInt("10 20 30");   // 10
    parseInt("10years");    // 10
    parseInt("years 10");   // NaN
    parseInt("0xA");        // 10
    parseInt("000xA");      // 0 
    parseInt("070");        // 70 

    parseInt("3.141e6");    // 3 
    parseInt("3e6");        // 3
    
    parseInt("0xAF", 16);   // 175
    parseInt("AF", 16);     // 175


    parseFloat("0xA");      // 0
    parseFloat("12.34.5");  // 12.34 
    parseFloat("012.2");    // 12.2
    parseFloat("3.141e6");  // 3141000
    parseFloat(3.141e6);    // 3141000
    parseFloat("3e6");      // 3000000
    ```

### Number properties
Number properties belongs to the JavaScript's number object wrapper called `Number`. These properties can only be accessed as `Number.MAX_VALUE`. Using `myNumber.MAX_VALUE`, where `myNumber` is a variable, expression, or value, will return *undefined*. 

property|Description
---|---
MAX_VALUE           |Returns the largest number possible in JavaScript
MIN_VALUE           |Returns the smallest number possible in JavaScript
NEGATIVE_INFINITY   |Represents negative infinity (returned on overflow)
NaN                 |Represents a "Not-a-Number" value
POSITIVE_INFINITY   |Represents infinity (returned on overflow)

 <a id="str"></a>

## [Strings](#)
- JavaScript was built at a time when Unicode was a 16-bit character set, so all characters in JavaScript are 16 bits wide. Strings can be delineated by either double quotes (`"`) or single quotes (`'`). JavaScript does not have a character type. To represent a character, make a string with just one character in it.
- `\xnn` is a character represented by hexadecimal code nn (where n is a hexadecimal digit 0-F). `\unnnn` is a  Unicode character represented by the hexadecimal code nnnn (where n is a hexadecimal digit 0-F). These character literals can be included anywhere with a string and will be interpreted as if they were a single character.

    ```javascript
    "A" === "\u0041";   // true
    "\u0041".length;    // 1
    ```

- Strings are immutable. Once it is made, its value cannot change. To change the string held by a variable, the original string must be destroyed and the variable filled with another string containing a new value. 

    ```javascript
    var lang = "java";
    lang += "Script";
    ```

    - This happens by creating a new string with enough space for 10 characters and then filling that string with "Java" and "Script". The last step in the process is to destroy the original string "Java" and the string "Script", because neither is necessary anymore. All of this happens behind the scenes, which is why older browsers had very slow string concatenation.

- Two strings containing exactly the same characters in the same order are considered to be the same string. 

    ```javascript
    'c' + 'a' + 't' === 'cat'
    ```

```javascript
var x = "John";             
var y = new String("John");
var z = new String("John");

// (x == y) is true because x and y have equal values
// (x === y) is false because x and y have different types (string and object)

// (y == z) and (y === z) are false because y and z are different objects
// so comparing two JavaScript objects using == or ===
// will always return false, using != or !== is otherwise  
```

- The `String` type is the object representation for strings and is created using the `String` constructor. The methods of a `String object` are available on all string primitives. All three of the inherited methods — `valueOf()`, `toLocaleString()`, and `toString()` — return the object's primitive string value. Each instance of `String` contains a single property, `length`, which indicates the number of characters in the string. Even if the string contains a **double-byte** character (as opposed to an ASCII character, which uses just one byte), each character is still counted as one.

<a id="cts"></a>

### [Converting to a string](#)
- `toString()` method return the string equivalent of the value. It is available on values that are numbers, Booleans, objects, and strings. (each string has a `toString()` method that simply returns a copy of itself.) If a value is *null* or *undefined*, this method is not available. When used on a number value, `toString()` actually accepts a single argument: the radix in which to output the number. By default, `toString()` always returns a string that represents the number as a decimal, but by passing in a radix, `toString()` can output the value in binary, octal, hexadecimal, or any other valid base.
- If the value isn't *null* or *undefined*, the `String()` casting function always returns a string regardless of the value type.
    - If the value has a `toString()` method, it is called (with no arguments) and the result is returned.
    - If the value is *null*, "null" is returned.
    - If the value is *undefined*, "undefined" is returned.
- Adding an empty string to a value using the `plus` operator will also convert a value to a string.

    ```javascript
    null.toString();        // TypeError
    undefined.toString();   // TypeError
    String(null);           // "null"
    String(undefined);      // "undefined"

    var myNumber = 128;
    var dec = -5;
    myNumber.toString();    // "128
    myNumber.toString(16);  // "80"
    myNumber.toString(8);   // "200"

    myNumber.toString(2);   //  "10000000"
    dec.toString(2);        // "-101"
    //binary 101 is decimal 5, that JS hiding the detail
    (dec >>> 0).toString(2) // "11111111111111111111111111111011"
    // [ ] replace >>> with >> or <<, the result is still -101. Reason? 
    ```

<a id="smd"></a>

### [String methods](#)
- **All string methods return a new string**. They don't modify the original string.  

#### **indexOf(), lastIndexOf()**
-  The `indexOf()` method will start searching from that position and go toward the end of the string, ignoring everything before the start position, whereas `lastIndexOf()` starts searching from the given position and continues searching toward the beginning of the string, ignoring everything between the given position and the end of the string.

    ```javascript
    "1234567890123456".indexOf("456");
    // --> 3
    "1234567890123456".lastIndexOf("456");
    // --> 13
    "1234567890123456".lastIndexOf("abc");
    // --> -1

    // indexOf() and lastIndexOf() accept a second parameter
    // as the starting position for the search
    "1234567890123456".indexOf("456", 4);
    // --> 13

    
    // locate all instances of a substring
    var str = "Lortetem ipsum tetdolor sit amet, consectetur adipisicing elit";
    var positions = [];
    var substring = "tet";
    var sublen = substring.length;
    var pos = str.indexOf(substring);

    while(pos > -1) {
        positions.push(pos);
        pos = str.indexOf(substring, pos + sublen);
    }
    positions;
    ```

#### **`slice()`, `substring()`, `substr()`**
- `slice()` extracts a part of a string and returns the extracted part in **a new string**. 
    - `slice()` takes 2 parameters: the starting index and the ending index (all characters up to this point are included except the character at that point). If the start index is undefined, `slice` begin from index `0`; if the end index it omitted or greater than the length of the sequence, `slice` extracts through the end of the sequence. 
    - For the `slice()` method, a negative argument is treated as the length of the string plus the negative argument.
- `substring()` is similar to `slice()`. For the `substring()` method, all negative numbers are converted to 0. This method **expects** that the smaller number is the starting position and the larger one is the ending position.
- `substr()` is similar to `slice()`. The second parameter specifies the **number of characters to return**. For the `substr()` method, a negative first argument is treated as the length of the string plus the number, whereas a negative second number is converted to 0. 
- If the second argument is omitted in any of the 3 methods, it is assumed that the ending position is the length of the string. 

    ```javascript
    var str = "hello JavaScript.";
    str.substring(10, -1);      // "hello Java"
    ```

#### **`match()`, `search()`, `replace()`, `split()`**
- `match()` is essentially the same as calling a `RegExp` object's `exec()` method. The `match()` method accepts a single argument, which is either a **regular-expression string** or a **`RegExp` object**.
    - If a non-RegExp object `obj` is passed, it is implicitly converted to a `RegExp` by using `new RegExp(obj)`. 
    - When the parameter is a string or a number, it is implicitly converted to a `RegExp` by using new `RegExp(obj)`. If it is a positive number with a positive sign,the `RegExp()` method will ignore the positive sign. 
    - If no parameter is specified, the result is an array with an empty string: `[""]`.
- The array returned from `match()` is the same array that is returned when the `RegExp` object's `exec()` method is called with the string as an argument: the first item is the string that matches the entire pattern, and each other item (if applicable) represents capturing groups in the expression. If there were no matches, `null` is returned.
    - The returned array has an extra `input` property, which contains the original string that was parsed. In addition, it has an `index` property, which represents the zero-based index of the match in the string.
    - If the regular expression does not include the `g` flag, `str.match()` will return the same result as `RegExp.exec()`. 
    - If the regular expression includes the `g` flag, the method returns an array containing all matched substrings rather than match objects. **Captured groups are not returned.** If there were no matches, the method returns `null`. So if `g` is set and captured groups are wanted, use `RegExp.exec()` instead.
- Patterns suffixed with `*` makes the whole pattern optional, with no point of matching at all. If the first character doesn't match, there'll be no match. 

    ```javascript
    var str = "abbbb";
    var re = /b*/;
    var re1 = /b*/g;
    var re2 = /b/g;

    console.log(str.match(re));             // ["", index: 0, input: "abbbb"]
    console.log(str.match(re1));            // ["", "bbbb", ""]
    console.log(str.match(re2));            // ["b", "b", "b", "b"]
    ```

- `search()` takes a regular expression specified by either a string or a `RegExp` object as its only argument. If a non-RegExp object `obj` is passed, it is implicitly converted to a `RegExp` by using new `RegExp(obj)`. It cannot take a second start position argument. The `search()` method returns the index of the **first** pattern occurrence in the string or –1 if it's not found. `search()` always begins looking for the pattern at the beginning of the string.

    ```javascript
    "123 456 789".search(/\b456\b/);
    // --> 4
    ```

- The `replace()` method accepts two arguments. The first argument can be a `RegExp` object or a string (the string is not converted to a regular expression), and the second argument can be a string or a function. 
    - If the first argument is a string, then only the first occurrence of the substring will be replaced. 
    - The only way to replace all instances of a substring is to provide a regular expression with the global flag specified.
- By default, the `replace()` function is case sensitive and replaces only the first match. It does not change the string it is called on. It returns a **new** string.

    ```javascript
    // replace all matches
    str = "Please visit Microsoft and Microsoft!";
    var n = str.replace(/Microsoft/g, "W3Schools");

    // make it case insensitive
    var m = str.replace(/MICROSOFT/i, "W3Schools");
    ```

- The **replacement string** can include the following special replacement patterns:

    Patterns|Inserts
    ---|---
    `$$`|	Inserts a "$".
    `$&`|	Inserts the matched substring.
    $`|	Inserts the portion of the string that precedes the matched substring.
    `$'`|	Inserts the portion of the string that follows the matched substring.
    `$n`|	Where n is a positive integer less than 100, inserts the nth parenthesized submatch string, provided the first argument was a `RegExp` object. Note that this is 1-indexed.
     | 
     
    ```javascript
    var re = /(\w+)\s(\w+)/;
    var str = "john doe";
    var newstr = str.replace(re, "$2, $1");
    console.log(newstr);
    ```

- If there's a function as the second parameter, the function will be invoked **after** the match has been performed. The function's result (return value) will be used as the replacement string. 
    - The above-mentioned special replacement patterns do not apply in this case. 
    - The function will be invoked multiple times for each full match to be replaced if the regular expression in the first parameter is global.
    - The exact number of arguments will depend on whether the first argument was a `RegExp` object and, if so, how many parenthesized submatches it specifies.The **arguments** to the function:

        Possible name|Supplied value
        ---|---
        `match`|	The matched substring. (Corresponds to `$&` above.)
        `p1, p2, ...`|	The nth parenthesized submatch string, provided the first argument to `replace()` was a `RegExp` object. (Corresponds to `$1`, `$2`, etc. above.) For example, if `/(\a+)(\b+)/`, was given, `p1` is the match for `\a+`, and `p2` for `\b+`.
        `offset`|	The offset of the matched substring within the whole string being examined. (For example, if the whole string was `'abcd'`, and the matched substring was `'bc'`, then this argument will be 1.)
        `string`|	The whole string being examined.
         | 

        ```javascript
        function replacer(match, p1, p2, p3, offset, string) {
        // p1 is nondigits, p2 digits, and p3 non-alphanumerics
        return [p1, p2, p3].join(' - ');
        }
        var newString = 'abc12345#$*%'.replace(/([^\d]*)(\d*)([^\w]*)/, replacer);
        console.log(newString);  // abc - 12345 - #$*%
        ```

- The `split()` method separates the string into an array of substrings based on a separator. The separator may be a string or a `RegExp` object. (The string is not considered a regular expression for this method.) An optional second argument, the **array limit**, ensures that the returned array will be no larger than a certain size.
- When found, `separator` is removed from the string and the substrings are returned in an array. If `separator` is not found or is omitted, the array contains one element consisting of the entire string. If `separator` is an empty string, `str` is converted to an array of characters. If `separator` appears at the beginning or end of the string, or both, the array begins, ends, or both begins and ends, respectively, with an empty string. Thus, if the string consists solely of one instance of `separator`, the array consists of two empty strings.
    - When the string is empty, `split()` returns an array containing one empty string, rather than an empty array. If the string and separator are both empty strings, an empty array is returned.
- If `separator` is a regular expression that contains capturing parentheses, then each time `separator` is matched, the results (including any undefined results) of the capturing parentheses are spliced into the output array. However, not all browsers support this capability.

    ```javascript
    var colorText = "red,blue,green,yellow";
    var color1 = colorText.split(",", 2);
    color1;     // ["red", "blue"]
    var color2 = colorText.split(/[^\,]+/);
    color2;     // ["", ",", ",", ",", ""]

    ",red,blue,green,yellow,".split(",");
    // ["", "red", "blue", "green", "yellow", ""]
    "a,a,a,a".split(/a/);
    // ["", ",", ",", ",", ""]

    var str = 'Hello 1 word. Sentence number 2.';
    var splits = str.split(/(\d)/);

    console.log(splits);    // ["Hello ", "1", " word. Sentence number ", "2", "."]
    ```

- Accessing a string as an array is unpredictable and unsafe.

    ```javascript
    var str = "HELLO WORLD";
    str[0]; //this is bad
    ```

- Convert a string to an array with `split()` first.

    ```javascript
    var txt = "a,b,c,d,e";

    var arr1 = txt.split(","); 
    // --> arr1 = ["a", "b", "c", "d", "e"]

    var arr2 = txt.split();
    // --> arr2[0] = "a,b,c,d,e"

    var arr3 = txt.split("");
    // --> arr3 = ["a", ",", "b", ",", "c", ",", "d", ",", "e"]
    ```

- Browsers vary in their exact support for regular expressions in the `split()` method. While simple patterns typically work the same way, patterns where no match is found and patterns with capturing groups can behave wildly different across browsers.
    - Internet Explorer through version 8 ignores capturing groups. ECMA-262 indicates that the groups should be spliced into the result array. Internet Explorer 9 correctly includes the capturing groups in the results. 
    - Firefox through version 3.6 includes empty strings in the results array when a capturing group has no match; ECMA-262 specifies that capturing groups without a match should be represented as *`undefined`* in the results array.
- There are other, subtle differences when using capturing groups in regular expressions. When using such regular expressions, make sure to **test** thoroughly across a host of browsers.
> [cross-browser `split()`](http://blog.stevenlevithan.com/archives/cross-browser-split)
#### **`trim()`, `toUpperCase()`, `toLowerCase()`, `toLocaleUpperCase()`, `toLocaleLowerCase()`**
- The `trim()` method creates a copy of the string, removes all leading and trailing white space, and then returns the result.
- The `toLocaleLowerCase()` and `toLocaleUpperCase()` methods are intended to be implemented based on a particular locale. Generally speaking, if you do not know the language in which the code will be running, it is safer to use the locale-specific methods.
#### **`concat()`**
- The `concat()` method accepts any number of arguments. The addition operator (`+`) is used more often and, in most cases, actually performs better than the `concat()` method even when concatenating multiple strings.

    ```javascript
    var text1 = "Hello";
    var text2 = "World";
    var text3 = "!";
    var text4 = text1.concat(" ", text2, text3);
    ```

- When the second argument is a string, there are several special character sequences that can be used to insert values from the regular-expression operations.

    ```javascript
    var text = "cat, bat, sat, fat";
    result = text.replace(/(.at)/g, "word ($1)");
    result; // "word (cat), word (bat), word (sat), word (fat)"
    ```

- The second argument of `replace()` may also be a function. 
    - When there is a **single** match (no group matches), the function gets passed three arguments: the string match, the position of the match within the string, and the whole string. 
    - When there are **multiple capturing groups**, each matched string is passed in as an argument, with the last two arguments being the position of the pattern match in the string and the original string. 
    - The function should return a string indicating what the match should be replaced with. 
- Using a function as the second argument allows more granular control over replacement text.

    ```javascript
    function htmlEscape(text) {
        return text.replace(/[<>"&]/g, function(match, pos, originalText) {
            switch (match) {
                case "<":
                    return "&lt;";
                case ">":
                    return "&gt;";
                case "&":
                    return "&amp;";
                case "\"":
                    return "&quot;";
            }
        });
    }
    htmlEscape("<p class=\"greeting\">hello</p>");  // "&lt;p class=&quot;greeting&quot;&gt;hello&lt;/p&gt;"
    ```

#### **`charAt()`, `charCodeAt()`, `fromCharCode()`**
- Two methods access specific characters in the string: `charAt()` and `charCodeAt()`. These methods each accept a single argument, which is the character's **zero-based position**. The `charAt()` method returns the character in the given position as a single-character string. (There is **no character type** in ECMAScript.) `charCodeAt()` returns the character's character code.
- There is one method on the `String` constructor: `fromCharCode()`. This takes one or more character codes and convert them into a string. Essentially, this is the reverse operation from the `charCodeAt()` instance method.

    ```javascript
    var str = "HELLO WORLD";
    str.charAt(0);            
    //--> returns H

    // returns the unicode of the character
    str.charCodeAt(0);
    // --> 72 (decimal)

    String.fromCharCode(104, 101, 108, 108, 111);       // "hello"
    ```

#### **`locateCompare()`**
- The `localeCompare()` method compares one string to another and returns one of three values:
    1. If the string should come alphabetically before the string argument, a negative number is returned. 
    1. If the string is equal to the string argument, 0 is returned.
    1. If the string should come alphabetically after the string argument, a positive number is returned.
- The unique part of `localeCompare()` is that an implementation's locale (country and language) indicates exactly how this method operates. In the United States, where English is the standard language for ECMAScript implementations, `localeCompare()` is case-sensitive, determining that uppercase letters come alphabetically after lowercase letters. However, this may not be the case in other locales. 

    ```javascript
    var m = ["AAA", "A", "aa", "a", "Aa", "aaa"];
    m.sort(function (a, b) {
        return a.localeCompare(b);
    });
    // m (in some locale) is
    // ['a', 'A', 'aa', 'Aa', 'aaa', 'AAA']
    ```

<a id="bln"></a>

## [Boolean](#)
- Falsy values:  
    - `false`
    - `null`
    - *`undefined`*
    - the empty string ""
    - the number 0, -0
    - the number `NaN`  
- All other values are truthy, including `true`, the string `"false"`, and all objects.
- The `Boolean()` casting function can be called on any type of data and will always return a `Boolean` value. Flow-control statements automatically perform this `Boolean` conversion. 
- Instances of `Boolean` object override the `valueOf()` method to return a primitive value of either *true* or *false*. The `toString()` method is also overridden to return a string of "true" or "false" when called.

    ```javascript
    var falseObject = new Boolean(false);
    var result = falseObject && true;
    result;         // true
    ```

    - The `falseObject` object is evaluated, not its value (*false*). All objects are automatically converted to *true* in `Boolean` expressions.

<a id="arrs"></a>

## [Arrays](#)
- Arrays are ordered lists of data. An array can hold any type of data in each slot. ECMAScript arrays are also **dynamically sized**, automatically growing to accommodate any data that is added to them. The full array can be accessed by referring to the array name.  
- Arrays can be created using `Array` constructor in two basic ways.
    - Use the `Array` constructor. Providing a single argument that is a number always creates an array with the given number of items, whereas an argument of any other type creates a one-item array that contains the specified value.

        ```javascript
        var arr1 = new Array();
        // creates an array with an initial length value of 3
        var arr2 = new Array(3);
        var arr3 = new Array("a", "b", "c");
        ```

    - Use array literal notation.
    
        ```javascript
        var array = [];  
        var cars = [
            "Saab",
            "Volvo",
            "BMW"
            ];
        ```

- The `length` is not read-only. Items can be easily removed or added to the the array by setting the `length` property. Arrays can contain a maximum of 4,294,967,295 items. Trying to create an array with an initial size approaching this maximum may cause a long-running script error.

    ```javascript
    var arr = ["a", "b", "c"];
    arr.length = 2;
    arr[2];         // undefined
    arr[5] = "d";
    arr.length;     // 6
    arr;            // ["a", "b", empty × 3, "d"]
    ```

- Arrays with named indexes are called associative arrays (or hashes). JavaScript does not support arrays with named indexes. If you use named indexes, JavaScript will redefine the array to a standard object. After that, some array methods and properties will produce incorrect results.

    ```javascript
    var person = [];
        person["firstName"] = "John";
        person["lastName"] = "Doe";
        person["age"] = 46;
        var x = person.length;         // person.length will return 0
        var y = person[0];             // person[0] will return undefined
    ```

- **Arrays are a special kind of objects, with zero-based numeric indexes**. Objects use name indexes in JS. Use objects when you want the element names to be strings (text). Use arrays when you want the element names to be numbers.
- When dealing with a single web page, and therefore a single global scope, the `instanceof` operator works well. `instanceof` assumes a single global execution context. If you are dealing with multiple frames in a web page, you're really dealing with two distinct global execution contexts and therefore two versions of the `Array` constructor. If you were to pass an array from one frame into a second frame, that array has a different constructor function than an array created natively in the second frame. To work around this problem, ECMAScript 5 introduced a new method `Array.isArray()` to definitively determine if a given value is an array regardless of the global execution context in which it was created.

    ```javascript
    var fruits = ["Banana", "Orange", "Apple", "Mango"];

    Array.isArray(fruits);      // returns true
    fruits instanceof Array     // returns true

    function isArray(x) {
        return x.constructor.toString().indexOf("Array") > -1;
    }

    function isArray(myArray) {
        return myArray.constructor === Array;
    }
    ```

<a id="amd"></a>

### **[Array methods](#)**
- A stack is referred to as a last-in-first-out (LIFO) structure, meaning that the most recently added item is the first one removed. The insertion (called a push) and removal (called a pop) of items in a stack occur at only one point: the top of the stack. ECMAScript arrays provide `push()` and `pop()` specifically to allow **stack-like** behavior.
- Queues restrict access in a first-in-first-out (FIFO) data structure. A queue adds items to the end of a list and retrieves items from the front of the list. `unshift()` adds any number of items to the front of an array. Using `unshift()` in combination with `pop()` emulates a queue in the opposite direction, where new values are added to the front of the array and values are retrieved off the back. `shift()` method emulates a queue to retrieve the first item in the array. Using `shift()` in combination with `push()` allows arrays to be used as queues.
#### **`push()`, `unshift()`**
- The `push()` method adds a new element to an array (at the end) and returns the new array length. 
- The `unshift()` method adds a new element to an array (at the beginning), "unshifts" older elements, and returns the new array length.
#### **`pop()`, `shift()`**
- The `pop()` method removes the last element from an array and returns the value that was "popped out". 
- The `shift()` method removes the first array element, "shifts" all other elements to a lower index and returns teh string that item that was shifted out.
- Since JavaScript arrays are objects, elements can be deleted by using the JavaScript operator delete. Using delete may leave *`undefined` holes* in the array. Use `pop()` or `shift(`) or `splice()` instead.

    ```javascript
    var fruits = ["Banana", "Orange", "Apple", "Mango"];
    delete fruits[0];           // Changes the first element in fruits to undefined
    ```

#### **`toString()`, `valueOf()`, `toLocaleString()`, `join()`**
- When called on an array, the `toString()` methods return the same a comma-separated string that contains the string equivalents of each value in the array, which is to say that each item has its `toString()` method called to create the final string. JavaScript automatically converts an array to the string when a primitive value is expected (**automatic `toString()`**). When `toLocaleString()` is called on an array, it creates a comma-delimited string of the array values, with `toLocaleString()` calling each item's `toLocaleString()` instead of `toString()` to get its string value.

    ```javascript
    var fruits = ["Banana", "Orange", "Apple", "Mango"];
    fruits.toString();      // "Banana,Orange,Apple,Mango"

    fruits.valueOf();       // ["Banana", "Orange", "Apple", "Mango"] 
    ```

- The `join()` method also joins all array elements into a string, but in addition you can specify the separator. If no value or *undefined* is passed into the `join()` method, then a **comma** is used as the separator.

    ```javascript
    var fruits = ["Banana", "Orange", "Apple", "Mango"];

    fruits.join(" * ");     // "Banana * Orange * Apple * Mango"
    furies.join();         // "Banana,Orange,Apple,Mango"
    ```

#### **`concat()`, `slice()`, `splice()`**
- The `concat()` method creates a new array by merging (concatenating) existing arrays. This method begins by creating a copy of the array and then appending the method arguments to the end and returning the newly constructed array. It can take any number of array and values as arguments. When no arguments are passed in, `concat()` simply clones the array and returns it. It does not change the existing array and always returns **a new array**.

    ```javascript
    var arr1 = ["Cecilie", "Lone"];
    var arr2 = ["Emil", "Tobias","Linus"]; 
    var myChildren = arr1.concat(arr2, ["Robin", "Morgan"]);    // ["Cecilie", "Lone", "Emil", "Tobias", "Linus", "Robin", "Morgan"]

    // clone an array
    arr1.concat();          // ["Cecilie", "Lone"]
    ```

- The `slice()` method slices out a piece of an array into **a new array** and does not remove any elements from the source array. It selects elements from the start argument, and up to (but not including) the end argument. If the end position is smaller than the start, then an empty array is returned. It slices out the rest of the array if the end argument is omitted.

    ```javascript
    var fruits = ["Banana", "Orange", "Lemon", "Apple", "Mango"];
    var citrus = fruits.slice(1, 3); 
    citrus;          // ["Orange", "Lemon"]
    ```

- The `splice()` method can be used to insert items into the middle of an array. It **alters the original array**. It always returns an array that contains any items that were removed from the array (or an empty array if no items were removed).
    1. The first parameter defines the position where new elements should be added (spliced in).
    2. The second parameter defines how many elements should be **removed**.
    3. The rest of the parameters defines the new element to be added.

    ```javascript
    var fruits = ["Banana", "Orange", "Apple", "Mango"];
    fruits.splice(2, 0, "Lemon", "Kiwi");
    // --> ["Banana", "Orange", "Lemon", "Kiwi", "Apple", "Mango"]

    fruits.splice(0, 1);        
    // removes and returns the first element of fruits
    // --> ["Banana"]
    ```

#### **`indexOf()`, `lastIndexOf`**
- ECMAScript 5 adds two item location methods to array instances: `indexOf()` and `lastIndexOf()`. Each accepts two arguments: the item to look for and an optional index from which to start looking. The `indexOf()` method starts searching from the front of the array (item 0) and continues to the back, whereas `lastIndexOf()` starts from the last item in the array and continues to the front. The methods each return the position of the item in the array or –1 if the item isn't in the array. An **identity comparison** is used when comparing the first argument to each item in the array
#### **`max()`, `min()`**

```javascript
function myArrayMax(arr) {
    return Math.max.apply(null, arr);
}

function myArrayMin(arr) {
    var len = arr.length;
    var min = Infinity;
    while (len--) {
        if (arr[len] < min) {
            min = arr[len];
        }
    }
}
```

#### ***Iterative methods***
- ECMAScript 5 defines 5 iterative methods for arrays. Each of the methods accepts 2 arguments: **a function** to run on each item and **an optional scope object** in which to run the function (affecting the value of *this*). The function passed into one of these methods will receive 3 arguments: the **array item** value, the **position of the item** in the array, and the **array object itself**. All of these array methods ease the processing of arrays by performing a number of different operations. These methods **do not change the values contained in the array**.
    - `every()` — Runs the given function on every item in the array and returns `true` if the given function returns true for every item.     
    - `some()` — Runs the given function on every item in the array and returns `true` if the given function returns true for any one item.

        ```javascript
        var numbers = [1,2,3,4,5,4,3,2,1];
        var everyResult = numbers.every(function(item, index, array) {
            return (item > 2);
        });
        var someResult = numbers.some(function(item, index, array) {
            return (item > 2);
        });
        everyResult;        // false
        someResult;         // true
        ```

    - `filter()` — Runs the given function on every item in the array and returns an **array** of all items for which the given function returns `true`. It is very helpful when querying an array for all items matching some criteria.

        ```javascript
        var filterResult = numbers.filter(function(item, index, array) {
            return (item > 2);
        });

        filterResult;       // [3, 4, 5, 4, 3]
        ```

    - `map()` — Runs the given function on every item in the array and returns the result of each function call in an **array**. It is helpful when creating arrays whose items correspond to one another.

        ```javascript
        var mapResult = numbers.map(function(item, index, array) {
            return item * 2;
        });
        mapResult;          // [2, 4, 6, 8, 10, 8, 6, 4, 2]
        ```

    - `forEach()` — Runs the given function on every item in the array. This method has no return value and is essentially the same as iterating over an array using a `for` loop.

        ```javascript
        myArr.forEach(myAwesomeFunction);
        
        function myAwesomeFunction(element, index, array) {
            ...
        }
        ```

#### ***Reduction methods***
- ECMAScript 5 introduced 2 reduction methods for arrays: `reduce()` and `reduceRight()`. Both methods iterate over all items in the array and build up a value that is ultimately returned. The `reduce()` method does this starting at the first item and traveling toward the last, whereas `reduceRight()` starts at the last and travels toward the first. Both methods accept 2 arguments: **a function** to call on each item and an **optional initial value** upon which the reduction is based. The function passed into `reduce()` or `reduceRight()` accepts 4 arguments: the previous value, the current value, the item's index, and the array object. **Any value returned from the function is automatically passed in as the first argument for the next item. The first iteration occurs on the second item in the array**, so the first argument is the first item in the array and the second argument is the second item in the array. The decision to use `reduce()` or `reduceRight()` depends solely on the direction in which the items in the array should be visited. They are exactly equal in every other way.

    ```javascript
    var values = [1, 2, 3, 4];
    var sum = values.reduce(function(prev, cur, index, array) {
        return prev + cur;
    });
    sum;            // 10
    ```

<a id="ast"></a>

### [**Array sort**](#)
- Both `reverse()` and `sort()` return a reference to the array on which they were applied.
- The `reverse()` method reverses the elements in an array **in place** and returns the array.

    ```javascript
    var a = ["a", "b", "c"];
    var b = a.reverse( );
    // both a and b are ["c", "b", "a"]
    ```

- The `sort()` method sorts an array alphabetically. By default, the `sort()` method puts the items in ascending order — with the smallest value first and the largest value last. To do this, the `sort()` method calls the `String()` casting function on every item and then compares the strings to determine the order. The `sort()` method accepts a comparison function parameter to indicate which value should come before which. A comparison function accepts 2 arguments and returns a negative number if the first argument should come before the second, a zero if the arguments are equal, or a positive number if the first argument should come after the second.

    ```javascript
    var n = [4, 8, 15, 16, 23, 42];
    n.sort(function (a, b) {
        return a - b;
    });
    // a < b --> return a negative number --> a (the smaller one) comes before b (the larger one) 
    // a > b --> return a positive number --> a (the larger one) comes after b (the smaller one)
    // --> sort a and b in ascending order

    n.sort(function (a, b) {
        return b - a;
    });
    // a > b --> return a negative number --> a (the larger one) comes before b (the bigger one) 
    // a < b --> return a positive number --> a (the smaller one) comes after b (the largger one)
    // --> sort a and b in descending order



    // sort numbers and strings
    var m = ['aa', 'bb', 'a', 4, 8, 15, 16, 23, 42];
    m.sort(function (a, b) {
        if (a === b) {
            return 0;
        }
        if(typeof a === typeof b) {
            return a < b ? -1 : 1;
        }
        return typeof a < typeof b ? -1 : 1;
        // "number" < "string", numbers always come before strings
    });
    // m is [4, 8, 15, 16, 23, 42, 'a', 'aa', 'bb' 
    ```

- A much simpler version of the comparison function can be used with numeric types, and objects whose `valueOf()` method returns numeric values (such as the `Date` object).

    ```javascript
    function compare(value1, value2){
        return value2 - value1;
    }
    ```

<a id="tc"></a>

## [Type conversion](#)
- JavaScript automatically calls the variable's `toString()` function when you try to "output" an object or a variable.
- [**Type  conversion table**](https://www.w3schools.com/js/js_type_conversion.asp):

Original Value|Converted to Number|Converted to String|Converted to Boolean
---|---|---|---|
"0"|0|-|**true**
"000"|**0**|-|true
NaN|NaN|"NaN"|false
-Infinity|-Infinity|"-Infinity"|true
""|0|""|false
[20]|**20**|**"20"**|true
[10, 20]|**NaN**|"10, 20"|true
["ten","twenty"]|NaN|"ten,twenty"|true
function(){}|NaN|"function(){}"|true
{ }|NaN|"[object Object]"|**true**
null|0|"null"|false
undefined|NaN|"undefined"|false

<a id="fc"></a>

# [Flow control](#cnt2)
- Flow-control statements automatically perform `Boolean` conversion using `Boolean()` casting function. 
## **if**
- The condition can be any expression; it doesn't even have to evaluate to an actual Boolean value. ECMAScript automatically converts the result of the expression into a Boolean by calling the `Boolean()` casting function on it.
## **Loop**
- The `do-while` statement is a post-test loop. The while statement is a pretest loop. The for statement is also a pretest loop.
- There are no **block-level** variables in ECMAScript, so a variable defined inside the loop is accessible outside the loop as well.

    ```javascript
    for (var i = 0; i < 10; i++){
        ;
    }
    i;      //10
    ```

- The `for-in` statement is a strict iterative statement. It is used to enumerate the properties of an object. As with the for statement, the var operator in the control statement is not necessary but is recommended for ensuring the use of a local variable. The `for-in` statement will throw an error if the variable representing the object to iterate over is *null* or *undefined*. ECMAScript 5 updates this behavior to not throw an error and simply doesn't execute the body of the loop. For best cross-browser compatibility, it's recommended to check that the object value isn't *null* or *undefined* before attempting to use a `for-in` loop.

    ```javascript
    // display all the properties of the BOM window object
    for (var propName in window) {
        document.write(propName);
    }
    ```

## **label, break, continue** 
- The label statements can be referenced later by using the break or continue statement. They are typically used with nested loops.
- The break statement exits the loop immediately, forcing execution to continue with the next statement after the loop. The continue statement exits the loop immediately, but execution continues from the top of the loop. 
- Always use descriptive labels and try not to nest more than a few loops.

    ````javascript
    var num = 0;
    outermost:
    for (var i = 0; i < 10; i++) {
        for (var j = 0; j < 10; j++) {
            if (i == 5 && j == 5) {
                break outermost;
            }
            num++;
        }
    }
    num;        //55
    ````

## **with**
- The `with` statement sets the scope of the code within a particular object. It was created as a convenience for times when a single object was being coded to over and over again. `with` statement is considered a syntax error in strict mode.

    ```javascript
    with (expression) statement;

    var qs = location.search.substring(1);
    var hostName = location.hostname;
    var url = location.href;

    with(location) {
        var qs = search.substring(1);
        var hostName = hostname;
        var url = href;
    }
    ```

    - **Each variable inside the statement is first considered to be a local variable**. If it's not found to be a local variable, the `location` object is searched to see if it has a property of the same name. If so, then the variable is evaluated as a property of location.

    > It is widely considered a poor practice to use the with statement in production code because of its negative performance impact and the difficulty in debugging code contained in the `with` statement.
## **switch**
- The `switch` statement works with all data types. The case values can be variables and expressions. The `switch` statement compares values using the identically equal operator, so no type coercion occurs (for example, the string "10" is not equal to the number 10).
- Without the `break` keyword, code execution falls through the original case into the following one. The `default` keyword indicates what is to be done if the expression does not evaluate to one of the cases.

<a id="ob"></a>

# [Reference types, objects](#)
- A reference value (object) is an instance of a specific reference type. Reference types are also called object definitions, because they describe the properties and methods that objects should have. 
- ECMA-262 defines an object as an **unordered** collection of properties each of which contains a primitive value, object, or function. This means that an object is an array of values in no particular order. Each property or method is identified by a name that is mapped to a value. So it helps to think of ECMAScript objects as **hash tables**: nothing more than a grouping of name-value pairs where the value may be data or a function.
- Arrays are objects, functions are objects, regular expressions are objects, objects are objects.

    ```javascript
    typeof {name:'John', age:34} //--> "object"
    typeof [1,2,3,4]             //--> "object" 
    typeof /\bcat\b/             //--> "object"
    typeof function myFunc(){}   //--> "function"
    ```

- JavaScript objects cannot not be compared. Comparing two JavaScript objects using `==` or `===` will always return `false`, using `!=` or `!==` is otherwise. Each object is created based on a reference type. Objects are passed around by reference.

    ```javascript
    var a = {}, b = {}, c = {};
    // a, b, and c each refer to a
    // different empty objects

    a = b = c = {};
    // a, b, and c all refer to
    // the same empty object
    ```

- Empty an object by setting it to `null`. Value is `null`, but type is still an `object`. Empty an object by setting it to *undefined*. Both value and type is *undefined*.
- A property name can be any string, including the empty string. Property names can also be numbers when using object literal notation. That numeric property names are automatically converted to strings. The quotes around a property's name in an object literal are optional if the name would be a legal JavaScript name and not a reserved word. A property value can be any JavaScript value except for *undefined*. A **method** is actually a function stored as object property and a function definition stored as a property value.
- The `Object` type in ECMAScript is the base from which all other objects are derived. All of the properties and methods of the `Object` type are also present on other, more specific objects. Each `Object` **instance** has the following properties and methods:
    - `constructor` — The function that was used to create the object. 
        ```javascript
        // constructor here is the Object() function.
        var o = new Object();
        ```
    - `hasOwnProperty(propertyName)` — Indicates if the given property exists on the object instance (not on the prototype). 
    - `isPrototypeOf(object)` — Determines if the object is a prototype of another object.
    - `propertyIsEnumerable(propertyName)` — Indicates if the given property can be
    enumerated using the `for in` statement.
    - `toLocaleString()` — Returns a string representation of the object that is appropriate for
    the locale of execution environment.
    - `toString()` — Returns a string representation of the object.
    - `valueOf()` — Returns a string, number, or Boolean equivalent of the object. It often returns the same value as `toString()`.

    > Objects that exist in the browser environment, such as those in the Browser Object Model (BOM) and Document Object Model (DOM), are considered host objects since they are provided and defined by the host implementation. Host objects aren't governed by ECMA-262 and, as such, may or may not directly inherit from `Object`.

<a id="top"></a>

## [Types of properties](#cnt2)
- ECMA-262 describes characteristics of properties through the use of internal-only attributes. **Attributes are used to define and explain the state of object properties**. These attributes are defined by the specification for implementation in JavaScript engines, and as such, these attributes are not directly accessible in JavaScript. To indicate that an attribute is internal, surround the attribute name with two pairs of square brackets, such as `[[Enumerable]]`. All attributes can be read, but only the `value` attribute can be changed (only if the property is writable). 
- There are 2 types of properties: data properties and accessor properties. 
### Data properties
`[[Configurable]]` indicates if the property may be redefined by removing the property via delete, changing the property's attributes, or **changing** the property **into an accessor property**. By default, this is true for all properties defined directly on an object.\
\
`[[Enumerable]]` indicates if the property will be returned in a for-in loop. By default, this is true for all properties defined directly on an object.\
\
`[[Writable]]` indicates if the property's value can be changed. By default, this is true for all properties defined directly on an object.\
\
`[[Value]]` contains the actual data value for the property. This is the location from which the property's value is read and the location to which new values are saved. The default value for this attribute is *undefined*.

- When a property is explicitly added to an object, `[[Configurable]]`, `[[Enumerable]]`, and `[[Writable]]` are all set to true while the `[[Value]]` attribute is set to the assigned value. Use the `Object.defineProperty()` method to change any of the default property attributes. When you are using `Object.defineProperty()`, the values for `configurable`, `enumerable`, and `writable` default to `false` unless otherwise specified. This method accepts 3 arguments: 
    1. the object on which the property should be added or modified,
    1. the name of the property,
    1. the properties on the descriptor object match the attribute names: `configurable`, `enumerable`, `writable`, and `value`. You can set one or all of these values to change the corresponding attribute values. 

    ```javascript
    var person = {};
    Object.defineProperty(person, "job", {
        // cannot delete
        configurable: false,
        //read-only
        writable: false,
        value: "software engineer"
    });
    ```

- Setting `configurable` to `false` means that the property cannot be removed from the object. Calling `delete` on the property has no effect in nonstrict mode and throws an error in strict mode. Once a property has been defined as nonconfigurable, it cannot become configurable again. Any attempt to call `Object.defineProperty()` and change any attribute other than `writable` causes an error.
### Accessor properties
Accessor properties contain a combination of a `getter` function and a `setter` function (though both are not necessary).\
When an accessor property is read from, the `getter` function is called, and it's the function's responsibility to return a valid value; when an accessor property is written to, a function is called with the new value, and that function must decide how to react to the data. Accessor properties have four attributes:
1. `[[Configurable]]`
1. `[[Enumerable]]`
1. `[[Get]]` is the function to     call when the property is read from. The default value is *undefined*.
1. `[[Set]]` is the function to call when the property is written to. The default value is *undefined*.
- It's not possible to define an accessor property explicitly. Use `Object.defineProperty()`.

    ```javascript
    var book = {
        // underscore  is a common notation to indicate that 
        // a property is not intended to be accessed from 
        // outside of the object's methods
        _year: 2012,
        edition: 1
    };

    // define year to be an accessor property
    Object.defineProperty(book, "year", {
        get: function() {
            return this._year;
        },
        set: function(newValue) {
            if (newValue > 2012) {
                this._year = newValue;
                this.edition += newValue - 2012;
            }
        }
    });

    // legacy accessor support prior to the ECMAScript 5 
    book.__defineGetter__("year", function() {
        return this.year;
    });
    book.__defineSetter__("year", function(newValue) {
        if (newValue > 2012) {
            this._year = newValue;
            this.edition += newValue - 2012;
        }
    });

    book.year = 2013;
    book.edition;   // 2
    ```

- Assigning just a `getter` means that the property cannot be written to and attempts to do so will be ignored. In strict mode, trying to write to a property with only a getter throws an error. Likewise, a property with only a `setter` cannot be read and will return the value *undefined* in nonstrict mode, while doing so throws an error in strict mode.
- `Object.defineProperties()` allows you to define multiple properties using **descriptors** at once. There is no way to modify `[[Configurable]]` or `[[Enumerable]]` in browsers that don't support `Object.defineProperty()`.

    ```javascript
    // two data properties
    var book = {};
    defineProperties(book, {
        _year: {
            value: 2012
        },
        edition: {
            value: 1
        },

        // an accessor property
        year: {
            get: function() {
                return this._year;
            },
            set: function(newValue) {
                if (newValue > 2012) {
                    this._year = newValue;
                    this.edition += newValue - 2012;
                }
            }
        }
    });
    ```

- Retrieve the property descriptor for a given property by using the ECMAScript 5 `Object.getOwnPropertyDescriptor()` method. The return value is an object with properties for `configurable`, `enumerable`, `get`, and `set` for accessor properties or `configurable`, `enumerable`, `writable`, and `value` for data properties. The method can be used on any object in JavaScript, including DOM and BOM objects. It accepts 2 arguments:
    - the object on which the property resides,
    - the name of the property whose descriptor should be retrieved.

        ```javascript
        var descriptor = Object.getOwnPropertyDescriptor(book, "_year");
        descriptor.value;           // 2012
        descriptor.configurable;    // false
        typeof descriptor.get;      // undefined

        var descriptor1 = Object.getOwnPropertyDescriptor(book, "year");
        descriptor.value;           // undefined
        descriptor.enumerable       // false
        typeof descriptor.get       // "function"
        ```
    
- The `Object.getOwnPropertyDescriptor()` method works only on instance properties; to retrieve the descriptor of a *prototype* property, you must call `Object.getOwnPropertyDescriptor()` on the *prototype* object directly.

<a id="cob"></a>

## [Creating objects](#cnt2)
<!-- ECMAScript supports object-oriented (OO) programming without the use of classes or interfaces. Objects are created and augmented at any point during code execution, making objects into dynamic rather than strictly defined entities. -->

<!-- 1. Use an object literal. When defining an object via object literal notation, the `Object` constructor is never actually called. Object literals have become a preferred way of passing a large number of optional arguments to a function. 

    ```javascript
    var car = {type:"Fiat", model:"500", color:"white", 5: true};

    function displayInfo(args) {
        var output = "";
        if (typeof args.name == "string") {
            output += "Name: " + args.name + "\n";
        }
        if (typeof args.name == "number") {
            output += "Age: " + args.age + "\n";
        }
        console.log(output);
    }
    displayInfo({
        name: "SB",
        age: 26
    });
    ```

    > No commas for the last `name:value` pair.  -->
<!-- 1. Use the `new` operator followed by a constructor. A constructor is simply a function whose purpose is to create a new object. ECMAScript requires parentheses to be used only when providing arguments to the constructor. If there are no arguments, then the parentheses can be omitted safely (though that's not recommended).

    ```javascript
    // built-in constructor

    var person = new Object();
    person.job = "software engineer";
    
    var x2 = new String();    // A new String object
    var x3 = new Number();    // A new Number object
    var x4 = new Boolean();   // A new Boolean object
    var x5 = new Array();     // A new Array object
    var x6 = new RegExp();    // A new RegExp object
    var x7 = new Function();  // A new Function object
    var x8 = new Date();      // A new Date object
    ```

    > **An obvious downside of using the `Object` constructor or an object literal to create objects is that creating multiple objects with the same interface requires a lot of code duplication**. -->
<!-- 1. Use factory pattern. It didn't address the issue of object identification (what type of object an object is).

    ```javascript
    function createPerson(name, age, job) {
        var o = new Object();
        o.name = name;
        o.age = age;
        o.job = job;
        o.sayName = function() {
            alert(this.name);
        };
        return o;
    }
    var p1 = createPerson("S", "26", "unemployed");
    ``` -->

<!-- 1. Use the constructor pattern to **define a custom object constructor**.

    ```javascript
    function Person(first, last, job) {
        this.firstName = first;
        this.lastName = last;
        this.job = job;
        this.sayJob = function() {
            alert(this.name);
        }
    }
    var boy = new Person("S", "B", "software engineer");
    boy.constructor;                // Person {firstName: "S", lastName: "B", job: "software engineer", sayJob: ƒ}
    boy.constructor === Person;     // true
    boy instanceof Object;          // true
    boy instanceof Person;          // true
    ```

    - By convention, constructor functions always begin with an uppercase letter, whereas nonconstructor functions begin with a lowercase. This convention is borrowed from other OO languages and helps to distinguish function use in ECMAScript, since **constructors are simply functions that create objects**. Constructor functions defined in this manner are defined on the `Global` object (the `window` object in web browsers).

    - The only difference between constructor functions and other functions is the way in which they are called. There's no special syntax to define a constructor that automatically makes it behave as such. Any function that is called with the `new` operator acts as a constructor, whereas any function called without it acts just as you would expect a normal function call to act.

        ```javascript
        // call as s constructor
        var person = new Person("S", "B", "software engineer");
        person.sayJob();                        // "soft engineer"

        // call as a function
        Person("John", "Doe", "psychologist");  // add to window
        window.sayJob();                        // "psychologist"

        // call in the scope of object o
        var o = new Object();
        Person.call(o, "Kristen", "Stewart", "actress");
        o.sayJob();     //"actress"
        ```

        - Calling a constructor in this manner essentially causes the following 4 steps to be taken:
            1. Create a new object.
            2. Assign the `this` value of the constructor to the new object (so `this` points to the new object).
            3. Execute the code inside the constructor (adds properties to the new object).
            4. Return the new object.
        - `this` object always points to the `Global` object (`window` in web browsers) when a function is called without an explicitly set `this` value (by being an object method or through `call()`/`apply()`).

    - The **major downside** to constructor functions is that methods are created once for each instance. Both `person1` and `person2` have a method called `sayJob()`, but those methods are not the same instance of `Function`. Functions are objects in ECMAScript, so every time a function is defined, it's actually an object being instantiated. It doesn't make sense to have two instances of `Function` that do the same thing, especially when the *this* object makes it possible to avoid binding functions to particular objects until runtime. 

        ```javascript
        function Person(first, last, job) {
            this.firstName = first;
            this.lastName = last;
            this.job = job;
            this.sayJob = new Function("alert(this.job)");     // logical equivalent though scope chains and identifier resolution are different
        }

        person1.sayJob == person2.sayJob;  // false
        ```

    - Work around this limitation by **moving the function definition outside of the constructor function**. Inside the constructor function, the `sayJob` property is set equal to the **global** `sayJob()` function. Since the `sayJob` property now contains just a pointer to a function, both `person1` and `person2` end up sharing the `sayJob()` function that is defined in the global scope. 

        ```javascript
        function Person(first, last, job) {
            this.firstName = first;
            this.lastName = last;
            this.job = job;
            this.sayJob = sayJob;
        }
        function sayJob() {
            alert(this.job);
        }
        ```

    - The **problem** of this approach is that it may introduce multiple global functions. These problems are addressed by using the prototype pattern. -->
1. **Use prototype pattern**.
    - Each function is created with a ***prototype*** property, which is an **object** containing properties and methods that should be available to instances of a particular reference type. This object is literally a prototype for the object to be created once the constructor function is called. The benefit of using the prototype is that all of its properties and methods are shared among object instances. Instead of assigning object information in the constructor function, they can be assigned directly to the prototype object. Unlike the constructor pattern, the properties and methods are all shared among instances. So `boy1` and `boy2` access **the same** set of properties and the same `sayName()` function. 

        ```javascript
        function Person() {
        }
        Person.prototype.firstName = "S";
        Person.prototype.lastName = "B";
        Person.prototype.job = "software engineer";
        Person.prototype.sayJob = function() {
            alert(this.job);
        };

        var boy1 = new Person();
        var boy2 = new Person();
        boy1.sayJob === boy2.sayJob;    // true
        ```

        - `Person.prototype` had to be typed out for each property and method, which is **redundant**.
    - To limit this redundancy and to better visually encapsulate functionality on the `prototype` object, it has become more common to simply overwrite the `prototype` with an object literal that contains all of the properties and methods to limit this redundancy and to better visually encapsulate functionality on the `prototype`. This syntax **overwrites** the default `prototype` object completely, meaning that the `constructor` property is equal to that of a completely new object (the `Object` constructor) instead of the (`Person`) function itself. The type of object indicated by `constructor` is no longer reliable. `instanceof` still works.

        ```javascript
        function Person(){
        }
        var p1 = new Person();
        Person.prototype = {
            firstName: "S",
            lastName: "B",
            job: "Software Engineer",
            sayJob: function() {
                alert(this.job);
            }
        };

        p1.sayJob();                    
        // cause an error because the old prototype doesn't have a property of that name
        var boy = new Person();
        boy.constructor;                // ƒ Object() { [native code] }
        boy.constructor === Object;     // true
        boy instanceof Person;          // true
        boy instanceof Object;          // true
        ```

        - The `[[Prototype]]` pointer (to the `prototype` object) is assigned when the constructor function is called, so changing the `prototype` to a different object severs the tie between the constructor and the original prototype. Overwriting the `prototype` object on the constructor function means that new instances will reference the new `prototype` while any previously existing object instances still reference the old `prototype`.
    - The prototype pattern negates the ability to pass initialization arguments into the constructor, meaning that all instances get the same property values by default. This is an **inconvenience**. The **real problem** occurs when a property contains a reference value.

        ```javascript
        function Person(){
        }
        Person.prototype = {
            constructor: Person,
            firstName: "S",
            lastName: "B",
            friends: ["Arron", "Ben"],
            job: "Software Engineer",
            sayJob: function() {
                alert(this.job);
            }
        };
        var p1 = new Person();
        var p2 = new Person();
        p1.friends.push("Curry");
        p2.friends;                 // ["Arron", "Ben", "Curry"]
        p1.friends === p2.friends;  // true
        ```

        - If the intention is to have an array shared by all instances, then this outcome is okay. Typically, though, instances want to have their own copies of all properties. This is why the prototype pattern is rarely used on its own.


1. [Use the combination constructor/prototype pattern.](#cnt2)  <a id="ccpp"></a>

    ```javascript
    function Person(name, age, job) {
        this.name = name;
        this.age = age;
        this.job = job;
        this.friends = ["John", "Marry"];
    }
    Person.prototype = {
        constructor: Person,
        sayName: function() {
            alert(this.name);
        }
    };
    var p1 = new Person("SB", 26, "software engineer");
    var p2 = new Person("House", 45, "Doctor");
    p1.friends.push("Dean");
    p1.friends;                 // ["John", "Marry", "Dean"]
    p2.friends;                 // ["John", "Marry"]
    p1.friends === p2.friends;  // false
    p1.sayName === p2.sayName;  // true
    ```

    - It's the most common way of defining custom reference types. The constructor pattern defines instance properties, whereas the prototype pattern defines methods and shared properties. With this approach, each instance ends up with its own copy of the instance properties, but they all share references to methods, conserving memory. This pattern allows arguments to be passed into the constructor as well. Generally speaking, this is the **default pattern** to use for defining reference types.
    - The visual separation between the constructor and the prototype confusing. 
1. Use the dynamic prototype pattern.


    ```javascript
    function Person(name, age, job) {
        this.name = name;
        this.age = age;
        this.job = job;
        if(typeof this.sayName != "function") {
            Person.prototype.sayName = function() {
                alert(this.name);
            };
        }
    }
    var p1 = new Person("SB", 26, "software engineer");
    p1.sayName();
    ```

    - The **dynamic prototype pattern** encapsulates all of the information within the constructor while maintaining the benefits of using both a constructor and a prototype by initializing the `prototype` object inside the constructor, but only if it is needed. Once initialized **for once**, changes to the prototype are reflected immediately in all instances. This pattern preserves the use of `instanceof` in determining what type of object was created.
    - You cannot overwrite the whole `prototype` object using an object literal when using the dynamic prototype pattern. Overwriting a prototype when an instance already exists effectively cuts off that instance from the new prototype.

1. Use the parasitic constructor pattern.

    ```javascript
    function Person(name, age, job) {
        var o = new Object();
        o.name = name;
        o.age = age;
        o.job = job;
        o.sayName = function() {
            alert(this.name);
        };
        return o;
    }
    var teacher = new Person("Nicholas", 29, "Software Engineer");
    teacher.sayName();          // "Nicholas"
    ```

    - It is typically a **fallback** (fallback how?) when the other patterns fail. The **basic idea** of this pattern is to create a constructor function that simply wraps the **creation and return** of another object. This is exactly the same as the factory pattern except that the function is called as a constructor, using the `new` operator. When a constructor doesn't return a value (aka, without a `return` statement), it returns the new object instance by default. Adding a `return` statement at the end of a constructor function allows you to override the value that is returned when the constructor is called. 
        - You want to create a special array that has an extra method but you don't have direct access to the `Array` constructor function. In this case, this pattern works.  

            ```javascript
            function SpecialArray() {
                var values = new Array();
                values.push.apply(values, arguments);   // 

                values.toPipedString = function() {
                    return this.join("|");
                }
                return values;
            }
            var colors = new SpecialArray("red", "blue", "green");
            colors.toPipedString();     //
            ```

            - A new array is created and initialized using the `push()` method (which has all of the constructor arguments passed in).

    - There is no relationship between the returned object and the constructor function or the constructor function's prototype; the object exists just as if it were created outside of a constructor. So `instanceof` is not reliable. This pattern should not be used when other patterns work.
1. Use durable constructor pattern

    ```javascript
    function Person(name, age, job) {
        // create the object to return
        var o = new Object();

        // optional: define private variables/functions here

        //attach methods
        o.sayName = function() {
            alert(name);
        }
        return o;
    }
    var teacher = Person("Nicholas", 29, "Software Engineer");
    teacher.sayName();      // "Nicholas"
    ```

    - Durable objects refers to objects that have no public properties and whose methods don't reference the *this* object. They're best used in secure environments (those that forbid the use of *this* and `new`) or to protect data from the rest of the application. The `teacher` variable is a durable object, and there is no way to access any of its data members without calling a method. Even if some other code adds methods or data members to the object later on, there is no way to access the original data that was passed into the constructor.
    - A durable constructor is a constructor that follows a pattern similar to the parasitic constructor pattern, with two differences: instance methods on the created object don't refer to `this`, and the constructor is never called using the `new` operator.
1. [Use the `Object.create()` method.](#objc)
## Accessing
- Values can be retrieved from an object by wrapping a string expression containing the property name in a `[ ]` suffix. The main advantage of bracket notation is that it allows you to use **variables** for property access. Property names containing characters that would be either a syntax error or a keyword/reserved word can also be accessed using bracket notation. If the string expression is a constant, and if it is a legal JavaScript name and not a reserved word, then the `.` notation can be used instead. The `.` notation is preferred because it is more compact and it reads better. The *undefined* value is produced if an attempt is made to retrieve a nonexistent member. Attempting to retrieve values out of *undefined* (property that doesn't exist) will throw a `TypeError` exception.

    ```javascript
    var propertyName = "name";
    person1[propertyName];
    ```

- A value in an object can be updated by assignment. If the property name already exists in the object, the property value is replaced. If the object does not already have that property name, the object is augmented.

```javascript
// fill in default value

var middle = stooge["middle-name"] || "(none)";
var status = flight.status || "unknown";
```

- **Object properties in ECMAScript are unordered**, so the order in which property names are returned in a `in` or `for in` statement cannot necessarily be predicted. All enumerable properties (including functions and prototype properties) will be returned once, but the order may differ across browsers. Make an array containing the names of the properties in the correct order and use `for` to make the properties appear in a particular order.
- Use the `typeof` operator to determine the type of a property and reject undesired properties (like function values) when retrieving properties, because any property on the `prototype` chain can produce a value. Another approach is to use `hasOwnProperty` method. 

    ```javascript
    typeof flight.toString // 'function'
    typeof flight.constructor // 'function'
    ```

- The `delete` operator removes a property from the object if it has one. It deletes both the value of the property and the property itself. It is designed to be used on object properties and has no effect on variables or functions. It should not be used on predefined JavaScript object properties because it can crash the application. It will not touch any of the objects in the *prototype* linkage, so removing a property from an object may allow a property from the prototype linkage to reveal that property's value.

<a id="pro"></s>

## [Prototype](#cnt2)
- Whenever a function is created, **its `prototype` property** is also created according to a specific set of rules. A `prototype` is one property of the (constructor) function, and **is an object** (named `prototype`) containing properties and methods that should be available to instances. By default, all prototypes automatically get a property called `constructor` that **points back to the function** on which it is a property.
    - For instance, `Person.prototype` points to, aka is, the *prototype* object. `Person.prototype.constructor` points to `Person`. Then, depending on the constructor, other properties and methods may be added to the *prototype*. 

- When defining a custom constructor function, its `prototype` property gets the `constructor` property only by default; all other methods are inherited from `Object`. Each time the constructor function is called to create a new instance, that **instance** has an internal **pointer** to the constructor function's `prototype` property (which is an object named `prototype`). In ECMA-262 fifth edition, that pointer is called `[[Prototype]]`. The **important thing** to understand is that a direct link exists between the instance and the constructor function's *prototype* but not between the instance and the constructor function.
- There is no standard way to access `[[Prototype]]` from script, but Firefox, Safari, and Chrome all support a property on every object called `__proto__`; in other implementations, this property is completely hidden from script. `isPrototypeOf()` returns true if `[[Prototype]]` (of an instance) points to the constructor function's `prototype` property on which the `isPrototypeOf()` method is being called. ECMAScript 5 adds a new method called `Object.getPrototypeOf()`, which returns the value of `[[Prototype]]` in all supporting implementations. It can be used to retrieve an object's *prototype* (the value of `[[Prototype]]`).

    ```javascript
    Person.prototype.isPrototypeOf(boy1);   //true

    Object.getPrototypeOf(boy1);
    // {firstName: "S", lastName: "B", job: "software engineer", sayJob: ƒ, constructor: ƒ} and more details
    Object.getPrototypeOf(boy1) === Person.prototype;                       // true
    Object.getPrototypeOf(boy1).firstName;  // "S"
    ```

- Whenever a property is accessed for reading on an object, the search begins on the object **instance** itself. If the property is not found, then the search **continues up the pointer to the `prototype`**, and the `prototype` is searched for a property with the same name. The `constructor` property exists only on the `prototype` object and so is accessible from object instances.
- It's possible to read values on the prototype from object instances but not possible to overwrite them. If a property that has the same name as a property on the `prototype` object is added to an instance, the property is on the instance, masking the property on the `prototype`.

    ```javascript
    boy1.firstName = "Slack";
    boy1.job = "psychologist";
    alert(boy1.firstName);  // "Slack"
    boy1.sayJob();          // "psychologist"
    ```

    - When `boy1.firstName` was accessed in the `alert()`, its value was read, so the search began for a property called `firstName` on the instance. Since the property exists, it is used without searching the `prototype`. *this* is bound to `boy1`, so the search for the property called `job` begins on `boy1`.
- Once a property is added to the object instance, it shadows any properties of the same name on the `prototype`, which means that it blocks access to the property on the `prototype` without altering it. Even setting the property to *null* only sets the property on the instance and doesn't restore the link to the `prototype`. The `delete` operator, however, completely removes the instance property and allows the `prototype` to be accessed again.
- The `hasOwnProperty()` method determines if a property exists on the instance or on the `prototype`. This method, which is inherited from `Object`, returns true only if a property of the given name exists on the object instance. It does not look at the `prototype` chain. 

    ```javascript
    // determine if an property exists only on the prototype
    function hasPrototypeProperty(object, name) {
        return !object.hasOwnProperty(name) && (name in object)
    }
    ```
- Use the ECMAScript 5 `Object.keys()` method to retrieve a list of enumerable instance properties on an object. It accepts an object as its argument and returns an array of strings containing the names of all enumerable properties. Use `Object.getOwnPropertyNames()` in the same way to get a list of all instance properties, whether enumerable or not. Both are **suitable replacements for `for in`**.

    ```javascript
    function Person() {
    }
    Person.prototype.firstName = "S";
    Person.prototype.lastName = "B";
    Person.prototype.job = "software engineer";
    Person.prototype.sayJob = function() {
        alert(this.job);
    };

    var keys = Object.keys(Person.prototype);
    keys;   //  ["firstName", "lastName", "job", "sayJob"]

    var p1 = new Person();
    p1.firstName = "Stussy";
    p1.job = "actor";
    var p1keys = Object.keys(p1);
    p1keys; //  ["firstName", "job"]

    var allkeys = Object.getOwnPropertyNames(Person.prototype);
    allkeys;    // ["constructor", "firstName", "lastName", "job", "sayJob"]
    ```

- Native `constructor` properties are not enumerable by default. Adding the `constructor` property back to the appropriate value will create a property with `[[Enumerable]]` set to `true`. Using the `Object.defineProperty()` method won't cause this problem.

    ```javascript
    function Person(){
    }
    Person.prototype = {
        constructor: Person,
        firstName: "S",
        lastName: "B",
        job: "Software Engineer",
        sayJob: function() {
            alert(this.job);
        }
    };
    Object.keys(Person.prototype);  // ["constructor", "firstName", "lastName", "job", "sayJob"]

    function Person1(){
    }
    Person1.prototype = {
        constructor: Person,
        firstName: "S",
        lastName: "B",
        job: "Software Engineer",
        sayJob: function() {
            alert(this.job);
        }
    };
    Object.defineProperty(Person1.prototype, "constructor", {
        enumerable: false,
        value: Person
    });
    Object.keys(Person1.prototype); // ["firstName", "lastName", "job", "sayJob"]
    ```

- Since the process of looking up values on a prototype is a search, changes made to the `prototype` at any point are immediately reflected on instances, even the instances that existed before the change was made.
- The native reference types (including `Object`, `Array`, `String`, and so on) has its methods defined on the constructor function's `prototype`. Native object prototypes can be modified just like custom object prototypes. (possible but not recommended)

    ```javascript
    String.prototype.startsWith = function (text) {
        return this.indexOf(text) == 0;
    };
    var msg = "Hello world!";
    msg.startsWith("Hello");    // true
    // the String primitive wrapper (for the string msg) is created behind the scenes
    ```

---
- Every object is linked to a `prototype` object from which it can inherit properties. All objects created from object literals are linked to `Object.prototype`, an object that comes standard with JavaScript.
- The `prototype` is not an existing object. To add a new property to a `prototype`, you add it to the constructor function.
- The standard way to create an object prototype is to use an object constructor function.

<a id="inher"></a>

## [Inheritance](#cnt2)
- Many OO languages support two types of inheritance: interface inheritance, where only the method signatures are inherited, and implementation inheritance, where actual methods are inherited. Since functions in ECMAScript don't have signatures, implementation inheritance is the only type of inheritance supported by ECMAScript.

- Inheritance in JavaScript is implemented primarily using the concept of prototype chaining. Prototype chaining involves assigning a constructor's prototype to be an instance of another type. In doing so, the subtype assumes all of the properties and methods of the supertype in a manner similar to class-based inheritance. The problem with prototype chaining is that all of the inherited properties and methods are shared among object instances, making it ill-suited for use on its own. The constructor stealing pattern avoids these issues, calling the supertype's constructor from inside of the subtype's constructor. This allows each instance to have its own properties but forces the types to be defined using only the constructor pattern. The most popular pattern of inheritance is combination inheritance, which uses prototype chaining to inherit shared properties and methods and uses constructor stealing to inherit instance properties.
### prototype chaining
- Prototype chaining as the primary method of inheritance in ECMAScript. The basic idea is to use the concept of prototypes to inherit properties and methods between two reference types. Each constructor function has a `prototype` object (it's its `constructor` property actually) that points back to the constructor function, and instances have an internal pointer to the `prototype` function. If the prototype were actually an **instance** of another type, then the prototype, being an instance, would have a pointer to that type's prototype that in turn, would have a pointer to its constructor. If that prototype were also an instance of another type, then the pattern would continue, forming a chain between instances and prototypes.

    ```javascript
    function SuperType() {
        this.property = true;
    }
    SuperType.prototype.getSuperValue = function() {
        return this.property;
    };

    // inherit from SuperType
    function SubType() {
        this.subproperty = false;
    }
    SubType.prototype = new SuperType();
    SubType.prototype.getSubValue = function() {
        return this.subproperty;
    };
    Object.keys(SubType.prototype);     // ["property", "getSubValue"] 

    var ins = new SubType();
    ins.getSuperValue();                // true
    ins.constructor === SuperType;      // true
    ins.toString();
    ```

    - A new prototype is assigned to the prototype of `SubType`. That new prototype is an **instance** of `SuperType`, so it get the properties and methods of a `SuperType` **instance** and also points back to the `SuperType`'s prototype.
    - `ins` points to `SubType.prototype`, `SubType.prototype` points to the `SuperType.prototype`.
    - The `getSuperValue()` method remains on the `SuperType.prototype` object, but `property` ends up on `SubType.prototype`. Because `getSuperValue()` is a **prototype method**, and `property` is an **instance property**. `SubType.prototype` is now an instance of `SuperType`, so `property` is stored there.
- All reference types inherit from `Object` by default, which is accomplished through prototype chaining. The **default** prototype for any function is an **instance** of `Object`, meaning that its internal prototype pointer points to `Object.prototype`. This is how custom types inherit all of the default methods such as `toString()` and `valueOf()`. So when `ins.toString()` is called, the method being called actually exists on `Object.prototype`.

    ```javascript
    Function.prototype.__proto__ === Object.prototype;          // true
    Object.prototype.isPrototypeOf(Function);                   // true
    ```

- The first way to determine the relationship between prototypes and instances is to use `instanceof` operator. The `ins` object is technically an instance of `Object`, `SuperType`, and `SubType` because of the prototype chain relationship. The second way is to use the `isPrototypeOf()` method. Each prototype in the chain has access to this method, which returns `true` for an instance in the chain

    ```javascript
    ins instanceof SubType;
    ins instanceof SuperType;
    ins instanceof Object;

    SubType.prototype.isPrototypeOf(ins);        // true
    SuperType.prototype.isPrototypeOf(ins);        // true
    Object.prototype.isPrototypeOf(ins);        // true
    ```

- Often a subtype will need to either override a supertype method or introduce new methods that don't exist on the supertype. The methods must be added to the prototype after the subtype's prototype has been assigned to an instance of the supertype. The object literal approach to creating prototype methods cannot be used with prototype chaining because it will break the prototype chain.
- The **major issue** revolves around prototypes that contain reference values. When implementing inheritance using prototypes, the prototype actually becomes an instance of another type, meaning that what once were instance properties are now prototype properties.

    ```javascript
    function SuperType() {
        this.colors = ["red", "blue"];
    }
    function SubType() {
    }
    SubType.prototype = new SuperType();
    var ins1 = new SubType();
    ins1.colors.push("black");
    ins1.colors;                    // ["red", "blue", "black"] 
    var ins2 = new SubType();
    ins2.colors === ins1.colors;    // true
    ```

- A **second issue** with prototype chaining is that you cannot pass arguments into the supertype constructor when the subtype instance is being created. In fact, there is no way to pass arguments into the supertype constructor without affecting all of the object instances. Because of this and the aforementioned issue with reference values on the prototype, prototype chaining is rarely used alone.
### Constructor stealing
- The constructor stealing is also called object masquerading or classical inheritance. The basic idea is quite simple: **call the supertype constructor from within the subtype constructor**. **Functions are simply objects that execute code in a particular context**, the `apply()` and `call()` methods can be used to execute a constructor **on the newly created object**. One advantage that constructor stealing offers over prototype chaining is the ability to pass arguments into the supertype constructor from within the subtype constructor.

    ```javascript
    function SuperType(name) {
        this.name = name;
        this.colors = ["red", "blue"];
    }
    function SubType() {
        // inherit from SuperType
        SuperType.call(this, "Nick");
        this.age = 29;
    }
    var ins1 = new SubType();
    ins1.name;                  // "Nick"
    this.age;                   // 29
    ins1.colors.push("black");
    ins1.colors;                // ["red", "blue", "black"] 
    var ins2 = new SubType();
    ins2.colors;                // ["red", "blue"]
    ```

    - By using the `call()` method (or alternately, `apply()`), the `SuperType` constructor is **called in the context of the newly created instance** of `SubType`. Doing this effectively runs all of the object initialization code in the `SuperType()` function on the new `SubType` object. The result is that each instance has its own copy of the `colors` property.
    - A value can be passed into the `SuperType` constructor when called from within the `SubType` constructor, effectively setting the `name` property for the `SubType` instance.
- The **downside** to using constructor stealing exclusively is that it introduces the same problems as the constructor pattern for custom types: methods must be defined inside the constructor, so there's no function reuse. Furthermore, methods defined on the supertype's prototype are not accessible on the subtype, so all types can use only the constructor pattern.

<a id="cinh"></a>

### [Combination inheritance](#cnt2)
- Combination inheritance (also called pseudoclassical inheritance) combines prototype chaining and constructor stealing. The basic idea is to use prototype chaining to inherit properties and methods on the prototype and to use constructor stealing to inherit instance properties. This allows function reuse by defining methods on the prototype and allows each instance to have its own properties. Combination inheritance is the **most frequently used** inheritance pattern in JavaScript. It also preserves the behavior of `instanceof` and `isPrototypeOf()` for identifying the composition of objects.

    ```javascript
    function SuperType(name) {
        this.name = name;
        this.colors = ["red", "blue"];
    }  
    SuperType.prototype.sayName = function() {
        console.log(this.name);
    };

    function SubType(name, age) {
        SuperType.call(this, name);
        this.age = age;
    }
    SubType.prototype = new SuperType();
    SubType.prototype.sayAge = function() {
        console.log(this.age);
    };

    var ins1 = new SubType("Nick", 29);
    ins1.colors.push("black");
    ins1.colors;                // ["red", "blue", "black"]
    ins1.sayName();             // "Nick"
    ins1.sayAge();              // 29
    
    var ins2 = new SubType("Greg", 27);
    ins2.colors;                // ["red", "blue"]
    ins2.sayName();             // "Greg"
    ins1.sayName === ins2.sayName;  // true
    ins2.sayAge();              // 27
    ```

- The most **inefficient** part of the combination inheritance pattern is that the supertype constructor is always called twice: once to create the subtype's prototype, and once inside the subtype constructor. Essentially, the subtype prototype ends up with all of the instance properties of a supertype object, only to have it overwritten when the subtype constructor executes.

    ```javascript
    function SuperType(name) {
        this.name = name;
        this.colors = ["red", "blue"];
    }  
    SuperType.prototype.sayName = function() {
        console.log(this.name);
    };

    function SubType(name, age) {
        SuperType.call(this, name); // second call to SuperType()
        this.age = age;
    }
    SubType.prototype = new SuperType();                // first call to SuperType()
    SubType.prototype.constructor = SubType;
    SubType.prototype.sayAge = function() {
        console.log(this.age);
    };

    var ins1 = new SubType("Nick", 29);    
    ```

    - After the first call to `SuperType()`, `SubType.prototype` ends up with two properties: `name` and `colors`. These are instance properties for `SuperType`, but they are now on the `SubType`'s prototype.
    - When the `SubType` constructor is called, the `SuperType` constructor is called a second time, which creates instance properties `name` and `colors` on the new object `ins1` that mask the properties on the prototype.
    - As a result, there are two sets of `name` and `colors` properties: one on the instance and one on the `SubType` prototype. This is the result of calling the `SuperType` constructor twice.

### Prototypal inheritance
- Prototypal inheritance is a method of inheritance that didn't involve the use of strictly defined constructors. The premise was that prototypes allow you to create new objects based on existing objects without the need for defining custom types.

    ```javascript
    function object(o) {
        function F() {}
        F.prototype = o;
        return new F();
    }

    var person = {
        name: "Nick",
        friends: ["S", "C", "V"]
    };
    var anotherPerson = object(person);
    anotherPerson.name = "Greg";
    anotherPerson.friends.push("Rob");
    var yetAnotherPerson = object(person);
    yetAnotherPerson.name = "Lin";
    yetAnotherPerson.friends.push("Linsanity");
    person.friends;     //  ["S", "C", "V", "Rob", "Linsanity"]
    ```

    - The `object()` function creates a temporary constructor, assigns a given object as the constructor's prototype, and returns a new instance of the temporary type. Essentially, `object()` performs a shadow copy of any object that is passed into it.

<a id="objc"></a>

- ECMAScript 5 formalized the concept of prototypal inheritance by adding the `Object.create()` method. This method accepts 2 arguments, an object to use as the prototype for a new object and an optional object defining additional properties to apply to the new object. 
    - When used with one argument, `Object.create()` behaves the same as the `object()` method.

        ```javascript
        var person = {
            name: "Nick",
            friends: ["S", "C", "V"]
        };
        var anotherPerson = Object.create(person);
        anotherPerson.name = "Greg";
        anotherPerson.friends.push("Rob");
        var yetAnotherPerson = Object.create(person);
        yetAnotherPerson.name = "Lin";
        yetAnotherPerson.friends.push("Linsanity");
        person.friends;     //  ["S", "C", "V", "Rob", "Linsanity"]
        ```

    - The second argument for `Object.create()` is in the same format as the second argument for `Object.defineProperties()`: each additional property to define is specified along with its descriptor. Any properties specified in this manner will shadow properties of the same name on the prototype object.

        ```javascript
        var person = {
            name: "Nick",
            friends: ["S", "C", "V"]
        };
        var anotherPerson = Object.create(person, {
            name: {
                value: "Greg"
            }
        });
        anotherPerson.name;     // "Greg" 
        ```

- Prototypal inheritance is useful when there is no need for the overhead of creating separate constructors, but you still need an object to behave similarly to another. Keep in mind that properties containing reference values will always share those values, similar to using the prototype pattern.
### Parasitic inheritance
- The idea behind parasitic inheritance is similar to that of the parasitic constructor and factory patterns: create a function that does the inheritance, augments the object in some way, and then returns the object as if it did all the work.

    ```javascript
    function createAnother(original) {
        // create a new object by calling a function
        var clone = object(original);
        // augment the object in some way
        clone.sayHi = function() {
            console.log("hi");
        }
        return clone;
    }

    var person = {
        name: "Nick",
        friends: ["S", "C", "V"]
    };
    var anotherPerson = createAnother(person);
    anotherPerson.sayHi();      // "hi"
    ```

    - The `createAnother()` function accepts a single argument, which is the object to base a new object on. The code returns a new object based on `person`. The `anotherPerson` object has all of the properties and methods of person but adds a new method called `sayHi()`.
    - The `object()` method is not required for parasitic inheritance; any function that returns a new object fits the pattern.
    - Adding functions to objects using parasitic inheritance leads to inefficiencies related to function reuse, similar to the constructor pattern.
- Parasitic inheritance is another pattern to use when you are concerned primarily with objects and not with custom types and constructors. 

<a id="pcp"></a>

### [Parasitic combination pattern](#cnt2)
- Parasitic combination inheritance uses constructor stealing to inherit properties but uses a hybrid form of prototype chaining to inherit methods. The basic idea is this: instead of calling the supertype constructor to assign the subtype's prototype, all you need is **a copy of the supertype's prototype**. Essentially, use parasitic inheritance to inherit from the supertype's prototype and then assign the result to the subtype's prototype.

    ```javascript
    function object(o) {
        function F() {}
        F.prototype = o;
        return new F();
    }
    function inheritPrototype(subType, superType) {
        var prototype = object(superType.prototype);
     // console.log(prototype.constructor === SuperType);       // true
        prototype.constructor = subType;       
        subType.prototype = prototype;
    }

    function SuperType(name) {
        this.name = name;
        this.colors = ["red", "blue"];
    }
    SuperType.prototype.sayName = function() {
        console.log(this.name);
    };
    function SubType(name, age) {
        SuperType.call(this, name);
        this.age = age;
    }
    inheritPrototype(SubType, SuperType);
    SubType.prototype.sayAge = function() {
        console.log(this.age);
    };
    var ins1 = new SubType("SB", 25);
    ```

    - `inheritPrototype()` accepts two arguments: the subtype constructor and the supertype constructor. The first step is to create a **clone** of the supertype's prototype. Next, the `constructor` property is assigned onto `prototype` variable to account for losing the default constructor property when the `prototype` variable is overwritten. Finally, the subtype's prototype is assigned to the newly created object.
    - This example is more efficient in that the `SuperType` constructor is being called only one time, avoiding having unnecessary and unused properties on `SubType.prototype`. Furthermore, the prototype chain is kept intact, so both `instanceof` and `isPrototypeOf()` behave as they would normally.
- Parasitic combination inheritance is considered the most optimal inheritance paradigm for reference types.

<a id="dat"></a>

## [Date](#cnt2)
- The `Date` object work with dates (years, months, days, hours, minutes, seconds, and milliseconds). GMT (Greenwich Mean Time) is a time zone and UTC (Coordinated Universal Time) is a time standard. GMT and UTC share the same current time.
- `Date` objects are **static**. Time is ticking, but date objects, once created, are not.
- `Data` objects are created with the `new Date()` constructor.
- When setting a date or getting a date, without specifying the time zone, JavaScript will use the browser's time zone.
- There generally are 4 types of JS date input formats. The ISO format follows a strict standard in JavaScript. The other formats are not so well defined and might be browser specific.

Type|Example
---|---
ISO Date	|"2015-03-25" (The International Standard)
Short Date	|"03/25/2015"
Long Date	|"Mar 25 2015" or "25 Mar 2015"
Full Date	|"Wednesday March 25 2015"

- ISO 8601 is the international standard for the representation of dates and times. The ISO 8601 syntax (YYYY-MM-DD) is the preferred JavaScript date format. The computed date will be relative to your time zone.
### Date methods
- When displayed in HTML, a date object is automatically converted to a string with the `toString()` method underneath the hood. `toUTCString()` method converts a date to a UTC string (a date display standard). The `toDateString()` method converts a date to a more readable format.
- `getTime()` returns the number of milliseconds since January 1, 1970. `getFullYear()` returns the year of a date as a four digit number. `getDay()` returns the weekday as a number (0-6). In JavaScript, the first day of the week (0) means "Sunday".
- `setFullYear()` sets a date object to a specific date. `setDate()` sets the day of the month (1 - 31).
- the `Date.parse()` method converts a valid date string to milliseconds between the date and January 1, 1970.

<a id="Reg"></a>

## [`RegExp` object](#cnt2)

<a id="sbio"></a>

## [Singleton built-in objects](#cnt2)
- ECMA-262 defines a built-in object as "any object supplied by an ECMAScript implementation, independent of the host environment, which is present at the start of the execution of an ECMAScript program." This means the developer does not need to explicitly instantiate a built-in object; it is already instantiated. `Object`, `Array`, and `String` are all built-in objects. There are 2 singleton built-in objects defined by ECMA-262: `Global` and `Math`.

<a id="tgo"></a>

### [The `Global` object](#cnt2)
- The `Global` object isn't explicitly accessible. ECMA-262 specifies the `Global` object as a sort of catchall for properties and methods that don't otherwise have an owning object. In truth, there is no such thing as a global variable or global function; all variables and functions defined globally become properties of the `Global` object. Functions such as `isNaN()`, `isFinite()`, `parseInt()`, and are actually methods of the `Global` object. In addition to these, there are several other methods available on the `Global` object.
#### URI-encoding methods
- The `encodeURI()` and `encodeURIComponent()` methods are used to encode URIs (Uniform Resource Identifiers) to be passed to the browser. To be valid, a URI cannot contain certain characters, such as spaces. The URI-encoding methods encode the URIs so that a browser can still accept and understand them, replacing all invalid characters with a special UTF-8 encoding. The `encodeURI()` method is designed to work on an **entire URI** (for instance, `www.wrox.com/ illegal value.htm`), whereas `encodeURIComponent()` is designed to work solely on a segment of a URI (such as `illegal value.htm` from the previous URI). The main difference between the two methods is that `encodeURI()` does not encode special characters that are part of a URI, such as the colon, forward slash, question mark, and pound sign, whereas `encodeURIComponent()` encodes every nonstandard (nonalphanumeric) character it finds.
- The two counterparts to `encodeURI()` and `encodeURIComponent()` are `decodeURI()` and `decodeURIComponent()`. The `decodeURI()` method decodes only characters that would have been replaced by using `encodeURI()`. For instance, `%20` is replaced with a space, but `%23` is not replaced because it represents a pound sign (#), which `encodeURI()` does not replace. `decodeURIComponent()` decodes all characters encoded by `encodeURIComponent()`, essentially meaning it decodes all special values.

    ```javascript
    var uri = "http://www.wrox.com/illegal value.htm#start";

    encodeURI(uri);
    /*    "http://www.wrox.com/illegal%20value.htm#start"
    */
    encodeURIComponent(uri);
    /*
    "http%3A%2F%2Fwww.wrox.com%2Fillegal%20value.htm%23start"
    */
    ```

#### The **`eval()`** method
- The `eval()` method works like an entire ECMAScript interpreter and accepts one argument, a string of ECMAScript (or JavaScript) to execute. When the interpreter finds an `eval()` call, it interprets the argument into actual ECMAScript statements and then inserts it into place. Code executed by `eval()` is considered to be part of the execution context in which the call is made, and the executed code has the same scope chain as that context. This means variables that are defined in the containing context can be referenced inside an `eval()` call. Likewise, functions or variables defined inside an `eval()` can be referenced by the code outside.
- Any variables or functions created inside of `eval()` will not be hoisted, as they are contained within a string when the code is being parsed. They are created only at the time of `eval()` execution. In strict mode, variables and functions created inside of `eval()` are not accessible outside. Assigning a value to `eval` causes an error.

    ```javascript
    eval("console.log('Hi')"); 
    // functionally equivalent to the following
    console.log('Hi');
    ```

### Global Object properties
- The special values of `undefined`, `NaN`, and `Infinity` are all properties of the `Global` object. Additionally, all native reference type constructors, such as `Object` and `Function`, are properties of the `Global` object. In ECMAScript 5, it's explicitly disallowed to assign values to `undefined`, `NaN`, and `Infinity`. Doing so causes an error even in nonstrict mode.
### The `window` object
- Though ECMA-262 doesn't indicate a way to access the `Global` object directly, web browsers implement it such that the `window` is the `Global` object's **delegate**. Therefore, all variables and functions declared in the global scope become properties on `window`.

    ```javascript
    var color = "red";
    function sayColor() {
        console.log(window.color);
    }
    window.sayColor();  // "red"
    ```

- Another way to retrieve the `Global` object: 

    ```javascript
    var global = function() {
        return this;
    }();
    ```

    - The `this` value is equivalent to the `Global` object when a function is executed with no explicit `this` value specified (either by being an object method or via `call()`/`apply()`). Thus, calling a function that simply returns `this` is a consistent way to retrieve the `Global` object in any execution environment.

<a id="mth"></a>

### [The **Math** object](#cnt2)
- The computations available on the `Math` object execute faster than if you were to write the computations in JavaScript directly. Unlike other global objects, the `Math` object has no constructor. Methods and properties are **static**. All methods and properties (constants) can be used without creating a `Math` object first.
### Math object properties (constants)

```javascript
Math.E        // returns Euler's number
Math.PI       // returns PI
Math.SQRT2    // returns the square root of 2
Math.SQRT1_2  // returns the square root of 1/2
Math.LN2      // returns the natural logarithm of 2
Math.LN10     // returns the natural logarithm of 10
Math.LOG2E    // returns base 2 logarithm of E
Math.LOG10E   // returns base 10 logarithm of E
```

### Math object methods
- `Math.round(x)` returns the value of x rounded to its nearest integer (rounds up if the number is at least halfway to the next integer value (0.5 or higher) and rounds down if not). `Math.ceil(x)` returns the value of x rounded up to its nearest integer. `Math.floor(x)` returns the value of x rounded down to its nearest integer. `Math.abs(x)` returns the absolute (positive) value of x.
- `Math.pow(x, y)` returns the value of x to the power of y. `Math.sqrt(x)` returns the square root of x.
- `Math.min()`, `Math.max()`

    ```javascript
    var min = Math.min(3, 54, 32, 16);
    min;        // 3

    var arr = [1, 2, 3, 4, 5, 6, 7, 8];
    var max = Math.max.apply(Math, arr);
    // var max = Math.max.apply(null, arr);      
    max;        // 8 
    ```

- `Math.random()` returns a random number between 0 (inclusive), and 1 (exclusive). `Math.random()` used with `Math.floor()` can be used to return random integers. 

    ```javascript
    //returns a random number between min (included) and max (excluded), [min, max)
    function getRndInteger(min, max) {
        return Math.floor(Math.random() * (max - min) ) + min;
    }

    //returns a random number between min and max (both included), [min, max]
    function getRndInteger(min, max) {
        return Math.floor(Math.random() * (max - min + 1) ) + min;
    }
    ```

<a id="tpo"></a>

## [Tamper-proof objects](#cnt2)
- One of the long-lamented downsides of JavaScript is its shared nature: every object can be modified by any code running in the same context.
### Nonextensible objects
- `Object.preventExtensions()`

    ```javascript
    var person = { name: "SB" };
    Object.preventExtensions(person);
    person.age = 26;
    person.age;                     // undefined

    Object.isExtensible(person);    // false
    ```

    - In nonstrict mode, an attempt to add a new **object member** is silently ignored. In strict mode, attempting to add an object member that doesn't allow extension causes an error to be thrown.

    - All of the existing members remain unaffected. You can still modify and delete already-existing members.
### Sealed objects
- Sealed objects aren't extensible and existing object members have their `[[Configurable]]` attribute set to `false`. This means properties and methods can't be deleted as data properties cannot be changed to accessor properties or vice versa using `Object.defineProperty()`. Property values can still be changed.

    ```javascript
    var person = { name: "SB" };
    Object.seal(person);
    person.age = 26;
    person.age;                     // undefined
    delete person.name;
    person.name;                    // "SB"
    person.name = "Ho";
    person.name;                    // "Ho"

    Object.isSealed(person);        // true
    Object.isExtensible(person);    // false
    ```

### Frozen objects
- The strictest type of tamper-proof object is a frozen object. Frozen objects aren't extensible and are sealed, and also **data properties** have their `[[Writable]]` attribute set to `false`. Accessor properties may still be written to but only if a `[[Set]]` function has been defined. 

    ```javascript
    var person = { name: "SB" };
    Object.freeze(person);
    person.age = 26;
    person.age;                     // undefined
    delete person.name;
    person.name;                    // "SB"
    person.name = "Ho";
    person.name;                    // "SB"

    Object.isSealed(person);        // true
    Object.isExtensible(person);    // false
    Object.isFrozen(person);        // true
    ```

    - Attempts to perform disallowed operations on a frozen object are ignored in nonstrict mode and throw an error in strict mode.

<a id="scp"></a>

# [Execution context and scope](#cnt2)
- There are only two primary types of execution contexts, **global** and **function** (the third exists inside of a call to `eval()`).

- The execution context of a variable or function defines what other data it has access to, as well as how it should behave. Each execution context has an associated ***variable object*** upon which all of its defined variables and functions exist. This object is not accessible by code but is used behind the scenes to handle data. 
- The global execution context is the outermost one. Depending on the host environment for an ECMAScript implementation, the object representing this context may differ. In web browsers, the global context is said to be that of the `window` object, so all global variables and functions are created as properties and methods on the `window` object. When an execution context has executed all of its code, it is destroyed, taking with it all of the variables and functions defined within it (the global context isn't destroyed until the application exits, such as when a web page is closed or a web browser is shut down).
- **Each function call has its own execution context**. Whenever code execution flows into a function, the function's context is pushed onto a **context stack**. After the function has finished executing, the stack is popped, returning control to the previously executing context.
- When code is executed in a context, a *scope chain* of **variable objects** is created to provide ordered access to all variables and functions that an execution context has access to. **The front** of the scope chain is always the variable object of the context whose code is executing. If the context is a function, then the *activation object* is used as the variable object. An activation object starts with a single defined variable called `arguments`. (This doesn't exist for the global context.) The next variable object in the chain is from the containing context, and the next after that is from the next containing context. This pattern continues until the global context is reached; the global context's variable object is always **the last** of the scope chain.
- Identifiers are resolved by navigating the scope chain in search of the identifier name. The search always begins at the front of the chain and proceeds to the back and stops searching as soon as the first matched identifier is found (objects in the scope chain also have a *prototype* chain, so searching may include each object's *prototype* chain). If the identifier isn't found, typically an error occurs. Function arguments are considered to be variables and follow the same access rules as any other variable in the execution context. Referencing local variables automatically stops the search from going into another variable object. This means that identifiers in a parent context cannot be referenced if an identifier in the local context has the same name.

    ```javascript
    var color = "blue";
    function changeColor() {
        if (color === "blue") {
            color = "red";
        } esle {
            color = "blue";
        }
    }
    changeColor();
    ```

    - The function `changeColor()` has a scope chain with two objects in it: its own variable object (upon which the `arguments` object is defined) and the global context's variable object. The variable `color` is accessible inside the function, because it can be found in the scope chain.

    ```javascript
    var color = "blue";
    function changeColor() {
        var anotherColor = "red";
        function swapColors () {
            var tempColor = anotherColor;
            anotherColor = color;
            color = tempColor;
            // color, anotherColor, and tempColor are all accessible here
        }
        // color and anotherColor are accessible here, but not tempColor
        swapColors();
    }
    // only color is accessible here
    changeColor();
    ```

    - There are three objects in the scope chain for the local context of `swapColors()`: the `swapColors()` variable object, the variable object from `changeColor()`, and the global variable object.

- There are other ways to augment the scope chain. Certain statements cause a temporary addition of variable object to the **front** of the scope chain that is later removed after code execution.
    - For the `catch` block in a `try-catch` statement, a new variable object is created and contains a declaration for the thrown error object.
    - For the `with` statement, the specified object is added to the scope chain.

        ```javascript
        function buildUrl() {
            var qs = "?debug=true";
            with(location) {
                var url = href + qs;
            }
            return url;
        }
        ```

        - The `with` statement is acting on the `location` object, so `location` itself is added to the front of the scope chain. When the variable `href` is referenced, it's actually referring to `location.href`, which is in its own variable object. When the variable `qs` is referenced, it's referring to the variable defined in `buildUrl()`, which is in the function context's variable object. Inside the `with` statement is a variable declaration for `url`, which becomes part of the function's context and can, therefore, be returned as the function value.

- In JavaScript, there's no block-level scope, just execution context. This is important to keep in mind when dealing with the `for` statement.

    ```javascript
    if(true) {
        var color = "blue";
    }
    color;          // "blue"

    for (var i = 0; i < 10; i++) {
        doSomething(i);
    }
    i;              // 10
    ```

    - In languages with block-level scoping, the `color` variable will be destroyed after the `if` statement is executed. And the initialization part of the `for` statement defines variables that exist only within the context of the loop. In JavaScript, the variable declaration adds a variable into the current execution context (the global context, in this case). The `i` variable is created by the `for` statement and continues to exist outside the loop after the statement executes.

- When a variable is declared using `var`, it is automatically added to the most immediate context available. In a function, the most immediate one is the function's local context; in a `with` statement, the most immediate is the function context. If a variable is initialized without first being declared using `var`, it gets added to the global context automatically.
- The execution context of variables helps to determine when memory will be freed.

<a id="gcll"></a>

## [Garbage collection](#cnt2)
- JavaScript is a garbage-collected language, meaning that the execution environment is responsible for managing the memory required during code execution. The basic idea is figuring out which variables aren't going to be used and free the memory associated with them. This process is periodic, with the garbage collector running at specified intervals (or at predefined collection moments in code execution).

- The amount of memory available for use in web browsers is typically much less than is available for desktop applications, which is more of a security feature. The memory limits affect not only variable allocation but also the call stack and the number of statements that can be executed in a single thread. When data is no longer necessary, it's best to set the value to *null*, freeing up the reference (called dereferencing the value). This advice applies mostly to global values, properties of global objects, and circular references. Local variables are dereferenced automatically when they go out of context. Dereferencing a value doesn't automatically reclaim the memory associated with it. The point of dereferencing is to make sure the value is out of context and will be reclaimed the next time garbage collection occurs.
## ***mark-and-sweep***
- The most popular form of garbage collection for JavaScript is called *mark-and-sweep*. When a variable comes into context, it is flagged as being in context. Variables that are in context, logically, should never have their memory freed, because they may be used as long as execution continues in that context. When a variable goes out of context, it is also flagged as being out of context.

- When the garbage collector runs, it **marks all** variables stored in memory. It then clears its mark off of variables that are in context and variables that are **referenced** by in-context variables. The variables that are marked after that are considered ready for deletion, because they can't be reached by any in-context variables. The garbage collector then does a memory sweep, destroying each of the marked values and reclaiming the memory associated with them.
## *Reference counting*
- The idea is that every value keeps track of how many references are made to it. When a variable is declared and a reference value is assigned, the reference count is one. If another variable is then assigned to the same value, the reference count is incremented. If a variable with a reference to that value is overwritten with another value, then the reference count of that variable is decremented. When the reference count of a value reaches 0, there is no way to reach that value and it is safe to reclaim the associated memory. The garbage collector frees the memory for values with a reference count of zero the next time it runs.
- A circular reference occurs when object A has a pointer to object B and object B has a reference to object A.

    ```javascript
    function problem(){
        var objectA = new Object();
        var objectB = new Object();
        objectA.someOtherObject = objectB;
        objectB.anotherObject = objectA;
    }
    ```

    - `objectA` and `objectB` reference each other through their properties, so each has a reference count of two. In a *mark-and-sweep* system, both objects go out of scope after the function has completed. In a reference-counting system, `objectA` and `objectB` will continue to exist after the function has exited, because their reference counts will never reach 0.
- Setting a variable to *null* effectively severs the connection between the variable and the value it previously referenced.
- JavaScript engines no longer use this algorithm, but it still affects Internet Explorer because of nonnative JavaScript objects (such as DOM elements) being accessed in JavaScript.

<a id="fu"></a>

# [Functions](#fun)
- Functions are objects. Each function is an instance of the `Function` type that has properties and methods just like any other reference type. Because functions are objects, **function names are simply pointers to function objects** and are not necessarily tied to the function itself. Function-declaration syntax:
    1. Use a function declaration.

        - Function declarations are read and added to the execution context before the code begins running through a process called ***function declaration hoisting***. As the code is being evaluated, the JavaScript engine does a first pass for function declarations and pulls them to the top of the source tree. So even though the function declaration appears after its usage in the actual source code, the engine changes this to *hoist* the function declarations to the top.

            ```javascript
            sum(1, 2);
            function sum(num1, num2) {
                return num1 + num2;
            }
            sum.name;       // "sum"
            ```

        - There's a nonstandard `name` property on functions to exposing the assigned name. This value is always equivalent to the identifier that immediately follows the `function` keyword.
    1. Use a function expression. 
        - Any time a function is being used as a value, it is a function expression.
        - The created function is considered to be an anonymous function, because it has no identifier after the `function` keyword. A function expression without a name is called an anonymous function. (also called lambda functions.) This means the `name` property is the empty string.
        - Function expressions aren't complete until the execution reaches that line of code. The function is part of an initialization statement, not part of a function declaration. 

            ```javascript
            sum(1, 2);      // cause an error
            var sum = function(num1, num2){
                return num1 + num2;
            };
            ```

            - The function isn't available in the variable `sum` until the second line has been executed, which won't happen, because the first line causes an "unexpected identifier" error.
        - The following usage of  function declaration is not valid syntax in ECMAScript while function expressions work fine in this case.

            ```javascript
            //never do this!
            if(condition){
                function sayHi(){
                    alert("Hi!");
                }
            } else {
            function sayHi(){
                    alert("Yo!");
                }
            }
            ```

            - JavaScript engines try to error correct the invalid syntax into an appropriate state. The problem is that browsers don't consistently error correct in this case. Most browsers return the second declaration regardless of `condition`; Firefox returns the first when condition is `true`. This pattern is dangerous and should not be used.


    1. Use the `Function` constructor (not recommended). It accepts any number of arguments. The last argument is always considered to be the function body, and the previous arguments enumerate the new function's arguments. It causes a double interpretation of the code (once for the regular ECMAScript code and once for the strings that are passed into the constructor) and thus can affect performance.

        ```javascript
        var sum = new Function("num1", "num2", "return num1 + num2");
        ```
    
- Because function names are simply pointers to functions, they act like any other variable containing a pointer to an object. This means it's possible to have **multiple names for a single function**. Using the function name without parentheses accesses the function pointer (or function definition) instead of executing the function. Thinking of function names as pointers explains why there can be no function overloading in ECMAScript. If two functions are defined to have the same name in ECMAScript, it is the last function that becomes the owner of that name.

    ```javascript
    function addN(num1, num2) {
        return arguments[0] + arguments[1];
    }
    function addN(num) {
        return num + 200;
    }
    addN(10, 1);       // 210

    // clearer version
    var addNumber = function(num1, num2) {
        return arguments[0] + arguments[1];
    };
    addNumber = function(num) {
        return num + 200;
    };
    addNumber(10, 1);       // 210
    ```

- Function **parameters** are the names listed in the function definition. Function **arguments** are the real values received by the function when it is invoked. 
- An ECMAScript function doesn't care how many arguments are passed in, nor does it care about the data types of those arguments. Arguments in ECMAScript are represented as an array internally. The array is always passed to the function, but the function doesn't care what (if anything) is in the array. It's a **workaround for overloading**. Named arguments are a convenience, not a necessity. Naming arguments in ECMAScript does not create a **function signature** that must be matched later on.
- Two special **objects** exist inside a function: `arguments` and `this`. 
- There is an `arguments` object that can be accessed while **inside a function** to retrieve the values of each argument that was passed in. The `arguments` object acts like an array (though it isn't an instance of `Array`) in that you can access each argument using bracket notation and determine how many arguments were passed in by using the `length` property. `aruments` has **only** the `length` property and no methods.
- Values in the arguments object are automatically reflected by the corresponding named arguments, **the change to `arguments[1]` also changes the value of num2**, so both have a value of 10. This doesn't mean that both access the same memory space, though; their memory spaces are separate but happen to be kept in sync. **This effect goes both ways**: changing the named argument (if passed in) results in a change to the corresponding value in arguments too. If only one argument is passed in, then setting `arguments[1]` to a value will not be reflected by the named argument. This is because **the length of the arguments object is set based on the number of arguments passed in**, not the number of **named arguments listed** for the function. Any named argument that is not passed into the function is automatically assigned the value *undefined*.

    ```javascript
    function doAdd(num1, num2) {
        arguments[1] = 10;
        console.log(isNaN(num2));
        return arguments[0] + num2;
    }
    doAdd(1, 2);        // 11
    doAdd(1);           // NaN 
    // isNaN(num2) is true

    function doAdd1(num1, num2) {
        num2 = 10;
        return arguments[0] + arguments[1];
    }
	doAdd1(1,2);        // 11
    ```

- Function names in ECMAScript are nothing more than variables, functions can be used any place any other value can be used. This means it's possible not only to pass a function into another function as an argument but also to return a function as the result of another function.

    ```javascript
    function callSomeFunction(someFunction, someArgument){
        return someFunction(someArgument); 
    }
    function add10(num) {
        return num + 10;
    }
    callSomeFunction(add10, 11);        // 21


    // sort array of objects by certain property name
    var byProperty = function (propertyName) {
        return function (obj1, obj2) {
            var a, b;
            if (obj1 && obj2 && typeof obj1 === "object" && typeof obj2 === "object") {
                a = obj1[propertyName];
                b = obj2[propertyName];
                if (a === b) {
                    return 0;
                }
                if (typeof a === typeof b) {
                    return a < b ? -1 : 1;
                }
                return typeof a < typeof b ? -1 : 1;
            }
            else {
                throw {
                    name: "Error",
                    message: "Expected an object when sorting by  " + propertyName
                };
            }
        };
    };
    var s = [
    {first: 'Joe', last: 'Besser'},
    {first: 'Moe', last: 'Howard'},
    {first: 'Joe', last: 'DeRita'},
    {first: 'Shemp', last: 'Howard'},
    {first: 'Larry', last: 'Fine'},
    {first: 'Curly', last: 'Howard'}
    ];
    s.sort(byProperty('first')); // s is [
    // {first: 'Curly', last: 'Howard'},
    // {first: 'Joe', last: 'DeRita'},
    // {first: 'Joe', last: 'Besser'},
    // {first: 'Larry', last: 'Fine'},
    // {first: 'Moe', last: 'Howard'},
    // {first: 'Shemp', last: 'Howard'}
    // ]


    // take a second parameter to break ties
    var byProperty2 = function (propertyName, breakTie) {
        return function (obj1, obj2) {
            var a, b;
            if (obj1 && obj2 && typeof obj1 === "object" && typeof obj2 === "object") {
                a = obj1[propertyName];
                b = obj2[propertyName];
                if (a === b) {
                    // type of byProperty2('first') is a function 
                    return typeof breakTie === "function" ? breakTie(obj1, obj2) : 0;   // not curry, just simple function invocation
                }
                if (typeof a === typeof b) {
                    return a < b ? -1 : 1;
                }
                return typeof a < typeof b ? -1 : 1;
            }
            else {
                throw {
                    name: "Error",
                    message: "Expected an object when sorting by  " + propertyName
                };
            }
        };
    };
    s.sort(byProperty2('last', byProperty2('first'))); // s is [
    // {first: 'Joe', last: 'Besser'},
    // {first: 'Joe', last: 'DeRita'},
    // {first: 'Larry', last: 'Fine'},
    // {first: 'Curly', last: 'Howard'},
    // {first: 'Moe', last: 'Howard'},
    // {first: 'Shemp', last: 'Howard'}
    // ]
    ```

- **All function arguments in ECMAScript are passed by value**. Either a primitive value or a pointer value outside of the function is copied into an argument on the inside of the function. 

    ```javascript
    function setName(obj) {
        obj.name = "SB";
        obj = new Object();
        obj.name = "Ho";
    }
    ver person = new Object();
    setName(person);
    person.name;    // "SB" instead of "Ho"
    ```

- Functions in ECMAScript need not specify whether they have a value to return. JavaScript does not allow a line end between the `return` and the expression. The return value will be returned to the caller statement. If a return expression is not specified, then the return value will be *undefined*. A function stops executing and exits immediately when it encounters the `return` statement. Any code that comes after a `return` statement will never be executed.
    > It's recommended that a function either always return a value or never return a value. Writing a function that sometimes returns a value causes confusion, especially during debugging.

<a id="rec"></a>
    
## [Recursion](#fun)
- A recursive function typically is formed when a function calls itself by name.
- The `arguments` object also has a **property** named `callee`, which is a **pointer** to the function (being executed) that **owns** the `arguments` object. The value of `arguments.callee` is not accessible to a script running in strict mode and will cause an error when attempts are made to read it.

    ```javascript
    function factorial(num) {
        if (num <= 1) {
            return 1;
        } else {
            return num * arguments.callee(num - 1);
         // return num * factorial(num-1);   
        }
    }
    var trueFactorial = factorial;
    factorial = function() {
        return 0;
    };
    trueFactorial(5);       // 120
    factorial(5);           // 0
    ```

    - `arguments.callee` **decouples** the tight binding between the the proper execution of the function with the function name "factorial".
    Without using `arguments.callee` in the original `factorial()` function's body, the call to `trueFactorial()` would return 0 (`num * factorial(num-1)` equals `num * 0`).
    - It's advisable to always use `arguments.callee` of the function name whenever you're writing recursive functions.
- Using named function expressions can achieve the same result.

    ```javascript
    var factorial = (function f(num) {
        if (num <= 1) {
            return 1;
        } else {
            return num * f(num - 1);
        }
    });
    ```

    - A named function expression `f()` is created and assigned to the variable `factorial`. The name `f` remains the same even if the function is assigned to another variable, so the recursive call will always execute correctly. This pattern works in both nonstrict mode and strict mode.

<a id="clo"></a>
    
## [Closure](#fun)
- **Closures** are functions that have access to variables from another function's scope. This is often accomplished by creating a function inside a function.
- When a function is called, an execution context is created, and its scope chain is created. The **activation object** for the function is initialized with values for `arguments` and any named arguments. The outer function's activation object is the second object in the scope chain. This process continues for all containing functions until the scope chain terminates with the global execution context. As the function executes, variables are looked up in the scope chain for the reading and writing of values.

    ```javascript
    function compare(value1, value2) {
        if (value1 < value2) {
            return -1;
        } else if (value1 > value2) {
            return 1;
        } else {
            return 0;
        }
    }
    var result = compare(5, 10);
    ```

    - When `compare()` is called for the first time, a new activation object is created that contains `arguments`, `value1`, and `value2`. The global execution context's variable object is next in the `compare()` execution context's scope chain, which contains `this`, `result`, and `compare`.
- Behind the scenes, ***an object* represents the variables in each execution context**. The global context's variable object always exists, whereas local context variable objects, such as the one for `compare()`, exist only while the function is **being executed**. When `compare()` is **defined**, its **scope chain** is created, preloaded with the global variable object, and saved to the internal `[[Scope]]` property. When the function is **called**, an **execution context** is created and its scope chain is built up by copying the objects in the function's `[[Scope]]` property. After that, an **activation object** (which also acts as a variable object) is created and pushed to the front of the context's scope chain. In this example, that means the `compare()` function's execution context has two variable objects in its scope chain: the local activation object and the global variable **object**.
- Whenever a variable is accessed inside a function, the scope chain is searched for a variable with the given name. Once the function has completed, the local activation object is destroyed, leaving only the global scope in memory. Closures behave differently.
- A function that is **defined** inside another function adds the containing function's **activation object** into its scope chain. That is to say, the inside function's scope chain has an reference to the containing function's activation object.

    ```javascript
    function createComparisonFunction(propertyName) {
        return function(object1, object2) {
            var value1 = object1[propertyName];
            var value2 = object2[propertyName];
            if (value1 < value2) {
                return -1;
            } else if (value1 > value2) {
                return 1;
            } else {
                return 0;
            }
        };
    }
    // create function
    var compareNames = createComparisonFunction("name");
    // call function
    var result = compareNames({ name: "Nick" }, { name: "Greg" });
    ```

    - In `createComparisonFunction()`, the anonymous function's scope chain contains a **reference** to the activation object for `createComparisonFunction()`.
    - When the anonymous function is returned from `createComparisonFunction()`, its scope chain has been initialized to contain the activation object from `createComparisonFunction()` and the global variable object. This gives the anonymous function access to all of the variables from `createComparisonFunction()`.
    - The activation object from `createComparisonFunction()` cannot be destroyed once the function finishes executing, because a reference still exists in the anonymous function's scope chain. Because the anonymous function hasn't finished yet.
    - After `createComparisonFunction()` completes, the scope chain for its execution context is destroyed, but **its activation object** will remain in memory until the anonymous function is destroyed.

        ```javascript
        //dereference function
        compareNames = null;
        ```

        - Setting `compareNames` equal to `null` dereferences the function and allows the garbage collection routine to clean it up. The scope chain will then be destroyed and, all of the scopes (except the global scope) can be destroyed safely.
- Since closures carry with them the containing function's scope, they take up more memory than other functions. Overuse of closures can lead to **excess memory consumption**, so it's recommended you use them only when absolutely necessary.
### Closures and variables
- Closure stores a reference to the entire variable object, not just to a particular variable. The closure always gets **the last value** of any variable from the containing function.

    ```javascript
    function createFunction() {
        var result = new Array();
        for (var i = 0; i < 10; i++) {
            result[i] = function() {
                return i;
            };
        }
        return result;  
    }
    var a = createFunction();
    a.forEach(function(item) {
        console.log(item());            // all 10
    });
    ```

    - The function returns an array of functions. Since each function has the `createFunctions()` activation object in its scope chain, they are all referring to the same variable object with the variable `i` in it. When `createFunctions()` finishes running, the value of `i` is 10, and since every function references the same variable object in which `i` exists, the value of `i` inside each function is 10.
- This version act appropriately.

    ```javascript
    function createFunctions(){
        var result = new Array();
        for (var i = 0; i < 10; i++) {
            result[i] = function(num) {
                return function() {
                    return num;
                };
            }(i);
        }
        return result;
    }
    console.log(createFunctions()[4]());                // 4
    ```

    - An anonymous function is defined and called immediately. The anonymous has one argument, `num`, which is the number that the result function should return. The variable `i` is passed in as an argument to the anonymous function. Since function arguments are passed by value, the current value of `i` is copied into the argument `num`. Inside the anonymous function, a closure that accessed `num` is created and returned. Now each function in the result array has its own copy of `num` and thus can return separate numbers.

<a id="thcl"></a>
    
### [The `this` object](#thi)
<!-- - The `this` object is bound at runtime based on the **context** in which a function is executed: when used inside global functions, `this` is equal to `window` in nonstrict mode and *`undefined`* in strict mode, whereas `this` is equal to the object when called as an object method. Anonymous functions are not bound to an object in this context, meaning the `this` object points to `window` unless executing in strict mode (where this is *`undefined`*).

    ```javascript
    var name = "The Window";
    var obj = {
        name: "My Object",
        getNameFunc: function() {
            console.log(this);          // obj        
            return function() {
                console.log(this);      // Window
                return this.name;
            };
        }
    };
    obj.getNameFunc()();                // "The Window"
    ```

    - The anonymous function that returns `this.name` is not bound to an object.

- Each function automatically gets two special variables as soon as the function is called: `this` and `arguments`. **An inner function can never access these variables directly from an outer function**. It is possible to allow a closure access to a different `this` object by storing it in another variable that the closure can access.

    ```javascript
    var name = "The Window";
    var obj = {
        name: "My Object",
        getNameFunc: function() {
            var that = this;        // obj
            return function() {
                return that.name;
            };
        }
    };
    obj.getNameFunc()();             // "My Object"
    ```

    - When closure is defined, the anonymous function has access to `that`. Even after the function is returned, `that` is still bound to `obj`.

    - Both `this` and `arguments` behave in this way. If you want access to a containing scope's `arguments` object, you'll need to save a reference into another variable that the closure can access.
- The value of `this` can change in unexpected ways when syntax is changed slightly.

    ```javascript
    var name = "The Window";
    var obj = {
        name: "My Object",
        getName: function() {
            return this.name;
        }
    };
    (obj.getName = obj.getName)();      // "The Window" in non-strict mode
    ```

    - The value of last-line **assignment expression** is the function definition in the global scope, so the `this` value is not maintained. -->
### Memory leaks
- The way closures work causes particular problems in Internet Explorer prior to version 9 because of the different garbage-collection routines used for JScript objects versus COM objects. Storing a scope in which an HTML element is stored effectively ensures that the element cannot be destroyed.

    ```javascript
    function assignHandler() {
        var element = document.getElementById("someElement");
        element.onclick = function() {
            alert(element.id);
        };
    }
    ```

    - This code creates a closure as an event handler on element, which in turn creates a circular reference. The anonymous function keeps a reference to the `assignHandler()` function's activation object, which prevents the reference count for element from being decremented. As long as the anonymous function exists, the reference count for element will be at least 1, which means the memory will never be reclaimed.
- Another version.

    ```javascript
    function assignHandler() {
        var element = document.getElementById("someElement");
        var id = element.id;
        element.onclick = function() {
            alert(id);
        };
        element = null;
    }
    ```

    - A copy of element's ID is stored in a variable that is used in the closure, eliminating the circular reference. The closure has a reference to the containing function's entire activation object, which contains element. Even if the closure doesn't reference element directly, a reference is still stored in the containing function's activation object.
    - It is necessary, therefore, to set the element variable equal to `null`. This dereferences the COM object and decrements its reference count, ensuring that the memory can be reclaimed when appropriate.
## Mimicking block scope
- JavaScript will never tell you if you've declared the same variable more than once; it simply **ignores all subsequent declarations** (though it will honor initializations).
- Anonymous functions can be used to mimic block scoping.

    ```javascript
    (function() {
        // block code here
    })();
    ```

    - What looks like a function declaration is **enclosed in parentheses** to indicate that it's actually a **function expression**.
- The following won't work.

    ```javascript
    function() {
        // block code here
    }();        // error!
    ```

    - This causes a syntax error because **JavaScript sees the `function` keyword as the beginning of a function declaration**, and function declaration cannot be followed by parentheses. Function expressions can be followed by parentheses.
- These private scopes can be used anywhere variables are needed temporarily.

    ```javascript
    function outputNumbers(count) {
        (function() {
            for (var i = 0; i < count; i++) {
                console.log(i);
            }
        })();
        console.log(i);     // error
    }
    ```

    - Any variables defined within the anonymous functions are destroyed as soon as it completes execution. The `count` variable is accessible inside the private scope because the anonymous function is a closure, with full access to the containing scope's variables. 
- This technique is often used in the global scope outside of functions to limit the number of variables and functions added to the global scope. Typically you want to avoid adding variables and functions to the global scope, especially in large applications with multiple developers, to avoid naming collisions. Private scopes allow every developer to use his or her own variables without worrying about polluting the global scope. This pattern limits the closure memory problem, because there is no reference to the anonymous function. Therefore the scope chain can be destroyed immediately after the function has completed.

<a id="pvar"></a>

## [Private variables](#fun)
- Strictly speaking, JavaScript has no concept of private members; all object properties are public. There is, however, a concept of ***private variables***. **Any variable defined inside a function is considered private** since it is inaccessible outside that function (because of the way in which variables are resolved). This includes function arguments, local variables, and functions defined inside other functions. 
- Using closures can create public methods that have access to private variables.
- A privileged method is a public method that has access to private variables and/or private functions. There are two ways to create privileged methods on objects. The first is to do so inside a **constructor**.

    ```javascript
    function MyObject() {
        // private variables and functions
        var privateVariable = 10;
        function privateFunction() {
            return false;
        }

        // privileged methods
        this.publicMethod = function() {
            privateVariable++;
            return privateFunction();
        };
    }
    ```

    - The variable `privateVariable` and the function `privateFunction()` ( of the constructor function `MyObject()` ) are accessed only by `publicMethod()` of an object instance.
- Define private and privileged members to hide data that should not be changed directly.

    ```javascript
    function Person(name) {
        this.getName = function() {
            return name;
        };
        this.setName = function(value) {
            name = value;
        }
    }
    ```

    - Since both methods are defined inside the constructor, they are closures and have access to `name` through the scope chain. 
    - The private variable `name` is unique to each instance of `Person` since the methods are being re-created each time the constructor is called.
    - The constructor pattern is **flawed** in that new methods are created for each instance.
### Static private variables
- Privileged methods can also be created by using **a private scope** to define the private variables or functions.

    ```javascript
    (function() {
        var privateVariable = 10;
        function privateFunction() {
            return false;
        }

        MyObject = function() {
        };
        MyObject.prototype.publicMethod = function() {
            privateVariable++;
            return privateFunction();
        };
    })();
    ```

    - This pattern defines the constructor not by using a function declaration but instead by using a function expression. **Function declarations always create local functions**, which is undesirable in this case. For this same reason, the `var` keyword is not used with `MyObject`. Initializing an undeclared variable always creates a global variable, so `MyObject` becomes global and available outside the private scope.

    - Private variables and functions are shared among instances since the privileged method is defined on the prototype.
- Creating static private variables in this way allows for better code reuse through prototypes, although each instance doesn't have its own private variable.

    ```javascript
    (function() {
        var name = "";
        Person = function(value) {
            name = value;
        }
        Person.prototype.getName = function() {
            return name;
        };
        Person.prototype.setName = function(value) {
            name = value;
        };
    })();
    var p1 = new Person("Nick");
    p1.getName();               // "Nick"
    p1.setName("Greg");
    p1.getName();               // "Greg"    
    var p2 = new Person("Michael");
    p2.getName();               // "Michael"
    p1.getName();               // "Michael"
    ```

    - The containing function has finished executed. All instances of the global constructor holds a reference to that **same** containing scope. Using this pattern, the `name` variable (it's in the containing function's activation object, but not `this.name`) becomes static and will be used among all instances. `name` is not a property for any instance.
### The module pattern
- Singletons are objects of which there will only ever be **one instance**. Traditionally, singletons are created in JavaScript using object literal notation.

    ```javascript
    var singleton = {
        name: value,
        method: function() {
            // method code here
        }
    };
    ```
- The module pattern augments the basic singleton to allow for private variables and privileged methods.

    ```javascript
    var singleton = function() {
        var privateVariable = 10;
        function privateFunction() {
            return false;
        }

        // privileged/public methods and properties
        return {
            publicProperty: true,
            publicMethod: function() {
                privateVariable++;
                return privateFunction();
            }
        };
    }();
    ```

    - The module pattern uses an anonymous function that returns an object literal. That object literal contains only properties and methods that should be public. Since the object is defined inside the anonymous function, all of the public methods have access to the private variables and functions. Essentially, **the object literal defines the public interface for the singleton**.
- This pattern be useful when the singleton requires some sort of initialization and access to private variables. In web applications, it's quite common to have a singleton that manages application-level information.

    ```javascript
    var application = function() {
        // private variables
        var components = new Array();
        // initialization
        components.push(new BaseComponent());
        // public interface
        return {
            getComponentCount: function() {
                return components.length;
            },
            registerComponent: function(component) {
                if (typeof component == "object") {
                    components.push(component);
                }
            }
        };
    }();
    ```

    - This code creates an application object that manages components. When the object is first created, the private components array is created and a new instance of `BaseComponent` is added to its list. (The code for `BaseComponent` is not important; it is used only to show initialization in the example.)
- The module pattern is useful for cases like this, when a single object must be created and initialized with some data and expose public methods that have access to private data. Every singleton created in this manner is an instance of `Object`, since ultimately an object literal represents it. This is inconsequential, because singletons are typically accessed globally instead of passed as arguments into a function, which negates the need to use the `instanceof` operator to determine the object type.
### The module-augmentation pattern
- Another take on the module pattern calls for the augmentation of the object before returning it. This pattern is useful when the singleton object needs to be an instance of a particular type but must be augmented with additional properties and/or methods.

    ```javascript
    var singleton = function() {
        var privateVariable = 10;
        function privateFunction() {
            return false;
        }
        var object = new CustomType();
        // add privileged/public properties and methods
        object.publicProperty = true;
        object.publicMethod = function() {
            privateVariable++;
            return privateFunction();
        };
        return object;
    }();
    ```
- A rewritten version of the application singleton.
    ```javascript
    var application = function() {
        // private variables
        var components = new Array();
        // initialization
        components.push(new BaseComponent());
        // create a copy of the application
        var app = new BaseComponent();
        // public interface
        app.getComponentCount = function() {
            return components.length;
        };
        app.registerComponent = function(component) {
            if (typeof component == "object") {
                components.push(component);
            }
        };
        return app;
    }();
    ```

    - The main difference is the creation of a variable named `app` that is a new instance of `BaseComponent`. This is the **local version** of what will become the `application` object. Public methods are then added onto the `app` object to access the private variables. 
    - The last step is to return the `app` object, which assigns it to `application`.

<a id="thi"></a>

## [***this***](#thcl)
<!-- - `this` is not a variable. It's a keyword and its value cannot be changed. `this` is the object that owns the code. The value of `this`, when used in a function, is the object that "owns" the function. The value of `this`, when used in an object, is the object itself.
- The `this` keyword in an object constructor does not have a value. It is only a **substitute** for the new object. The value of `this` will become the new object when the constructor is used to create an object.
- In the global execution context (outside of any function), `this` refers to the global object whether in strict mode or not. -->
<!-- - The `this` object reference to the **context object** that the function is operating on — often called the `this` value (when a function is **called** in the global scope of a web page, the this object points to `window`). The value of `this` is not determined **until the function is called**, so its value may not be consistent throughout the code execution.

    ```javascript
    window.color = "red";
    var o = { color: "blue" };
    function sayColor() {
        console.log(this.color);
    }

    sayColor();         // "red"
    o.sayColor = sayColor;
    o.sayColor();       // "blue"
    ```

    - The function `sayColor()` is defined globally but references the `this` object. When `sayColor()` is called in the global scope, it outputs "red" because `this` is pointing to `window`, which means `this.color` evaluates to `window.color`. By assigning the function to the object `o` and then calling `o.sayColor()`, the `this` object points to `o`, so `this.color` evaluates to `o.color` and "blue" is displayed. Function names are simply variables containing pointers, so the global `sayColor()` function and `o.sayColor()` point to the same function even though they execute in different contexts. -->
<!-- - When a function is called as a method of an object, its `this` is set to the object the method is called on. 

    ```javascript
    var o = {
        prop: 37,
        f: function() {
            return this.prop;
        }
    };

    console.log(o.f()); // 37


    var o = {prop: 37};

    function independent() {
        return this.prop;
    }

    o.f = independent;

    console.log(o.f()); // 37
    ```

    - This behavior is not at all affected by how or where the function was defined. It matters only that the function was invoked from the `f` member of `o`. -->
<!-- - The `this` binding is only affected by the most immediate member reference. 

    ```javascript
    o.b = {g: independent, prop: 42};
    console.log(o.b.g()); // 42
    ```

    - `this` inside the will refers to `o.b`. The fact that the object is itself a member of `o` has no consequence; the most immediate reference is all that matters.
- The same notion holds true for methods defined somewhere on the object's prototype chain. If the method is on an object's prototype chain, `this` refers to the object the method was called on, as if the method were on the object.

    ```javascript
    var o = {f: function() { return this.a + this.b; }};
    var p = Object.create(o);
    p.a = 1;
    p.b = 4;

    console.log(p.f()); // 5
    ```

    - The object assigned to the variable `p` doesn't have its own f property, it inherits it from its prototype. But it doesn't matter that the lookup for `f` eventually finds a member with that name on `o`; the lookup began as a reference to `p.f`, so `this` inside the function takes the value of the object referred to as `p`. That is, since `f` is called as a method of `p`, its `this` refers to `p`. This is an interesting feature of JavaScript's prototype inheritance. -->
- <!-- The same notion holds true when a function is invoked from a getter or a setter. --> A function used as getter or setter has its `this` bound to the object from which the property is being set or gotten.

    ```javascript
    function sum() {
        return this.a + this.b + this.c;
    }

    var o = {
        a: 1,
        b: 2,
        c: 3,
        get average() {
            return (this.a + this.b + this.c) / 3;
        }
    };

    Object.defineProperty(o, 'sum', {
        get: sum, enumerable: true, configurable: true});

    console.log(o.average, o.sum); // 2, 6
    ```

<!-- - When a function is used as a constructor (with the `new` keyword), its `this` is bound to the new object being constructed. While the default for a constructor is to return the object referenced by `this`, it can instead return some other object (if the return value isn't an object, then the `this` object is returned).

    ```javascript
    /*
    * Constructors work like this:
    *
    * function MyConstructor(){
    *   // Actual function body code goes here.  
    *   // Create properties on |this| as
    *   // desired by assigning to them.  E.g.,
    *   this.fum = "nom";
    *   // et cetera...
    *
    *   // If the function has a return statement that
    *   // returns an object, that object will be the
    *   // result of the |new| expression.  Otherwise,
    *   // the result of the expression is the object
    *   // currently bound to |this|
    *   // (i.e., the common case most usually seen).
    * }
    */

    function C() {
        this.a = 37;
    }

    var o = new C();
    console.log(o.a); // 37


    function C2() {
        this.a = 37;
        return {a: 38};
    }

    o = new C2();
    console.log(o.a); // 38
    ```
    
    - In the last example, because an object was returned during construction, the new object that `this` was bound to simply gets discarded. (This essentially makes the statement `this.a = 37;` dead code. It's not exactly dead, because it gets executed, but it can be eliminated with no outside effects.) -->

- Some JavaScript functions create instances not only when invoked as constructors, but also when invoked as functions. For example `RegExp`. But in most cases omitting the `new` will cause problems.

    ```javascript
    var reg1 = new RegExp("//w+");
    var reg2 = RegExp("//w+");
    reg1 instanceof RegExp;         // true
    reg2 instanceof RegExp;         // true
    reg1.source === reg2.source;    // true


    function Vehicle(type, wheelsCount) {
        this.type = type;
        this.wheelCount = wheelsCount;
        return this;
    }
    var car = Vehicle("car", 4);
    car === window;         // true
    car.wheelCount;         // 4


    function Vehicle(type, wheelCount) {
        if(!(this instanceof Vehicle)) {
            throw Error("Error: incorrect invocation.");
        }
        this.type = type;
        this.wheelCount = wheelCount;
        return this;
    }
    var brokenCar = Vehicle("car", 3);      // error thrown    
    var car = new Vehicle("car", 4);
    car instanceof Vehicle;                 // true
    ```

- ECMAScript 5 also formalizes an additional property on a function object: `caller`, which contains a reference to the function that called this function or `null` if the function was called from the global scope.

    ```javascript
    function outer() {
        inner();
    }
    function inner() {
            console.log(arguments.callee.caller);        
        //  console.log(inner.caller);
    }
    outer();
    ```

<!-- - A common trap with the function invocation is thinking that `this` is the same in an inner function as in the outer function. Correctly the context of the `inner` function depends only on invocation, but not on the outer function's context. If the inner function's immediate context is a containing function, `this` is `window` or *`undefined`*.

    ```javascript
    var numbers = {  
        numberA: 5,
        numberB: 10,
        sum: function() {
            console.log(this === numbers); // => true
            function calculate() {
                // this is window or undefined in strict mode
                console.log(this === numbers); // => false
                return this.numberA + this.numberB;
            }
            return calculate();
            // use .call() method to modify the context
            // return calculate.call(this);
        }
    };
    numbers.sum(); // => NaN or throws TypeError in strict mode 
    ```

- Method invocation and function invocation.

    ```javascript
    var obj = {};
    obj.myFunction = function() {
        return new Date().toString();
    }
    obj.myFunction();   // method invocation
    var oFunction = obj.myFunction;
    oFunction();        // function invocation
    ```

    - If the method is called without an object, then a function invocation happens: where `this` is the global object `window` or *`undefined`* in strict mode. Creating a bound function `var alone = myObj.myMethod.bind(myObj)` fixes the context, making it the object that owns the method.

- A method of an object will be separated from its object when passed as a parameter.

    ```javascript
    function Animal(type, legs) {
        this.type = type;
        this.leg = legs;
        this.logInfo = function() {
            console.log("The " + this.type + " has " + this.leg + " legs");
        };
    }
    var myCat = new Animal("cat", 4);
    // logs "The undefined has undefined legs"
    // or throws a TypeError in strict mode
    setTimeout(myCat.logInfo, 1000); 
    // setTimeout(myCat.logInfo.bind(myCat), 1000);  
    ``` -->

### [**`this` in closures**](#thcl)

> [MDN this](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this)

> [Gentle explanation of 'this' keyword in JavaScript](https://dmitripavlutin.com/gentle-explanation-of-this-in-javascript/)  

> [all this](https://web.archive.org/web/20170303233359/http://bjorn.tipling.com:80/all-this)

<a id="fpm"></a>

## [Function properties and methods](#fun)
- Each function has 2 properties: `length` and `prototype`. 
- The `length` property indicates the number of **named** arguments that the function expects.

    ```javascript
    function sum(num1, num2){
        return num1 + num2;
    }
    function sayHi(){
        console.log("hi");
    }
    sum.length;     // 2
    sayHi.length;   // 0
    ```

- The `prototype` is the **actual location of all instance methods** for reference types, meaning methods such as `toString()` and `valueOf()` actually exist on the `prototype` and are then accessed from the object instances. In ECMAScript 5, the `prototype` property is not enumerable and so will not be found using `for in`. 
### **`apply()`**, **`call()`**
<!-- - `apply()` and `call()` both ***call a function*** with a specific `this` value, effectively setting the value of the `this` object inside that function body. They are used to specify the executing scope for a function. With them, you can write a method once and then **inherit** it in another object, without having to rewrite the method for the new object (as if that method is also an instance property of the new object). -->
<!--     - The `apply()` method accepts 2 arguments: the value of `this` inside the function and an array of arguments. This second argument may be an instance of `Array`, the `arguments` object, or *`null`* or *`undefined`* if no arguments should be provided. The return value is the result of calling the function with the specified `this` value and arguments.

    - The `call()` method exhibits the same behavior as `apply()`, but arguments are passed to it individually. Using `call()` arguments must be **enumerated specifically**.  -->

<!--     ```javascript
    function sum(num1, num2){
        return num1 + num2;
    }
    function callSum1(num1, num2){
     // console.log(this.valueOf());  
     // console.log(this === window);  
        return sum.apply(this, arguments); // passing in arguments object of callSum1
    }
    function callSum2(num1, num2){
        return sum.apply(this, [num1, num2]); 
    }
    function callSum3(num1, num2){
        return sum.call(this, num1, num2);
    }

    callSum1(1, 2);     // 3
    callSum2(1, 2);     // 3
    callSum3(1, 2);     // 3
    ```

    - The `this` value is equal to `window` because it's being called in the global scope. -->
<!-- - With `call` and `apply`, if the value passed as `this` is not an object, an attempt will be made to convert it to an object using the internal `ToObject` operation (**boxed**). So if the value passed is a primitive like `7` or `"foo"`, it will be converted to an `Object` using the related constructor, so the primitive number `7` is converted to an object as if by `new Number(7)` and the string `"foo"` to an object as if by `new String("foo")`, e.g.

    ```javascript
    function bar() {
        console.log('this: ', this);
        console.log(Object.prototype.toString.call(this));
    }
    bar.call(7);     // Number {7}, [object Number]
    bar.call('foo'); // String {"foo"}, [Object String]
    ``` -->

<!-- - The decision to use either `apply()` or `call()` depends solely on the easiest way for you to pass arguments into the function. -->
<!-- - The true power of `apply()` and `call()` lies  in their ability to augment the `this` value inside of the function. The advantage of using `call()` or `apply()` to augment the scope is that the object doesn't need to know anything about the method.

    ```javascript
    window.color = "red";
    var o = { color: "blue" };
    function sayColor() {
        console.log(this.color);
    }
    sayColor();             // "red"
    sayColor.call(this);    // "red"
    sayColor.call(window);  // "red"
    sayColor.call(o);       // "blue"
    // as if `o` has its own `sayColor` method. same as `o.sayColor()`
    ```
 -->
- Using `apply()` or `call()` to chain constructors for an object.
    - Functions are simply **objects** that **execute code in a particular context**, the `apply()` and `call()` methods can be used to execute a constructor function on the newly created object.

    ```javascript
    Function.prototype.construct = function(aArgs) {
	// console.log('this inside the prototype: ', this);

        var oNew = Object.create(this.prototype);
        console.log('oNew before apply:', oNew);
        // MyConstructor {}

        /* 此处 this, 即 MyConstructor 作为一个函数，将运行时 this 绑定为 oNew */
        /* later ?! */
        this.apply(oNew, aArgs);
        // console.log('this after apply', this);

        console.log('oNew after apply:', oNew);
        // MyConstructor {property0: 4, property1: "Hello world!", property2: false}

        return oNew;
    };

    /*
    Function.prototype.construct = function (aArgs) {
    var fNewConstr = new Function("");
    fNewConstr.prototype = this.prototype;
    var oNew = new fNewConstr();
    this.apply(oNew, aArgs);
    return oNew;
    };
    */

    function MyConstructor() {
        for (var nProp = 0; nProp < arguments.length; nProp++) {
            this['property' + nProp] = arguments[nProp];
        }
    }

    var myArray = [4, 'Hello world!', false];
    /* MyConstructor 作为对象调用 construct 方法， this 自然指向 MyConstructor */
    var myInstance = MyConstructor.construct(myArray);
    myInstance;                             // {property0: 4, property1: "Hello world!", property2: false}
    myInstance.constructor;                 // MyConstructor(){...}
    myInstance instanceof MyConstructor;    // true

    /* 
    (Function.prototype.bind.apply(Date, [null].concat([2012, 11, 4])))();      // "Sun Nov 12 2017 20:45:10 GMT+0800 (China Standard Time)"   ? see Date


    function Product(name, price) {
        this.name = name;
        this.price = price;
    }

    function Food(name, price) {
        Product.call(this, name, price);
        this.category = 'food';
    }

    function Toy(name, price) {
        Product.call(this, name, price);
        this.category = 'toy';
    }

    var cheese = new Food('feta', 5);
    var fun = new Toy('robot', 40);
    */
    ```

### **`bind()`**
<!-- - Contrary to `apply()` and `call()` methods, which invokes the function right away, the `bind()` method only ***returns a new function*** that it supposed to be invoked later with a pre-configured `this`. -->
<!-- - ECMAScript 5 defines an additional method called `bind()`. The `bind()` method creates a new function instance whose `this` value is bound to the value that was passed into `bind()`. Its return value is a copy of the given function with the specified `this` value and initial arguments.  -->
<!-- - Bound functions are automatically suitable for use with the `new` operator to construct new instances created by the target function. When a bound function is used to construct a value, the provided `this` is ignored. However, provided arguments are still prepended to the constructor call. -->
<!-- - The simplest use of `bind()` is to make a function that, no matter how it is called, is called with a particular `this` value.

    ```javascript
    window.color = "red";
    var o = { color: "blue" };
    function sayColor() {
        console.log(this.color);
    }
    var objectSayColor = sayColor.bind(o);
    objectSayColor();       // "blue"
    ```

    - A new function called `objectSayColor()` is created from `sayColor()` by calling `bind()` and passing in the object `o`. The `objectSayColor()` function has a `this` value equivalent to `o`.

    ```javascript
    function f() {
        return this.a;
    }

    var g = f.bind({a: 'azerty'});
    console.log(g()); // azerty

    var h = g.bind({a: 'yoo'}); // bind only works once!
    console.log(h()); // azerty

    var o = {a: 37, f: f, g: g, h: h};
    console.log(o.f(), o.g(), o.h()); // 37, azerty, azerty
    ```

    - Calling `f.bind(someObject)` creates a new function with the same body and scope as `f`, `this`  in the new function is permanently bound to the first argument of `bind`, regardless of how the function is being used. -->
<!-- - The next simplest use of `bind()` is to make a function with **pre-specified initial arguments**. These arguments (if any) follow the provided `this` value and are then inserted at the start of the arguments passed to the **target function**, followed by the arguments passed to the **bound function**, whenever the bound function is called.

    ```javascript
    function list() {
        // it's equivalent to `arguments.slice();` if arguments has the method!
        // a typical way of converting the `arguments` to a real array
        return Array.prototype.slice.call(arguments);  
    }
    var list1 = list(1, 2, 3);
    var leadingThirtysevenList = list.bind(null, 37);
    var list2 = leadingThirtysevenList();
    // [37]
    var list3 = leadingThirtysevenList(1, 2, 3);
    // [37, 1, 2, 3]
    ``` -->

<!-- - With `setTimeout`

    ```javascript
    function LateBloomer() {
        this.petalCount = Math.floor(Math.random() * 12) + 1;
    }
    LateBloomer.prototype.bloom = function() {
        /* 仅设置将来某个时间执行 this.declare 指向的函数， this 并不是函数的调用者。 
        this.declare() 这种写法 this 才是调用者 */
        window.setTimeout(this.declare, 1000);
        window.setTimeout(this.declare.bind(this), 1000);
    };
    LateBloomer.prototype.declare = function() {
        console.log("I'm a beautiful flower with " + this.petalCount + " petals!");
    };
    var flower = new LateBloomer();
    flower.bloom();
    ``` -->

<!-- - Bound functions used as constructors

    ```javascript
    function Point(x, y) {
        this.x = x;
        this.y = y;
    }
    Point.prototype.toString = function() {
        return this.x + "," + this.y;
    };
    var p = new Point(1, 2);
    p.toString();       // "1,2"

    var YAxisPoint = Point.bind(null, 0/*x*/);
    var emptyObj = {};
    // bound functions used as constructors
    var axisPoint = new YAxisPoint(5);
    axisPoint.toString();                       // "0,5"
    axisPoint instanceof Point;                 // true
    axisPoint instanceof YAxisPoint;            // true
    new Point(3, 4) instanceof YAxisPoint;      // true
    ``` -->

<!-- - Creating shortcuts

    ```javascript
    var slice = Array.prototype.slice;
    function listA() {
        return slice.apply(arguments);
    }
    var list1 = listA(1, 2, 3);
    list;                           // [1, 2, 3]

    var unboundSlice = Array.prototype.slice;
    var slice = Function.prototype.apply.bind(unboundSlice);
    function listB() {
        return slice(arguments);
    }
    var list2 = listB(1, 2, 3);
    list2;
    ```

    - `slice` is a bound function to the `apply()` function of `Function.prototype`, with the `this` value set to the `slice()` function of `Array.prototype`.  -->

### Other methods
- For functions, the inherited methods `toLocaleString()` and `toString()` always return the function's code. The exact format of this code varies from browser to browser, so you can't rely on what is returned for any important functionality, though this information may be useful for debugging purposes. The inherited method `valueOf()` simply returns the function itself.
### The constructor property
- The `constructor` property returns the constructor function for all JavaScript variables. It was originally intended for use in identifying the object type. However, the `instanceof` operator is considered to be a safer way of determining type.

    ```javascript
    "John".constructor                // Returns function String()  {[native code]}
    (3.14).constructor                // Returns function Number()  {[native code]}
    false.constructor                 // Returns function Boolean() {[native code]}
    [1,2,3,4].constructor             // Returns function Array()   {[native code]}
    {name:'John',age:34}.constructor  // Returns function Object()  {[native code]}
    new Date().constructor            // Returns function Date()    {[native code]}
    function () {}.constructor        // Returns function Function(){[native code]}


    // check a Date object
    function isDate(myDate) {
        return myDate.constructor.toString().indexOf("Date") > -1;
    // return myDate.constructor === Date;
    }
    ```

<a id="advf"></a>

## [Advanced functions](#)

<a id="std"></a>

### [Safe type detection](#fun)
- It' difficult to definitively determine if a value is a function.
    - The `typeof` operator has several quirks that can make it unreliable in detecting certain types of data. Safari (through version 4) returns "function" when typeof is applied to a regular expression.
    - The `instanceof` operator is also problematic in that it's difficult to use when multiple global scopes are present, such as when there are multiple frames.

        ```javascript
        var isArray = value instanceof Array;
        ```
        
        - This code returns true only if `value` is an array and was created in the same global scope as the `Array` constructor. (Remember, `Array` is a property of `window`.) If `value` is an array from another frame, this code returns `false`.
    - Another problem with type detection comes when trying to determine if an object is a native implementation or a developer-defined one. This problem came to the forefront as browsers began to natively implement the `JSON` object. Since many were already using Douglas Crockford's `JSON` library, which defined a global `JSON` object, developers struggled to determine which object was present on the page.
- The solution to all of these problems is the same. The native `toString()` method of `Object` can be called with any value to return a string in the format "[object NativeConstructorName]". Each object has an internal `[[Class]]` property that specifies the constructor name that is returned as part of this string.
- Since the native constructor name for a certain type is the same regardless of the global context in which it was created, using `toString()` returns a consistent value.

    ```javascript
    function isArray(value) {
        return Object.prototype.toString.call(value) === "[object Array]";
    }    

    function isFunction(value) {
        return Object.prototype.toString.call(value) === "[object function]";
    }   

    function isRegExp(value) {
        return Object.prototype.toString.call(value) === "[object RegExp]";
    }
    ```

    - `isFunction()` will return false in Internet Explorer for any functions that are implemented as COM objects rather than native JavaScript functions.
- This technique is also largely in use for identifying the native JSON object. The `toString()` method of `Object` can't determine constructor names for nonnative constructors, so any objects that are instances of developer-defined constructors return `"[object Object]"`. Several JavaScript libraries contain code similar to the following:

    ```javascript
    var isNativeJSON = window.JSON && Object.prototype.toString.call(JSON) == "[object JSON]";
    ```

- It's possible to assign `Object.prototype.toString()` to a different value. The technique assumes that `Object.prototype.toString()` is the native version and has not been overwritten by a developer.

<a id="ssc"></a>

### [Scope-safe constructors](#fun)
- A constructor is simply a function that is called using the `new` operator. When used in this way, the `this` object used inside the constructor points to the newly created object instance. The problem occurs when the constructor is called without the `new` operator. Since the `this` object is bound at runtime, calling `Person()` directly maps this to the global object (`window`), resulting in accidental augmentation of the wrong object.

    ```javascript
    function Person(name, age, job) {
        this.name = name;
        this.age = age;
        this.job = job;
    };
    var p = Person("Nick", 29, "Software Engineer");
    window.job;             // "Software Engineer"
    ```

    - Here the constructor was called as a regular function, omitting the `new` operator.
    - This issue occurs as a result of `late binding` of the `this` object.
- Scope-safe constructors first check to ensure that the `this` object is an instance of the correct type before applying any changes. If not, then a new instance is created and returned.

    ```javascript
    function Person(name, age, job) {
        if (this instanceof Person) {
            this.name = name;
            this.age = age;
            this.job = job;
        } else {
            return new Person(name, age, job);
        }
    }
    var p = Person("Nick", 29, "Software Engineer");
    window.name;                // ""
    p.name;                     // "Nick"          
    ```
- By implementing this pattern, you are locking down the context in which the constructor can be called. If you're using the constructor-stealing pattern of inheritance without also using prototype chaining, your inheritance may break.

    ```javascript
    function Polygon(sides) {
        if (this instanceof Polygon) {
            this.sides = sides;
            this.getArea = function() {
                return 0;
            };
        } else {
            return new Polygon(sides);
        }
    }
    function Rectangle(width, height) {
        Polygon.call(this, 2);
        this.width = width;
        this.height = height;
        this.getArea = function() {
            return this.width * this.height;
        };
    }
    var rect = new Rectangle(5, 10);
    rect.sides;         // "undefined"
    rect.height;        // 10
    ```

    - The `Polygon` constructor is scope-safe, whereas the `Rectangle` constructor is not. When a new instance of `Rectangle` is created, it should inherit the sides property from `Polygon` through the use of `Polygon.call()`.
    - Since the `Polygon` constructor is scope-safe, the `this` object is not an instance of `Polygon`, so a new `Polygon` object is created and returned. 
    - The `this` object in the `Rectangle` constructor is not augmented, and the value returned from `Polygon.call()` is not used, so there is no `sides` property on the `Rectangle` instance.
- This issue resolves itself if prototype chaining or parasitic combination is used with constructor.

    ```javascript
    function Polygon(sides) {
        if (this instanceof Polygon) {
            this.sides = sides;
            this.getArea = function() {
                return 0;
            };
        } else {
            return new Polygon(sides);
        }
    }
    function Rectangle(width, height) {
        Polygon.call(this, 2);
        this.width = width;
        this.height = height;
        this.getArea = function() {
            return this.width * this.height;
        };
    }
    Rectangle.prototype = new Polygon();
    var rect = new Rectangle(5, 10);
    rect.sides;         // 2
    ```

    - In this version, an instance of `Rectangle` is also an instance of `Polygon` `Polygon.call()` works, ultimately adding a `sides` property to the `Rectangle` instance.

- Scope-safe constructors are helpful in environments where multiple developers are writing JavaScript code to run on the same page. In that context, accidental changes to the global object may result in errors that are often difficult to track down. Scope-safe constructors are recommended as a best practice unless you're implementing inheritance based solely on constructor stealing.

<a id="llf"></a>

### [Lazy loading functions](#fun)
- Because of differences in browser behavior, most JavaScript code contains a significant amount of `if` statements that fork execution toward code that should succeed.

    ```javascript
    function createXHR() {
        if (typeof XMLHTTPRequest != "undefined") {
                return new XMLHttpRequest();
        } else if (typeof ActiveXObject != "undefined") {
            if (typeof arguments.callee.activeXString != "string") {
                var versions = ["MSXML2.XMLHttp.6.0", "MSXML2.XMLHttp.3.0", "MSXML2.XMLHttp"],
                    i, len;

                for (i = 0, len = versions.length; i < len; i++) {
                    try {
                        new ActiveXObject(versions[i]);
                        arguments.callee.activeXString = version[i];
                        break;
                    } catch (ex) {
                        //skip
                    }
                }
                
            }
            return new ActiveXObject(arguments.callee.activeXString);
        } else {
            throw new Error("No XHR object available.");
        }
    }
    ```

    - Every time `createXHR()` is called, it goes through and checks which capability is supported for the browser. First it checks for native XHR, then it tests for ActiveX-based XHR, and finally it throws an error if neither is found. This happens each and every time the function is called, even though the result of this branching won't change from call to call: if the browser supports native XHR, it supports native XHR always, so the test becomes unnecessary.
- The solution is a technique called laze loading. Lazy loading means that the branching of function execution happens only once. There are two ways to accomplish lazy loading.
    1. The first is by manipulating the function the first time it is called. During that first call, the function is **overwritten** with another function that executes in the appropriate way such that any future calls to the function needn't go through the execution branch.

        ```javascript
        function createXHR() {
            if (typeof XMLHTTPRequest != "undefined") {
                createXHR = function() {                // overwrite
                    return new XMLHttpRequest();
                };
            } else if (typeof ActiveXObject != "undefined") {
                createXHR = function() {                // overwrite
                    if (typeof arguments.callee.activeXString != "string") {
                        var versions = ["MSXML2.XMLHttp.6.0", "MSXML2.XMLHttp.3.0", "MSXML2.XMLHttp"],
                            i, len;
                        for (i = 0, len = versions.length; i < len; i++) {
                            try {
                                new ActiveXObject(versions[i]);
                                arguments.callee.activeXString = version[i];
                                break;
                            } catch (ex) {
                                //skip
                            }
                        }
                        
                    }
                    return new ActiveXObject(arguments.callee.activeXString);
                };
            } else {
                createXHR = function() {                // overwrite
                    throw new Error("No XHR object available.");
                };
            }
            return createXHR();
        }
        ```

        - In the lazy loading version of `createXHR()`, each branch of the `if` statement assigns a different function to the `createXHR` variable, effectively overwriting the original function. The last step is then to call the newly assigned function. The next time `createXHR()` is called, it will call the assigned function directly so the `if` statements won't be reevaluated.
    1. The second lazy loading pattern is to assign the appropriate function immediately when the function is declared. So instead of taking a slight performance hit when the function is **called** for the first time, there's a slight performance hit when the code is **loaded** for the first time.

        ```javascript
        var createXHR = (function () {
            if (typeof XMLHTTPRequest != "undefined") {
                return function() {               
                    return new XMLHttpRequest();
                };
            } else if (typeof ActiveXObject != "undefined") {
                return function() {                
                    if (typeof arguments.callee.activeXString != "string") {
                        var versions = ["MSXML2.XMLHttp.6.0", "MSXML2.XMLHttp.3.0", "MSXML2.XMLHttp"],
                            i, len;
                        for (i = 0, len = versions.length; i < len; i++) {
                            try {
                                new ActiveXObject(versions[i]);
                                arguments.callee.activeXString = version[i];
                                break;
                            } catch (ex) {
                                //skip
                            }
                        }
                        
                    }
                    return new ActiveXObject(arguments.callee.activeXString);
                };
            } else {
                return function() {               
                    throw new Error("No XHR object available.");
                };
            }
        })();
        ```

        - The approach used is to create an anonymous, self-executing function that determines which of the different function implementations should be used. Each branch now returns the correct function definition so that it gets assigned to `createXHR()` immediately.
- Lazy loading functions have an advantage in that you pay a performance penalty just once for forking the code.

<a id="fbd"></a>

### [Function binding](#fun)
- Function binding involves creating a function that calls another function with a specific `this` value and with specific arguments. This technique is often used in conjunction with callbacks and event handlers to **preserve code execution context while passing functions around as variables**.

    ```javascript
    var handler = {
        message: "Event handled",
        handleClick: function(event) {
            alert(this.message);
        }
    };
    var btn = document.getElementById("my-btn");
    EventUtil.addHandler(btn, "click", handler.handleClick);
    ```

    - The `handler.handleClick()` method is assigned as an event handler to a DOM button. When the button is clicked, the function is called, and an alert is displayed. Even though it may seem as if the alert should display "Event handled", it actually displays "undefined".
    - The problem is that the context of `handler.handleClick()` is not being saved, so the `this` object ends up pointing to the **DOM button** instead of handler in most browsers. (In Internet Explorer through version 8, `this` points to `window`.)
- Using closure can fix this.

    ```javascript
    var handler = {
        message: "Event handled",
        handleClick: function(event) {
            alert(this.message);
        }
    };
    var btn = document.getElementById("my-btn");
    EventUtil.addHandler(btn, "click", function(event) {
        handler.handleClick(event);
    });         // event handler ???
    ```

    - This solution uses a closure to call `handler.handleClick()` directly inside the `onclick` event handler.
    - Creating multiple closures can lead to code that is difficult to understand and debug.
- Many JavaScript libraries have implemented a function that can bind a function to a specific context. Typically, this function is called `bind()`. 
- A simple `bind()` function takes a function and a context, returning a function that calls the given function in the given context with all arguments intact.

    ```javascript
    function bind(fn, context) {
        return function() {
            return fn.apply(context, arguments);        
        };
    }
    ```

    - A closure is created within `bind()` that calls the passed-in function by using `apply()` and passing in the `context` object and the arguments. The `arguments` object, as used here, is for the inner function, not for `bind()`. When the returned function is called, it executes the passed-in function in the given context and passes along all arguments.
- The `bind()` function is used as follows:

    ```javascript
    var handler = {
        message: "Event handled",
        handleClick: function(event) {
            alert(this.message);
        }
    };
    var btn = document.getElementById("my-btn");
    EventUtil.addHandler(btn, "click", bind(handler.handleClick, handler));
    ```

    - In this code, the `bind()` function is used to create a function that can be passed into `EventUtil.addHandler()`, maintaining the context. The `event` object is also passed through to the function.

        ```javascript
        var handler = {
            message: "Event handled",
            handleClick: function(event) {
                alert(this.message + ":" + event.type);
            }
        }
        var btn = document.getElementById("my-btn");
        EventUtil.addHandler(btn, "click", bind(handler.handleClick, handler));
        ```

        - The `handler.handleClick()` method gets passed the `event` object as usual, since all arguments are passed through the bound function directly to it.
- ECMAScript 5 introduced a native `bind()` method on all functions to make this process even easier.

    ```javascript
    var handler = {
        message: "Event handled",
        handleClick: function(event) {
            alert(this.message);
        }
    };
    var btn = document.getElementById("my-btn");
    EventUtil.addHandler(btn, "click", handler.handleClick.bind(handler));;
    ```

- Bound functions are useful whenever a function pointer must be passed as a value and that function needs to be executed in a particular context. They are most commonly used for event handlers and with `setTimeout()` and `setInterval()`. But they require more memory and are slightly slower than regular functions because of multiple function calls.

<a id="fcur"></a>

### [Function currying](#fun)
- Function currying creates functions that have one or more arguments already set (also called partial function application). The basic approach is the same as function binding: use a closure to return a new function. The difference with currying is that this new function also sets some arguments to be passed in when the function is called.

    ```javascript
    function add(num1, num2) {
        return num1 + num2;
    }
    function curriedAdd(num2) {
        return add(5, num2);
    }
    add(2, 3);
    curriedAdd(3);
    ```

    - `curriedAdd()` here is not technically a curried function, but it demonstrates the concept well.
- Curried functions are typically created dynamically by calling another function and passing in the function to curry and the arguments to supply.

    ```javascript
    function curry(fn) {
        var args = Array.prototype.slice.call(arguments, 1);
        return function() {
            var innerArgs = Array.prototype.slice.call(arguments),
                finalArgs = args.concat(innerArgs);
            return fn.apply(null, finalArgs);
        };
    }
    ```

    - The `curry()` function's primary job is to arrange the arguments of the returned function in the appropriate order. The first argument to `curry()` is the function that should be curried; all other arguments are the values to pass in.
    - In order to get all arguments after the first one, the `slice()` method is called on the arguments object, and an argument of `1` is passed in, indicating that the returned array's first item should be the second argument. The `args` array then contains arguments from the outer function.
    - The `innerArgs` array is created to contain all of the arguments that were passed in (once again using `slice()`). With the arguments from the outer function and inner function now stored in arrays, you can use the `concat()` method to combine them into `finalArgs` and then pass the result into the function, using `apply()`. This function doesn't take context into account, so the call to `apply()` passes in `null` as the first argument.

        ```javascript
        function add(num1, num2) {
            return num1 + num2;
        }
        var curriedAdd = curry(add, 5);
        curriedAdd(3);              // 8
        ```

        - A curried version of `add()` is created that has the first argument bound to 5. When `curriedAdd()` is called and 3 is passed in, the 3 becomes the second argument of `add()`, while the first is still 5, resulting in the sum of 8. 
        - Both arguments can be provided at the same time.

            ```javascript
            function add(num1, num2) {
                return num1 + num2;
            }
            var curriedAdd = curry(add, 5, 12);
            curriedAdd();               // 17
            ```

- Function currying is often included as part of function binding, creating a more complex `bind()` function. 

    ```javascript
    function bind(fn ,context) {
        var args = Array.prototype.slice.call(arguments, 2);
        return function() {
            var innerArgs = Array.prototype.slice.call(arguments),
                finalArgs = args.concat(innerArgs);
            return fn.apply(context, finalArgs);
        };
    }
    ```

    - Whereas `curry()` simply accepts a function to wrap, `bind()` accepts the function and a `context` object. That means the arguments for the bound function start at the third argument instead of the second, which changes the first call to `slice()`.
    - The only other change is to pass in the `context` object to `apply()`. When `bind()` is used, it returns a function that is bound to the given context and may have some number of its arguments set already. This can be useful when you want to pass arguments into an event handler in addition to the `event` object.

        ```javascript
        var handler = {
            message: "Event handled",
            handleClick: function(name, event) {
                alert(this.message + ":" + name + ":" + event.type);
            }
        };
        var btn = document.getElementById("my-btn");
        EventUtil.addHandler(btn, "click", bind(handler.handleClick, handler, "my-btn"));
        ```

        - The `handler.handleClick()` method accepts two arguments: the name of the element that you're working with and the `event` object. The name is passed into the `bind()` function as the third argument and then gets passed through to `handler.handleClick()`, which also receives the `event` object.
- The ECMAScript 5 `bind()` method also implements function currying. Just pass in the additional arguments after the value for `this`.

    ```javascript
    var handler = {
        message: "Event handled",
        handleClick: function(name, event) {
            alert(this.message + ":" + name + ":" + event.type);
        }
    };
    var btn = document.getElementById("my-btn");
    EventUtil.addHandler(btn, "click", handler.handleClick.bind(handler, "my-btn"));
    ```

- The use of either `bind()` or `curry()` is determined by the requirement of a context object or the lack of one, respectively.

<a id="bom"></a>

# [The Browser Object Model](#fun)

<a id="err"></a>

# [Errors](#fcl)
- `try-catch` statement: `try`, `catch`, `finally`. Between `catch` and `finally`, only one or the other is required.
- The `try` statement executes a block and catches any exceptions that were thrown by the block. Any code that might possibly throw an error should be placed in the `try` portion of the statement, and the code to handle the error is placed in the `catch` portion.
    - `EvalError`: an error in the `eval()` function (newer versions of JavaScript does not throw any `EvalError` and use `SyntaxError` instead)
    - `SyntaxError`: evaluate code with a syntax error
    - `RangeError`: use a number that is outside the range of legal values
    - `ReferenceError`: use (reference) a variable that has not been declared.
    - `TypeError`: use a value that is outside the range of expected types.
    - `URIError`: use illegal characters in a URI function
- The `throw` statement raises an exception. If the `throw` statement is in a `try` block, then control goes to the `catch` clause. Otherwise, the function invocation is abandoned, and control goes to the `catch` clause of the `try` in the calling function.
- The `catch` **clause** of the statement defines a new variable to receive an object containing information about the error that occurred. The error object's name needs to be defined. The error object contains at least a message property that holds the error message. ECMA-262 also specifies a name property that defines the type of error. Other properties can also be added.
- A `try` statement has a single `catch` statement will catch all exceptions. If your handling depends on the type of the exception, then the exception handler will have to inspect the name to determine the type of the exception.

    ```javascript
    try {
        myroutine(); // may throw three types of exceptions
    } catch (e) {
        if (e instanceof TypeError) {
            // statements to handle TypeError exceptions
        } else if (e instanceof RangeError) {
            // statements to handle RangeError exceptions
        } else if (e instanceof EvalError) {
            // statements to handle EvalError exceptions
        } else {
        // statements to handle any unspecified exceptions
        logMyErrors(e); // pass exception object to error handler
        }
    }
    ```

- The optional `finally` clause of the `try-catch` statement always runs its code no matter what. If the `finally` block returns a value, this value becomes the return value of the entire `try-catch-finally` production, overriding any return and throw statements in the `try` and `catch` blocks.

    ```javascript
    (function() {
    try {
        try {
        throw new Error('oops');
        }
        catch (ex) {
        console.error('inner', ex.message);
        throw ex;     // this throw is short-circuit
        }
        finally {
        console.log('finally');
        return;
        }
    }
    catch (ex) {
        console.error('outer', ex.message);
    }
    })();

    // Output:
    // "inner" "oops"
    // "finally"
    ```

<a id="dbg"></a>

# [Debugging](#fcl)
- The debugger keyword stops the execution of JavaScript, and calls (if available) the debugging function. It has the same function as setting a breakpoint in the debugger. If no debugging is available, the debugger statement has no effect.

    ```javascript
    var x = 15 * 5;
    debugger;
    ...
    ```

<a id="strm"></a>

# [Strict mode](#fcl)
- It's new in JavaScript 1.8.5 (ECMAScript version 5). It is not a statement, but a literal expression, ignored by earlier versions of JavaScript. 
- The "use strict" directive is only recognized at the beginning of a script or a function.
    - Declared at the beginning of a script, it has global scope (all code in the script will execute in strict mode).
    - Declared inside a function, it has local scope (only the code inside the function is in strict mode).


<a id="bp"></a>

# [Best Practices](#fcl) 
- Placing scripts at the bottom of the element improves the display speed, because script compilation slows down the display.
- A good practice is to put spaces around operators ( `=` `+` `-` `*` `/` )
- Avoid code lines longer than 80 characters for best readability.

    ```javascript
    // after an operator
    document.getElementById("demo").innerHTML =
    "Hello Dolly!";

    document.getElementById("demo").innerHTML = "Hello \
    Dolly!";

    document.getElementById("demo").innerHTML = "Hello" + 
    "Dolly!";
    ```