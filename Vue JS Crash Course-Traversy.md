# Intro & Slides
## 什么是 vue？
## 为什么使用 Vue？
# 7 :17 - User Generator Mini Project (CDN)
## v-bind
可以简写为`:data=" "`
```html
<img :class="gender" v-bind:src="picture" v-bind:alt=" `${firstName}`" />
```
## v-click
点击按钮实现功能
```html
<button v-on:click="getUser()" :class="gender">Get Random User </button>
```
## Button 更换数据
### 更换一次固定数据
通过 this.属性名更换值
```js
  methods: {
    getUser() {
      this.firstName = 'WuWei';
      this.email = 'wuwei0529@gmail.com';
      this.gender = 'female';
      this.picture = 'https://randomuser.me/api/portraits/women/10.jpg';
    },
  },
```
### 随机获取数据API
```js
methods: {
  // 定义一个异步方法 getUser，用于获取随机用户数据并更新Vue实例的数据
  async getUser() {
    // 使用 fetch 函数从指定API获取随机用户数据
    const res = await fetch('https://randomuser.me/api');
    // 将API响应转换为JSON格式
    const { results } = await res.json();

    // 更新Vue实例的数据属性，使用从API获取的随机用户信息
    this.firstName = results[0].name.first;
    this.email = results[0].email;
    this.gender = results[0].gender;
    this.picture = results[0].picture.large;
  },
},
```
# 21 :35 - Vue CLI Setup
任务追踪程序


24:30 - Files, Dev Server & Cleanup
28:22 - Global Styles
29:06 - Header Component
30:44 - Component Props
32:06 - Button Component
35:25 - Events
36:09 - Task Data & created() Method
38:22 - Tasks Component & v-for Loop
41:09 - Single Task Component
44:34 - Dynamic Classes
45:53 - Emit Events (Delete Task)
52:14 - Toggle Reminder
56:20 - AddTask Component & v-model
1:04:57 - Toggle Form & Template Conditionals
1:11:20 - Building For Production
1:13:33 - JSON-Server Setup
1:17:18 - Refactoring to Use The Backend
1:30:48 - Implementing the Router
1:48:23 - Restrict a Component to a Route