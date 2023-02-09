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


**any类型**
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
**void类型**
只能将其赋值为null或undefind，多用于函数返回值
**never类型**
 永远不会出现的值的类型（或永远不会发生的类型）

 ``` javascript
let fn = () => {
  // 手动通过 throw 抛出一个异常（错误）
  throw new Error('err...')
}
 ```
