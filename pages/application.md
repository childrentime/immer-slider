# 不可变数据有什么用


<div class="grid grid-cols-2 gap-x-4">
<div v-click>

## 时光回溯
<br/>
<img src="https://pic4.zhimg.com/80/v2-62b9585b6fa768b1d6fb141beb3dd2b3_1440w.jpg"/>
<br/>
<br/>
<img src="https://pic4.zhimg.com/80/v2-86b9a4b3025069bebeebdfb42fe6a957_1440w.jpg"/>
<br/>

[在Vue3中使用](https://cn.vuejs.org/guide/extras/reactivity-in-depth.html#integration-with-external-state-systems)
</div>

<div v-click>

## React Diff算法

<img src = "https://media.geeksforgeeks.org/wp-content/cdn-uploads/20220131100246/Group-2-2.jpg"/>

<br/>
<br/>
<br/>

[在React中使用](https://media.geeksforgeeks.org/wp-content/cdn-uploads/20220131100246/Group-2-2.jpg)
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
接下来让我们看看不可变数据的作用。第一个作用是时光回溯，比如google文档一般有个历史版本的功能，我们可以任意地回退到某个版本，那么显然用不可变数据来记录对象状态的变更是非常合适的。

其次的一个应用是在react中，react在进行diff算法的某一过程中会对比两个结点的地址是否相同。
当然其实不可变数据这个概念就是react推行起来的。
-->
