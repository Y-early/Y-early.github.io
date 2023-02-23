---
title: Vue
date: 2022-12-27 15:44:47
image: '/images/theme/bj/Vue.png'
---

Vue (读音 /vjuː/，类似于 view) 是一套用于构建用户界面的渐进式框架。与其它大型框架不同的是，Vue 被设计为可以自底向上逐层应用。Vue 的核心库只关注视图层，不仅易于上手，还便于与第三方库或既有项目整合。另一方面，当与现代化的工具链以及各种支持类库结合使用时，Vue 也完全能够为复杂的单页应用提供驱动。

### 事件修饰符
1、.stop阻止事件冒泡，相当于event.stopPropagation方法。
2、.prevent阻止事件默认行为，相当于event.preventDefault方法。
3、.once 只执行一次以后不再执行。
4、.captuer 当元素发生冒泡时，谁带有此修饰符就先执行谁，若有多个则从外向内触发。
5、.native 给组件绑定原生事件，当成普通的html标签看待。
6、.passive 执行默认行为和prevent 是对立关系 每次产生时间浏览器都会查询是否有preventDefault阻止该次事件的默认动作 此修饰符就是为了告诉浏览器不用查询我们没有preventDefault阻止默认动作。
7、.self 只有触发当前事件的时候才执行冒泡不会执行。

### 表单修饰符
1、.number 只能是数字
2、.trim 过滤用户输入的首尾空字符
2、.lazy 在我们填完信息，光标离开标签的时候，才会将值赋予给value，也就是在change事件之后再进行信息同步


### 虚拟Dom和diff算法Vue2
虚拟Dom就是一个普通的js对象是用来描述真实Dom结构的js对象，因为不是真是的Dom结构，所以叫做虚拟Dom。
虚拟Dom是个对象有6个属性 。
 (sel) 表示当前节点的标签名。
 (data) 表示节点上的属性。
 (elm)表示虚拟节点对应的真是Dom节点。
 (text)对应当前节点下的文本。
 (key)当前节点的表示。
 (childre) 表示当前节点下的其他子节点。
 **虚拟Dom的作用**
 传统的Dom在数据发生改变时，需要不断的去操作Dom，虽然后面出现了模板引擎虽然它可以一次性更新多个Dom，但是它没有一个追踪状态的机制，当引擎内的某个数据发生变化时它依然需要操作Dom去重现渲染整个引擎。
 虚拟Dom有可以很好的跟踪当前Dom的状态，虚拟Dom会根据当前的数据生成一个描述当前Dom的虚拟Dom，在数据发生变化时又会生成一个新的虚拟Dom，这两个虚拟Dom正好就是变化前和变化后的状态，然后通过diff算法进行比较，哪里有变化就更新哪里。可以大大的提高页面渲染的效率，提高用户的体验。
![虚拟Dom结构](/images/theme/screenshot/vmDom.png)
vue2后使用的都是snabbdom 虚拟dom类库

snabbdom 中几个重要的和新方法
h函数
patch函数
patchVnode函数
updateChildren函数

h函数是在render函数内运行的vue在created > beforeMount之间的时候会将模板编译成某种格式放到render函数内，执行render函数的时候生成虚拟Dom。
![h函数](images/theme/screenshot/functionH.png)
h函数以函数重载的方式定义的
**什么是函数重载**
函数重载就是定义多个同名的函数，利用函数的类型以及参数类型来区分，当参数个数不同，参数类型不同时，函数内执行的代码也会不同。
h函数内最重要的就是执行了vnode函数 vnode函数主要作用就将h函数传来的参数转成了js对象，既虚拟Dom。

vnode函数就是生成了js对象就是虚拟Dom

代码初次运行时生命周期走到created和beforeMount 之间时会把template模板编译成某种格式放到render函数内，然后当render函数执行时，h函数被调用，而h函数内调用啦vnode函数并生成虚拟Dom，并返回结果。
之后每次数据发生改变时都会生成新的虚拟dom，再然后就是新旧虚拟Dom的对比。

**diff比较规则**
diff整体策略：深度优先，同层比较
1、diff比较两个虚拟Dom只会在同层级比较不会跨层比较。
2、比较的过程中循环从两边向中间收拢

**patch**
patch函数是比较的开始，patch函数中对根节点进行比较
非根节点都是在updateChildren函数中执行
**patcVnode**
patchVnode是比较两个相同节点的子级(文本|子节点)的一个函数，所以它的调用是在新dom判断之后，只有判断两个节点相同的时候才会被执行。
作用：对比新旧两个节点，更新dom的子级(子级包含文本或子节点)