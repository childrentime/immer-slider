# 不可变数据实现方式

<div class="grid grid-cols-2 gap-x-4">
<div v-click>

## 浅拷贝

```ts
const baseState = [
  {
    title: "Learn TypeScript",
    done: true,
  },
  {
    title: "Try Immer",
    done: false,
  },
];

const nextState = baseState.slice(); // 浅拷贝数组
nextState[1] = {
  // 替换第一层元素
  ...nextState[1], // 浅拷贝第一层元素
  done: true, // 期望的更新
};
// 因为 nextState 是新拷贝的, 所以使用 push 方法是安全的,
// 但是在未来的任意时间做相同的事情会违反不变性原则并且导致 bug！
nextState.push({ title: "Tweet about it" });
```

</div>
<div v-click>

## Immer

```ts {14-17}
import produce from "immer";

const baseState = [
  {
    title: "Learn TypeScript",
    done: true,
  },
  {
    title: "Try Immer",
    done: false,
  },
];

const nextState = produce(baseState, (draft) => {
  draft[1].done = true;
  draft.push({ title: "Tweet about it" });
});
```

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

<!--那么我们怎么来实现不可变数据结构呢，一个很直接的想法是，我们将去浅拷贝每层受我们更改影响的 state 结构，可以看到这是非常繁琐和麻烦的。或者我们也可以直接使用深拷贝，但是也许我们并不会去改变对象的所有属性，因此深拷贝的效率是非常低的。所以这个immer就出现了，来解决这个问题。
使用immer的好处是，我们可以简单地通过修改临时drart来达到我们想要的目的。也就是说，这个nextstate中，它的第二项和原来的basestate是相同的，而一三项被修改过的是不同的，immer让我们可以精确地作出修改。当然也有其他的不可变数据结构实现方式，比如facebook出的immutablejs，但是这个现在用的不多了。然后immer也是非常简单的，基本上我们只需要使用produce这一个api就够了，它接受一个基本状态，一个对草稿修改的函数并且返回一个新的结果。这就是它的核心api。
-->
