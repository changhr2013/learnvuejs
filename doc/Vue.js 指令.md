Vue.js常用指令
===
指令 (Directives) 是带有 `v-` 前缀的特殊属性。指令属性的值预期是单个 JavaScript 表达式 (`v-for` 是例外情况，稍后我们再讨论)。指令的职责是，当表达式的值改变时，将其产生的连带影响，响应式地作用于 DOM。

1. `v-if` & `v-else` & `v-elseif`

```
<p v-if="seen">现在你看到我了</p>
```
`v-else-if` 表示 `v-if` 的 “else if 块”。可以链式调用。
```
<div v-if="type === 'A'">
  A
</div>
<div v-else-if="type === 'B'">
  B
</div>
<div v-else-if="type === 'C'">
  C
</div>
<div v-else>
  Not A/B/C
</div>
```

2. `v-show`

根据表达式之真假值，切换元素的 `display` CSS 属性。

当条件变化时该指令触发过渡效果。

3. `v-for`
基于源数据多次渲染元素或模板块。此指令之值，必须使用特定语法 `alias in expression` ，为当前遍历的元素提供别名：
```
<div v-for="item in items">
  {{ item.text }}
</div>
```
`v-for` 默认行为试着不改变整体，而是替换元素。迫使其重新排序的元素，你需要提供一个 `key` 的特殊属性：
```
<div v-for="item in items" :key="item.id">
  {{ item.text }}
</div>
```
另外也可以为数组索引指定别名 (或者用于对象的键)：
```
<div v-for="(item, index) in items"></div>
<div v-for="(val, key) in object"></div>
<div v-for="(val, key, index) in object"></div>
```

4. `v-text`
更新元素的 `textContent`。如果要更新部分的 `textContent` ，需要使用 `{{ Mustache }}` 插值。
```
<span v-text="msg"></span>
<!-- 和下面的一样 -->
<span>{{msg}}</span>
```

5. `v-html`

```
<span v-html="rawHtml"></span>
```

6. `v-on`

```
<!-- 完整语法 -->
<a v-on:click="doSomething">...</a>

<!-- 缩写 -->
<a @click="doSomething">...</a>
```
用于监听 DOM 事件：
```
<a v-on:click="doSomething">...</a>
```

7. `v-model`
在表单控件或者组件上创建双向绑定。  
修饰符：  
+ `.lazy` - 取代 `input` 监听 `change` 事件
+ `.number` - 输入字符串转为数字
+ `.trim` - 输入首尾空格过滤

8. `v-bind`

```
<!-- 完整语法 -->
<a v-bind:href="url">...</a>

<!-- 缩写 -->
<a :href="url">...</a>
```
在布尔特性的情况下，它们的存在即暗示为 `true`，`v-bind` 工作起来略有不同，在这个例子中：  
```
<button v-bind:disabled="isButtonDisabled">Button</button>
```
如果 `isButtonDisabled` 的值是 `null`、`undefined` 或 `false`，则 `disabled` 特性甚至不会被包含在渲染出来的 `<button>` 元素中。

9. `v-pre`

将内容原样输出
```
<p v-pre>{{message}}</p>
```

10. `v-cloak`

延迟渲染

11. `v-once`

```
<span v-once>这个将不会改变: {{ msg }}</span>
```
