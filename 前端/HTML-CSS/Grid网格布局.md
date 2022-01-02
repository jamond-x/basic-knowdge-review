## 前端CSS基础知识篇——Grid网格布局

<img src="C:\Users\xiangxinqiang\Desktop\FWF\周贴\1.9第一周\img\1.png" style="zoom: 25%;" />  <img src="C:\Users\xiangxinqiang\Desktop\FWF\周贴\1.9第一周\img\2.png" style="zoom:25%;" />

####      直接切入主题......

​	Grid网格布局是一种强大二维布局系统，它可以同时处理行与列，将页面分割为数个网格，并且能够将其任意排列。它将整个页面或页面中你所指定的区域这个大容器任意分割为网状般的数个小容器，每个网格小容器内的内容相对独立，当行高、列宽设定为定值时即使格子内容溢出也不会挤压其他格子里的内容（但是会重叠，可通过z-index属性设置优先显示）。整个网格可以放在一个盒子里，通过对盒子的移动实现对网格整体位置的控制，也可通过Justify-content等属性在盒子内对网格位置进行控制。网格能够覆盖较大的区域，意味着它可以架构你的页面的一大板块，撑起一个版块的骨架！

<img src="C:\Users\xiangxinqiang\Desktop\FWF\周贴\1.9第一周\img\show2.png" style="zoom: 67%;" />



#### 首先，我们了解一些基本概念

- ##### 行、列(row,column)

> 网格布局中的行、列和我们平常理解的行、列一样，如图...
>
> 行↓↓↓

<img src="C:\Users\xiangxinqiang\Desktop\FWF\周贴\1.9第一周\img\行最终图.png" style="zoom: 50%;" />

> 列↓↓↓

<img src="C:\Users\xiangxinqiang\Desktop\FWF\周贴\1.9第一周\img\列column.png" style="zoom: 67%;" />

- ##### 网格线（grid line)

> 网格线是定位子网格的依据，它穿插在整个网格之间，分为行线(row line)、列线(column line)
>
> 如拥有x行，y列的网格，就有x+1条row lines，y+1条column lines

![](C:\Users\xiangxinqiang\Desktop\FWF\周贴\1.9第一周\img\网格线不要再改了.png)

> 例：在上图3*3的网格中，网格A位于第2条与第3条row line 和  第1条与第2条column line 之间

```css
#A{
    grid-row:2/3;
    grid-column:1/2;
}
```



#### 建立网格

- ##### 在包含网格的容器中使用Display:grid;属性

  可以在body标签下给出**Display:grid;**用网格搭建整个页面的骨架,或者在一个div盒子container中搭建网格

  ```css
  #container{
  	display:grid;
  	grid-template-rows:100px 50px 40px;
  	grid-template-columns:50px 50px 50px;
  }
  body{
  	display:grid;
  	grid-template-rows:repeat(12,1fr);
  	grid-template-columns:repeat(12,1fr);
  }
  ```

- ##### 使用grid-template-columns，grid-template-rows初始化行高，列宽

   grid-template-columns: col1value  col2value col3value;

  含有三个值表示建立3列(column)并分别给出1,2,3列的列宽

  grid-template-rows: row1value  row2value ;

  同理建立2行(row)并分别给出1,2行的行高

   ↓↓↓

  ```css
  #container{
      	grid-template-columns: 100px  50px 25px//建立3列(column)并分别给出1，2,3列的列宽分别为 100px 50px 25px
          grid-template-rows:40px 40px;//两行的行高均为40px;
  }
  ```

  ![](C:\Users\xiangxinqiang\Desktop\FWF\周贴\1.9第一周\img\设置行高列宽最终.png)

  - **Repeat函数，fr关键字**

    当设置多列相同网格时，每列的宽度相等，这时可以用Reprat()函数

    Repeat(重复次数，单个值)

    ```css
    grid-template-columns:Repeat(5,100px);
    ```

    表示创建5列相同且列宽为100px的column

    

    fr为fraction 的缩写，意为"片段"，设置列或行占剩余空间的一个比例，很适合用做响应式布局！

    ```css
    grid-template-columns:100px 1fr 1fr;
    ```

    第一例宽度固定为100px，第二三列在容器剩余空间以1:1占据

    ![](C:\Users\xiangxinqiang\Desktop\FWF\周贴\1.9第一周\img\fr.png)

    ```
    grid-template-columns:100px 2fr 1fr;
    ```

    容器剩余空间二三列以2:1占据

    ![](C:\Users\xiangxinqiang\Desktop\FWF\周贴\1.9第一周\img\fr2.png)

- #### grid-gap

  grid-gap属性用于设置单位子网格之间的距离；

  grid-gap:  rowgap  columngap;两个值分别表示行间距，列间距。

  grid-gap: value;若只给一个值表示rowgap =columngap=value

  ![](C:\Users\xiangxinqiang\Desktop\FWF\周贴\1.9第一周\img\gap1.png)

  ![](C:\Users\xiangxinqiang\Desktop\FWF\周贴\1.9第一周\img\gap2.png)

  

#### 创建子网格区域模板

##### grid-area可将指定元素覆盖到多个单位子网格，也可将指定元素进行位置移动

- ##### grid-area用法一——设置单个元素的覆盖区域及位置

  格式为：

  grid-area: row-start / column-start / row-end/ column-end;

  四个值表示为该元素在网格中对应的位置， row-start为行开始的网格线，column-start为列开始的网格线，row-end为行结束的网格线，column-end为列结束的网格线

  通过四个值可以准确的将一个元素定位在网格中

  例1：

  在3*3网格中让元素5占据底端位置

  ```css
   .container {
      font-size: 40px;
      min-height: 300px;
      width: 100%;
      background: LightGray;
      display: grid;
      grid-template-columns: 1fr 1fr 1fr;
      grid-template-rows: 1fr 1fr 1fr;
      grid-gap: 10px;
    }
  .item5 {
      background: PaleGreen;
      grid-area:3/1/4/4;      //直接给出网格线
    }
  <div class="container">
    <div class="item1">1</div>
    <div class="item2">2</div>
    <div class="item3">3</div>
    <div class="item4">4</div>
    <div class="item5">5</div>
  </div>
  ```

  ![](C:\Users\xiangxinqiang\Desktop\FWF\周贴\1.9第一周\img\例1.png)

例2：

​	

```css
.item5 {
    background: PaleGreen;
    grid-area:2/2/4/4;
  }
```

![](C:\Users\xiangxinqiang\Desktop\FWF\周贴\1.9第一周\img\例2.png)

例3：

```
.item5 {
    background: PaleGreen;
    grid-area:1/1/3/3;
  }
```

![](C:\Users\xiangxinqiang\Desktop\FWF\周贴\1.9第一周\img\例3.png)



- ##### grid-area用法二——组合排列

    首先需要给单个元素用grid-area设置元素名字

  ```css
  #one{
      grid-area:name1;
  }
  #two{
      grid-area:name2;
  }
  ...
  ```

  再于创建网格的大容器(body或div大盒子container）的CSS中使用grid-template-area属性利用元素名称进行排列，grid-template-area属性后给出名字的顺序即位置就是元素在网格中排列的顺序和位置

  如在3*3的网格里

  ```css
  grid-template-area:"name1 name2 name3"
  				   "name4 name5 name6"
  				   "name7 name8 name9";
  ```

  每一个**“name”**所在位置即为一个网格，每一个name的元素会处于对应的网格中，其中的不同name可以进行组合

  如果一个name位置是 **"."**，则表示该网格为空，不放置任何元素

  ```
  grid-template-area:"name1 name1 name3"
  				   "name4   .   name6"
  				   "name7 name7 name7";
  ```

  例：

  ```css
  //为了阅读方便省去了多余代码
  #container{
              grid-template-areas: "name1 name1 name2"
                                   "name3   .   name4"
                                   "name5 name5 name5";
          }
          #item1{
              grid-area: name1;
          }
          #item2{
              grid-area: name2;
          }
          #item3{
              grid-area: name3;
          }
          #item4{
              grid-area: name4;
          }
          #item5{
              grid-area: name5;
          }
  ```

  ![](C:\Users\xiangxinqiang\Desktop\FWF\周贴\1.9第一周\img\area用法二.png)













