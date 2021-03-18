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

  ![](.\images\1.png)
  
  总宽度为1259，红色div宽度为679.5，蓝色和黄色的div宽度为289.75

### flex-shrink

定义子项目的缩放比例，默认是 `0`，即存在剩余空间也不会缩小

- 不管 `flex-shrink` 的值是否为 `0` ，如果没有给元素给定宽度，则元素的宽度为 `0`
- 若每个元素的 `width` 不同，分别为 `w1`, `w2`, `w3`, 父 `div` 的宽度为 `w` ，`flex-shrink` 的值分别为  `a` , `b` , `c` ，`x` 为实际缩放比例，则：`(w1 * x) / a + (w2 * x) / b + (w3 * x) / c = w`
- 若每个元素的 `width` 相同，则缩放的计算公式如下：
  - 假设父 `div` 的宽度为 `w`，有三个子 `div`，宽度都为  `cw`， 且三个子 `div` 的宽度大于父 `div` 的宽度，`flex-shrink` 的值分别为  `a` , `b` , `c` ，则： `(a + b + c) * x = w`， 缩放后三个子 `div` 的宽度分别是 `a * (w / (a + b +c))`, `b * (w / (a + b +c))`, `c * (w / (a + b +c))`



### flex: 1

```
// flex 是 flex-grow、flex-shrink和flex-base的缩写
flex: 1 === flex: 1 1 任意数字+任意长度单位
```

 **flex-basis给上面两个属性分配多余空间之前, 计算项目是否有多余空间, 默认值为 auto, 即项目本身的大小** 

 **如果设置为 auto, 那么这每个盒子就会按照自己内容的多少来等比例的放大和缩小** 