# CSS常见布局

## 目录
1. flex弹性布局
2. grid网格布局
3. 移动端适配布局
4. 响应式布局

 ## flex弹性布局
###  1.设置flex容器
####  声明
-  `display:flex`声明**父容器**是弹性盒子,扩展至所有有效宽度
-  `display:inline-flex` 收缩至内容宽度

####  设置排列方向
-  `flex-direction` 设置排列方向：

属性值 | 描述
---|---
row | 从左到右水平排列子元素（默认值）
column | 从上到下垂直排列子元素
row-reverse | 从右向左排列子元素
column-reverse |从下到上垂直排列子元素

####  溢出处理
- `flex-wrap` 进行溢出处理，是否换行

属性值 | 描述
---|---
nowrap | 弹性容器为单行，会溢出（默认值）
wrap | 弹性容器为多行，会自动换行
wrap-reverse | 反转 wrap 排列。

####  设置主轴方向上的对齐方式。
`justify-content` 属性

属性值 | 描述
---|---
flex-start | 弹性项目向行头紧挨着填充。（默认值）
flex-end | 弹性项目向行尾紧挨着填充。
center | 弹性项目居中紧挨着填充。
space-between |弹性项目平均分布在该行上,两边顶满。
space-around |弹性项目平均分布在该行上，两边留有一半的间隔空间。
space-evenly |弹性项目平均分布在该行上，两边留有相等的间隔空间。
![](https://s2.loli.net/2022/05/10/ZmcCQTLWJbeHzR3.png)

#### 设置子元素在侧轴上的对齐方式
`align-items` 属性

属性值 | 描述
---|---
stretch | 使项目的边距盒的尺寸尽可能接近所在行的尺寸，但同时会遵照'min/max-width/height'属性的限制（默认值）
flex-start | 子元素的侧轴起始位置的边界紧靠住该行的侧轴起始边界。
flex-end | 子元素的侧轴起始位置的边界紧靠住该行的侧轴结束边界。
center | 弹性盒子元素在该行的侧轴上居中放置
baseline |如弹性盒子元素的行内轴与侧轴为同一条，则该值与'flex-start'等效。其它情况下，该值将参与基线对齐。

![](https://s2.loli.net/2022/05/10/4GfilmZ1uIXpFKb.png)

#### 设置各个行的对齐
`align-content` 属性

属性值 | 描述
---|---
stretch | 各行将会伸展以占用剩余的空间。（默认值）
flex-start | 各行向弹性盒容器的起始位置堆叠。
flex-end | 各行向弹性盒容器的结束位置堆叠。
center | 各行向弹性盒容器的中间位置堆叠。
space-between |各行在弹性盒容器中平均分布，两端顶满。
space-around |各行在弹性盒容器中平均分布，两端保留子元素与子元素之间间距大小的一半。
![](https://s2.loli.net/2022/05/10/OA4x3rnb8TIK1J7.png)

#### 简写
`flex-flow` 属性：flex-direction 和 flex-wrap 属性的缩写形式，默认是 row nowrap。


```css
flex-flow: <‘flex-direction’> || <‘flex-wrap’>
```



### 2.设置flex子项

#### 设置顺序
`order` 属性，值为数字，数字越小排越前面，允许负值

#### 单个子项居中
设置`margin: auto`
 
#### 单独某个子项垂直对齐方式
`align-self` 

```css
align-self: auto | flex-start | flex-end | center | baseline | stretch
```

#### 可用剩余空间时拉伸比例
`flex-grow` ,默认值为0。将剩余空间，按每个子项的比例分配给子项。

#### 定义了子项的收缩的能力
`flex-shrink`,默认值为1，决定 flex 项允许收缩多少比例。

#### 设置子项在主轴方向的默认大小
`flex-basis` ,默认值auto

#### 简写
`flex` 用法：
```
flex: none | [ < 'flex-grow'> < 'flex-shrink'>? || < 'flex-basis'> ]
//第二三个参数可选
```
### 3.应用

- 两列等高布局：两列元素，一列内容变多，另一列跟着拉伸。父盒子为flex，左右列的盒子默认stretch，因此会自动拉伸。
- 不定项居中：设置`justify-content: center;  align-items: flex-end;`,比如轮播图下面的小圆点。
- 两列或三列布局：其中一列会自己调整宽度，父盒子为flex，然后要自适应的一列设置grow为1，就会自动填充剩余空间。
- 溢出项布局：如轮播图，直接设置flex盒子，默认一行会溢出
- 子项分组布局：当子元素总宽度不及父盒子时，为其中一个子元素设置margin为auto，可以将剩余空间自动分配为外边距。
