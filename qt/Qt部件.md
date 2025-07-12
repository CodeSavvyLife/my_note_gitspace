### 三、Qt部件

#### 1、基本概念



Qt把建立用户界面的元素称为窗口部件，简称<span style=color:red;background:yellow;font-size:20px>部件</span> 。

<span style=color:red;background:yellow;font-size:20px>把没有嵌入到其它部件中的部件被称为窗口</span>，通常来说窗口是没有父部件的部件（也可以有父部件，比如一个部件设置了父部件，但是设置 Qt::Window标志，那么该部件也是窗口 ）  

## 2、布局管理器

<span style=color:red;background:yellow;font-size:20px>Qt的布局管理类或由这些类创建的对象称为布局管理器，简称布局</span>，对于主窗口而言，默认的已经将菜单栏、状态栏、工具栏等等进行了布局，所以主窗口不需要布局管理器，但是对于QWidget等等，没有设置部件到底存在哪里，所以需要进行布局。 

### 3、UI界面的设计

也可以称为设计师模式，对于设置静态界面而言（也就是窗口中的部件不会改变相对位置，不会出现某个部件突然因为某些条件而消失的情况），这种情况下，推荐大家使用UI界面设计的方式设计界面。

#### 3.1、使用UI界面的步骤

- 第一步：首先根据需要选择合适的部件（比如：按钮、标签、行文本）;
- 第二步：各个部件之间的布局，可以将各个部件放在不同的Widget中，然后点击水平、垂直、网格、二维表格布局，如下图：

<img src="./Qt%E9%83%A8%E4%BB%B6.assets/image-20250712212710147.png" alt="image-20250712212710147" style="zoom:50%;" />





然后可以根据需求设置弹簧，

<img src="./Qt%E9%83%A8%E4%BB%B6.assets/image-20250711180617793.png" alt="image-20250711180617793" style="zoom:50%;" />

弹簧是可以设置大小的，比如：固定宽度与高度；

- 如果不满足上一次的布局，可以打破布局，使用如下按钮：

![image-20250711180746656](./Qt%E9%83%A8%E4%BB%B6.assets/image-20250711180746656.png)

然后进行重新布局

- 如果还有资源文件，可以进行资源文件的添加，添加方式一样，但是可以在右下角找到icon关键字进行设置。



##### 3.2、登录窗口的设计过程

<img src="./Qt%E9%83%A8%E4%BB%B6.assets/image-20250711164433232.png" alt="image-20250711164433232" style="zoom: 33%;" />



##### 3.3、登录窗口的设计结果

<img src="./Qt%E9%83%A8%E4%BB%B6.assets/image-20250711164400393.png" alt="image-20250711164400393" style="zoom:50%;" />

#### <span style=color:red;background:yellow;font-size:30px>4、布局管理器（非常重要）</span>

##### 4.0、<span style=color:red;background:yellow;font-size:25px>布局管理器的使用步骤</span>

























