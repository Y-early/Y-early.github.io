---
title: JavaScript
date: 2022-12-27 15:41:02
image: '/images/theme/bj/JavaScript.jpg'
---
JavaScript（JS）是一种具有函数优先特性的轻量级、解释型或者说即时编译型的编程语言。虽然作为 Web 页面中的脚本语言被人所熟知，但是它也被用到了很多非浏览器环境中，例如 Node.js、Apache CouchDB、Adobe Acrobat 等。进一步说，JavaScript 是一种基于原型、多范式、单线程的动态 (en-US)语言，并且支持面向对象、命令式和声明式（如函数式编程）风格。

## JS代码质量工具
JavaScript Booster

### js获取dom元素的八种方法
通过ID获取（getElementById）
通过name属性（getElementsByName）
通过标签名（getElementsByTagName）
通过类名（getElementsByClassName）
获取html的方法（document.documentElement）
获取body的方法（document.body）
通过选择器获取一个元素（querySelector）
通过选择器获取一组元素（querySelectorAll）

### get和post的区别
1、get一般用来获取数据（也可以提交请求）post基本上都是用来提交请求
2、get 因为参数会放在url中所以隐私性比post差一点get请求的数据长度有大小限制不同的浏览器和服务器不同，一般限制在2~8k左右更见常见的是1k以内
post 放在body内没有大小限制。
3、get请求刷新服务器或者回退没有影响，post会重新提交数据请求
3、get请求可以被浏览器缓存，post 不会被缓存。
4、get请求可以被保存到浏览器历史记录中或者添加为标签，而post不可以因为get的参数都放在url中。
5、get请求支持的编码只支持application-x-www-from-urlencoded,post支持多种muilpart、from-data
深入理解
1、报文上的区别
get和post 都是http的请求方式 在传输上没有区别，因为http协议是居于tcp/ip协议的应用层，协议报文格式上带参数和不带参数最大的区别就是第一行的方法名不同，一个是get一个是post
get直接往后面拼 post在content-type 
2、get参数写法是固定的吗？
在约定中参数一般卸载？后面用&分割
解析报文的过程是通过tcp获取数据，用正则等工具从数据中获取header和body，从而提取数据。
所以也可以不用http 规定的只要后台能解析就行
3、post比get安全吗？
从传输的角度上讲它们都不是安全的，因为http在网络上是明文传输，只要在网络节点上抓包，就能完整的获取报文。
想要安全的传输只有https。


### 一、作用域
1、作用域的目的限制变量访问的环境，在查找某个变量的时候子级作用域会一层一层的往上找，找不到会报错is not defind
es6快捷作用域，要配合es6定义变量的方法如const、let 

2、全局作用域没有回收机制
### 二、闭包
专业的文献：闭包（closure）是一个函数以及其捆绑的周边环境状态（lexical environment，词法环境）的引用的组合。换而言之，闭包让开发者可以从内部函数访问外部函数的作用域。在 JavaScript 中，闭包会随着函数的创建而被同时创建。
自己理解：闭包就是函数嵌套函数子函数可以访问父级函数里的变量
闭包的优缺点：
优点：
1、可以将一个变量或者方法长期存储在内存中，用于缓存。
2、闭包的变量或者方法一直处于引用的状态所以变量不会销毁
3、可以避免全局变量的污染。
4、比局部变量使用起来更加灵活
缺点：
由于闭包不会自动释放内存和销毁变量，也就是说当闭包的变量过多时就会占用更多的内存从而导致运行变慢
解决方法：在闭包使用结束后手动清楚或者把值置空


``` JavaScript
function init() {
  var name = "Mozilla"; // name 是一个被 init 创建的局部变量
  function displayName() { // displayName() 是内部函数，一个闭包
      alert(name); // 使用了父函数中声明的变量
  }
  displayName();
}
init();
```
### 三、this

this的值是在函数执行时决定的，不是在函数定义时决定
在绝大多数情况下，函数的调用方式决定了 this 的值（运行时绑定）。this 不能在执行期间被赋值，并且在每次函数被调用时 this 的值也可能会不同。ES5 引入了 bind 方法来设置函数的 this 值，而不用考虑函数如何被调用的。ES2015 引入了箭头函数，箭头函数不提供自身的 this 绑定（this 的值将保持为闭合词法上下文的值）。

### 原型
1、什么是原型。
 每一个js 对象都有它的原型对象，它可以使用原型对象上的所有属性和方法 。
 获取原型的方法有两种
 1、__proto__获取
 2、通过prototype获取 

### 四、JavaScript的六种继承方法
**new关键字在创建对象的时候具体都干了什么事？？ 背**
  在内存中创建了一个虚拟的空对象（为了方便理解 例如：var json = {}）
  将json对象结构传入到这个函数对象结构本身，
  运行当前构造函数对象结构，看在其this环境指向上有无属性或者是方法，
  如果函数的this指向上有属性或者是方法，则在这个json对象上进行添加
  如果没有则直接返回最初创建的那个空的json对象

-----------------------------------------



``` javascript 
new实例对象，原型对象，构造函数，prototype __proto__ constructor 之间的关系
function Foo(){
  this.a='小明'
} 
var foo = new Foo()
 构造函数可以通过new的方式来执行
 构造函数通过new的方式来执行的话Foo 内部的this指向将指向当前实例对象 foo
 它和函数唯一的区别就是通过函数的执行方式 this 指向会有所区别
 prototype是所有实例的公共祖先 实例有能力拿到原型上的属性和方法
Object.prototype===null //true 是终点

constructor 原型上的一个属性 它指向实例对象
```

### 1、原型链继承
 数组的原型是array -->array 的原型的对象是Object，只要在原型链上的属性都可以访问 
 ``` javascript
 function Student() {
        this.name = '小明'
        this.age = 12
        this.school = ['语文', '数学']
    }
    Student.prototype.say = function () {
        console.log('初中')
    }
    function Age() {
    }
    Age.prototype = new Student()
    var age1 = new Age()
*     var age2 = new Age()
    age1.name = '小红'
    age1.age = 18
    age1.school.splice(0, 1)
    console.log(age1)
    console.log(age2)

 ```

  原型链继承的问题：引用值会共享,无法解决

![](/images/theme/screenshot/yxl.png)
 
 
### 2、构造函数继承

``` javascript
 function Student() {
        this.school = ['语文', '数学']
    }
    Student.prototype.say = function () {
        console.log('初中')
    }
    function Age() {
        Student.call(this)
    }
    var age1 = new Age()
    var age2 = new Age()
    age1.school.splice(0, 1)
    console.log(age1)
    console.log(age2)
```
构造函数继承解决了引用值共享的问题，但是无法拿到原型上的方法
![](/images/theme/screenshot/gzhs.png)

### 3、组合继承（伪经典继承）

``` javascript
 function Student() {
        this.school = ['语文', '数学']
    }
    Student.prototype.say = function () {
        console.log('初中')
    }
    function Age() {
        Student.call(this) 1
    }
   2 Age.prototype = new Student() //会调用两次Student
    var age1 = new Age()
    var age2 = new Age()
    age1.school.splice(0, 1)
    console.log(age1)
    console.log(age2)
```


### 4、原型式继承
这里主要借助 **Object.create** 方法实现普通对象的继承
``` javascript
 function Student() {
       this.school = ['语文', '数学']
   }
   Student.prototype.say = function () {
       console.log('初中')
   }
   function Age() {
       Student.call(this)
   }
   Age.prototype = Object.create(Student.prototype)
   var age1 = new Age()
   var age2 = new Age()
   age1.say()
   age2.say()
   console.log(age1)
   console.log(age2)
```
这种继承方式的缺点也很明显，用为object.create 方法实现的是浅拷贝，多个实力的引用类型属性或指向
相同的内存，存在篡改的可能

### 5、寄生式继承
寄生式继承在上面继承基础上进行优化，利用这个浅拷贝的能力再进行增强，添加一些方法

``` javascript
 const aa = {
        name: "parent5",
        friends: ["p1", "p2", "p3"],
        getName: function () {
            return this.name;
        }
    }
    function Age(a) {
        let conle = Object.create(a)
        conle.getSchool = function () {
            return this.friends
        }
        return conle
    }
    let school =Age(aa)
    console.log(school.getName());
    console.log(school.getSchool())
```
![](/images/theme/screenshot/jssjc.png)
优缺点和原型式继承一样的缺点

### 6、寄生组合式继承(经典继承)

``` javascript
function Student() {
       this.school = ['语文', '数学']
   }
   Student.prototype.say = function () {
       console.log('初中')
   }
   function Age() {
       Student.call(this)
   }
   Age.prototype = Object.create(Student.prototype)
   var age1 = new Age()
   var age2 = new Age()
   age1.say()
   age2.say()
   console.log(age1)
   console.log(age2)
   
```


### 7、clss类继承（es6）
constructor,extends,super
constructor 构造器用来初始化对象成员，可定义属性和方法
extends 子类继承父类 例：子 extends 父
super 用来获取父类初始化的成员
父类不能调用子类的属性和方法，也就是说子类的变化不会影响到父类。 

``` javascript
 class Percons{
        constructor(name){
            this.name=name
        }
    }
 class Student extends Percons{
        constructor(name,age){
            super(name)
            this.score=age
        }
        fs(){
            console.log(`我是${this.name} 今年${this.age}`)
        }
    }
    var student=new Student('张三',12)
    console.log(student)
    student.fs()
```
![](/images/theme/screenshot/classjc.png)

### ES6和ES5继承的区别
1、ES5的继承是通过prototype或构造函数的机制来实现的。ES5的继承实质上是先创建子类的实例对象，让后将父类的方法添加到this上call(this)或apply(this)
2、ES6的继承机制完全不同，**实质上是先创建父类的实例对象this（所以必须先调用父类的super（）方法），然后再用子类的构造函数修改this。**
具体的：ES6通过**class**关键字定义类，里面有构造方法，类之间透过**extends**关键字实现继承。子类必须在**constructor**方法中调用**super**方法，否则新建实例报错。
因为子类没有自己的this对象，而是继承了父类的this对象，然后对其进行加工。如果不调用super方法子类得不到this对象。
ps:**super**方法指代父类的实例，即父类的this对象，在子类的构造函数中，调用**super**后，才可以使用this关键字，否则报错。

### Promise

Promise 是异步编程的一种解决方案，比传统的解决方案回调函数, 更合理和更强大。
解决了回调地狱代码过多难以维护的问题
Promise 的三种状态
reslove 成功时的状态
reject  失败时的状态
pedding 未完成时的状态
从未完成到成功，从未完成到失败


``` javascript
     function ajax(url){
        return new Promise((reslove,reject)=>{
            reslove({
                aa:1,
                bb:2,
                cc:3
            })
            // reject({code:500,error:'请求失败'})
        })
    }
    var por=ajax('111')
    por.then((res)=>{
        console.log('请求成功',res)
        console.log(por)
    }).catch((error)=>{
        console.log('请求失败',error)
    })
   
```
then()
catch()
finally()
then是实例状态发生改变时的回调函数，第一个参数是resolved状态的回调函数，第二个参数是rejected状态的回调函数
then方法返回的是一个新的Promise实例，也就是promise能链式书写的原因
catch()方法是.then(null, rejection)或.then(undefined, rejection)的别名，用于指定发生错误时的回调函数
finally()方法用于指定不管 Promise 对象最后状态如何，都会执行的操作
调用reslove()方法才能调用then，reslove传出来的值是then的形参

### async await
async和await 是Generator的语法糖，async关键字代表后面的函数中有异步操作，await 表示等待一个异步方法执行完成。
``` javascript
    async function A(){
        let a= await ...
    }
```
async函数 返回一个promise 对象，单独一个async函数 和promise执行的功能是一样的。
await 就是等promise的返回结果后才会继续往下执行
await 异步等待 等待的是一个promise对象，后面必须跟一个promise对象但是不用写 .then()，直接就可以拿到返回值
调用async 函数不会造成代码堵塞，但是在await 会引起async函数内部代码的堵塞

promise 和async/await区别
promise是通过.thne()和.catch()来去处理数据和捕获异常的，并且是链式调用，虽然比回调函数好很多但是还是容易造成代码多层堆叠难以维护；
async/await则是通过tyr{}.catch{}进行捕获直接抛出异常
async/await最大的优点是使代码看起来更像同步遇到await立即执行返回结果在执行后面的操作，promise.then()的方式有可能结果还没返回就已经执行了外面的操作

### 深拷贝和浅拷贝
原始类型：数值（Number）、字符串（String）、布尔（Boolean）、空（Null）、未定义（Undefined），**存在于栈内存**。
引用类型：对象、数组、function，**存在与堆内存**
浅拷贝
```javascript 
function fn() {
        console.log("hello world");
        console.log(this.name);
    }
    let cat = {
        name: '旺财'
    }
    let dog = {
        name: '喵喵',
        seayName: function (food1, food2) {
            console.log('我是' + this.name + '我喜欢吃' + food1 + '和' + food2);
        }
    }
    // fn.call(cat)
    // dog.seayName.call(cat,'鱼','rou')
    // dog.seayName.apply(cat,['鱼','肉'])
    // let a= dog.seayName.bind(cat,'鱼','rou')
    a()
```
深拷贝
```javascript 
const Student1 = {
        name: '小明',
        age: '2',
        grieFrind: {
            user: '小花'
        }
    }
    function copy(obj) {
        let newObj = {}
        for (let i in obj) {
            if (obj[i] instanceof Object) {
                newObj[i] = copy(obj[i])
            } else {
                newObj[i] = Student1[i]
            }
        }
        return newObj
    }
    const Student2 = copy(Student1)
    // Student1.grieFrind.name='小王'
    console.log(Student1);
    console.log(Student2);
```


### 防抖节流
防抖
```javascript
 var ipt = document.querySelector("input")
    ipt.oninput = denounce(function () {
        console.log(this.value);
    }, 500)

    function denounce(fn, del) { //防抖，只执行最后一次
        var tiem = null
        return function () {
            if (tiem !== null) {
                clearTimeout(tiem)
            }
            tiem = setTimeout(() => {
                fn.call(this)

            }, del)
        }
    }
```
节流
```javascript
 window.onscroll = throttle(function () { //节流 作用：控制高频事件的发生 隔一段时间执行一次
        console.log(this);
    }, 500)
    function throttle(fn, del) {
        var t = true
        return function () {
            if (t) {
                setTimeout(() => {
                    fn.call(this)
                    t = true
                }, del);
                t = false
            }
        }
    }
```
### call、apply、bind的基本概念
三种都是用来改变this指向的，其中call和apply的传参方式不同apply的传参方式是数组而call是逗号隔开依次往后排，
bind的传参方式和call一摸一样但是不会调用函数它会以返回值的形式返回
  ```javascript
 function fn() {
        console.log("hello world");
        console.log(this.name);
    }
    let cat = {
        name:'旺财'
    }
    let dog={
        name:'喵喵',
        seayName:function(food1,food2){
            console.log('我是'+this.name+'我喜欢吃'+food1+'和'+food2);
        }
    }
    // fn.call(cat)
    // dog.seayName.call(cat,'鱼','rou')
    // dog.seayName.apply(cat,['鱼','肉'])
    let a= dog.seayName.bind(cat,'鱼','rou')
    a()
  ```

### 运行机制 
先执行同步任务后执行异步任务
**一、单线程**
一个任务执行完之后才能执行另一个
**二、process.nexTick和setlmmediate方法**
process.nexTick()在同步之后异步之前执行
setlmmediate()异步之后执行
**三、事件循环**
事件循环会持续的循环任务队列里的方法有任务则放到运行栈里
**宏任务，微任务**
宏任务：计时器，ajax，读取文件
微任务：promise,.then 
**注意：new Promise里的代码是同步的，then放到任务队列是异步的**
执行顺序：
1、同步程序
2、process.nexTick()
3、微任务
4、宏任务
5、setlmmediate()
![运行机制图解](/images/theme/screenshot/JavaScriptYXJZ.png)

### 垃圾回收机制
JavaScript的垃圾回收机制，清除无用的变量释放多余的内存，展现更好的性能。
在JavaScript中，具有自动垃圾回收机制，也就是说执行环境会自动负责管理代码执行过程中的内存使用情况，会自动清除一些用不到的变量，
以此来释放内存，该机制每隔一段时间会执行一次。
JavaScript中能实现垃圾回收机制的方式一共有两种：**标记清除，引用计数**
**标记清除**
标记清除是JavaScript中最常用的垃圾回收方式。它的执行方式是在执行环境中每创建一个变量，就会对该变量进行标记，等到执行垃圾回收机制时在根据标记来决定是否进行回收。
**引用计数**
引用计数 是一种不太常用的回收机制 顾名思义就是针对值为引用数据类型的变量进行计数。
引用计数的回收机制是当声明一个变量就会给改变量设定一个值为0的引用次数，当改变量被引用了引用次数就会+1取消则-1若引用次数不变一直为0就会被回收机制给清除不为0则不做任何更改

### 跨域
#### jsonp 
通过script标签没有跨域限制的漏洞来获取数据
缺点：不安全只能用于get方式
优点：兼容性好
#### cors 
需要浏览器和后端同时支持
浏览器会自动进行cors 通讯实现cors通信的关键是后端。
虽然设置cors 后前端没什么关系但是通过这种方式解决跨域，会在发送请求时会出现两种情况，分别是简单跨域和复杂跨域。
条件：1
1、简单跨域使用下列条件之一
  get、head、post
条件：2
2、Content-type 的值仅限于下列三者之一
  text/plain
  multipart/form-data
  application/x-www-form-urlencoded

  不符合以上条件的请求就是复杂请求，cors会在正式请求之前发送一个普通的http请求，称为 **预检** 请求
  是cors用来确定服务端是否允许跨域请求。

#### node中间件代理(两次跨域)
    同源策略是浏览器需要遵循的标注，如果是服务器向服务器发送请求就不需要遵循同源策略
原理：
    1、客户端向代理服务器发送请求，代理服务器转发给服务器
    2、服务器响应返回给代理服务器，代理服务器在返回给客户端

#### 反向代理
``` javascript
 server: {
    // 设置为0.0.0.0则所有的地址均能访问
      host: '0.0.0.0', 
      port: 5001,
      https: false,
      hmr: {
        overlay: false
      },
       // 跨域问题解决 代理（关键部分）
      proxy: {
        '/api': {
          target: env.VITE_BASE_URL, //接口地址
          changeOrigin: true,//允许跨域
          rewrite: (path) => path.replace(/^\/api/, '')//路径重写
        }
      }
    }
```

#### 大白话
跨域的解决方案思路两种，躲避绕过去和cors；
各种iframe方式可传递数据，但组织和控制代码逻辑太复杂，鸡肋；
jsonp前几年使用，现在浏览器兼容性高了，以及受限于仅get方式，逐步淘汰了；
nginx反向代理是绕过去的方式，是从古至今通吃的没完解决方案，缺点也许是服务器压力大一点，实际中那点压力根本不是大问题；同时反向代理更适合内部应用间访问和共享；
cors才是真正的称得上跨域请求解决方案，因为请求存在跨域，结果是拿到了数据，也就是说服务器和浏览器之间进行了协商通信控制后，才得以允许或拒绝；
最后说明下，跨域请求产生时，请求是发出去了，也是有响应的，仅仅是浏览器同源策略，认为不安全，拦截了结果，不将数据传递我们使用罢了




