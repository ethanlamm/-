MongoDB的安装

官网：www.mongodb.com

一、安装MongoDB

下载地址：[Download MongoDB Community Server | MongoDB](https://www.mongodb.com/try/download/community)

![image-20221115231521342](https://alicloud-imgs.oss-cn-guangzhou.aliyuncs.com/img/image-20221115230317716.png)



<img src="https://alicloud-imgs.oss-cn-guangzhou.aliyuncs.com/img/image-20221115230333936.png" alt="image-20221115230333936"  />



下载完成后，双击下载的msi文件，进入安装引导界面，点击Next：

![img](https://img2022.cnblogs.com/blog/1653712/202211/1653712-20221107160412122-1017564212.png)



在协议界面，勾选协议，点击Next：

![img](https://img2022.cnblogs.com/blog/1653712/202211/1653712-20221107160424877-1459659307.png)



选择Custom自定义安装，进入自定义安装界面：(默认安装到C盘)

![img](https://img2022.cnblogs.com/blog/1653712/202211/1653712-20221107160438212-1887494666.png)



在自定义安装界面，选择安装在D盘，点击Next：

![img](https://img2022.cnblogs.com/blog/1653712/202211/1653712-20221107160451233-732672359.png)



默认配置，点击Next

![img](https://img2022.cnblogs.com/blog/1653712/202211/1653712-20221107160504554-1575511196.png)



建议不勾选`Install MongoDB Compass`——MongoDB的官方图形用户界面，可以后自行安装 [MongoDB Compass Download | MongoDB](https://www.mongodb.com/try/download/compass)，点击Next

<img src="https://alicloud-imgs.oss-cn-guangzhou.aliyuncs.com/img/image-20221115230945994.png" alt="image-20221115230317716"  />





点击Install，开始安装：

![img](https://img2022.cnblogs.com/blog/1653712/202211/1653712-20221107160540049-66618815.png)



点击Finish，**若要重启，选择稍后重启**

![img](https://img2022.cnblogs.com/blog/1653712/202211/1653712-20221107160549875-1863817766.png)



二、安装Mongo Shell

下载地址：https://www.mongodb.com/try/download/shell

下载zip格式，完事后解压

在安装MongoDB的文件夹中，新建一个文件夹`Client`，将刚才解压的其中文件复制到`Client`文件夹中

![image-20221115230945994](https://alicloud-imgs.oss-cn-guangzhou.aliyuncs.com/img/image-20221115231521342.png)



将Mongo Shell添加到系统环境变量中（mongosh.exe在刚才复制过来的bin文件中）

电脑搜索`查看高级系统设置`=>`环境变量`=>选中`系统变量`中的`Path`=>点击`编辑`=>选择`新增`=>将`D:\MongoDB\Client\bin`添加=>`确定`.....

查看是否成功：

打开终端，输入**mongsh**，出现以下内容就OK

![image-20221115232906896](https://alicloud-imgs.oss-cn-guangzhou.aliyuncs.com/img/image-20221115232300856.png)





三、重启电脑

若发现重启后电脑不能连网，右键=>打开"网络和Internet"设置

选择  网络和共享中心

![image-20221115232300856](https://alicloud-imgs.oss-cn-guangzhou.aliyuncs.com/img/image-20221115232706160.png)

选择 Internet 选项(左下角)

![image-20221115232706160](https://alicloud-imgs.oss-cn-guangzhou.aliyuncs.com/img/image-20221115232744908.png)



连接 => 局域网配置

![image-20221115232744908](https://alicloud-imgs.oss-cn-guangzhou.aliyuncs.com/img/image-20221115232906896.png)





四、文档

![image-20230106091803662](https://alicloud-imgs.oss-cn-guangzhou.aliyuncs.com/img/image-20230106091803662.png)



查看所有API

- 方法一：点击左侧`MongoDB Shell(mongosh)`=>`Reference`=>`Methods`
- 方法二：点击左侧`Reference`=>`mongosh Methods`

