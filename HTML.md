# HTML

语义化标签

nav、header、footer、section、asdie

SEO网站优化



### html5语义性解决（ie兼容问题）

ie低版本不认识语义化标签    

```javascript
解决！

// 1.在js中创建nav元素   这样  ie就可以识别  并且需要在css中设置 display:block;
document.createElement('nav')

// 2.js插件  html5shiv.min.js

// 3、cc:ie6    tab键    ie浏览器才会认识
[if lte IE 8]
   //引入html5shiv.js  插件
[endif]
```



**文字水平分布**

```

text-align-last: justify;
```