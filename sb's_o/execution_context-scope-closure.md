# Execution context
- *Lexical scope*: the region of the code where you can refer to a variable by name without getting access errors. 
    - It can be understood without running the code.
    - A new lexical scope is created every time you type out a function definition.
        - A function definition spans from the letter f of function to the end curly brace of the function.
        - The two curly braces around the function's body enclosed the area of the code where different access rules will apply.
    - A lexical scope is just characters of code defined in a file somewhere. That's not a value that can be stored in a variable.
- When a program runs, it builds up internal data storage systems for keeping track of all the variables that are available to different function objects. These in-memory scope structures are called *execution contexts*.
    - An execution context is not something that can have a reference to. It cannot be stored in a variable.
    - Although execution contexts are also key-value data storage constructs, interacting with them are totally different from with objects.
    - Execution contexts or in-memory scopes differ from lexical scopes in that they are built as the code runs, not as it's typed.
- There are only **two** primary types of **execution contexts** (referred to as **context** for simplicity), **global** and **function**.
    - The third exists inside of a call to `eval()`.
- Before the first line of code runs, the interpreter will start out by setting out an execution context environment. The first step will be to create an in-memory global scope context to hold all of the global variables.
- When a function is **defined**, its scope chain is created, preloaded with the global variable object, and saved to the internal `[[Scope]]` property.
    - When the interpreter meets a function expression, it just adds a new key-value pair to the current execution context and the function definition code is ignored for now. They will only get run when the function is actually called.
- Each execution context has an associated **variable object** upon which all of its defined variables and functions exist.
    - This object is **not accessible** by code but is used behind the scenes to handle data.  
    - The global context's variable object always exists, whereas local context variable objects, exist only while the function is **being executed**.
- A new execution context is created every a function is run. Each **function call** has its own execution context.
    - The new context will become the interpreter's new current context, for as long as that function is running.
    - The context for a function will always be created as a child of the context that it was defined within. A new context always gets created in the same context as its function was defined within.
- When code is executed in an execution context, a **scope chain** of  **variable objects** is created to provide **ordered access** to all variables and functions that an execution context has access to. 
    - **The front** of the scope chain is always the variable object of the context whose code is executing. If the context is a **function**, then the *activation object* is used as the variable object. 
        - An activation object starts with a single defined variable called **`arguments`**. (This doesn't exist for the global context.) 
    - The next variable object in the chain is from the containing context, and the next after that is from the next containing context. 
    - This pattern continues until the global context is reached; the global context's variable object is always **the last** of the scope chain.
- When a function is **called**, an execution context is created, and its scope chain is built up by copying the objects in the function's `[[Scope]]` property. After that, the **activation object** (acting as a variable object) for the function is initialized with values for `arguments` and any named arguments and pushed to the front of the context's scope chain.
- Once the function has completed, the local activation object is destroyed, leaving only the global scope in memory. (Closures behave differently.)
- When a variable is declared using `var`, it is automatically added to the most immediate context available. In a function, the most immediate one is the function's local context; in a `with` statement, the most immediate is the function context. 
    - If a variable is initialized without first being declared using `var`, it gets added to the global context automatically.
# Closure
- A function **defined** inside another function adds the containing function's **activation object** into its scope chain, which means the inside function's scope chain has an **reference** to the containing function's whole activation object. So a function has access to all the variables from all the scopes that surrounds it. 
- A ***closure*** is any function that remains available after the outer scopes have returned. 
    - It's often accomplished by creating a function inside a function.
- When an inner anonymous function (which **hasn't finish executing**) is returned from its containing function, its scope chain contains the activation object from the containing function. After the containing function finishes executing, the **scope chain** for its executing context **is destroyed**, but the activation object of the containing function cannot not be destroyed because a **reference** to the activation object still exists in the returned inner function's scope chain. It will remain in memory until the anonymous function is destroyed.
    - Setting the variable that holds the containing function to `null` dereferences it and allows the garbage collection routine to clean it up.
- Two unsuccessful try.

    ```javascript
    // createFunction() returns an array of function
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
        console.log(item());// all 10
    });  


    function createFunction() {
        var result = new Array();
        for (var i = 0; i < 10; i++) {
            result[i] = function() {
                return function(num) {
                    return num;
                }(i);       // this won't execute right away, because its containing function is not self-executing immediately
            };
        }
        return result;  
    }

    var a = createFunction();
    a.forEach(function(item) {
        console.log(item());// all 10
    });                     
    ```

    - Closure stores a reference to the entire variable object, not just to a particular variable. 
    - Each function in the returned array has the `createFunctions()` activation object in its scope chain, referring to the same variable `i` of the same variable object. (Because the `createFunction()` is called only once, it only has one execution context.)
    - By the time `createFunction()` finishes executing, `i` is 10.
-  Maintain the value of certain variable by taking advantage the nested function's reference to its containing function. As long as that reference still exists, the containing function's variable object cannot be destroyed and access to it preserves.

    ```javascript
    function createFunction() {
        var result = [];
        for (var i = 0; i < 10; i++) {
            result.push(function(num) {
                return function() {
                    return num;
                }
            }(i));
        }
        return result;
    }
    var a = createFunction();
    a.forEach(function(item) {
        console.log(item());// 0 - 9, works
    }); 
    ```

    - Pass the variable whose value needs to be preserved to the containing function and make it immediately self-executing.

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

    - Each function automatically gets two special variables as soon as the function is called: `this` and `arguments`, to which the function's inner function can never have access. 
    - Save the value in another variable for inner function to manipulate it later.
- Since closures carry with them the containing function's scope, they take up more memory than other functions. Overuse of closures can lead to **excess memory consumption**, so it's recommended to use them only when absolutely necessary.

- Any time you see a function, with an input parameter that's quite static, meaning you don't expect the parameter to take on a new value every time you call the function, that's a opportunity to re-factor your code, such that you store the value in a variable form an outer scope. Because the way closures work, the inner function will always have access to the outer scope variable even after the outer function returns.
- Approaches of retaining access to an inner function after the its containing function has returned: 
    - passing the inner function to a `setIimeout()`
    - returning the inner function from the containing function
    - saving the inner function to a global variable 
## Mimicking block scope
## Private variables