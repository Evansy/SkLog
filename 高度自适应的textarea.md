## 高度自适应的`textarea`
> 众所周知，`textarea`的高度是不会随内容变化而变化的，有时候有些场景会用到`textarea`高度自适应，下面是我用到的一些方法

#### 1. 用`div`替换`textarea`，然后把div的`contenteditable`设置为`true`。
> 缺点就是对IE的支持不是很好
```html
<div class="expandingArea" contenteditable="true"></div>
```

#### 2. 通过添加pre标签解决。
> 原理就是把`pre`标签设置为不可见`visibility:hidden`，`textarea`设置高度`100%`, `textarea`覆盖在`pre`上面，并且`textarea`的宽，字体大小和`pre`一致，这样，用户输入文字后，`pre`标签会被撑开，外框的高度就会被撑开，
```html
<div class="expandingArea">
    <pre><span v-html="productDetail.Description"></span><br></pre>
    <textarea class="edit-product-input" placeholder="填写商品的描述" v-model="productDetail.Description" maxlength="100"></textarea>
</div>
```
```css
.expandingArea{
    position:relative;
}
textarea{
    position:absolute;
    top:0;
    left:0；
    height:100%;
}
pre{
    display:block;
    visibility:hidden;
}
```

#### 3. 监听textarea的input事件
```js
var txt = document.querySelector('textarea');
txt.style.height = `${txt.scrollHeight}px`;

if (typeof text.oninput = 'undefined') {
    txt.onpropertychange = function() {
        if(event.propertyName === 'value') {
            this.style.height = "20px";
            this.style.height = `${scrollHeight}px`;
        }
    }
} else {
    txt.oninput = function () {
        this.style.height = 'auto';
        this.style.height = `${scrollHeight}px`;
    }
}
```