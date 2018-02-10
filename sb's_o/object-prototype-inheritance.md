# 构建对象
1. 字面表示
2. 內建构造函数
    - `String()`, `Number()`, `Boolean()`, `Array()`, `RegExp()`, `Function()`, `Date()`
3. Decorator function
    - 对象作为参数传入，在函数内增加对象的属性和方法后将其返回。
    - 各个实例之间相同的方法无法复用。
4. Factory pattern
    - 函数内创建对象，增加属性和方法后将其返回。
    - 各个实例之间相同的方法无法复用。

    ```javascript
    function createPerson(name, job) {
        var o = new Object();
        o.name = name;
        o.job = job;
        o.sayName = function() {
            alert(this.name);
        };
        return o;
    }
    ```

5. prototype
    - 将共有方法移出来解决复用问题。

        ```javascript
        var carlike = function(obj, loc) {
            obj.loc = loc;
            obj.move = move;
            return obj;
        };
        var move = function() {
            this.loc++;
        };
        var ben = carlike({}, 9);
        ```

        - 潜在问题是若 `move` 需要更名，`carlike` 里也必须同时更新。
    - 将共有方法移出的同时将他们存储在一个对象中。

        ```javascript
        function extend(obj, methods) {
            for (var key in methods) {
                obj[key] = methods[key];
            }
        }
        var carlike = function(obj, loc) {
            obj.loc = loc;
            extend(obj, methods);
            return obj;
        };
        var methods = {
            move: function() {
                this.loc++;
            },
            on: function() {},
            off: function() {}
        };
        ```