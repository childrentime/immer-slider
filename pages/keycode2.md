---
title: 关键代码
---

# 关键代码

## 原理流程图


<img src = "/flow.svg" style = "width: 100%"/>



<div style = "color: red" v-click>为什么要对Get的对象进行代理？</div>
<br/>
<div style = "color: red" v-click>为什么要有Modified属性？</div>


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
OK。我画了一个对象内部结构变更的图，来帮助我们理解immer是怎么做到这一点的。我们的目标呢是将这个对象中的c的值改为2，也就是 draft.a.b.c = 1。
首先我们有一个state对象，可以看到他这个对象啊，嵌套的层级非常深。那么我们首先对他创建代理，得到proxystate对象，它有四个属性，modified，是否被修改过，base指向我们的state对象，copy对象为空，parent对象为undidined。

然后我们会执行 Get a的操作，就是当你去修改这个对象的属性的时候，它会先去获取这个对象，这个是和AST抽象语法树有关系，当我们执行 draft.a.b.c = 1的时候，它实际上会先get draft对象的a属性，然后 get a对象的b属性，在 get b对象的c属性，我们拿到 c属性之后，再对 c属性执行 set操作。

所以这个我们 Get a对象的时候，我们也要对a对象进行同样地代理创建，因为只有这样我们才能捕获到对 a对象的 get 和 set操作。然后这个时候我们还需要做的一件事，就是把proxystate的base进行浅拷贝copy一份到copy对象中，然后将我们的copy.a指向这个a对象的代理。

所以我们为什么要对 get的对象进行代理呢，因为我们需要对所有的拦截操作进行捕获。state对象只可以拦截对ad的操作，感知不到对b的操作。

// 讲图
执行完成之后，我们还需要把代理的对象进行一个终结，也就是生成我们的下一个对象。我们怎么去生成呢，它是这样的，我们首先看这个对象的modified属性，如果为true，直接返回copy，如果为false，代表这个对象没有被修改过，我们就返回base。

// 讲图
所以modified属性实际上是为终结服务的，比如我们没有对对象的修改，它最后一层一层base返回的也就是原对象。

那么这个时候我们可以思考一下，如果d属性也是一个嵌套结构的话，这个时候它只是一层浅拷贝，实际上还指向原来的地址。那么通过这种方式，我们就实现了新对象和旧对象的结构共享，也就是只有修改的地方地址会发生变化，没修改的对象依然指向原来的地址，那么它的一个效率就会比深拷贝要好得多。

所以immer实际上是帮我们把手动的浅拷贝给隐藏掉了，让我们可以通过直接操作对象这种mutation的方式来获得不可变数据，非常的巧妙，也非常的简单，相对于其他的不可变数据库没有很重的心智负担。
-->
