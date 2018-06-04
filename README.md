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
