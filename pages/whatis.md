# 什么是 Immer

Immer（德语为：always）是一个小型包，可让您以更方便的方式使用不可变状态。

<div class="grid grid-cols-2 gap-x-4">
<div>

## 不使用 Immer

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
<div>

## 使用 Immer

```ts
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


