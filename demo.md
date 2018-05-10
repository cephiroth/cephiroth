# CSS / SCSS 规范

## 目录

一、 [CSS](#css)
1. [格式](#格式)
2. [注释](#注释)
3. [引用顺序](#引用顺序)
4. [引号](#引号)
5. [媒体查询的位置](#媒体查询的位置)
6. [边框](#边框)
7. [链接的样式顺序](#链接的样式顺序)

二、 [SCSS](#scss)
1. [属性声明的排序](#属性声明的排序)
2. [变量](#变量)
3. [Mixins](#mixins)
5. [扩展指令](#扩展指令)
6. [嵌套选择器](#嵌套选择器)

## CSS

### 格式

* 使用 2 个空格作为缩进。
* 类名建议使用驼峰法（因为`css modules`）。
* 不要使用 ID 选择器。
* 在一个规则声明中应用了多个选择器时，每个选择器独占一行。
* 在规则声明的左大括号 `{` 前加上一个空格。
* 在属性的冒号 `:` 后面加上一个空格，前面不加空格。
* 规则声明的右大括号 `}` 独占一行。
* 规则声明之间用空行分隔开。
```css
/*  不推荐  */
.avatar{
    border-radius:50%;
    border:2px solid white; }
.no, .nope, .not_good {
    // ...
}
#lol-no {
  // ...
}
/* 推荐 */
.avatar {
  border-radius: 50%;
  border: 2px solid white;
}

.one,
.selector,
.perLine {
  // ...
}
```
* 一般以逗号分隔的属性值，每个逗号后应添加一个空格；
* `rgb()`、`rgba()`、`hsl()`、`hsla()` 或 `rect()` 括号内的值，逗号分隔，但逗号后不添加一个空格；
* 对于属性值或颜色参数，省略小于 1 的小数前面的 0 （例如，.5 代替 0.5；-.5px 代替-0.5px）；
* 十六进制值应该全部小写和尽量简写，例如，`#fff` 代替 `#ffffff`；
* 避免为 0 值指定单位，例如，用 `margin: 0;` 代替 `margin: 0px;`；
* 不要使用单行写法，使用多行写法方便后续阅读和维护；
```css
/*  不推荐  */
.selector, .selector-secondary, .selector[type=text] {
    padding:15px;
    margin:0px 0px 15px;
    background-color:rgba(0, 0, 0, 0.5);
    box-shadow:0px 1px 2px #CCC,inset 0 1px 0 #FFFFFF
}

/* 推荐 */
.selector,
.selector-secondary,
.selector[type="text"] {
    padding: 15px;
    margin-bottom: 15px;
    background-color: rgba(0,0,0,.5);
    box-shadow: 0 1px 2px #ccc, inset 0 1px 0 #fff;
}

/*  不推荐  */
.nav { width: 15px; height: 15px; }

/*  推荐  */
.nav { 
    width: 15px; 
    height: 15px; 
}
```

### 注释

* 建议使用行注释 (在 Sass 中是 //) 代替块注释。
* 建议注释独占一行。避免行末注释。
* 给没有自注释的代码写上详细说明，比如：
    + 为什么用到了 `z-index`
    + 兼容性处理或者针对特定浏览器的 hack

### 引用顺序
相关属性应为一组，推荐的样式编写顺序

1. Positioning
2. Box model
3. Typographic
4. Visual

由于定位（positioning）可以从正常的文档流中移除元素，并且还能覆盖盒模型（box model）相关的样式，因此排在首位。盒模型决定了组件的尺寸和位置，因此排在第二位。

其他属性只是影响组件的内部（inside）或者是不影响前两组属性，因此排在后面。
```css
.declaration-order {
  /* Positioning */
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: 100;

  /* Box model */
  display: block;
  box-sizing: border-box;
  width: 100px;
  height: 100px;
  padding: 10px;
  border: 1px solid #e5e5e5;
  border-radius: 3px;
  margin: 10px;
  float: right;
  overflow: hidden;

  /* Typographic */
  font: normal 13px "Helvetica Neue", sans-serif;
  line-height: 1.5;
  text-align: center;

  /* Visual */
  background-color: #f5f5f5;
  color: #fff;
  opacity: .8;

  /* Other */
  cursor: pointer;
}
```

### 引号
`url()` 、属性选择符、属性值使用双引号。
```css
/* 不推荐 */
@import url(//www.google.com/css/maia.css);

html {
  font-family: 'open sans', arial, sans-serif;
}

/* 推荐 */
@import url("//www.google.com/css/maia.css");

html {
  font-family: "open sans", arial, sans-serif;
}

.selector[type="text"] {

}
```
### 媒体查询的位置
将媒体查询放在尽可能相关规则的附近。不要将他们打包放在一个单一样式文件中或者放在文档底部。如果你把他们分开了，将来只会被大家遗忘。
```css
.element { ... }
.element-avatar { ... }
.element-selected { ... }

@media (max-width: 768px) {
  .element { ...}
  .element-avatar { ... }
  .element-selected { ... }
}
```

### 边框
在定义无边框样式时，使用 0 代替 none。
```css
/* 不推荐 */
.foo {
  border: none;
}

/* 推荐 */
.foo {
  border: 0;
}
```

### 链接的样式顺序
a:link -> a:visited -> a:hover -> a:active（LoVeHAte）

## SCSS

### 属性声明的排序
1. 属性声明

首先列出除去 `@include` 和嵌套选择器之外的所有属性声明。
```css
.btn-green {
  background: green;
  font-weight: bold;
  // ...
}
```
2. @include 声明

紧随后面的是 `@include`，这样可以使得整个选择器的可读性更高。
```css
.btn-green {
  background: green;
  font-weight: bold;
  @include transition(background 0.5s ease);
  // ...
}
```
3. 嵌套选择器

如果有必要用到嵌套选择器，把它们放到最后，在规则声明和嵌套选择器之间要加上空白，相邻嵌套选择器之间也要加上空白。嵌套选择器中的内容也要遵循上述指引。
```css
.btn {
  background: green;
  font-weight: bold;
  @include transition(background 0.5s ease);

  .icon {
    margin-right: 10px;
  }
}
```
### 变量
变量名应使用破折号（例如 $my-variable）代替 camelCased 和 snake_cased 风格。对于仅用在当前文件的变量，可以在变量名之前添加下划线前缀（例如 $_my-variable）。


### Mixins
为了让代码遵循 DRY 原则（Don't Repeat Yourself）、增强清晰性或抽象化复杂性，应该使用 `mixin`，这与那些命名良好的函数的作用是异曲同工的。虽然 `mixin` 可以不接收参数，但要注意，假如你不压缩负载（比如通过 gzip），这样会导致最终的样式包含不必要的代码重复。


### 扩展指令
应避免使用 `@extend` 指令，因为它并不直观，而且具有潜在风险，特别是用在嵌套选择器的时候。即便是在顶层占位符选择器使用扩展，如果选择器的顺序最终会改变，也可能会导致问题。（比如，如果它们存在于其他文件，而加载顺序发生了变化）。其实，使用 `@extend` 所获得的大部分优化效果，gzip 压缩已经帮助你做到了，因此你只需要通过 `mixin` 让样式表更符合 DRY 原则就足够了。


### 嵌套选择器
请不要让嵌套选择器的深度超过 3 层！
```css
.page-container {
  .content {
    .profile {
      // STOP!
    }
  }
}
```
当遇到以上情况的时候，你也许是这样写 CSS 的：

* 与 HTML 强耦合的（也是脆弱的）—或者—
* 过于具体（强大）—或者—
* 没有重用

再说一遍: **永远不要嵌套 ID 选择器！**

如果你始终坚持要使用 ID 选择器（劝你三思），那也不应该嵌套它们。如果你正打算这么做，你需要先重新检查你的标签，或者指明原因。如果你想要写出风格良好的 HTML 和 CSS，你是不应该这样做的。
