# Qt主窗口 

## 一、主窗口介绍

QMainWindow类继承自QWidget类，<span style=color:red;background:yellow;font-size:20px>**因此主窗口就是一个普通的部件，只不过主窗口拥有自已的布局，在主窗口中特定的位置只能添加特定的子部件而已**</span>。 因为主窗口有自已的布局，因此不能在主窗口上设置布局管理器。  

QMainWindow是一个为用户提供主窗口程序的类，包含一个菜单栏、多个工具栏(停靠范围是上下左右)、多个铆接部件(也叫浮动窗口)、一个状态栏、一个中心部件，[是一个应用程序的基础]()。

## 下图为主窗口的布局图：



<img src="./Qt%E4%B8%BB%E7%AA%97%E5%8F%A3.assets/image-20250711190403370.png" alt="image-20250711190403370" style="zoom: 50%;" />

下面给出一个在实际情况下的案例图，并于主窗口进行一一对应，图形如下：

<img src="./Qt%E4%B8%BB%E7%AA%97%E5%8F%A3.assets/image-20250711190518562.png" alt="image-20250711190518562" style="zoom:50%;" />





## 菜单栏

+ 在主窗口中，菜单栏只有一个，使用的是QMenuBar类展示

+ 菜单项用使用的是QMenu类展示，菜单栏可以添加多个菜单，用mbar->addMenu(fileMenu)，菜单中还可以继续添加菜单项，用fileMenu->addMenu("打开")

```c++
#include "mainwindow.h"

#include <QMenuBar>
#include <QMenu>
#include <QPushButton>

MainWindow::MainWindow(QWidget *parent)
    : QMainWindow(parent)
{
   setWindowTitle("测试主窗口中的菜单栏");
   resize(1000,800);

//   创建菜单栏对象的时候指定父对象
//  this 是在主函数中创建 w 对象时传入构造函数中
//  所有类的成员函数都有一个隐藏参数：this，此时this指向w对象
    QMenuBar *mbar = new QMenuBar(this);

//    创建对象之后，调用setParent指定父对象
        //mbar->setParent(this);
    mbar->resize(500,100);

//    创建菜单
    QMenu *fileMenu = new QMenu("文件",this);
    QMenu *editMenu = new QMenu("编辑",this);
    QMenu *toolMenu = new QMenu("工具",this);
//   菜单栏添加菜单
    mbar->addMenu(fileMenu);
    mbar->addMenu(editMenu);
    mbar->addSeparator();
    mbar->addMenu(toolMenu);
//  菜单添加菜单项
    fileMenu->addMenu("新建");
    fileMenu->addMenu("打开");
    fileMenu->addSeparator();
    fileMenu->addMenu("保存");

//
    QPushButton *btn = new QPushButton("按钮",this);
    btn->move(50,40);
    btn->resize(150,60);

    connect(btn,&QPushButton::clicked,[=](){
        close();
    });

}

MainWindow::~MainWindow()
{
}


```



测试结果

<img src="./Qt%E4%B8%BB%E7%AA%97%E5%8F%A3.assets/image-20250711202628812.png" alt="image-20250711202628812" style="zoom:50%;" />





## 工具栏



+ 在主窗口中，工具栏有多个，使用的是QToolBar类展示。
+ 可以往工具栏 tbar 添加多个动作（Action）







### 添加资源文件的步骤

- 在Qt项目中经常会使用资源文件，所以就需要添加资源文件，以图片为例，**<span style=color:red;background:yellow;font-size:30px>添加的步骤如下：</span>**

  - 右键项目-> Add New(添加新文件)->Qt->Qt Resource File(Qt资源文件)，然后给资源文件取名，如果文件名叫res，就会生成res.qrc；
  - 点击项目下的任何一个文件，右键，然后选择"Show in Explorer"打开项目路径，将事先图片文件夹拷贝到项目路径下；
  - 点击Resources下的res.qrc，右键"Open in Edit"，点击"Add Prefix"添加前缀（可以修改默认前缀），点击"Add Files"添加资源文件到项目，点击"Build"(左下角的锤子图标)，这样就可以在项目"Resources"资源文件夹下看到新添加的所有图片，资源文件添加成功；
  - 后续代码中使用资源文件就可以使用 “冒号 + 前缀名 + 文件名”形式即可。

### 工具栏的使用代码

```c++
#include "mainwindow.h"

#include <QToolBar>
#include <QAction>

MainWindow::MainWindow(QWidget *parent)
    : QMainWindow(parent)
{
    setWindowTitle("测试主窗口中的工具栏");
    resize(600,480);

    QToolBar *tbar = new QToolBar("工具栏",this);
    tbar->resize(300,100);

    //往工具栏 tbar 添加一个动作（Action），这个动作的名称是 "AAA"
    tbar->addAction("AAA");
    tbar->addAction(QIcon(":/image1/Image/bee.jpg"),"BBB");
    tbar->setToolButtonStyle(Qt::ToolButtonTextBesideIcon);
    //几个常用属性
    tbar->setMovable(true);//工具栏是否可以移动（默认是可以的,也就是true）
    tbar->setFloatable(true);// 工具栏是否可以漂浮
    tbar->setAllowedAreas(Qt::RightToolBarArea);//设置可以停靠的位置

}

MainWindow::~MainWindow()
{
}


```





测试结果

<img src="./Qt%E4%B8%BB%E7%AA%97%E5%8F%A3.assets/image-20250711212008898.png" alt="image-20250711212008898" style="zoom:50%;" />

## 主窗口程序





```c++
#include "mainwindow.h"

#include <QMenuBar>
#include <QMenu>
#include <QAction>
#include <QToolBar>
#include <QDockWidget>
#include <QStatusBar>
#include <QPushButton>

MainWindow::MainWindow(QWidget *parent)
    : QMainWindow(parent)
{
    setWindowTitle("测试主窗口");
    resize(600,480);

    //---------------添加菜单栏（主窗口中只有一个）--------------
    //菜单栏创建（菜单栏，最多只能有一个,所以是setXXX）
    //注意：menuBar()使用懒加载机制，只有在首次调用时才会创建菜单栏对象;
    //QMainWindow会自动将菜单栏添加到窗口的顶部布局中，菜单栏的位置和大小
    //由QMainWindow的布局管理器控制;
    QMenuBar *mbar = menuBar();//该函数会创建一个菜单栏

     //将菜单栏放在窗口中，可以不加
     setMenuBar(mbar);

     //创建菜单
    QMenu *fileMenu = mbar->addMenu("文件");
    QMenu *editMenu = mbar->addMenu("编辑");
    QMenu *saveMenu = mbar->addMenu("保存");

    //创建菜单项
    QAction *newAc = new QAction("新建");
    QAction *openAc = new QAction("编辑");
    QAction *saveAc = new QAction("保存");

    //菜单添加菜单项
    fileMenu->addAction(newAc);
    fileMenu->addAction(openAc);
    fileMenu->addAction(saveAc);

    //--------------添加工具栏--------------
    //创建工具栏，可以有多个，所以是addXXX
    QToolBar *tBar = new QToolBar();

    // 将工具栏添加到窗口中
    addToolBar(Qt::TopToolBarArea,tBar);

    //这个是设置 “允许用户拖动到哪些区域”
    //这里限制了：只能拖到左侧或右侧！
    tBar->setAllowedAreas(Qt::LeftToolBarArea | Qt::RightToolBarArea);

    //    工具栏中可以设置内容
    tBar->addAction(newAc);
    tBar->addAction(openAc);
    tBar->addAction(saveAc);

    //-------------添加浮动窗口--------------
     //铆接部件可以有多个，所以是addXXX
    QDockWidget *dock = new QDockWidget("浮动窗口");
    //将铆接部件添加到窗口中，同时指定添加到左边
    addDockWidget(Qt::LeftDockWidgetArea,dock);

    //-------------添加中心部件------------
    //中心部件只能有一个,所以是setXXXX
    QPushButton *btn = new QPushButton("中心按钮");
    //将中心部件添加到窗口中
    setCentralWidget(btn);

    //-------------添加状态栏（主窗口中只有一个）-------------
    //statusBar() 函数，用于获取或创建主窗口的状态栏（QStatusBar）。状态栏
        //通常用于显示应用程序的临时消息、进度、提示信息等内容
        //懒加载机制，只有在首次调用时才会创建状态栏对象,QMainWindow会自动将状态栏
        //添加到窗口的底部布局中；状态栏的位置和大小由QMainWindow的布局管理器控制。
        //状态栏只能有一个，所以说是setXXX
        //创建状态栏
     QStatusBar *sBar = statusBar();
//     (这个可以不写)
    setStatusBar(sBar);

    QPushButton *btn1 = new QPushButton("按钮1");
    QPushButton *btn2 = new QPushButton("按钮2");
    QPushButton *btn3 = new QPushButton("按钮3");

//    向状态栏添加按钮
    sBar->addWidget(btn1); //左对齐，可以被其他控件挤压

    sBar->addWidget(btn2);

    sBar->addPermanentWidget(btn3);//  右对齐，固定显示，不会被遮挡。

}

MainWindow::~MainWindow()
{
}


```



<img src="./Qt%E4%B8%BB%E7%AA%97%E5%8F%A3.assets/image-20250712092720525.png" alt="image-20250712092720525" style="zoom:50%;" />



