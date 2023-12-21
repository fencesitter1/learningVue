
```toc
```
# VueCounterAPP
## 创建 vue 应用
```shell
npm create vue@latest


  cd CounterApp
  npm install
  npm run dev
```

## APP.vue
```html
<template>
  <main>
    <div class="counter">
      <h4>The current count is...</h4>
      <h1>{{ count }}</h1>
      <button @click="count--">-</button>
      <button @click="count++">+</button>
    </div>
  </main>
</template>

<script setup>
import { ref } from 'vue';
const count = ref(0);//定义state变量
</script>

<style scoped>
<style>
```
**几个要点**:
- `<template>`
- `<script setup>`
- `@click="count--"` , `count--` 相当于一个函数执行
- `<script setup>`:Vue.js 单文件组件（SFC）中的一部分，用于在组件中使用局部样式。这样做的目的是将样式限定在组件范围内，避免全局样式污染。

# Vue 基础
## 获取变量
`{{varaible}}`
## 事件处理
`@click=""`
## 定义状态变量
`ref`
```js
<script setup>
import { ref } from 'vue';
const count = ref(0);
const addCount = () => {
  count.value++;
};
const subCount = () => {
  count.value--;
};
</script>
```
# NotesAPP
## HTML 和 CSS 设置
- `flex-wrap`
```css
.card-container {
  display: flex;
  flex-wrap: wrap;
}
```
### 模态框的搭建
```html

<div class="overlay">
  <div class="modal">
	<textarea name="note" id="note" cols="20" rows="10"></textarea>
	<button>Add Note</button>
	<button class="close">Close</button>
  </div>
</div>

<style scoped>
.overlay {
  position: absolute;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.77);
  z-index: 100;
  display: flex;
  align-items: center;
  justify-content: center;
}
.modal {
  width: 500px;
  background-color: wheat;
  border-radius: 10px;
  padding: 30px;
  position: relative;
  display: flex;
  flex-direction: column;
}
</style>
```
## 模态框的展示(条件渲染)
### 功能实现
点击 Add button 出现模态框
#### v -if 和 v-show
v-if 是“真实的”按条件渲染，因为它确保了在切换时，条件区块内的事件监听器和子组件都会被销毁与重建。
v-if 也是惰性的：如果在初次渲染时条件值为 false，则不会做任何事。条件区块只有当条件首次变为 true 时才被渲染。
相比之下，v-show 简单许多，元素无论初始条件如何，始终会被渲染，只有 CSS display 属性会被切换。
总的来说，v-if 有更高的切换开销，而 v-show 有更高的初始渲染开销。因此，如果需要频繁切换，则使用 v-show 较好；如果在运行时绑定条件很少改变，则 v-if 会更合适。
## 表单数据的存储/读取
输入的表单数据传入变量
```html
<script setup>

</script>

<template>

</template>
```

```html
<script setup>
const newNote = ref(' ');
</script>

<template>
<textarea
v-model="newNote"
name="note"
id="note"
cols="20"
rows="10"
></textarea>
</template>
```
### v-model
## 事件处理:存储新的 Note 
通过 addnote button 实现新的笔记数据的存储
```html
<script setup>
const notes = ref([]);
const addNote = () => {
  notes.value.push({
    id: Math.floor(Math.random() * 100000),
    text: newNote.value,
    data: new Date().toDateString(),
    backgroundColor: generateRandomLightColor(),
  });
  showModal.value = false;
  newNote.value = '';
};
</script>

<template>
<button @click="addNote()">Add Note</button>
</template>
```
注意点:
- 一般都是变量.value 赋值
- data: `new Date().toDateString()`:生成最新时期和时间
- 监听事件: `v-on:click="handler"` 或 `@click="handler"`。
## v-for 渲染 note 数据对应的卡片

```html
<script setup>

</script>

<template>
<div
	  class="card"
	  v-for="note in notes"
	  :style="{ backgroundColor: note.backgroundColor }"
>
	  <p class="main-text">
		{{ note.text }}
	  </p>
	  <p class="date">{{ note.date }}</p>
</template>
```
### v-for(迭代生成内容)
### : key(特殊 attribute)
key 这个特殊的 attribute 主要作为 Vue 的虚拟 DOM 算法提示，在比较新旧节点列表时用于识别 vnode。
在没有 key 的情况下，Vue 将使用一种最小化元素移动的算法，并尽可能地就地更新/复用相同类型的元素。如果传了 key，则将根据 key 的变化顺序来重新排列元素，并且将始终移除/销毁 key 已经不存在的元素。
同一个父元素下的子元素必须具有唯一的 key。重复的 key 将会导致渲染异常。
最常见的用例是与 v-for 结合：
```html
<div
	class="card"
	v-for="note in notes"
	:key="note.id"
	:style="{ backgroundColor: note.backgroundColor }"
>
```
> [!important] 重要性
>体现在删除数组中的某个元素
### :style(绑定内联样式)
## 错误提示
```html
<script setup>
const errorMessage = ref('');
const addNote = () => {
  if (newNote.value.trim().length < 10) {//
    toast.info('Note needs to be characters or more');//
    return (errorMessage.value = 'Note needs to be characters or more');//
  }
  notes.value.push({
    id: Math.floor(Math.random() * 100000),
    text: newNote.value,
    date: new Date().toDateString('en-US'),
    backgroundColor: generateRandomLightColor(),
  });
  showModal.value = false;
  newNote.value = '';
  errorMessage.value = '';
};
</script>

<template>

</template>
```
### 修正字符串前后的空格
1. `newNote.value.trim()`
2. `v-model.tirm=newNote`

# Quiz APP
## HTML CSS

> [!NOTE] 小技巧
> `div.container` 会自动生成 `<div class="container"> </div>`
### 卡片横排自动添加(flex-wrap)
```html
<script setup>

</script>

<template>

</template>
```

```html
<script setup>

</script>

<template>
<div class="options-container">
  <div v-for="quiz in quizs" :key="quiz.id" class="card">
	<img :src="quiz.img" alt="" />
	<div class="card-text">
	  <h2>{{ quiz.name }}</h2>
	  <p>15 questions</p>
	</div>
  </div>
</div>
</template>

<style scoped>
.options-container {
  display: flex;
  flex-wrap: wrap;
  margin-top: 40px;
}
</style>
```
####  `<img :src="quiz.img" alt="" />`
## 显示 search 匹配的内容(watch)
- watch
侦听一个或多个响应式数据源，并在数据源变化时调用所给的回调函数。
常用于与响应式数据同时变化的变量.
有两种形式:
```html
<script setup>
import q from './data/quizes.json';
import { ref, watch } from 'vue';
const quizs = ref(q);
const search = ref('');

watch(search, () => {
  quizs.value = q.filter((quiz) =>
quiz.name.toLowerCase().includes(search.value.toLowerCase())
  );
  //或者是()=>ref("").value
watch( ()=>search.value, () => {
  quizs.value = q.filter((quiz) =>
quiz.name.toLowerCase().includes(search.value.toLowerCase())
  );
});
</script>
```
- 一些参考:
[watch/computed/watchEffect的区别](https://juejin.cn/post/7306266546968887311?searchId=20231215223145CF51ECA3C9AA44CCC765)
## 父组件传递数据至子组件(props)
- 父组件 APP.vue
```html
<script setup>
import Card from './components/Card.vue';
</script>

<template>
<Card :quizs="quizs" />
<!--使用子组件,并传递quizs参数-->
</template>
```
- 子组件 card.vue
```html
<template>
  <div v-for="quiz in props.quizs" :key="quiz.id" class="card">
    <img :src="quiz.img" alt="" />
    <div class="card-text">
      <h2> {{ quiz.name }} </h2>
      <p>{{ quiz.questions.length }} questions</p>
    </div>
  </div>
</template>

<script setup>
import { defineProps } from 'vue';
const props = defineProps(['quizs']);
<!--使用props传递变量-->
</script>
```
## 跳转新页面(Vue-router)
### 安装 vue-router
`npm install vue-router`
### 定义 router-rules
```js
// Define our routing rules
import { createRouter, createWebHistory } from 'vue-router';
import HomeQuizs from '../views/HomeQuizs.vue';
const router = createRouter({
  history: createWebHistory(import.meta.env.BASE_URL),
  routes: [
    {
      path: '/',
      name: 'quizs',
      component: HomeQuizs,
    },
    {
      path: '/home',
      redirect: '/',
    },
  ],
});

export default router;
```
### main .js 设置
```js
import './assets/main.css';
import { createApp } from 'vue';
import App from './App.vue';
import router from './router/index';
const app = createApp(App);
app.use(router);
app.mount('#app');
```
### 主页面 -->RouterView
APP.vue
```html
<template>
  <div class="container">
    <RouterView></RouterView>
    <!-- <HomeQuizs></HomeQuizs> -->
  </div>
</template>

<script setup>
import HomeQuizs from './views/HomeQuizs.vue';
import { RouterView } from 'vue-router';
</script>

<style scoped>
.container {
  max-width: 1300px;
  margin: 0 auto;
}
</style>
```
### 卡片可点击化,生成单独路由地址
`navigateToQuiz` 函数
```html
<template>
  <div class="card" @click="navigateToQuiz(quiz)">
    <img :src="quiz.img" alt="" />
    <div class="card-text">
      <h2>{{ quiz.name }}</h2>
      <p>{{ quiz.questions.length }} questions</p>
    </div>
  </div>
</template>

<script setup>
import { defineProps } from 'vue';
import { useRouter } from 'vue-router';
const props = defineProps(['quiz']);
const router = useRouter();
const navigateToQuiz = (quiz) => {
  router.push(`/quiz/${quiz.id}`);
};
</script>
```
- **注意点**:区别于 [[#具有动态地址的页面]]中的 [RouterLink和v-for](#^d33b37) 方法
## 单独测验页面(QuizView)
分为 Questions.vue 和 QuizHeader.vue 两个组件
### 单独卡片的 html 和 css 设置
### 传递 props 给子组件
### 监听生成派生数据 (watch,computed )
#### 进度条数据(barPercentage)(:style)
```js
const barPercentage = computed(
  () => `${((curQuestionIndex.value + 1) / questionLength) * 100}%`
);
```
- QuizHeader.vue
`:style="{ width: props.barPercentage }"` 的形式
```html
<script setup>
import { defineProps } from 'vue';
const props = defineProps(['questionStatus', 'barPercentage']);
</script>
<template>
  <h1>QuizView</h1>
  <header>
    <h3>Question {{ questionStatus }}</h3>
    <div class="bar">
    <div class="completion" :style="{ width: props.barPercentage }"></div>
    </div>
  </header>
</template>
<style>
.completion {
  height: 100%;
  width: 0%;
  background-color: bisque;
}
</style>
```
### 点击答案切换下一题(emits)
### 答完显示结果组件(v-if 和v-else)
# 页面和路由

## 添加路由(createRouter,createWebHistory)
- 在 router/index.js
```js
// Define our routing rules
import { createRouter, createWebHistory } from 'vue-router';
import HomeView from '../views/HomeView.vue';
import AboutView from '../views/AboutView.vue';
import CarView from '../views/CarView.vue';
import ContactView from '../views/ContactView.vue';
import NotfoundView from '../views/NotfoundView.vue';
const router = createRouter({
  history: createWebHistory(import.meta.env.BASE_URL),
  routes: [
    {
      path: '/',
      name: 'home',
      component: HomeView,
    },
    {
      path: '/home',
      redirect: '/',
    },
    {
      path: '/about',
      name: 'about',
      component: AboutView,
    },
    {
      path: '/cars/:id',
      name: 'car',
      component: CarView,
      children: [
        {
          path: 'contact',
          name: 'conatact',
          component: ContactView,
        },
      ],
    },
    {
      path: '/:pathMatch(.*)*',
      name: 'Notfound',
      component: NotfoundView,
    },
  ],
});

export default router;

```
- APP.vue
```html
<template>
  <div>
    <Nav></Nav>
    <RouterView></RouterView>
  </div>
</template>

<script setup>
import HomeView from './views/HomeView.vue';
import AboutView from './views/AboutView.vue';
import Nav from './components/Nav.vue';
import CarView from './views/CarView.vue';
import { RouterView } from 'vue-router';
</script>
```
## 路由链接(router-link)
- router-link
请注意，我们没有使用常规的 a 标签，而是使用一个自定义组件 router-link 来创建链接。这使得 Vue Router 可以在**不重新加载页面**的情况下更改 URL，处理 URL 的生成以及编码。
- Nav.vue
```html
<template>
  <div>
    <RouterLink to="/" active-class="active">Home</RouterLink>
    <RouterLink to="/about" active-class="active">About</RouterLink>
  </div>
</template>

<script setup>
import { RouterLink } from 'vue-router';
</script>
```
### router-link 样式
**active-class**
- Nav.vue
```html
<style scoped>
.active {
  font-weight: 900;
  color: rgb(219, 149, 19);
}
</style>
```
![|500](photo&pdf/Pasted%20image%2020231215182351.png)
## 具有动态地址的页面
index.js 中设置`:id`
```js
{
      path: '/cars/:id',
      name: 'car',
      component: CarView,
      children: [
        {
          path: 'contact',
          name: 'conatact',
          component: ContactView,
        },
      ],
    },
```
HomeView.vue
```html
<template>
  <div>
    <h1>home view</h1>
    <div class="cars">
      <RouterLink
        :to="`/cars/${car.id}`"
        v-for="car in cars"
        :key="car.id"
        href=""
      >
        {{ car.name }}
      </RouterLink>
    </div>
  </div>
</template>

<script setup>
import cars from '../data/cars.json';
import { RouterLink } from 'vue-router';
</script>

<style scoped>
.cars {
  display: flex;
}
.cars a {
  text-decoration: none;
  color: black;
  font-size: 25px;
  box-shadow: 1px 1px 10px rgba(0, 0, 0, 0.388);
  margin: 10px;
}
</style>
```

^d33b37

效果:
![](photo&pdf/Pasted%20image%2020231215185206.png)
## 提取路由地址参数(route.params.id)
- CarView.vue
```html
<template>
  <div>
    <h1>Car View</h1>
    <p>{{ car.name }}</p>
    <p>{{ car.price }}</p>
  </div>
</template>

<script setup>
import { useRoute } from 'vue-router';
import cars from '../data/cars.json';
const route = useRoute();
const car = cars.find((c) => c.id == parseInt(route.params.id));
console.log(car);
</script>
```

## 嵌套子路由(children:[{path}])
- index.js
```js
{
      path: '/cars/:id',
      name: 'car',
      component: CarView,
      children: [
        {
          path: 'contact',
          name: 'conatact',
          component: ContactView,
        },
      ],
    },
```
- CarView.vue
```html
<template>
  <div v-if="car">
    <h1>Car View</h1>
    <p>{{ car.name }}</p>
    <p>{{ car.price }}</p>
    <button @click="router.push(`/cars/${carId}/contact`)">
      Click for cotact
    </button>
    <RouterView></RouterView>
    <!--这里注意--->
  </div>
  <div v-else>
    <h1>Car not found</h1>
  </div>
</template>

<script setup>
import { useRoute, useRouter, RouterView } from 'vue-router';
import cars from '../data/cars.json';
const route = useRoute();
const router = useRouter();
console.log(router);
const car = cars.find((c) => c.id == parseInt(route.params.id));
const carId = parseInt(route.params.id);
</script>
```
- **注意点**:当有嵌套路由时,父路由对应的父组件需要插入 `<RouterView></RouterView>`.
## 按钮实现地址跳转(useRouter)
```html
<template>
  <div>
    <button @click="router.push(`/cars/${carId}/contact`)">
      Click for cotact
    </button>
    <RouterView></RouterView>
  </div>
</template>

<script setup>
import { useRoute, useRouter, RouterView } from 'vue-router';
import cars from '../data/cars.json';
const route = useRoute();
const router = useRouter();
console.log(router);
const car = cars.find((c) => c.id == parseInt(route.params.id));
const carId = parseInt(route.params.id);
</script>
```
## 404NotFound
- index.js
```js
const router = createRouter({
  history: createWebHistory(import.meta.env.BASE_URL),
  routes: [
    // ...其他路由规则
    {
      path: '/:pathMatch(.*)*',
      name: 'Notfound',
      component: NotfoundView,
    },
  ],
});
```
在这个示例中，当用户访问任何未匹配到的路径时，会被路由规则 `{ path: '/:pathMatch(.*)*', name: 'NotFound', component: NotFound }` 捕获。然后，会渲染 NotFound 组件，显示 "404 Not Found" 页面的内容。

## 路由重定向(redirect)
```js
const router = createRouter({
history:createWebHistory(import.meta.env.BASE_URL),
  routes: [
  {
     path: '/home',
     redirect: '/',
    },
 ]
});
```


# 过渡相关的 JavaScript 钩子
