# CSS常见布局

## 目录
1. flex弹性布局
2. grid网格布局
3. 移动端适配布局
4. 响应式布局

## flex弹性布局
 适合单列的布局
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

## grid网格布局
适合多列网格布局
![](https://s2.loli.net/2022/05/11/dsMUiJkq29IPxYQ.png)
###  1.设置grid容器

#### 声明
`display:grid`  只创建了一个只有一列的网格,网页并不会马上发生变化,需要设置
#### fr单位

fr单位规定了可用空间的分配比例
#### 定义网格

- `grid-template-columns: 1fr 1fr 1fr` 设置列数和大小
- `grid-template-rows: 1fr 1fr 1fr` 设置行数和大小
- `grid-template-areas` 合并单元格，使用如下

```
//在父盒子中设置区域
.grid-father{
    grid-template-areas:"a1,a1,a2"
                        "a1,a1,a2"
                        "a3,a3,a2";
    }
.child{
    grid-area: a1;  //在子盒子中生效 
}
```
grid盒子里的子盒子会按上面的设置自动填充进盒子里去，相当于设置了一个模板，往里面填盒子

**简写**

使用`grid-template:` 进行简写
```
grid-template: 
            "a1 a1 a2" 1fr   //每一行后面跟着的是行rows的单位
            "a1 a1 a2" 1fr
            "a3 a3 a3" 1fr
            / 100px 100px 100px;  //最后一行是列columns的单位（记得斜线）
```
#### 网格间隙

- `grid-column-gap` 列间隙
- `grid-row-gap`  行间隙
- `grid-gap`  复合写法，先写行row，再写列column

现在更推荐
- `column-gap`
- `row-gap`
- `gap`

#### 网格对齐方式
- `justify-items` 水平方向，子项在自己单元格里的对齐方式
- `align-items`  垂直方向，子项在自己单元格里的对齐方式
- 参数有 start/end/center 默认stret
- `place-items` 复合写法 垂直 水平


- `justify-content` 水平方向
- `align-content`  垂直方向
- 上述两个属性，设置网格整体（模板），相对父盒子的位置
- 属性有start/end/center/space-between/space-around/space-evenly 默认stretch
- `place-content`  复合写法  垂直 水平

以上设置==网格小于容器==才能看到效果

#### 隐式网格的设置
当子项溢出时，会自动布局新网格，就是隐式网格
- `grid-auto-flow`  属性控制着自动布局算法怎样运作
- `grid-auto-columns`  指定了隐式创建的网格纵向轨道（track）的宽度
- `grid-auto-rows`   设置网格中行的默认尺寸

```
grid-auto-flow: row;    //在必要时增加新行(默认)
grid-auto-flow: column;     //在必要时增加新列
grid-auto-flow: dense;  //如果后面出现了稍小的元素，则会试图去填充网格中前面留下的空白。可能导致原来出现的次序被打乱
grid-auto-flow: row dense;
grid-auto-flow: column dense;
```


###  2.设置grid子项

#### 基于线的元素放置

**线**：即开篇图片中编了序号123...的线（间隙所在的位置），从1开始编号命名，n行就n+1条线

用以下几个属性可以设置子项的起始位置(基于线)
- `grid-column-start` 属性：单元格左边框所在的垂直网格线
- `grid-column-end` 属性：单元格右边框所在的垂直网格线
- `grid-row-start` 属性：单元格上边框所在的水平网格线
- `grid-row-end` 属性：单元格下边框所在的水平网格线

后面跟线的编号数字

==注意==：只设置前一个盒子的grid-column，后面的盒子会放入前一个盒子后面的格子，因为grid-row默认是auto。如果设定了grid-row，就明确了位置，其他盒子会自动从第一个格子开始排列。

grid-template还可以给线**命名**：
- `grid-template-columns: [col1] 1fr [col2] 1fr [col3] 1fr [col4]` 用中括号设置线的名称。命名就可以代替上面四个属性的数字参数

**简写**：

- `grid-column: 2/4` `grid-row: 2/3;`用斜线分割  起始/结束
- `grid-column: span 2/span 2;` 表示行列占据两格
- `grid-area: 2/2/4/3;` grid-column-start/rid-row-start/grid-column-end/grid-row-end
- `grid-area: 1/1/span 2/span 2;` 表示行列从基线1开始，上下占据两格

grid-area既可以用命名设置子项，也可以用基线设置

#### 子项对齐方式

操作某一个子项
- `justify-self`
- `align-self`

### 3.网格相关方法
repeat(number,size)
-  `grid-template-columns:repeat(5,100px);` 设置五个重复的列，每个100px
-  `grid-template-columns:repeat(auto-fill,100px);` 根据父容器大小，自动设置列数

minmax(min,max)
- `grid-template-columns:100px minmax(100px,1fr) 100px;` 设定最小值为100px，最大值自适应。
- 复合用法`grid-template-column:repeat(auto-fill,minmax(200px,1fr));`

###  4.应用

1. ==叠加布局==：用`grid-area`将几个盒子装进同一个格子，再用`align-self`和`justif-self`对每个盒子单独定位。
2. ==多组合布局==：直接利用盒子的特性即可。
3. ==栅格布局==：父容器设置`grid-template-columns:repeat(12,1fr)` 即划分12个栅格，子容器用`grid-area: auto/auto/auto/1` 控制跨越几个栅格（最后数字是几就跨过几个栅格）
4. ==容器行列自适应布局==: 利用子项溢出会自动产生隐式网格折行，控制`grid-auto-flow` 就可以控制行(默认row)还是列(column)的自适应


