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

## CSS中的布局

[flex 布局测试](https://flexboxfroggy.com/#zh-cn)。以玩游戏的方式熟练掌握flex布局，游戏共有24个等级像练级一样学习和掌握flex布局。在游戏中你需要更具要求提示靠 **写CSS代码** 来帮助青蛙🐸和他的朋友们到目标布局的位置，快来送青蛙🐸回家吧！


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


<div id="gitalk-container"></div>

<script type="text/javascript">
  var gitalk = new Gitalk({
  clientID: 'f4cf3934cb701cb3eb66',
  clientSecret: '978c5b687161057c41859fda0b35bc17efccca5d',
  repo: 'https://github.com/aoxiaoqiang/aoxiaoqiang.github.io',
  owner: 'aoxiaoqiang',
  admin: ['aoxiaoqiang'],
  id: location.href,      // Ensure uniqueness and length less than 50
  distractionFreeMode: false  // Facebook-like distraction free mode
})
gitalk.render('gitalk-container');
</script>