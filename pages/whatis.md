# Immer 实现原理

<div class="grid grid-cols-2 gap-x-4">
<div v-click>

## Proxy

<br/>
<br/>

```ts
const target = {
  message1: "hello",
  message2: "everyone",
};

const handler = {
  get(target, prop, receiver) {
    return "world";
  },
};

const proxy = new Proxy(target, handler);
```

<br/>
<br/>

[Vue3为什么使用Proxy](https://vuejs.org/guide/essentials/reactivity-fundamentals.html#reactive-proxy-vs-original)

</div>
<div v-click>

## 写时拷贝（Copy On Write）

<br/>

<img src = "https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/21158ca9a4134b0f9a66247c9245c492~tplv-k3u1fbpfcp-zoom-in-crop-mark:3024:0:0:0.awebp" style = "width: 85%"/>

<img src = "https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/1b8044ca487240e8892214997aff7025~tplv-k3u1fbpfcp-zoom-in-crop-mark:3024:0:0:0.awebp" style = "width: 85%"/>

[Linux中的COW技术](https://juejin.cn/post/6844903702373859335)

</div>

</div>

<style>
h1 {
  color: rgb(238, 77, 45)
}
h2 {
  color: #1791f2
}
a {
  border-bottom-width: 0px !important;
  text-decoration: underline;
  color: #1791f2
}
a:hover {
  color: #1791f2 !important
}
</style>

<!--
那么immer是怎么实现不可变数据的呢？其实它主要使用了两个技术。一个是我们熟知的proxy对象，proxy的作用了和defineProperty方法很相似，我们定义一个原始对象，定义一个对象的拦截器，然后我们就可以对这个对象的操作进行拦截，这里我们就是对它的get操作进行拦截，那么无论我们访问message1还是message2，都会返回world字符串。immer使用proxy的目的就是拦截直接对原始对象的修改操作。像vue3的响应式系统就是依赖proxy进行实现。

另外一个叫做cow，奶牛技术。它是什么意思呢？一般啊，我们对对象进行复制的时候，就是对它进行深克隆，创建两份独立的内容。而cow技术，或者说策略的思想是，只用在写内容的时候才去复制对应的一部分内容。也就是说，我们对A对象进行浅克隆一份，内部的属性还是完全指向B对象，只有当需要修改B对象的属性的时候，我们再将这个属性对应的内容复制一份进行修改，当然其他地方依然是指向于a对象。cow的应用比较底层，像linux系统中的文件复制或者fork进程都会使用这个策略。
-->

