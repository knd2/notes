1. {}的hasOwnProperty方法返回对象是否包含某个属性，只能检测对象自身的属性，不能检测从原型中继承来的属性。

2. JS中的根对象是Object.prototype对象。

3. 一个对象的prototype只能通过`Object.getPrototype()`方法或者自身的`__proto__`属性来获取；通过对该对象赋值`prototype`属性并不会覆盖它的原型，而是为其增加了一个名为`prototype`的属性，而它的原型保持不变。

4. 使用`new`创建一个对象的过程：先从`Object.prototype`克隆一个对象，然后为它设置正确的`__proto__`即它的原型，最后通过外部构造器函数为其设置属性，最后返回对象。

5. JS函数的两个作用：普通函数；函数构造器。

6. 一个对象的属性与其构造器函数原型无关，属性的构造器函数为其设置了自身属性；构造器原型使得创建的对象继承了额外的可追溯的属性；即一个是自身的属性，另一部分是从构造器继承来的。

7. 承上一条，为一个对象设置与构造器原型同名的属性值，则对象本身发生变化：本质是多了一个属性。而构造器原型保持不变，通过构造器创建新的对象，它所继承的原型属性值也不变。

8. `<script>`标签中根据是否有`async`和`defer`分为3种处理情况：
  * 没有标记：此时DOM暂停解析，同步下载并执行script，然后恢复解析。
  * async：DOM解析和script下载并行执行，等下载完成后暂停解析，等待script执行完成后恢复解析。
  * defer：DOM解析和script下载并行执行，下载完成后继续解析，等DOM完成解析后再执行script。

9. JSONP的原理是在script中编写回调函数，然后编写script标签，其中src设置为接口地址，并且通过url参数的方式传递回调函数名。接口获取函数名，并且将数据和函数绑定拼装为回调函数调用数据参数的执行语句字符串返回给客户端。客户端获取该脚本内容（内容是回调函数执行字符串）后会执行回调函数。

10. 事件触发有capture和bubble两种方式， 前者是从父元素向子元素依次触发handler，后者反之。事件代理是指在父元素上绑定handler，然后通过事件冒泡来触发handler，这样既减少了事件绑定的数量提升性能，又能在新添加子元素也不需要为子元素添加handler。

11. HTTP请求包括状态行（method, url, version）、Header和消息主体构成。

12. POST请求传输的数据格式通过在Header中设置`Content-Type`来实现，常用的有：
  * `application/x-www-form-urlencoded;charset=utf-8`：内容中通过key/value的形式传输数据。
  * `multipart/form-data`：常用来实现文件上传，将消息主体分为多个部分，并且通过----boundary来分割，以----boundary--来结尾。
  * `application/json`：消息主体直接使用json数据。
  * `text/xml`：消息主体是一段xml。

13. es5只有函数作用域，因此要严格区别变量/函数的声明和赋值之间的不同。一个变量进入一个作用域有4种方式：
  * 语言自定义变量：所有作用域都存在`this`和`arguments`两个默认变量。
  * 函数形参
  * 函数声明：`function foo () {}`
  * 变量生命：`var x`
  但是es6中引入了块级作用域，使用`let`来声明或定义变量。

14. 变量提升中，如果同时有同名的函数声明和变量声明，则只有函数声明生效，和两个声明的前后顺序无关。

15. CSRF攻击是利用用户的会话标志cookie来实现登录，然后执行一些恶意操作。解决方法为在提交表单信息中增加伪随机数校验，即server在客户端种下一个伪随机数cookie，并要求每次表单提交时都要带上该cookie。因为攻击者不知道该校验cookie的值，所以提交表单后虽然登录状态没问题，但因表单信息不完整（或不正确）而无法完成操作。

16. 使用`new`时，在构造函数中返回不同类型变量的结果：
  * `this`：正常
  * object 类型对象：返回该对象
  * 非 object 类型对象：返回同`this`

17. `escape`用来转义一个字符串，和 URL 无关，`encodeURIComponent`比`encodeURI`的转义范围更大，比如它会转义`/`而后者不会，根据需要转义的内容的用途来选择使用哪个转义函数。

18. es6 中 arrow function 中的`this`是直接在语义上静态绑定的，而不是运行时动态绑定。总是和 enclosing context 中的环境绑定。而且他没有`arguments`这个参数，但是可以使用 rest arguments 来获取参数。

19. 调用 generator 函数返回一个指针，每次执行`next()`指向下一个`yield`表达式的位置。结果是一个对象，有`value`和`done`两个属性，`value`表示`yield`后表达式的值，`done`表示当前 generator 函数是否执行完毕。

20. npm 中的`peerDependencies`主要用于 plugin，因为 plugin 不显示依赖它的 host 包，但是它用到的 API 会依赖。所以它不需要安装指定版本的依赖，因为它的代码中没用到类似`require('host-pkg')`，但需要安装指定版本的同级依赖（在`peerDependencies`中指定）。

21. 使用`sessionStorage`保证在同一个窗口（标签页）而且是同一个 host 下，数据可以共享。如果窗口关闭，则数据清除。

22. 使用`referrer`这个 name 的 meta 标签来使得网页去掉 referrer 信息，值为`no-referrer/never`，never 是为了兼容部分老的设备。其中安卓需要 5.0 版本以上可以支持该配置。

23. TS 中的 interface 和其它语言中的接口作用不同，它主要用来描述一种类型，可以是对象、数组、函数和累等，而不是仅限于描述一个类需要实现的部分方法集合。

24. 使用 npm i 不加任何参数时，会在安装完依赖后，执行`package.json`中`scripts`节点下的`prepublish`命令。

25. 使用`pushState`时，第三个参数 URL 是有层级关系的。如果是相对地址且其中有`/`，则会增加一个层级，下次 push 时会从新的层级开始修改 URL。如果为绝对地址，则会直接使用该 URL 并覆盖之前的层级。

26. `Object.seal`返回一个对象，该对象无法添加/删除新的属性，并且只能修改已有属性的值，而不能修改他们的可枚举性、可配置性、可写性。

27. `ES7 stage-2`现在有了 decorator，但是和 Python 中的装饰器还有较大差别。他可以用来修饰类、类属性、方法和参数，但它接收的参数都是类似的。第一个参数对于静态成员来说是类的构造函数，对实例成员来说是类的原型对象。第二个参数是成员的名字。第三个参数如果存在，是成员的属性描述符或者参数在函数参数列表中的索引。

28. Chrome 51 开始支持 IntersectionObserver，用来检测一个元素是否在 viewport 内并执行回调逻辑。

29. Observable 的`subscribe`方法类似一种延迟执行，并且可以实现返回多个值。当执行`subscribe`的时才会执行默认 Observable 上的函数。它是一种 push 模型。

30. Observable 中的 next 方法只能传递一个参数，如果设置多个，其它参数会在 observer 的调用中被设置为`undefined`。并且 Observable 中可以执行多次 next，但是只能执行一次 error 或 complete（而且二者只能执行其一），并且在执行 error/complete 后执行终止，后续 next 没有效果，但是可以继续执行其它逻辑。

31. Fetch API 提供了以下几个对象：
  * fetch 方法
  * Headers
  * Request
  * Response

32. 通过选择器直接赋值的属性默认是 enumerable 的，且值可修改；通过`Object.defineProperty`定义的属性默认是 immutable 的，不可修改也不可删除，可以通过设置`configurable`为`true`来修改该特性；同时通过该方法定义的属性也默认不可枚举，可设置`enumerable`为`true`来修改，可枚举是指能被`for...in/Object.keys`遍历。

33. `for...in`会遍历一个对象所有可枚举属性，包括其原型链上的属性，`Object.keys`不会，前者可以配合`Object.hasOwnProperty`来过滤掉原型上的属性，`Object.getOwnPropertyNames`和`keys`的区别在于它可以获取不可枚举的属性。

34. `Object.assign`会复制源对象上的 enumerable 且非原型链上的属性到目标对象。

35. `Object.setPrototypeOf`为 ES6 新增的方法，可以设置一个对象的原型。

36. 使用`in`判断属性是否在一个对象中，会查找对象自身属性、prototype 上的属性，同时也会查找 enumerable 为`false`的属性。

37. 
