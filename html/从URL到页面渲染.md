## 从 `URL` 输入到浏览器展示出页面的过程是什么

1. `DNS` 解析
2. `TCP` 三次握手
3. 发送请求，分析 `url` ，设置请求报文（头、主体）
4. 服务器返回请求的文件（`html`）
5. 浏览器渲染
   - `HTML Paser` -->  `DOM Tree`
     - 标记化算法，进行元素状态的标记
     - `dom` 树构建
   - `CSS Paser`  -->  `Stype Tree`
     - 解析 `css` 代码，生成样式树
   - `Attachment`  --> `Render Tree`
     - 结合 `dom` 树与 `style` 树，生成渲染树
   - `layout` 布局
   - `GPU painting` 像素绘制页面