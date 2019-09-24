### 块元素垂直水平居中

第一种
`position: absolute; top: 0;right: 0;bottom: 0;left: 0; magin:auto`

第二种
`.cs{ position: absolute; top: 50%; left: 50%; transform:translate(-50%,-50%); }`

第三种(已知自身高宽)
`.cs{ position: absolute; top: 50%; left: 50%; margin-left:-自身一半宽度;margin-top:自身高度一半; }`

##img
img 属于行内块元素,可以用`vertical-align`调节位置;
img 标签直接添加图片.会使其高度额外多 4px 留白,使用`display:block`解决;

##width:fit-content
兼容性问题代码:`width: -webkit-fit-content; width: -moz-fit-content; width: fit-content;`
使元素的宽度以内容决定,而不会占满整一行;
可以使高宽未知的块元素水平居中,需要配合一个 `margin: auto;`,例如:

```html
<ul class="nav">
  <li>a</li>
  <li>b</li>
  <li>c</li>
  <li>d</li>
  <li>e</li>
</ul>
<a href="">测试</a>
<style>
  .nav {
    width: fit-content;
    margin: auto;
  }
  .nav li {
    float: left;
  }

  a {
    display: block;
    margin: auto;
    width: fit-content;
  }
</style>
```

### 清除浮动

方法 1:
给浮动元素的父元素添加`overflow: hidden;`

方法 2:
在父元素下同级最后添加一个空的 div,为它添加样式`clear:both;`

方法 3:
使用伪元素来清除浮动:

```html
div:afte{ content:"";//设置内容为空 　　　　　　 height:0;//高度为0
　　　　　　line-height:0;//行高为0
　　　　　　display:block;//将文本转为块级元素
　　　　　　visibility:hidden;//将元素隐藏 　　　　　　 clear:both//清除浮动 }
```

### 大小不固定的图片统一水平垂直居中

```html
.img-box{ width: 200px; height: 200px; line-height: 200px; text-align: center;
font-size: 0; } .img-box img{ max-width: 90%; max-height: 90%; vertical-align:
middle; }
```

### 单行文本溢出后省略号

`overflow: hidden; text-overflow:ellipsis; white-space: nowrap;`

###多行文本溢出后省略号

- webkit-line-clamp 用来限制在一个块元素显示的文本的行数。 为了实现该效果，它需要组合其他的 WebKit 属性。常见结合属性：
- display: -webkit-box; 必须结合的属性 ，将对象作为弹性伸缩盒子模型显示 。
- webkit-box-orient 必须结合的属性 ，设置或检索伸缩盒对象的子元素的排列方式 。

##### 适用范围：

因使用了 WebKit 的 CSS 扩展属性，该方法适用于 WebKit 浏览器及移动端
使用方式:
`display: -webkit-box; -webkit-box-orient: vertical; -webkit-line-clamp: 3; overflow: hidden;`

### :nth-child(n) 使用注意

`E:nth-child(n)`--->选中某子元素,为父元素下的第 N 个子元素,;
`e:nth-child(odd)` --->奇数

`e:nth-child(even)` --->偶数

###### 正方向范围

`e:nth-child(n+6)`选择从 6 个元素开始的子元素;

###### 负方向范围

`e:nth-child(-n+9)`选择从 1 至 9 的几个元素;

###### 范围性选择

`e:nth-child(n+4):nth-child(-n+8)` 选择从 4 至 8 这个区间内的元素;

###### 范围高级用法

`nth-child(n+2):nth-child(odd):nth-child(-n+9)`

使用 `nth-child(n+2):nth-child(odd):nth-child(-n+9)`我们将会选中的子元素是从第 2 位到第 9 位，并且只包含奇数位。

### ~选择器的用法

选择某元素后面的所有元素;
例子评分系统,关键在与`float: right;`,使其倒数;

```html
<div class="conter">
  <input type="radio" name="rate" />
  <input type="radio" name="rate" />
  <input type="radio" name="rate" />
  <input type="radio" name="rate" />
  <input type="radio" name="rate" />
  <input type="radio" name="rate" />
</div>
<style>
  .conter {
    width: 500px;
    height: 500px;
    background-color: pink;
  }
  input {
    float: right;
    -webkit-appearance: none;
    border: none;
    outline: none;
    cursor: pointer;
  }
  input[name='rate']::after {
    content: '☼';
    color: black;
    font-size: 60px;
    width: 100px;
    height: 100px;
  }
  input[name='rate']:hover::after {
    transform: scale(1.2);
  }
  input[name='rate']:hover::after {
    color: red;
  }
  input[name='rate']:hover ~ input[name='rate']::after {
    color: red;
  }
  input[name='rate']:checked::after {
    content: '☀';
    color: red;
  }
  input[name='rate']:checked ~ input[name='rate']::after {
    content: '☀';
    color: red;
  }
</style>
```

### 文字阴影

水平偏移量 正值向右 负值向左 垂直偏移量 正值向下 负值向上 模糊半径是不能为负值

可以有多个影子，用逗号隔开
text-shadow: h-shadow(x) v-shadow(y) blur(模糊半径) color(颜色)

```html
<style>
  body {
    background-color: gray;
    color: gray;
  }
  p {
    font-size: 64px;
    /* 凸 */
    text-shadow: -1px -1px 1px #fff, 1px 1px 1px #000;
    /* 凹 */
    /* text-shadow: -1px -1px 1px #000, 1px 1px 1px #fff; */
  }
</style>

<p>测试</p>
```

### background

##### background-size

`background-size:cover/contain`;
cover 不保证图片展示完整,图片比例大小不变;
contain 会保证把 图片显示完整,但是可能会有留白;
background-size: 100% 100%; 背景图片宽高以盒子为准;

##### background-clip

裁剪背景:
`background-clip:content-box/padding-box/border-box;`

content-box:以内容范围裁剪背景,裁剪出背景的一部分;
padding-box:padding 也算内容范围来裁剪背景,裁剪出背景的一部分;
border-box:默认属性,延申到盒子所有内容,包括 border;

##### background-origin

背景的起点
background-origin:padding-box/content-box/border-box;
padding-box:从 padding 起始点开始布置背景;默认
content-box;以内容布置背景;
border-box:以边线位置布置背景;
