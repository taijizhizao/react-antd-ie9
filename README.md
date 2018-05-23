# react-antd-ie9

项目通过 `create-react-app` 创建，引入 `antd` 作为UI库。

本文把项目开发过程中遇到的兼容性问题和解决思路整理出来。



## babel-polyfill

创建的项目一开始在IE9是无法运行的，需要引入 `babel-polyfill` 。

执行以下命令：

```sh
npm install babel-polyfill --save
```



然后在 `src/index.js` 的第一行编写如下代码：

```react
import 'babel-polyfill';
```

​	

## css样式不加载

如果项目运行后发现编写的css样式没有效果，则可能是由于css文件过大造成。IE9最大支持250KB的样式文件，而antd的样式文件有500多KB，会造成样式加载失败。

解决方案是手动把antd的样式代码分在三个文件中，保证每个文件小于200KB，然后依次引入到 `public/index.html` 中，代码如下：

```html
<!-- 在public/index.html中引入antd的样式 -->
<link rel="stylesheet" href="%PUBLIC_URL%/antd1.css">
<link rel="stylesheet" href="%PUBLIC_URL%/antd2.css">
<link rel="stylesheet" href="%PUBLIC_URL%/antd3.css">
```

​	

## 常见报错分析

​	

### SCRIPT5009: “File”未定义

IE9中不支持 `File` 对象，不可以使用。

​	

## 常见样式问题

​	

### 渐变色

IE9不支持 `background: linear-gradient` 的语法，需要使用滤镜。代码如下：

```css
/* IE中实现渐变色 */
/* gradientType为0时代表垂直，为1时代表水平 */
filter: progid:DXImageTransform.Microsoft.Gradient(startColorStr='#FF0000',endColorStr='#F9F900',gradientType='0'); 
```

