# 1.content宽度和高度
使用宽度属性width和高度属性height可以对盒子的大小进行控制。

width和height的属性值可以为不同单位的数值或相对于父元素的百分比%，实际工作中最常用的是像素值。

大多数浏览器，如Firefox、IE6及以上版本都采用了W3C规范，符合CSS规范的盒子模型的总宽度和总高度的计算原则是：

      /*外盒尺寸计算（元素空间尺寸）*/
      Element空间高度 = content height + padding + border + margin
      Element 空间宽度 = content width + padding + border + margin
      /*内盒尺寸计算（元素实际大小）*/
      Element Height = content height + padding + border （Height为内容高度）
      Element Width = content width + padding + border （Width为内容宽度）

注意：

1、宽度属性width和高度属性height仅适用于块级元素，对行内元素无效（ img 标签和 input除外）。

2、计算盒子模型的总高度时，还应考虑上下两个盒子垂直外边距合并的情况。

3、如果一个盒子则会和父亲一样宽 占满父亲的宽度， 如果此盒子没有给定宽度 则padding 不会影响本盒子大小。

# 2.外边距合并
相邻块元素垂直外边距的合并

当上下相邻的两个块元素相遇时，如果上面的元素有下外边距margin-bottom，下面的元素有上外边距margin-top，则他们之间的垂直间距不是margin-bottom与margin-top之和，而是两者中的较大者。这种现象被称为相邻块元素垂直外边距的合并（也称外边距塌陷）。



解决方案：  避免就好了。

嵌套块元素垂直外边距的合并

对于两个嵌套关系的块元素，如果父元素没有上内边距及边框，则父元素的上外边距会与子元素的上外边距发生合并，合并后的外边距为两者中的较大者，即使父元素的上外边距为0，也会发生合并。



解决方案：

1. 可以为父元素定义1像素的上边框或上内边距。
2. 可以为父元素添加overflow:hidden。
# 3.盒子模型布局稳定性
按照 优先使用  宽度 （width）  其次 使用内边距（padding）    再次  外边距（margin）。   

      width >  padding  >   margin   
    

原因：

1. margin 会有外边距合并 还有 ie6下面margin 加倍的bug（讨厌）所以最后使用。
2. padding  会影响盒子大小， 需要进行加减计算（麻烦） 其次使用。
3. width   没有问题（嗨皮）我们经常使用宽度剩余法 高度剩余法来做。
   
# 4.盒子阴影


    box-shadow:水平阴影 垂直阴影 模糊距离（虚实）  阴影尺寸（影子大小）  阴影颜色  内/外阴影；



1. 前两个属性是必须写的。其余的可以省略。
2. 外阴影 (outset) 但是不能写    默认      想要内阴影  inset 

    div {
    			width: 200px;
    			height: 200px;
    			border: 10px solid red;
    			/* box-shadow: 5px 5px 3px 4px rgba(0, 0, 0, .4);  */
    			/* box-shadow:水平位置 垂直位置 模糊距离 阴影尺寸（影子大小） 阴影颜色  内/外阴影； */
    			box-shadow: 0 15px 30px  rgba(0, 0, 0, .4);
    			
    }
    # 5.清除浮动
    清除浮动主要为了解决父级元素因为子级浮动引起内部高度为0 的问题。
  其实本质叫做闭合浮动更好一些, 记住，清除浮动就是把浮动的盒子圈到里面，让父盒子闭合出口和入口不让他们出来影响其他元素。

在CSS中，clear属性用于清除浮动，其基本语法格式如下：

    选择器{clear:属性值;}   clear 清除 
    

  属性值  	描述                   
  left 	不允许左侧有浮动元素（清除左侧浮动的影响）
  right	不允许右侧有浮动元素（清除右侧浮动的影响）
  both 	同时清除左右两侧浮动的影响        

额外标签法

    是W3C推荐的做法是通过在浮动元素末尾添加一个空的标签例如 <div style=”clear:both”></div>，或则其他标签br等亦可。

优点： 通俗易懂，书写方便

缺点： 添加许多无意义的标签，结构化较差。 
父级添加overflow属性方法

可以通过触发BFC的方式，可以实现清除浮动效果。

    可以给父级添加： overflow为 hidden|auto|scroll  都可以实现。

优点：  代码简洁

缺点：  内容增多时候容易造成不会自动换行导致内容被隐藏掉，无法显示需要溢出的元素。

使用after伪元素清除浮动

:after 方式为空元素的升级版，好处是不用单独加标签了 

使用方法：

     .clearfix:after {  content: ""; display: block; height: 0; clear: both; visibility: hidden;  }   
    
     .clearfix {*zoom: 1;}   /* IE6、7 专有 */

优点： 符合闭合浮动思想  结构语义化正确

缺点： 由于IE6-7不支持:after，使用 zoom:1触发 hasLayout。

注意： content:""   尽量不带点

使用before和after双伪元素清除浮动

使用方法：

    .clearfix:before,.clearfix:after { 
      content:"";
      display:table;  /* 这句话可以出发BFC BFC可以清除浮动,BFC我们后面讲 */
    }
    .clearfix:after {
     clear:both;
    }
    .clearfix {
      *zoom:1;
    }

优点：  代码更简洁

缺点：  由于IE6-7不支持:after，使用 zoom:1触发 hasLayout。


