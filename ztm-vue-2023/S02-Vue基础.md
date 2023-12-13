# CDN
CDN 是内容分发网络（Content Delivery Network）的缩写，它是一种构建在互联网上的系统，用于加速内容传递到用户的网络设备，提高网站和应用程序的性能和可用性。
CDN 的主要目标是通过在全球范围内分布内容的多个节点（也称为边缘服务器或边缘节点），将内容更接近最终用户，从而减少用户请求的响应时间。这种分布式的部署方式可以有效减轻原始服务器的负载，提高用户访问网站或应用时的速度和体验。
# 创建 Vue
## CDN 方法
1. html 绑定 vue 文件
```html
<!DOCTYPE html>
<html>
  <head>
    <title>VueJS Course</title>
    <link rel="stylesheet" type="text/css" href="main.css" />
  </head>
  <body>
    <div id="app"></div>
    <script src="https://unpkg.com/vue@3/dist/vue.global.js">//这行!
    </script>
    <script src="app.js"></script>
  </body>
</html>
```
> [!tip] CDN 引入需要在引入 app.js 之前
2. js 文件中将应用程序实例安装在容器app元素中。
```js
const app = Vue.createApp({});
app.mount('#app');
```
# Vue 浏览器工具
# 数据data


