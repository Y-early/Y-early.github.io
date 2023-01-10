---
title: JavaScript
date: 2022-12-27 15:41:02
image: '/images/theme/bj/JavaScript.jpg'
---
JavaScript（JS）是一种具有函数优先特性的轻量级、解释型或者说即时编译型的编程语言。虽然作为 Web 页面中的脚本语言被人所熟知，但是它也被用到了很多非浏览器环境中，例如 Node.js、Apache CouchDB、Adobe Acrobat 等。进一步说，JavaScript 是一种基于原型、多范式、单线程的动态 (en-US)语言，并且支持面向对象、命令式和声明式（如函数式编程）风格。

## JS代码质量工具
JavaScript Booster
## 面试重点

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

### 防抖节流

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
