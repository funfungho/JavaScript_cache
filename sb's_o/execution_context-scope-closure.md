- 词法作用域即静态分析代码时各变量的作用域。
- 解释器开始解析代码时，首先创建一个全局上下文来存放全局变量。解释器遇到函数表达式时，暂时忽略函数的定义，仅加入一个键-值对到当前的执行上下文中。
<!-- - *Lexical scope*: the region of the code where you can refer to a variable by name without getting access errors. 
    - It can be understood without running the code.
    - A new lexical scope is created every time you type out a function definition.
        - A function definition spans from the letter f of function to the end curly brace of the function.
        - The two curly braces around the function's body enclosed the area of the code where different access rules will apply.
    - A lexical scope is just characters of code defined in a file somewhere. That's not a value that can be stored in a variable. -->
- 程序运行时，产生不同的执行上下文，负责管理不同函数的变量作用域。
    - 执行上下文是不同于对象的键-值存储结构。
    - 主要分全局上下文和函数上下文。
<!-- - When a program runs, it builds up internal data storage systems for keeping track of all the variables that are available to different function objects. These in-memory scope structures are called *execution contexts*.
    - An execution context is not something that can have a reference to. It cannot be stored in a variable.
    - Although execution contexts are also key-value data storage constructs, interacting with them are totally different from with objects. -->
<!--     - Execution contexts or in-memory scopes differ from lexical scopes in that they are built as the code runs, not as it's typed. -->
<!-- - There are only **two** primary types of **execution contexts** (referred to as **context** for simplicity), **global** and **function**.
    - The third exists inside of a call to `eval()`. -->
<!-- - Before the first line of code runs, the interpreter will start out by setting out an execution context environment. The first step will be to create an in-memory global scope context to hold all of the global variables. -->
- 每个执行上下文都有一个与之关联的 ***variable object***, 它所有定义的变量和函数都存在于该对象中。
- 定义函数时，函数的作用域链同时被创建并预载入了全局的 variable object. 作用域链保存在 `[[Scope]]` 属性中。
<!-- - When a function is **defined**, its scope chain is created, preloaded with the global variable object, and saved to the internal `[[Scope]]` property.
    - When the interpreter meets a function expression, it just adds a new key-value pair to the current execution context and the function definition code is ignored for now. They will only get run when the function is actually called. -->
<!-- - Each execution context has an associated **variable object** upon which all of its defined variables and functions exist.
    - This object is **not accessible** by code but is used behind the scenes to handle data.  
    - The global context's variable object always exists, whereas local context variable objects, exist only while the function is **being executed**. -->
<!-- - A new execution context is created every a function is run. Each **function call** has its own execution context.
    - The new context will become the interpreter's new current context, for as long as that function is running.
    - The context for a function will always be created as a child of the context that it was defined within. A new context always gets created in the same context as its function was defined within. -->
- 某个执行上下文中的代码被执行时，会创建一条 variable objects 的作用域链，函数通过该作用域链来确定具有访问权限的变量。
    - 查询过程从自身的 variable object 开始，逐层向外向向它的 containing context 的 variable object 查询，直至全局上下文。
- 函数的每次执行时都会创建一个执行上下文。作用域链通过复制存放在 `[[Scope]]` 属性里的 variable objects 来创建。每个函数都有自己的执行上下文。
<!-- - When code is executed in an execution context, a **scope chain** of  **variable objects** is created to provide **ordered access** to all variables and functions that an execution context has access to. 
    - **The front** of the scope chain is always the variable object of the context whose code is executing. If the context is a **function**, then the *activation object* is used as the variable object. 
        - An activation object starts with a single defined variable called **`arguments`**. (This doesn't exist for the global context.) 
    - The next variable object in the chain is from the containing context, and the next after that is from the next containing context. 
    - This pattern continues until the global context is reached; the global context's variable object is always **the last** of the scope chain. -->
<!-- - When a function is **called**, an execution context is created, and its scope chain is built up by copying the objects in the function's `[[Scope]]` property. After that, the **activation object** (acting as a variable object) for the function is initialized with values for `arguments` and any named arguments and pushed to the front of the context's scope chain. -->
<!-- - Once the function has completed, the local activation object is destroyed, leaving only the global scope in memory. (Closures behave differently.) -->
<!-- - When a variable is declared using `var`, it is automatically added to the most immediate context available. In a function, the most immediate one is the function's local context; in a `with` statement, the most immediate is the function context. 
    - If a variable is initialized without first being declared using `var`, it gets added to the global context automatically. -->
# Closure
<!-- - A function **defined** inside another function adds the containing function's **activation object** into its scope chain, which means the inside function's scope chain has an **reference** to the containing function's whole activation object. So a function has access to all the variables from all the scopes that surrounds it.  -->
<!-- - A ***closure*** is any function that remains available after the outer scopes have returned. 
    - It's often accomplished by creating a function inside a function. -->
- 闭包指函数结束调用后仍能访问到它的 variable object 的现象。原因是该函数的 variable object 中的变量仍在其他地方被引用，导致垃圾回收机制无法销毁它。
    - 手动设置为 `null` 可以解绑引用。
<!-- - When an inner anonymous function (which **hasn't finish executing**) is returned from its containing function, its scope chain contains the activation object from the containing function. After the containing function finishes executing, the **scope chain** for its executing context **is destroyed**, but the activation object of the containing function cannot not be destroyed because a **reference** to the activation object still exists in the returned inner function's scope chain. It will remain in memory until the anonymous function is destroyed.
    - Setting the variable that holds the containing function to `null` dereferences it and allows the garbage collection routine to clean it up. -->
- 闭包错误示范

    ```javascript
    // createFunction() returns an array of functions
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
                }(i);       
                // this won't execute right away, because its containing function (result[i]) is not self-executing immediately
            };
        }
        return result;  
    }

    var a = createFunction();
    a.forEach(function(item) {
        console.log(item());// all 10
    });                     
    ```

    - `createFunctions()` 函数只被调用一次，所以只有一个 variable object, 返回的数组里的函数都引用同一个 variable object.
<!--     - Closure stores a reference to the entire variable object, not just to a particular variable. 
    - Each function in the returned array has the `createFunctions()` activation object in its scope chain, referring to the same variable `i` of the same variable object. (Because the `createFunction()` is called only once, it only has one execution context.)
    - By the time `createFunction()` finishes executing, `i` is 10. -->
<!-- -  Maintain the value of certain variable by taking advantage the nested function's reference to its containing function. As long as that reference still exists, the containing function's variable object cannot be destroyed and access to it preserves. -->
- 正确姿势

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

    - 非闭包。将需要用到实时值的变量作为参数传入外层函数中并立即调用，内层函数得到实时值的副本，实现实时值的保存。
   <!--  - Pass the variable whose value needs to be preserved to the containing function and make it immediately self-executing. -->

    ```javascript
    var name = "The Window";
    var obj = {
        name: "My Object",
        getNameFunc: function() {
            // obj 对象调用此函数
            var that = this;        
            return function() {
                return that.name;
            };
        }
    };
    obj.getNameFunc()();             // "My Object"
    ```

    - 内层函数访问不到外层函数的 `this` 和 `arguments`, 可以通过闭包的方式实现访问。
<!--     - Each function automatically gets two special variables as soon as the function is called: `this` and `arguments`, to which the function's inner function can never have access. 
    - Save the value in another variable for inner function to manipulate it later. -->
<!-- - Since closures carry with them the containing function's scope, they take up more memory than other functions. Overuse of closures can lead to **excess memory consumption**, so it's recommended to use them only when absolutely necessary. -->
- 不当使用闭包会造成内存泄漏。
<!-- - Any time you see a function, with an input parameter that's quite static, meaning you don't expect the parameter to take on a new value every time you call the function, that's a opportunity to re-factor your code, such that you store the value in a variable form an outer scope. Because the way closures work, the inner function will always have access to the outer scope variable even after the outer function returns. -->
<!-- - Approaches of retaining access to an inner function after the its containing function has returned: 
    - passing the inner function to a `setIimeout()`
    - returning the inner function from the containing function
    - saving the inner function to a global variable  -->
- 闭包可以实现块级作用域和私有变量。
<!-- ## Mimicking block scope
## Private variables -->