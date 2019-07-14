# matplotlib入门基础

* 注：考虑到Jupyter notebook的便捷性，且能够让我们编写代码边运行边做笔记，本次学习均在该平台上。

* 如果发现图表上的中文字符或是负数数值无法加载，请输入：

  ```python
  plt.rcParams['font.sans-serif']=['SimHei'] #用来正常显示中文标签
  plt.rcParams['axes.unicode_minus']=False #用来正常显示负号
  ```

  

**matplotlib是一个数据绘图库，可以将枯燥的数据转换成容易接收信息的图表**

​	我们来了解下一幅matplotlib图像的组成结构

* 第一层：`canvas` 类似画板 
* 第二层：`figure` 类似画布（或理解为画图区域） 
* 第三层：`axes` 子图（或理解为坐标系） 
* 第四层：各类图表信息，包括：xaxis（x轴），yaxis（y轴），title（标题），legend（图例）， grid（网格线），spines（边框线）,data（数据）等等
* 所以， `canvas`位于最底层，当我们导入matplotlib库的时候就已经存在了，我们不需要多管这个 `figure`建立在`canvas`之上，从这里就需要我们开始操作了`axes`建立在`figure`之上 图形以及坐标轴、图例等信息都是建立在`Axes`之上

使用`matplotlib`需要我们导入模块：

```python
import numpy as np
import matplotlib.pyplot as plt
%matplotlib inline #将生成的图表显示（内嵌）在Jupyter页面中
```

首先我们先举一些小例子来说明一下：

声明两个numpy数组a和b：

```python
a = np.arange(1,10,0.2)
b = np.sin(a)#b是a的正弦函数
```

我们想要在他们之间建立联系，并画出图像。

画图分为三个步骤：

1、生成画布：

```python
plt.figure()
```

2、准备数据：

```python
plt.plot()#折线图
plt.bar()#柱状图
plt.pie()#饼状图
plt.hist()#直方图
#其余还有散点图，箱线图等，大家可以自行去了解
```

3、展示：

```python
plt.show()						
```



在画图之前，我们应该要新建一个画布：

```python
plt.figure(figsize=(20,5))#定义一个画布
```

接着我们就可以调用plot函数进行画图啦：

```python
plt.plot(a,b,'bo')#画图函数，第三个参数是控制字符串
```

运行结果：

![1563075413704](C:\Users\李瀚哲\AppData\Roaming\Typora\typora-user-images\1563075413704.png)

`plot`函数可以接受很多参数：

```
plot函数基本的用法有以下四种：
1、默认参数
	plt.plot(x,y)
2、指定参数
	plt.plot(x,y, format_str)
3、默认参数，x 为 0~N-1
	plt.plot(y)
4、指定参数，x 为 0~N-1
	plt.plot(y, format_str)
```

其中字符参数可以有表示颜色的和表示风格类型的：

![1563075551956](C:\Users\李瀚哲\AppData\Roaming\Typora\typora-user-images\1563075551956.png)

![1563075584233](C:\Users\李瀚哲\AppData\Roaming\Typora\typora-user-images\1563075584233.png)



在上例中，我们将a作为横坐标，b作为纵坐标，字符参数为'bo'，意味着生成蓝色的圆点折线图。

我们再新增一条线条c：

```python
c=np.cos(a)
plt.plot(a,b,color='r',linestyle='--',linewidth=3.0)
plt.plot(a,c,"g-.",label='cos',linewidth=3.0)#若不加lable 就容易把两条线弄混
plt.legend()#该函数用于给图像加上图例
plt.xlabel("弧度")#在x轴上加入标签
plt.ylabel("正/余弦值")
```

运行结果：

![1563075818790](C:\Users\李瀚哲\AppData\Roaming\Typora\typora-user-images\1563075818790.png)

在上面的例子中可以发现，我们可以在参数中设置label属性来表示线条所代表的信息；通过设置`color`属性来改变线条的颜色，通过`linestyle`和`linewidth`属性来改变线条的样式和宽度。

如果要显示图例，我们则需要通过`plt`的`legend`函数来实现

可以通过`plt.xlabel`和`plt.ylabel`函数来设置x轴和y轴的标签。



####  接下来我们会分析一些数据样例，直接通过matplotlib或者是pandas来进行绘图

在使用pandas绘图之前，我们来看看它的思维导图

* 折线图：

  ![1563076653683](C:\Users\李瀚哲\AppData\Roaming\Typora\typora-user-images\1563076653683.png)

* 柱状图：

  ![1563076691657](C:\Users\李瀚哲\AppData\Roaming\Typora\typora-user-images\1563076691657.png)

* 饼图：

![1563076730277](C:\Users\李瀚哲\AppData\Roaming\Typora\typora-user-images\1563076730277.png)

* 直方图：

![1563076811615](C:\Users\李瀚哲\AppData\Roaming\Typora\typora-user-images\1563076811615.png)

导入模块：

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
%matplotlib inline
```

首先我们找了一个大学生薪资排行榜的`csv`数据，并通过`pandas`的`read_csv`函数去进行读取：

```python
df=pd.read_csv("salary.csv")
```

我们打印`df`的部分信息看看：

```python
df.head(5)
```

![1563077044135](C:\Users\李瀚哲\AppData\Roaming\Typora\typora-user-images\1563077044135.png)

发现通过`head`函数可以指定观看的条目数量。

我们可以直接通过`df.category`或者`df[category]`来对`category`列进行查看。

这里我们要说明一个用的十分广泛的函数：`value_counts()`。它是一种查看表格某列中有多少个不同值的快捷方法，并计算每个不同值有在该列中有多少重复值。

```python
df.category.value_counts()#查看各种类型的学校都有多少个
```

运行结果：

![1563088314874](C:\Users\李瀚哲\AppData\Roaming\Typora\typora-user-images\1563088314874.png)



如果我们要对以上显示的信息用图像表示出来，我们可以直接调用`plot`函数，这属于`pandas`的绘图方法，与`plt`十分类似。

```python
df.category.value_counts().plot(kind='bar')#可以通过设置参数figsize来改变图像大小
```

运行结果：

![1563088419327](C:\Users\李瀚哲\AppData\Roaming\Typora\typora-user-images\1563088419327.png)

我们也可以画折线图：

```python
a=df.category.value_counts().plot()#可以自己设置参数
a.set_xticklabels(df.category.value_counts().index)#设置横坐标的值
```

运行结果：

![1563089391677](C:\Users\李瀚哲\AppData\Roaming\Typora\typora-user-images\1563089391677.png)



我们也直接用matplotlib画折线图：

```python
a=['理工','综合','财经','师范','医药','语言','艺术','农林','政法','体育']
b=df.category.value_counts().values
plt.xticks(np.arange(len(a)),a)#重新调整x轴的刻度
plt.plot(b,color='r')
plt.xlabel("category")
plt.ylabel("数量")
```

运行结果：

![1563089690881](C:\Users\李瀚哲\AppData\Roaming\Typora\typora-user-images\1563089690881.png)

其中`plt.xticks(np.arange(len(a)),a)`函数是为了重新调整x轴的顺序，否则将会按照字典序，与我们输入数组时的顺序不一致。

* 代码中a也可以用`df.category.value_counts().index`来代替

我们再借上述例子来画一个**饼形图**：

```python
plt.pie(b,labels=a,autopct='%.0f%%',textprops = {'fontsize':15, 'color':'k'},radius=2)
# 设置x，y轴刻度一致，这样饼图才能是圆的 
plt.axis('equal') 
```

运行结果：

![1563089859232](C:\Users\李瀚哲\AppData\Roaming\Typora\typora-user-images\1563089859232.png)

`matplotlib`画饼图用到的是pie()函数，其中`autopct`属性是为了设置显示数值的精度，`textprops`属性是为了设置字体的样式，`radius`代表圆的半径。由于饼形图默认为椭圆，`axis`函数用于设置为正圆。饼形图还有很多设置参数的方法，留给大家自己去查阅探索。



使用`pandas`绘图则调用`plot`函数的子函数`pie`函数：

```python
df.category.value_counts().plot.pie(figsize=(6,6))
```

![1563090179963](C:\Users\李瀚哲\AppData\Roaming\Typora\typora-user-images\1563090179963.png)

用`pandas`画饼图时，圆的宽扁则是通过设置`figsize`属性来实现。



画**直方图**的方法则是调用hist函数

```python
df.category.value_counts().hist(alpha=0.5,bins=20,color='r')
```

运行结果：

![1563090344824](C:\Users\李瀚哲\AppData\Roaming\Typora\typora-user-images\1563090344824.png)

其中`alpha`属性表示透明度，`bins`属性表示图将条状图划分的个数（数据的宽度）。

`matplotlib`画直方图的方法则是调用`plt.hist()`函数，区别不大，可以通过以上其他图例进行类比。



在使用`pandas`时，我们往往要对一组数据进行分析，当我们想要以某一属性划分时，可以采用`groupby`函数：

```python
nef=df.groupby('province')['985'].sum()#根据'province'进行分组，查看'985'列的信息。
```

我们也可以通过以下表示来同时查看按某属性分组时的多列信息：

```python
df.groupby('province')[['985','211']].sum().sort_values(by='985',ascending=False).plot(kind='bar',figsize=(15,5))
```

运行结果：

![1563090840197](C:\Users\李瀚哲\AppData\Roaming\Typora\typora-user-images\1563090840197.png)

这样就可以在一张图上查看两组数据的信息。

我们也可以通过聚合函数，对多组数据进行多种特征的分析：

```python
df.groupby(by='category').agg(['max','min','mean'])[['2017','2015','2013']]#现根据学校类别进行分组，看三年的最大值、最小值、平均值。要用列表来表示取三列
```

运行结果：

![1563090949481](C:\Users\李瀚哲\AppData\Roaming\Typora\typora-user-images\1563090949481.png)



未完待续……