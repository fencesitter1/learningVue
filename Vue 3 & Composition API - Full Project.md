**Contents**

1. [目录](#%E7%9B%AE%E5%BD%95)
1. [3 :21 - Vue.Js Setup](#3-21---vuejs-setup)
	1. [选择文件](#%E9%80%89%E6%8B%A9%E6%96%87%E4%BB%B6)
	1. [9 :06 - Create Component Files & Templates](#9-06---create-component-files--templates)
1. [12 :30 - Create and import Components](#12-30---create-and-import-components)
	1. [如何使用自定义的组件内容 ?](#%E5%A6%82%E4%BD%95%E4%BD%BF%E7%94%A8%E8%87%AA%E5%AE%9A%E4%B9%89%E7%9A%84%E7%BB%84%E4%BB%B6%E5%86%85%E5%AE%B9-)
	1. [实现悬浮才出现的删除按钮](#%E5%AE%9E%E7%8E%B0%E6%82%AC%E6%B5%AE%E6%89%8D%E5%87%BA%E7%8E%B0%E7%9A%84%E5%88%A0%E9%99%A4%E6%8C%89%E9%92%AE)
	1. [html 的输入框](#html-%E7%9A%84%E8%BE%93%E5%85%A5%E6%A1%86)
	1. [18 :50 - TransactionList Display](#18-50---transactionlist-display)
		1. [定义数据](#%E5%AE%9A%E4%B9%89%E6%95%B0%E6%8D%AE)
		1. [循环读取和显示数据](#%E5%BE%AA%E7%8E%AF%E8%AF%BB%E5%8F%96%E5%92%8C%E6%98%BE%E7%A4%BA%E6%95%B0%E6%8D%AE)
1. [28 :37 - Transactions in Global State](#28-37---transactions-in-global-state)
1. [响应式状态](#%E5%93%8D%E5%BA%94%E5%BC%8F%E7%8A%B6%E6%80%81)
	1. [ref](#ref)
1. [30 :12 - Pass & Recieve Props (defineProps)](#30-12---pass--recieve-props-defineprops)
	1. [defineProps](#defineprops)
	1. [例子:变量传入组件](#%E4%BE%8B%E5%AD%90%E5%8F%98%E9%87%8F%E4%BC%A0%E5%85%A5%E7%BB%84%E4%BB%B6)
1. [32 :30 - Balance Component & computed()](#32-30---balance-component--computed)
	1. [代码](#%E4%BB%A3%E7%A0%81)
	1. [computed()](#computed)
1. [37 :21 - Income & Expenses Component](#37-21---income--expenses-component)
	1. [props 传入多个属性](#props-%E4%BC%A0%E5%85%A5%E5%A4%9A%E4%B8%AA%E5%B1%9E%E6%80%A7)
	1. [筛选大于0的部分](#%E7%AD%9B%E9%80%89%E5%A4%A7%E4%BA%8E0%E7%9A%84%E9%83%A8%E5%88%86)
1. [42 :34 - AddTransaction Form Component](#42-34---addtransaction-form-component)
	1. [表单提交监听](#%E8%A1%A8%E5%8D%95%E6%8F%90%E4%BA%A4%E7%9B%91%E5%90%AC)
1. [44 :58 - Binding Form Inputs](#44-58---binding-form-inputs)
	1. [具体实现](#%E5%85%B7%E4%BD%93%E5%AE%9E%E7%8E%B0)
	1. [监听输入 v-model](#%E7%9B%91%E5%90%AC%E8%BE%93%E5%85%A5-v-model)
1. [46 :41 - Validation & Toasts](#46-41---validation--toasts)
	1. [vue-toastification](#vue-toastification)
		1. [使用](#%E4%BD%BF%E7%94%A8)
		1. [提示设置](#%E6%8F%90%E7%A4%BA%E8%AE%BE%E7%BD%AE)
1. [52 :05 - Emit Custom Events (defineEmits)](#52-05---emit-custom-events-defineemits)
	1. [Emit](#emit)
1. [54 :45 - Add Transaction to State](#54-45---add-transaction-to-state)
	1. [案例 :emit+监听](#%E6%A1%88%E4%BE%8B-emit%E7%9B%91%E5%90%AC)
		1. [案例说明](#%E6%A1%88%E4%BE%8B%E8%AF%B4%E6%98%8E)
1. [59 :30 - Deleting Transactions](#59-30---deleting-transactions)
	1. [实现](#%E5%AE%9E%E7%8E%B0)
1. [Fetch From Local Storage & OnMounted() &Save to Local Storage](#fetch-from-local-storage--onmounted-save-to-local-storage)

# 目录

Timestamps: 
0:00 - Intro & Demo
# 3 :21 - Vue.Js Setup
```shell
npm create vue@latest

✔ Project name: … <your-project-name>
✔ Add TypeScript? … No / Yes
✔ Add JSX Support? … No / Yes
✔ Add Vue Router for Single Page Application development? … No / Yes
✔ Add Pinia for state management? … No / Yes
✔ Add Vitest for Unit testing? … No / Yes
✔ Add an End-to-End Testing Solution? … No / Cypress / Playwright
✔ Add ESLint for code quality? … No / Yes
✔ Add Prettier for code formatting? … No / Yes

> cd <your-project-name>
> npm install
> npm run dev
```

## 选择文件
ctrl +click
shift+第一个文件,shift+最后一个文件 ==> 选择其中的全部文件
4:57 - File Structure
7:44 - Boilerplate Clean Up
## 9 :06 - Create Component Files & Templates
根据网页的需要添加不同功能分区的 Vue 文件
![|320](photo&pdf/Pasted%20image%2020231208151138.png)
![](photo&pdf/Pasted%20image%2020231208151609.png)
# 12 :30 - Create and import Components
## 如何使用自定义的组件内容 ?
导入+注册
1. 写法1:选项式 API 写法
```html
<template>
  <Header />
</template>

<script>
// 导入名为 Header 的组件
import Header from './components/Header.vue';
// 在组件中注册 Header 组件
export default {
  components: {
    Header,
  },
};
</script>
```
2.组合式 API
```html
<script setup>
// 导入名为 Header 的组件
import Header from './components/Header.vue';
</script>
```
无需注册,直接导入
**法2:懒加载**
`懒加载`（Lazy Loading）是一种在需要的时候再加载资源的策略，而不是在页面加载时一次性加载所有资源。
```html
<script>
export default {
  components: {
    Header: () => import('./components/Header.vue'),
  },
};
//会报错,需要用到异步组件
</script>

<script>
//第一种写法:异步组件 选项式API
import { defineAsyncComponent } from 'vue';
export default {
  components: {
    Header:defineAsyncComponent(() => import('./components/Header.vue')),
    Balance:defineAsyncComponent(()=>import('./components/Balance.vue')),
  },
};
</script>


<script setup>
//第二种写法:组合式API
import { defineAsyncComponent } from 'vue';
const Header = defineAsyncComponent(() => import('./components/Header.vue'));
const Balance = defineAsyncComponent(() => import('./components/Balance.vue'));
</script>
```
这种方式在用户访问该组件时才会下载和解析相应的组件代码。
[vue3异步组件]( https://cn.vuejs.org/guide/components/async.html
## 实现悬浮才出现的删除按钮
```css
.delete-btn {
  cursor: pointer;            
  background-color: #e74c3c;  
  border: 0;                   
  color: #fff;                 
  font-size: 20px;             
  line-height: 20px;           
  padding: 2px 5px;            
  position: absolute;          /* 使用绝对定位 */
  top: 50%;                    /* 位于父容器顶部的50%位置 */
  left: 0;                     /* 位于父容器的最左边 */
  transform: translate(-100%, -50%);  /* 将按钮向左平移100%（自身宽度），向上平移50%（自身高度的一半），使其位于父容器的左上角 */
  opacity: 0;                  /* 初始透明度为0，即隐藏 */
  transition: opacity 0.3s ease;     /* 添加过渡效果，当透明度改变时，过渡时间为0.3秒，过渡效果为 ease */
}

/* 当鼠标悬浮在列表项上时，显示删除按钮 */
.list li:hover .delete-btn {
  opacity: 1;  /* 当鼠标悬浮在列表项上时，将删除按钮的透明度设为1，即显示出来 */
}
```
## html 的输入框
- 数字输入框
- ![](photo&pdf/Pasted%20image%2020231208170711.png)
```html
  <input type="number" id="amount" placeholder="Enter amount..." />
```
## 18 :50 - TransactionList Display
### 定义数据
```js
//选项式API
export default {
  data() {
    return {
      transactions: [
        { id: 1, text: 'Flower', amount: -19.99 },
        { id: 2, text: 'Salary', amount: 299.97 },
        { id: 3, text: 'Book', amount: -10 },
        { id: 4, text: 'Camera', amount: -150 },
      ],
    };
  },
};

//组合式API
<script setup>
const transactions = [
  { id: 1, text: 'Flower', amount: -19.99 },
  { id: 2, text: 'Salary', amount: 299.97 },
  { id: 3, text: 'Book', amount: -10 },
  { id: 4, text: 'Camera', amount: -150 },
];
</script>
```
### 循环读取和显示数据
涉及指令: `v-for="循环"` ; `:key=" "`
```html
<template>
  <h3>History</h3>
  <ul id="list" class="list">
    <li
      v-for="t in props.transactions"
      v-bind:key="t.id"
      :class="t.amount < 0 ? 'minus' : 'plus'"
    >
      {{ t.text }} <span>${{ t.amount }}</span
      ><button @click="deleteTransaction" class="delete-btn">x</button>
    </li>
  </ul>
</template>

<script setup>
import { defineProps } from 'vue';
// const props = defineProps({
//   transactions: {
//     type: Array,
//     required: true,
//   },
// });
const props = defineProps(['transactions']);
console.log(props.transactions);
</script>
```

> [!warning] 父组件和子组件的 transactions 属性区别
> 父组件中是 ref 对象 RefImpl,调用数组需要 `transactions.value`
> 子组件中是 `Proxy(Array) {0: {…}, 1: {…}, 2: {…}, 3: {…}}`,直接 `transactions`
77 

# 28 :37 - Transactions in Global State
# 响应式状态
## ref
`ref` 是 Vue 3 中用于创建响应式数据的函数。它有两个主要用途：
1. **创建响应式数据：** 使用 `ref` 可以将普通的 JavaScript 数据变成响应式数据。这意味着当数据发生变化时，与该数据相关的视图会自动更新。
2. **访问和修改数据：** 通过 `ref` 创建的响应式数据实际上是一个包装对象，它有一个 `value` 属性，通过 `ref` 返回的对象上的 `value` 属性是存储数据的地方。你可以直接读取和修改 `value` 属性来访问和修改数据。
下面是一个简单的使用示例：
```javascript
import { ref } from 'vue';
// 创建一个响应式数据
const count = ref(0);
// 读取数据
console.log(count.value); // 输出: 0
// 修改数据
count.value += 1;
console.log(count.value); // 输出: 1
```
在上述例子中，`count` 是一个包含响应式数据的对象。我们可以通过 `count.value` 来访问和修改数据。

在组合式 API 中，`ref` 主要用于在 `setup` 函数中创建和管理组件的响应式数据。例如，在 `setup` 中使用 `ref` 定义数据：
```html
<script setup>
import { ref } from 'vue';

// 创建响应式数据
const message = ref('Hello, Vue!');
</script>
```
在模板中，你可以直接使用 `message`，而不需要使用 `message.value`：
```vue
<template>
  <div>{{ message }}</div>
</template>
```

# 30 :12 - Pass & Recieve Props (defineProps)
**功能实现**:父组件向子组件传变量
## defineProps
在使用 `<script setup>` 的单文件组件中，props(属性) 可以使用 `defineProps()` 宏来声明
有两种形式定义:
1. 对象形式
```js
const props=defineProps({
  title: String,
  likes: Number
})
```
2. 数组
```js
const props = defineProps(['foo'])
```

> [!warning] 
>defineProps 一定得加`[ ]`

## 例子:变量传入组件
- APP.Vue 内
```html
<TransactionList :transactions="transactions" />
```
transactions 是父组件中的数据
- TransactionList.Vue 内
```html
<script setup>
import { defineProps } from 'vue';
//1.
const props = defineProps({
  transactions: {
    type: Array,
    required: true,
  },
})
//2.
const props = defineProps(['transactions']);
</script>
```
# 32 :30 - Balance Component & computed()
## 代码
Balance.vue
```html
<template>
  <h4>Your Balance</h4>
  <h1 id="balance">${{ props.total.toFixed(2) }}</h1>
</template>

<script setup>

import { defineProps } from 'vue';
const props = defineProps(['total']);
console.log(props);
</script>
```

> [!NOTE] 建议:使用 props.total
> 保留响应性

> [!NOTE] 保留小数点两位
> `number.toFixed(2)`

APP.vue
```html
<template>
  <div class="container">
    <Balance :total="total"/>
  </div>
</template>

<script setup>
import { defineAsyncComponent, ref, computed } from 'vue';
const total = computed(() =>
  transactions.value.reduce((acc, transaction) => acc + transaction.amount, 0)
);
console.log(total);
</script>
```
## computed()
在 Vue.Js 中，`computed` 是一个用于创建计算属性的辅助函数。计算属性是一种依赖于其他属性值并动态计算得出的属性。使用 `computed` 可以方便地定义这样的属性。
在 Vue 3 中，由于使用了 Composition API，计算属性可以通过 `computed` 函数来创建。以下是一个简单的示例：
```vue
<template>
  <div>
    <p>Original Value: {{ value }}</p>
    <p>Doubled Value: {{ doubledValue }}</p>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue';
// 创建响应式数据
const value = ref(10);
// 使用 computed 创建计算属性
const doubledValue = computed(() => value.value 或者 value * 2);
</script>
```

> [!NOTE] `<script setup>` 解构
> 可以直接使用变量里的属性,但在 props 中不建议使用.
> 如果你解构了 props 对象，解构出的变量将会丢失响应性。因此我们推荐通过 `props.xxx` 的形式来使用其中的 props。

# 37 :21 - Income & Expenses Component
## props 传入多个属性
```html
<script setup>
import { defineProps } from 'vue';
const props = defineProps(['income', 'expenses']);
</script>
```
## 筛选大于0的部分
```js
//Get income
const income = computed(() =>
  transactions.value
    .filter((transaction) => transaction.amount > 0)
    .reduce((acc, transaction) => acc + transaction.amount, 0)
);
```
`transactions.value.filter((transaction) => transaction.amount > 0)`:
`transaction` 作为指针遍历 `transactions.value` 数组,
`(transaction) => transaction.amount > 0` 作为筛选的条件

# 42 :34 - AddTransaction Form Component
## 表单提交监听
```html
<template>
  <form @submit.prevent="onSubmit">
    <!-- 表单内容 -->
    <button type="submit">Submit</button>
  </form>
</template>

<script setup>
// 定义组件逻辑
const onSubmit = () => {
  // 处理表单提交逻辑
  console.log('Form submitted!');
};
</script>
```
在这个例子中, `@submit.prevent ="onSubmit"` 表示当表单提交时，调用组件中名为 onSubmit 的方法，并在调用之前阻止默认的表单提交行为。

# 44 :58 - Binding Form Inputs
## 具体实现
```html
<template>
  <form id="form" @submit.prevent="onSubmit">
    <div class="form-control">
      <label for="text">Text</label>
      <input type="text" v-model="text" id="text"  />
    </div>
    <div class="form-control">
      <input
        type="number" v-model="amount" id="amount" 
        placeholder="Enter amount..."
      />
    </div>
    <button class="btn">Add transaction</button>
  </form>
</template>

<script setup>
import { ref } from 'vue';
const text = ref('');
const amount = ref('');
const onSubmit = () =>
  console.log(`Form submitted!:${text.value}, ${amount.value}`);
</script>
```
## 监听输入 v-model
`v-model` 是 Vue.Js 中用于实现双向数据绑定的指令。它可以在表单元素（如 `<input>`、`<textarea>`、`<select>`）上创建双向数据绑定，将表单元素的值与组件的数据属性进行关联。

基本语法如下：
```vue
<template>
  <input v-model="message">
  <p>{{ message }}</p>
</template>

<script setup>
// 在 setup 函数中定义组件的数据
import { ref } from 'vue';
const message = ref('Hello, Vue!');
</script>
```

在这个例子中，`v-model` 将 `<input>` 元素的值与 `message` 数据属性进行了绑定。当用户在输入框中输入文本时，`message` 的值会自动更新。反之，如果你在组件代码中修改了 `message` 的值，输入框的内容也会相应地更新。

请注意，`v-model` 本质上是一种语法糖，实际上是绑定了 `:value` 和 `@input` 两个属性。上述的例子等价于：
```vue
<template>
  <input :value="message" @input="updateMessage">//监听input事件
  <p>{{ message }}</p>
</template>

<script setup>
const message = ref('Hello, Vue!');

const updateMessage = (event) => {
  message.value = event.target.value;
};
</script>
```

`v-model` 简化了双向数据绑定的写法，使得代码更为简洁。在实际应用中，你可以在各种表单元素上使用 `v-model`，包括文本输入框、复选框、单选框、下拉框等。
# 46 :41 - Validation & Toasts

##  vue-toastification
Vue Toastification 是一个轻量、易用且美观的提示条通知组件，提供了大量的选项来支持大部分自定义选择。
### 使用
- 导入模块 Main.js 文件
```js
//main.js
import { createApp } from 'vue';
import Toast from 'vue-toastification';//
import 'vue-toastification/dist/index.css';//
import './assets/style.css';
import App from './App.vue';

const app = createApp(App);
app.mount('#app');
app.use(Toast);
```
- 具体组件文件中导入和使用 AddTransaction.Vue
```js
import { ref } from 'vue';
import { useToast } from 'vue-toastification';
const text = ref('');
const amount = ref('');
const toast = useToast();
const onSubmit = () => {
  if (!text.value || !amount.value) {
    toast.error('Both must be filled');
  }
```
### 提示设置

Type:default,success,info, warning ,error
Position: ![|left|200](photo&pdf/Pasted%20image%2020231213212136.png)

# 52 :05 - Emit Custom Events (defineEmits)
## Emit
- 定义
	用于声明由组件触发的自定义事件

# 54 :45 - Add Transaction to State
## 案例 :emit+监听
子组件
```js
const emit = defineEmits(['TransactionSubmitted']);
  const newTransactionData = {
    text: text.value,
    amount: amount.value,
  };
  emit('TransactionSubmitted', newTransactionData);
```
父组件
```html
<template>
<AddTransaction @TransactionSubmitted="AddnewTransactionData" />
</template>
<script>
const AddnewTransactionData = (newTransactionData/i) => {
  transactions.value.push({
    id: generateUniqueId(),
    text: newTransactionData/i.text,
    amount: newTransactionData/i.amount,
  });
};
const generateUniqueId = () => Math.floor(Math.random() * 100000);
</script>
```
### 案例说明
1.子组件emit 定义一个事件名和变量,传入父组件
2.父组件监听事件,并执行监听后的函数,事件对应的变量为监听函数的输入(所以这里 `newTransactionData` 换成 `i` 没什么区别)
3. emit 提交的变量好像自动传入父组件定义的函数,**一定不要自己加参数**
# 59 :30 - Deleting Transactions
## 实现
- 子组件
```js
<template>
  <h3>History</h3>
  <ul id="list" class="list">
    <li
      v-for="t in transactions"
      v-bind:key="t.id"
      :class="t.amount < 0 ? 'minus' : 'plus'"
    >
      {{ t.text }} <span>${{ t.amount }}</span
      ><button @click="deleteTransaction(t.id)" class="delete-btn">x</button>
    </li>
  </ul>
</template>

<script setup>
import { defineProps } from 'vue';
const props = defineProps(['transactions']);
const emit = defineEmits(['transactionDeleted']);
const deleteTransaction = (id) => {
  return emit('transactionDeleted', id);
};
</script>
```
说明: 删除按钮监听鼠标点击,点击之后执行 `deleteTransaction(t.id)`,函数向父组件传事件和参数.
- 父组件
```html
<template>
    <TransactionList
      :transactions="transactions"
      @transactionDeleted="handleTransactionDeleted"
    />
</template>
<script>
const handleTransactionDeleted = (id) => {
  console.log(id);
  transactions.value = transactions.value.filter(
    (transaction) => transaction.id !== id
  );
  toast.success('Transaction deleted');
};
</script>
```
首先监听子组件传来的事件,并执行函数 `handleTransactionDeleted`.
# Fetch From Local Storage & OnMounted() &Save to Local Storage
1. **挂载时获取已保存的交易记录：**
   ```javascript
   import { defineAsyncComponent, ref, computed, onMounted } from 'vue';
   onMounted(() => {
     const savedTransactions = JSON.parse(localStorage.getItem('transactions'));
    if (savedTransactions) {
     transactions.value = savedTransactions;
   }
   });
   ```
   这段代码使用 `onMounted` 来在组件挂载时执行一个函数。在这个函数内部，它从 `localStorage` 中获取已保存的交易记录，使用 `localStorage.getItem('transactions')` 获取并解析 JSON 数据。
2. **如果已存在保存的交易记录，则更新交易记录：**
   如果存在已保存的交易记录（`savedTransactions` 为真），则将交易记录的值更新为从 `localStorage` 中检索到的交易记录。
3. **将交易记录保存到本地存储：**
   ```javascript
   const savedTransactionsToLocalStorage = () => {
     localStorage.setItem('transactions', JSON.stringify(transactions.value));
   };
   ```
   这个函数 (`savedTransactionsToLocalStorage`) 的目的是将当前的交易记录状态保存到 `localStorage`。它使用 `JSON.stringify` 将交易记录转换为 JSON 字符串，然后使用 `localStorage.setItem` 将其保存到 `localStorage` 中。transactions 是对应的键.
   需要将此函数加入到添加表单和表单的函数当中去.
![](photo&pdf/Pasted%20image%2020231209190747.png)
