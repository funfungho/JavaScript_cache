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
    
<!-- - Contrary to `apply()` and `call()` methods, which invokes the function right away, the `bind()` method only ***returns a new function*** that it supposed to be invoked later with a pre-configured `this`. -->
