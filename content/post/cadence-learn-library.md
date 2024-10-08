+++
title = '使用cadence orcad capture搭建元器件库'
date = 2024-10-08
draft = false

+++

## <center>认识元器件库</center>

原理图是用来体现电子电路的工作原理的一种电路图。它直接体现了电子电路的结构和工作原理，详细绘制了电路的全部元器件和它们的连接方式，那么第一步就是要得到元器件，这些元器件都存在元器件库中，元器件库就是一个存储元器件的仓库。

cadence提供了官方元器件库，里面包含了我们常用到的元器件

![cadence元器件库](C:\Users\liuchao\AppData\Roaming\Typora\typora-user-images\cadence%E5%85%83%E5%99%A8%E4%BB%B6%E5%BA%93.png)

按住快捷键P，可以唤出place part边框，如上图所示，在libraries处我们可以添加和删除元器件库，点击图中“+”图标会唤出文件夹窗口，如下图所示：

![image-20241007102641002](C:\Users\liuchao\AppData\Roaming\Typora\typora-user-images\image-20241007102641002.png)

元器件库的后缀是.olb，为了方便认识元器件库的用途，一般在命名上会写出元器件的英文名，如Amplifier.olb就是运算放大器的元器件库，打开该文件即可完成添加。

<img src="C:\Users\liuchao\AppData\Roaming\Typora\typora-user-images\image-20241007103035648.png" alt="image-20241007103035648" style="zoom: 50%;" />

可以看到**Libraries**里完成了AMPLIFIER的添加，在**Part**里便能看到该库里的具体元器件型号，点击**Part**里元器件，用鼠标下滑寻找元器件，当然也可以在**Par**里搜索，如果库里有想要的元器件，找到后双击便能添加到原理图页面了。

## <center>制作元器件库</center>

### 新建一个元器件库

元器件库添加步骤：
1.左键点击该项目，确保我们要添加的元器件库放在这个项目里
2.添加元器件库：File->New->Library，可以看到库已经添加到项目里
3.右击该库，save一下，可以选择Library的添加位置，同时还能够重命名
4.右击该库，点击**new part**添加元器件,会唤出属性框如下图所示
![image-20241007105523246](C:\Users\liuchao\AppData\Roaming\Typora\typora-user-images\image-20241007105523246.png)

### 元器件制作

Name是元器件名字，part reference是元器件编号，例如电阻编号R1,R2等，PCB Footprint是PCB封装，对于封装确定的我们可以提前写好名字，如果封装不确定可以后面再添加，比如电阻有0603 0402 0805等封装，根据电路情况使用不同封装。

Create Convert View为同一个零件创建另一种图形表示方式，这种功能允许设计者为同一零件提供多种视觉表现形式，而不改变零件的基本属性或功能。常用的地方是芯片周围有电阻电容时我们可以选择大小小一些的，方便放置，效果如下图所示：

<img src="C:\Users\liuchao\AppData\Roaming\Typora\typora-user-images\image-20241007113952905.png" alt="image-20241007113952905" style="zoom:50%;" />

Multiple-Part Package是指一个元件包含多个部分(Parts)的封装类型。这种设计方式在创建复杂元件时非常有用，特别是对于大型集成电路(IC)或多功能器件，允许在一个元件符号中定义多个功能部分或子单元。每个部分可以独立绘制和使用，但它们属于同一个物理封装。在Cadence OrCAD中创建Multiple-Part Package时：
1. 在"New Part"对话框中，设置"Parts per "为大于1的值。

2. 选择"Package Type"为"Homogeneous"（同质）或"Heterogeneous"（异质）。Homogeneous：所有部分相同，只需绘制一个部分。Heterogeneous：各部分不同，需分别绘制。

3. 选择"Part Numbering"为"Alphabetic"（字母）或"Numeric"（数字），一般选择字母，比如U4A、U4B都属于U4，其中A、B就是Part Numbering，如下图所示：
    ![image-20241007122658214](C:\Users\liuchao\AppData\Roaming\Typora\typora-user-images\image-20241007122658214.png)

  上图的Package Type是同质，Parts per为2


4. 使用"View -> Next Part"或快捷键(Ctrl + N)在不同部分间切换。

**Part Aliases**（零件别名）是一种为零件或元件创建替代名称的功能。比如对于NPN晶体管，我有好几种NPN产品，产品命名不同，但是原理图都是一个画法，那么我就能用part aliases将产品名字都写出来，这些产品的原理图就都是它了，不需要每个产品都画一遍。Part aliases在以下情况下特别有用：

- **跨项目兼容性**：当不同项目使用不同的命名约定时。
- **供应商特定命名**：在使用多个供应商的零件时保持一致性。
- **功能描述**：使用功能性描述作为零件的别名。

**Attach implementation**允许将原理图中的元件或模块与其对应的PCB封装或更详细的设计实现关联起来，我们一般用来将原理图与Pspice Model关联起来，这样搭建好原理图以后，我们可以跑个Pspice仿真，验证一下电路功能是否是自己想要的。在Implementation type那里选择Pspice Model，Implementation选择自己的Pspice Model模型名字，Implementation Path选择模型路径。

做完上面我们就完成了元器件属性的添加,点击OK，我们就能够进入元器件的具体编辑页面了。

<img src="C:\Users\liuchao\AppData\Roaming\Typora\typora-user-images\image-20241007144750925.png" alt="image-20241007144750925" style="zoom:50%;" />

编辑页面的右边是Package Properties和Part Properties，我们可以在这里修改属性。

<img src="C:\Users\liuchao\AppData\Roaming\Typora\typora-user-images\2024-10-07_145026.png" alt="2024-10-07_145026" style="zoom: 25%;" />

编辑下面的.Normal和.Convert是上面创建元器件属性时Create Convert View引起的，我们可以在两者间切换，画出两种不同的图形。

接下来就是画我们具体原理图了，原理图中的黄色虚线是我们的主体框架，当我们放置PIN脚时，PIN脚不能进入虚框内，我们画图的线或者图形可以用菜单栏里的Place里的组件，有Line,Rectangle,Polyline等，用这些基础图线画出我们想要的波形，如下图所示

<img src="C:\Users\liuchao\AppData\Roaming\Typora\typora-user-images\image-20241007150148748.png" alt="image-20241007150148748" style="zoom: 50%;" />

<img src="C:\Users\liuchao\AppData\Roaming\Typora\typora-user-images\image-20241007150635171.png" alt="image-20241007150635171" style="zoom:50%;" />

<img src="C:\Users\liuchao\AppData\Roaming\Typora\typora-user-images\image-20241007150703643.png" alt="image-20241007150703643" style="zoom:50%;" />

上图是.Normal和.Convert界面的图形，画完图形后回到原理图PAGE页面，如下图所示：

<img src="C:\Users\liuchao\AppData\Roaming\Typora\typora-user-images\image-20241007151915546.png" alt="image-20241007151915546" style="zoom:50%;" />

我们发现电阻R已经在库中了，它有Normal和Convert两种图形可以切换，如果在Part Aliases写上Resistor1，那么Part里也有Resistor1，与R只有名字不同。



## <center>使用第三方库</center>

因为画元器件比较耗时间，如果能够直接添加第三方库到自定义库，那么是一劳永逸的事情，尤其是画MCU这样PIN脚非常多的元器件，可以大大节省时间。一般有两种方式使用第三方库。

### 通过第三方库添加到自定义库

我们在软件页面左边的项目树中，将鼠标移到Library处，右键添加Add file，然后就导入第三方库到自己的项目了，展开第三方库，我们可以看到许多器件

<img src="C:\Users\liuchao\AppData\Roaming\Typora\typora-user-images\image-20241007153543289.png" alt="image-20241007153543289" style="zoom:50%;" />

鼠标左键点击选中想要的元器件，右键复制一下，然后移到自定义库，选择粘贴，就完成了通过第三方库添加元器件到自定义库的所需步骤。

### 通过Design Cache添加到自定义库

当我们拿到一些原理图时，有时没有附加元器件库，那么怎么把原理图中的元器件导入到自己的自定义库呢。我们打开原理图时，Design cache会记录这个过程，我们可以在Design cache中找到所需的元器件

<img src="C:\Users\liuchao\AppData\Roaming\Typora\typora-user-images\image-20241007154113541.png" alt="image-20241007154113541" style="zoom:50%;" />

复制Design cache中的元器件，然后粘贴到自己的自定义库即可

![image-20241007154238927](C:\Users\liuchao\AppData\Roaming\Typora\typora-user-images\image-20241007154238927.png)

至此，元器件库的添加，修改，制作，利用第三方库的使用方式已全部完成，至于更多的功能，读者可以自行摸索。
