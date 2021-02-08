# flex 布局

`flex` 布局可以去参考 [阮一峰大神的博客](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html)

[TOC]

## 子项目的属性理解



### flex-grow

定义子项目的放大比例，默认是 `0` ，即如果存在剩余空间也不放大

- 当 `flex-grow` 的值为 `0` ，而且没有为此元素给定宽度，则当前元素的宽度为 `0`

- 当 `flex-grow` 的值不为 `0` ，而且给定了此元素的宽度，则当前元素的宽度为 **flex自动计算的宽度值 + 给定的宽度值**

  ```css
  .div { display: flex; flex-direction: row; align-items: center; justify-content: flex-start; }
  .item { height: 100px; }
  .red { background: red; width: 100px; flex-grow: 2; }
  .blue { background: blue; flex-grow: 1; }
  .yellow { background: yellow; flex-grow: 1; }
  ```

  ![](E:\X_学习\blogs\css\1. flex\images\1.png)
  
  总宽度为1259，红色div宽度为679.5，蓝色和黄色的div宽度为289.75

### flex-shrink

定义子项目的缩放比例，默认是 `0`，即存在剩余空间也不会缩小

- 不管 `flex-shrink` 的值是否为 `0` ，如果没有给元素给定宽度，则元素的宽度为 `0`