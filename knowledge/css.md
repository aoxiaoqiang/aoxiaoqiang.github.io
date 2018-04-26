# CSS

<!--
 {docsify-ignore-all}
 {docsify-ignore}
-->

![img](../assets/image/site/code-map-1.png)

## 网站字体设置 {docsify-ignore}

```css
body {
  font-family: 'Helvetica Neue', Helvetica, Arial, 'PingFang SC',
    'Hiragino Sans GB', 'Heiti SC', 'Microsoft YaHei', 'WenQuanYi Micro Hei',
    sans-serif;
}
```

* [如何优雅的选择字体(font-family)](https://segmentfault.com/a/1190000006110417)
* [Fonts.css -- 跨平台中文字体解决方案)](https://github.com/zenozeng/fonts.css)
* [typo.css -- 中文网页重设与排版：一致化浏览器排版效果](https://github.com/sofish/typo.css)

## 三角形

> `<div class="triangle"></div>`

```css
.triangle {
  width: 0;
  height: 0;
  border-top: 20px solid #333;
  border-left: 20px solid transparent;
  border-right: 20px solid transparent;
}
```
