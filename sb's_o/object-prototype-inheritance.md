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

5. Functional shared pattern
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

    - `methods` 这样的写法不直观，不容易建立起与 `carlike` 的关联性，于是让 `methods` 成为 `carlike` 函数（对象）的属性。

        ```javascript
        function extend(obj, methods) {
            for (var key in methods) {
                obj[key] = methods[key];
            }
        }
        var carlike = function(obj, loc) {
            obj.loc = loc;
            extend(obj, carlike.methods);
            return obj;
        };
        carlike.methods = {
            move: function() {
                this.loc++;
            },
            on: function() {},
            off: function() {}
        };
        ```

- How it comes to `Object.create()` 
# 操作对象
- `Object.keys(obj)`, `Object.values(obj)`, 
---
- 自定义构造函数

    ```javascript
    function Person() {
        this.name = name;
        this.sayHello = function(name) {
            console.log('hello' + this.name);
        };
    }
    ```

    - 缺点：实例之间相同的方法无法重用，造成冗余。
    - 改进：将方法移出构造函数并定义成全局函数，构造函数内的方法指向全局变量。
    - 新问题：引入全局变量；修改时需同时改两处。
- prototype pattern
    - 一个构造函数的 `prototype` 对象用于存放其实例共有的方法和属性。实例可以通过委托字段查找到 `prototype` 对象来实现访问。
    - `prototype` 对象上存在一个 `constructor` 属性，属性值是该 `prototype` 对应的构造函数。

        ```javascript
        function Person() {
        }
        Person.prototype.name = 'sb';
        Person.prototype.friends = ['Tim', 'Phil'];
        Person.prototype.sayHello = function() {
            console.log('hello' + this.name);
        };
        var p1 = new Person();
        var p2 = new Person();
        var p3 = new Person();

        /* 此处用 . 操作符（后跟赋值操作符）访问 name 和 friends 字段时，并未向 prototype 查找，直接在实例上新增了，所以不会影响其他实例对应字段的值 */
        p1.name = 'ho';
        p1.friends = ['nobody'];
        console.log('p1 在自身定义与 prototype 上相同的属性后\n');
        /* 'name' 必须加引号 */
        console.log(`p1.hasOwnProperty("name", "friends"): ${p1.hasOwnProperty('name')}, ${p1.hasOwnProperty('friends')}`);     /* true, true*/
        console.log(`p2.hasOwnProperty("name", "friends"): ${p2.hasOwnProperty('name')}, ${p2.hasOwnProperty('friends')}`);     /* true, false */
        console.log(`p1's name and friends: ${p1.name}; ${p1.friends}`);
        console.log(`p2's name and friends: ${p2.name}; ${p2.friends}`);
        /*
        p1's name and friends: ho; nobody
        p2's name and friends: sb; Tim,Phil
        */

        /* friends 是引用类型，p2 实例操作它在 prototype 上找到的 friends (此处的 . 操作符未在 p2 上新增实例字段) 会影响其他所有已经存在或是将会创建的将 friends 的查找委托到 prototype 上的实例 */
        p2.friends.push('Gloria');
        /* name 字段虽非引用类型，但由于直接在 prototype 上改动，会立刻映射到 blabla */
        Person.prototype.name = 'Slack';
        var p3 = new Person();
        p3.friends.shift();
        console.log('更新 prototype 后\n');
        /* p1 的字段查找并未委托到 prototype */
        console.log(`p1: name - ${p1.name}; friends - ${p1.friends}`);        
        console.log(`p2: name - ${p2.name}; friends - ${p2.friends}`);        
        console.log(`p3: name - ${p3.name}; friends - ${p3.friends}`);     
        /*
        p1: name - ho; friends - nobody
        p2: name - Slack; friends - Phil,Gloria
        p3: name - Slack; friends - Phil,Gloria
        */
        ```

        - 