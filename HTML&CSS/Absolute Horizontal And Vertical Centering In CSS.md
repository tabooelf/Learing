# Absolute Horizontal And Vertical Centering In CSS

## 1.Height & Line height

```css
.container-vertical {
  height:100px;
  line-height:100px;/*设置line-height等于height*/
}
```

- 优点：适用所有浏览器，没有足够空间时，内容不会被切掉

- 缺点：只适用于单元素，如单行文本或图片（单个block元素）




## 2.负Margin

```css
.is-Negative {
        width: 300px;
        height: 200px;
        padding: 20px;
        position: absolute;
        top: 50%; left: 50%;
        margin-left: -170px; /* (width + padding)/2 */
        margin-top: -120px; /* (height + padding)/2 */
}
```

- 优点：适用所有浏览器
- 缺点：固定高度和宽度，容器空间不足时异常。




## 3.translate(-50%,-50%)

```css
.vertical {
  position:absolute;/*绝对定位*/
  top:50%;/*top定位为父元素的一半*/
  left:50%/*left定位为父元素的一半*/
  transform:translate(-50%,-50%);/* 50%为自身尺寸的一半 */
```

- 优点：适用所有浏览器
- 缺点：IE 6/7 无效




## 4 Margin:auto

```css
.Absolute-Center {
  width: 50%; 
  height: 50%; /* 需设置 */
  overflow: auto; /* 防止溢出 */
  margin: auto;
  position: absolute;
  top: 0; left: 0; bottom: 0; right: 0;
}
```

**注意：高度必须定义，建议加 overflow: auto，防止内容溢出。**

### 视口居中

```css
.Absolute-Center.is-Fixed {
  width: 50%;
  height: 50%;
  overflow: auto;
  margin: auto;
  position:fixed;/* 视口定位 */
  top: 0; left: 0; bottom: 0; right: 0;
  z-index: 999;/* 顶层显示 */
}
```

### 可变高度

高度必须定义，但可以是百分比或 max-height。不想定义高度的话，用 `display: table` （需要考虑 Table-Cell 兼容性）。

```css
.Absolute-Center.is-Variable {
  display: table;
  width: 50%;
  overflow: auto;
  margin: auto;
  position: absolute;
  top: 0; left: 0; bottom: 0; right: 0;
}
```

### 调整尺寸

**resize** 属性可以让尺寸可调。
设置 **min- /max-** 限制尺寸，确定加了 `overflow: auto` 。

```css
.Absolute-Center.is-Resizable {
  min-width: 20%;
  max-width: 80%;
  min-height: 20%;
  max-height: 80%;
  resize: both;
  overflow: auto;
  margin: auto;
  position: absolute;
  top: 0; left: 0; bottom: 0; right: 0;
}
```



## 5.Table-Cell

```html
div class="Container is-Table">
  <div class="Table-Cell">
    <div class="Center-Block">
    &lt!-- CONTENT -->
    </div>
  </div>
</div>
```

```css
.Container.is-Table { display: table; }
.Table-Cell {
  display: table-cell;
  vertical-align: middle;
}
.Center-Block {
  width: 50%;
  margin: 0 auto;
}
```

- 优点：兼容性强
- 缺点：结构复杂



## 6.弹性盒子 flexbox

```css
.Container.is-Flexbox {
  display: flex;
  align-items: center;
  justify-content: center;
}
```

- 缺点：兼容性差



## 7.inline-block

```html
<div class="Container is-Inline">
  <div class="Center-Block">
    <!-- CONTENT -->
  </div>
</div>
```

```css
.Container.is-Inline {
  text-align: center;
  overflow: auto;
}

.Container.is-Inline:after,
.is-Inline .Center-Block {
  display: inline-block;
  vertical-align: middle;
}

.Center-Container.is-Inline:after {
  content: '';
  height: 100%;
  margin-left: -0.25em; /* To offset spacing. May vary by font */
}

.is-Inline .Center-Block {
  max-width: 99%; /* Prevents issues with long content causes the content block to be pushed to the top */
  /* max-width: calc(100% - 0.25em) /* Only for IE9+ */
}
```



## 附.javacript

```javascript
//获取元素的内容高度
var h = Math.ceil($(this).height());
//outerHeight=padding+border+height
var oh = Math.ceil($(this).outerHeight());
//取得margin-top值
var mt = Math.ceil(oh / 2);
//取得元素宽度
var w = Math.ceil($(this).width());
//outerWidth=padding+border+width
var ow = Math.ceil($(this).outerWidth());
//取得margin-left
var ml = Math.ceil(ow / 2);
//实现元素居中效果
$(this).css({
    "margin-top": "-" + mt + "px",
    "top": "50%",
    "margin-left": "-" + ml + "px",
    "left": "50%",
    "width":w,
    "height":h,
    "position": "absolute"
}); 
```

带研究