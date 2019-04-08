> > # CSS
> >
> > es6引入了类，es5还没引

## 样式操作

```javascript
设置图片在哪显示
background-clip 属性规定背景的绘制区域。

background-clip:border-box;    //在盒子内部显示（默认 方式）
backgrouond-clip:padding-box;  //在padding内部显示
background-clip:content-box;  //文本内容区域显示这个图片

background-size：contain； 设置背景按照比例缩放完整的显示
background-size：cover； 这是北京按照自己的比例铺满，不确定是否完整显示

box-shadow：10px 20px 10px blue  inset； 
   			水平  垂直  模糊度 颜色  内部
            
//切割图片
border-image-slice:19;
//选择图片作为边框背景
border-image-source：url（）；
//border-image-repeat:round;//铺满  stretch 拉伸  repeat 平铺  

text-shadow：10px 20px 10px,10px 20px 10px blue;//文字加阴影 水平  垂直  模糊度 颜色 

```



## 选择器

```javascript
属性选择器
p~ul{}   // p后面所有的ul
a[herf^='E']{}  //具有href属性，值是以'E'开头的
a[herf$='E']{}  //具有href属性，值是以‘E’结尾的
a[herf*='E']{}  //具有href属性，值是里面有‘l’的

// 目标选择器  点击a标签  p的样式改变
p：target｛color:red｝
<p id='one'></p>
<a href='#one'></a>

div:first-letter{}  // 设置第一个字符
div:first-line{}  // 设置第一行的文字样式


```



### 颜色渐变

```javascript
// 线性渐变
background-image:linear-gradient(0deg,red,green)
background-image:linear-gradient(to right,red,green)
background-image:linear-gradient(
    to right(90deg),red 20%,green 20%,red 20%,green 60%
)

// 径向渐变
// 半径及开化寺的为孩子，开始的渐变颜色，结束的渐变颜色
background-image:radial-grdient(100px at center，red，green)
background-image:radial-grdient(100px at 150px，red，green)
background-image:radial-grdient(100px at 150px，red 15%，green 15%，yellow 15%，pink 15%，blue 15%)
```



2D\3D转换

动画操作

网页布局

```java
display:flex;
justify-content:space-between; //center,space-around,flex-end.flex-satrt
flax-direction:row-reverse;  //设置主轴方向水平反转 column垂直方向  column-reverse反向

align-items:flex-satrt;   //侧轴对齐：对齐方式
align-content:flex-satrt；  //子元素换行后有空白行，希望没有空白行，需要重新确定主轴的方向

flax-wrap:wrap;  //子元素换行
```





### vertical-align设置元素的垂直对齐方式

| 值          | 描述                                                         |
| :---------- | :----------------------------------------------------------- |
| baseline    | 默认。元素放置在父元素的基线上。                             |
| sub         | 垂直对齐文本的下标。                                         |
| super       | 垂直对齐文本的上标                                           |
| top         | 把元素的顶端与行中最高元素的顶端对齐                         |
| text-top    | 把元素的顶端与父元素字体的顶端对齐                           |
| middle      | 把此元素放置在父元素的中部。                                 |
| bottom      | 把元素的顶端与行中最低的元素的顶端对齐。                     |
| text-bottom | 把元素的底端与父元素字体的底端对齐。                         |
| length      |                                                              |
| %           | 使用 "line-height" 属性的百分比值来排列此元素。允许使用负值。 |
| inherit     | 规定应该从父元素继承 vertical-align 属性的值。               |

`vertical-align`对`::first-lette`r和`::first-line`同样适用。