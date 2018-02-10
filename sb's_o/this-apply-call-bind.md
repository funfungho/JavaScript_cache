- `this` 对象指向函数操作的 ***context object***.
    - 在全局的执行上下文里， `this` 总是指向 global object, 不论是否是 strict mode.
- `this` 是一个关键字，不是变量，不能被重新赋值。
- 函数的 `this` 在**运行时**绑定。
    - 函数在网页的全局作用域下被调用时， nonstrict 模式下 `this` 是 `window`, strict 模式下是 `undefined` 或 `null`.
    - 函数在另一个函数里被调用时，`this` 同函数在全局作用域下被调用的情况。
    - 函数被一个对象作为的方法调用时，`this` 是作为调用者的对象。
        - 对象方法在 prototype 上时， `this` 还是调用该方法的对象实例。
        - `this` 就近绑定，调用 `o.b.foo()` 时 `this` 是 `o.b`.
        - 函数的方法被赋值给其它变量或当做参数传递时，`this` 同函数在全局作用域下被调用的情况。
    - 构造函数被调用时 (`new`), `this` 默认是新建的实例，且该实例被默认返回。若自定义返回其它对象，`this` 则是自定义返回的对象。

        ```javascript
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

    - 匿名函数被调用时，`this` 同函数在全局作用域下被调用的情况。
- **某个被调用函数的 `this` 是“拥有”该函数的对象；对象实例中的 `this` 是该对象本身。**
- `apply()` 第一个参数为 `this`, 第二个参数为数组， `arguments` 对象， `null`, 或者 `undefined`. 调用 `apply()` 的结果是按照传入的参数执行函数。
<!-- - The `apply()` method accepts 2 arguments: the value of `this` inside the function and an array of arguments. This second argument may be an instance of `Array`, the `arguments` object, or *`null`* or *`undefined`* if no arguments should be provided. The return value is the result of calling the function with the specified `this` value and arguments. -->
- `call()` 除 `this` 外的参数要单个列出。
<!-- - The `call()` method exhibits the same behavior as `apply()`, but arguments are passed to it individually. Using `call()` arguments must be **enumerated specifically**. --> 
- 传递参数的方式决定了用 `call()` 还是 `apply()`.
- 传入 `apply()` 和 `call()` 的 `this` 若不是一个对象，JS 会尝试转换。

    ```javascript
    function bar() {
        console.log('this: ', this);
        console.log(Object.prototype.toString.call(this));
    }
    bar.call(7);     // this: Number {7}\n[object Number]
    bar.call('foo'); // this: String {"foo"}\n[Object String]
    ```

<!-- - With `call` and `apply`, if the value passed as `this` is not an object, an attempt will be made to convert it to an object using the internal `ToObject` operation (**boxed**). So if the value passed is a primitive like `7` or `"foo"`, it will be converted to an `Object` using the related constructor, so the primitive number `7` is converted to an object as if by `new Number(7)` and the string `"foo"` to an object as if by `new String("foo")`, e.g. -->
- `bind()` 返回预绑定 `this` 的函数，并不立刻执行。

    ```javascript
    var logApp = function() {
        <!-- console.log 方法的 this 仍旧绑定为 console, 没有改变 -->
        console.log.apply(console, arguments);
    };

    var logBd = console.log.bind(console);
    ```
- 由 `apply()`, `call()` 或 `bind()` 绑定 `this` 后，用其它对象的 `.` 操作符去调用该函数也不能改变 `this`.
- `setTimeout`

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
    ```

- 传入 `bind()` 的除 `this` 以外的其它参数是绑定 `this` 的新函数的初始化参数。

    ```javascript
    function list() {
        /* it's equivalent to `arguments.slice();` if arguments has the method! */
        /* a typical way of converting the `arguments` to a real array */
        return Array.prototype.slice.call(arguments);  
    }
    var list1 = list(1, 2, 3);
    var leadingThirtysevenList = list.bind(null, 37);
    var list2 = leadingThirtysevenList();           // [37]

    var list3 = leadingThirtysevenList(1, 2, 3);    // [37, 1, 2, 3]
    ```

- 若绑定的函数时构造函数，当它用来新建实例时，预绑定好的 `this` 将被忽略，其它参数会保留。 
    
<!-- - Contrary to `apply()` and `call()` methods, which invokes the function right away, the `bind()` method only ***returns a new function*** that it supposed to be invoked later with a pre-configured `this`. -->
