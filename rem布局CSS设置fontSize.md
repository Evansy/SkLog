## rem布局CSS设置fontSize
以`750px`设计稿为基准，根据`font-size`为`100px`，这里只是动态设置根`font-size`部分，dpr还是需要动态设置的。

#### js方法
```js
document.querySelector('html').style.fontSize = `${window.innerWidth / 7.5}px`;
```

#### css方法(支持安卓4.4.4及以上, ios支持比较好)

```css
html{
    font-siez: 100vw / 750;
}
```