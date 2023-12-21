# 过渡组件
## 官网参考
[vue官网-transition](https://cn.vuejs.org/guide/built-ins/transition.html#transition)
## 背景颜色的过渡变化
按键实现标题的展示,以及标题背景颜色的过渡变化
```html
<script setup>
import { ref } from 'vue';
const showText = ref(false);
</script>

<template>
  <main>
    <Transition name="color">
      <h1 v-if="showText">hello,world</h1>
    </Transition>
    <button @click="showText = !showText">Toggle</button>
  </main>
</template>

<style scoped>
.color-enter-from {
  background-color: yellow;
}

.color-enter-to {
  background-color: blue;
}

.color-enter-active {
  transition: all 2s ease;
}
</style>
```
## 淡入淡出
![](photo&pdf/Pasted%20image%2020231220222115.png)
```html
<style scoped>
.fade-enter-from {
  opacity: 0;
}

.fade-enter-to {
  opacity: 1;
}

.fade-enter-active {
  transition: all 0.5s ease;
}

.fade-leave-from {
  opacity: 1;
}
.fade-leave-to {
  opacity: 0;
}

.fade-leave-active {
  transition: all 1s ease;
}
</style>
```
### css 过渡 class
- `v-enter-from`：表示进入动画的起始状态。在元素插入之前添加，在元素插入完成后的下一帧移除。

- `v-enter-active`：表示进入动画的生效状态。应用于整个进入动画阶段。在元素被插入之前添加，在过渡或动画完成之后移除。可以用来定义进入动画的持续时间、延迟与速度曲线类型。

- `v-enter-to`：表示进入动画的结束状态。在元素插入完成后的下一帧被添加（也就是 `v-enter-from` 被移除的同时），在过渡或动画完成之后移除。

- `v-leave-from`：表示离开动画的起始状态。在离开过渡效果被触发时立即添加，在一帧后被移除。

- `v-leave-active`：表示离开动画的生效状态。应用于整个离开动画阶段。在离开过渡效果被触发时立即添加，在过渡或动画完成之后移除。可以用来定义离开动画的持续时间、延迟与速度曲线类型。

- `v-leave-to`：表示离开动画的结束状态。在一个离开动画被触发后的下一帧被添加（也就是 `v-leave-from` 被移除的同时），在过渡或动画完成之后移除。
淡入淡出动画和垂直平移动画:
```css
.v-enter-from, .v-leave-to {
  opacity: 0;
  transform: translateY(-20px);
}

.v-enter-active, .v-leave-active {
  transition: opacity 0.5s, transform 0.5s;
}

.v-enter-to, .v-leave-from {
  opacity: 1;
  transform: translateY(0);
}
```

# 过渡组件的限制
一个 `<transaction>` 每次只能渲染一个 `<h1>` 元素
## 按钮实现不同元素的过渡出现
```html
    <Transition name="fade">
      <h1 v-if="showText">hello,world</h1>
      <h1 v-else>byebye,world</h1>
    </Transition>
```
这样的问题在于过渡时,两个标题元素都会占据位置,元素和按钮的位置不固定,需要进行元素位置的固定.
![|300](photo&pdf/Pasted%20image%2020231220210732.png)
![|300](photo&pdf/Pasted%20image%2020231220210751.png)
### 位置固定后
```html
<template>
  <main>
    <div class="container">
      <Transition name="fade" class="trans">
        <h1 v-if="showText">hello,world</h1>
        <h1 v-else>byebye,world</h1>
      </Transition>
      <button @click="showText = !showText">Toggle</button>
    </div>
  </main>
</template>

<style scoped>
.container {
  position: relative;
}

.trans {
  position: absolute;
}

button {
  margin-top: 50px;
}
</style>
```
- 效果: 元素的位置不会变化,两个需要过渡的元素在同一个位置进行变化
![](photo&pdf/Pasted%20image%2020231220211303.png)
# 添加姓名卡片
![](photo&pdf/Pasted%20image%2020231220221816.png)
## css 设置
### 输入框
![](photo&pdf/Pasted%20image%2020231220212855.png)
```css
.container input {
  width: 100%;
  border-radius: 5px;
  border: 1px solid rgba(128, 128, 128, 0.13);
  padding: 10px;
  margin-bottom: 20px;
  box-shadow: 1px 1px 10px rgba(0, 0, 0, 0.12);
}
```
这段代码定义了 CSS 样式，适用于所有 `.container` 元素内部的 `input` 元素。以下是各个属性的解释：
* **border-radius: 5px;** - 设置输入框边框的圆角半径为 5px，使其呈现柔和的圆角效果。
* **border: 1px solid rgba(128, 128, 128, 0.13);** - 设置输入框的边框样式：
    * `1px`: 边框宽度为 1px。
    * `solid`: 边框类型为实线。
    * `rgba(128, 128, 128, 0.13)`: 边框颜色为半透明的灰色，透明度为 13%。
* **margin-bottom: 20px;** - 设置输入框下方的外边距为 20px，增加输入框之间的垂直间隔。
* **box-shadow: 1px 1px 10px rgba(0, 0, 0, 0.12);** - 设置输入框的阴影效果：
    * `1px 1px`: 阴影的偏移量，分别为水平和垂直方向的偏移。
    * `10px`: 阴影的模糊程度。
    * `rgba(0, 0, 0, 0.12)`: 阴影的颜色为半透明的黑色，透明度为 12%。

## 监听按键事件
### 键盘事件
在浏览器中，常用的键盘事件有：
1. `keydown`：当用户按下任意键时触发，按住不放会重复触发。
2. `keyup`：当用户释放键盘上的键时触发。
3. `keypress`：当用户按下字符键（包括字母、数字、符号等）时触发，按住不放会重复触发。但要注意的是，`keypress` 事件在实际应用中使用较少，因为它对于一些特殊键（如 Shift、Ctrl、Alt 等）的处理不够灵活，推荐使用 `keydown` 和 `keyup`。
这些事件通常与键盘的各种按键配合使用，包括字母、数字、功能键、控制键（Shift、Ctrl、Alt）、方向键等。
### 按键修饰符
`.enter`
`.tab`
`.delete` (捕获“Delete”和“Backspace”两个按键)
`.esc`
`.space`
`.up`
`.down`
`.left`
`.right`
`.ctrl`
`.alt`
`.shift`
`.meta`
### 例子
```html
<!-- 仅在 `key` 为 `Enter` 时调用 `submit` -->
<input @keyup.enter="submit" />

<input @keyup.page-down="onPageDown" />

<!-- Alt + Enter -->
<input @keyup.alt.enter="clear" />

<!-- Ctrl + 点击 -->
<div @click.ctrl="doSomething">Do something</div>
```
# 多个组件的统一过渡效果(TransitionGroup)
##  输入变成新卡片时的过渡效果
### TransitionGroup
```html
      <ul>
        <TransitionGroup name="invitees">
          <li v-for="name in names" :key="name">{{ name }}</li>
        </TransitionGroup>
      </ul>
```
### 淡入淡出和弹出效果
```css
.invitees-enter-from {
  opacity: 0;
  transform: scale(0.5);/*由窄变宽*/
}
.invitees-enter-to {
  opacity: 1;
  transform: scale(1);/*由窄变宽*/
}
.invitees-enter-active {
  transition: all 1s ease;
}
```
# 加入新卡片后旧卡片的下降动画(name-move)
```css
.invitees-move {
  transition: all 0.5s ease;
}
```
# 删除最新卡片时的上升迟钝
## 原因
删除一个项目时,它实际上仍然存在与文档流里面,直到过渡完成才删除.
## 解决方法
`eave-active` 属性添加绝对定位
```css
.invitees-leave-active {
  position: absolute;
}```

> [!NOTE] `enter-active` 不需要添加
> 
# 路由动画
实现切换主页面和 about 页面时,内容划动效果
```html
  <Transition name="route">
    <RouterView />
  </Transition>
```
```css
.route-enter-from {
  opacity: 0;
  transform: translateX(100px);
}

.route-enter-to {
  opacity: 1;
  transform: translateX(0);
}

.route-enter-active {
  transition: all 0.5s ease;
}
```
# quiz 卡片的出现过渡
## 卡片同时出现
```html
<Transition appear>
  ...
</Transition>
```
## 卡片依次出现(transitionDelay)
### css+绑定样式
```html
<TransitionGroup name="invitees" appear>
  <li
	v-for="(name, index) in names"
	:key="name"
	@click="DeleteName(name)"
	:style="{ transitionDelay: `${index * 0.2}s` }"
>
	{{ name }}
  </li>
</TransitionGroup>
```
> [!NOTE]  v-for 带上索引值
> `v-for="(name, index) in names"`
### 无 css+钩子函数+js

```html
<TransitionGroup
          appear
          @before-enter="onBeforeEnter"
          @enter="onEnter"
          @after-enter="onAfterEnter"
        >
          <li
            v-for="(name, index) in names"
            :key="name"
            @click="DeleteName(name)"
            :data-index="index"
          >
            {{ name }}
          </li>
        </TransitionGroup>
<script setup>
import { gsap } from 'gsap';
const onEnter = (el) => {
  //card-enter-to
  gsap.fromTo(
    el,
    { opacity: 0, scale: 0.5 },
    {
      opacity: 1,
      scale: 1,
      duration: 1.5,
      delay: el.dataset.index * 0.5,
    }
  );
  </script>
```
#### gap 包
- 传递 index 参数并使用
```js
:data-index="index"
delay: el.dataset.index * 0.5,
```

# 生命周期钩子-过渡
1. **`onBeforeEnter(el)`**: 在元素被插入到 DOM 之前调用。用于设置元素的 "enter-from" 状态。

2. **`onEnter(el, done)`**: 在元素被插入到 DOM 之后的下一帧被调用。用于开始进入动画。`done` 是一个回调函数，用于表示过渡结束。如果与 CSS 结合使用，`done` 回调是可选参数。

3. **`onAfterEnter(el)`**: 当进入过渡完成时调用。

4. **`onEnterCancelled(el)`**: 当进入过渡在完成之前被取消时调用。

5. **`onBeforeLeave(el)`**: 在 leave 过渡之前调用。大多数情况下，你应该只会用到 `leave` 钩子。

6. **`onLeave(el, done)`**: 在离开过渡开始时调用。用于开始离开动画。`done` 是一个回调函数，用于表示过渡结束。如果与 CSS 结合使用，`done` 回调是可选参数。

7. **`onAfterLeave(el)`**: 在离开过渡完成，且元素已从 DOM 中移除时调用。

8. **`onLeaveCancelled(el)`**: 仅在 `v-show` 过渡中可用，当离开过渡在完成之前被取消时调用。


```js
<Transition
  @before-enter="onBeforeEnter"
  @enter="onEnter"
  @after-enter="onAfterEnter"
  @enter-cancelled="onEnterCancelled"
  @before-leave="onBeforeLeave"
  @leave="onLeave"
  @after-leave="onAfterLeave"
  @leave-cancelled="onLeaveCancelled"
>
  <!-- ... -->
</Transition>
```

```js
// 在元素被插入到 DOM 之前被调用
// 用这个来设置元素的 "enter-from" 状态
function onBeforeEnter(el) {}

// 在元素被插入到 DOM 之后的下一帧被调用
// 用这个来设置元素的 "enter-to" 状态
function onEnter(el, done) {
  // 调用回调函数 done 表示过渡结束
  // 如果与 CSS 结合使用，则这个回调是可选参数
  done()
}

// 当进入过渡完成时调用。
function onAfterEnter(el) {}

// 当进入过渡在完成之前被取消时调用
function onEnterCancelled(el) {}

// 在 leave 钩子之前调用
// 大多数时候，你应该只会用到 leave 钩子
function onBeforeLeave(el) {}

// 在离开过渡开始时调用
// 用这个来开始离开动画
function onLeave(el, done) {
  // 调用回调函数 done 表示过渡结束
  // 如果与 CSS 结合使用，则这个回调是可选参数
  done()
}

// 在离开过渡完成、
// 且元素已从 DOM 中移除时调用
function onAfterLeave(el) {}

// 仅在 v-show 过渡中可用
function onLeaveCancelled(el) {}
```

# Gsap 插件