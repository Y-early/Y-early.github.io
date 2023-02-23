---
title: TypeScript
date: 2022-12-27 15:47:19
image: '/images/theme/bj/typescript.jpg'
---

什么是 TypeScript？
TypeScript，简称 ts，是微软开发的一种静态的编程语言，它是 JavaScript 的超集。 那么它有什么特别之处呢?

简单来说，js 有的 ts 都有，所有js 代码都可以在 ts 里面运行。
ts 支持类型支持，ts = type +JavaScript。
那么 ts 和 js 有什么区别呢？
JavaScript 属于动态编程语言，而ts 属于静态编程语言。
js：边解释边执行，错误只有在运行的时候才能发现
ts：先编译再执行，在写的时候就会发现错误了（ts不能直接执行，需要先编译成 js ）
ts 完全支持 js ，可以直接转换

### 类型
1·基础类型
string、number、Boolean、null、undefined、symbol、Biglnt。
``` javascript
//列
let a:string='aa'
let a:string|number='aa'
// 变量：类型|...


```
2·引用类型
array、object

```javascript
//列 
let a:(number|string|boolean)[]=[]
//加括号表示这个数组可以写入上边三个类型的值
let a:number|boolean|string[]=[]
//多个类型不加括号表示string类型的只能是数组
```


### **any类型**
包括了所有类型,和js一样没有类型校验，不推荐使用
**unknow类型**
特点：unknown 类型可以接受任意类型，但是无法赋值给其他类型
```javascript
let a:unknown='haha'
let b:string=a as string
console.log(b);
console.log(a);
let a:string='99'
let b:number=a as number //这样不可以转换
let b:number=a as unKnown as number //用unknow 作为中间转换层 在进行转换
// as 类型断言|类型转换
```
### **void类型**
只能将其赋值为null或undefind，多用于函数返回值
**never类型**
可以赋值给任意类型，但是无法给never赋值其他类型
 ``` javascript
let fn = () => {
  // 手动通过 throw 抛出一个异常（错误）
  throw new Error('err...')
}
 ```

 ### **enum枚举**
 枚举是列举固定几个值，用于取值被限定在一定范围内的场景，比如一周只能有七天，颜色限定为红绿蓝等。
直接定义变量的话的话可以随意定义，枚举只能使用你定义好的几个值
例如你定义一个方法接收一个参数，这个参数如果是int型，别人在调用你这个方法时可以传1或2等任意数字，虽然你告诉了同事，只能传0或1,
如果你把参数定义成只能传某个类型，例如是个枚举类，那么别人只能传你枚举类里定义好的几个类型，传其它的就会在编译时期报错

``` javascript
enum type{
  boy='nan',
  gril='nv'
}
console.log(type.boy);
```

### **断言**
我想让它是什么类型就是什么类型
```javascript
function a(ags: boolean):string|number {
  return ags ? '断言' : '断言失败'
}
let b = a(true) as number
b=2
console.log(b);

```
### **值类型**
```javascript
//值类型 as const断言
let c = 'aaa'
let a: '12' = '12'
let b = 1 as const
const arr = [c, a, 111, 222,true] as const
//as const 拿的是具体的值 来判断类型
```
### **数组使用const断言**
```javascript
let a='123'
let b=123
let c=[a,b]as const
// let c=<const>[a,b]
let d =c[0] 
d='123'
```
### **赋值结构中使用as**

``` javascript
// 赋值结构中使用断言
function hd() {
  let a = '周'
  let b = (x: number, y: number): number => x + y
  return [a, b]as [string, Function]
}
// const [n, m] = hd() 
// (m as Function)(1,2)

const [n, m] = hd()
console.log(n);
console.log(m(12,22));
```
### **非空断言**
？！

### **constructor构造函数在ts 中的特性**
```typescript
class User {
  // public name: string  先声明后使用 可以缩写为在使用的时候用修饰符进行修饰，不修饰会报错
  constructor(public name: string) {
      this.name = this.initName(name)
  }
  private initName(name:string){
    return `${name}-zzzz`
  }
}
const aa = new User('吱吱吱吱')
console.log(aa.name);

```
### **static静态属性语法使用**

```typescript
class User {
  static site:string='123'
  public static getSite():string{
    return User.site
  }
}
// 静态属性只能通过构造函数调用，实例里面是没有的
const instance=new User()
// console.log(User.site);
console.log(User.getSite());
```

### **单例模式**
``` typescript
class Axios {
  private static instance: Axios | null
  private constructor() {
    // console.log('121')
  }
  static make(): Axios {
    if (Axios.instance == null) {
      console.log('创建实例');
      Axios.instance = new Axios
    }
    return new Axios()
  }
}
const instance = Axios.make()
const instance2 = Axios.make()
const instance3 = Axios.make()
// 通过静态函数生成实例 只生成一次实例
```

### **访问器get和set**