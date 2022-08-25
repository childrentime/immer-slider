# 关键代码

## API设计

<br/>
<br/>

```ts
export default function produce<T>(
  base: T,
  recipe: (draft: DeepWritable<T>) => void
): DeepReadonly<T>;

export default function produce(base: any, recipe: (draft: any) => void) {
  const proxy = createProxy(base);
  recipe(proxy);
  return finalize(proxy);
}
```


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
接下来呢我们就来具体的看一下immer是怎么实现的。这个是produce方法的api设计，当然这不是immer源代码里的，因为那个produce方法它的代码很多，他还支持柯里化模式，重载比较多。我们现在看到的这个是经过我简化的最小版本。它的过程只有简单的三步，第一步是对原始对象创建代理，第二步是将代理对象使用我们的修改函数执行，第三步是清理我们的代理对象，生成我们需要的下一个对象。
-->