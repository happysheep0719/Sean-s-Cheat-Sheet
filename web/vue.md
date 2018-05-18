# Vue 踩坑

第一天使用Vue就踩了这么多坑。

##vue响应式原理

把对象的属性变成setter和getter，以此监听属性的改变
vue不能检测非对象的变化
vue不能检测数组的变化，要用专门的列表渲染部分
vue不能检测对象新增的属性，所以最好创建vue对象前，需要对外部的data的所有属性初始化

##三种绑定数据方法

https://www.tangshuang.net/3507.html

1. {{name}}插值
2. v-bind 单向绑定？一般用于属性？
3. v-model - v-bind和v-on的语法糖

##组件嵌套

1. 设置props
2. template加入`:attr:"father-attr"`

```js
Vue.component('blog-post', {
  // 在 JavaScript 中是 camelCase 的
  props: ['postTitle'],
  template: '<h3>{{ postTitle }}</h3>'
})
<!-- 在 HTML 中是 kebab-case 的 -->
<blog-post post-title="hello!"></blog-post>
```

## router

通过检测hashtag的变化，改变出现的组件

同时满足以下需求：

- hashtag以子路径作为标识，每个独特的hashtag url可以映射到一个资源
- 所有的子应用都可以放在单页中。