---
title: Aseprite源码编译-Win
tags:
- 软件
- 像素画
- Aseprite
- win
categories: 
- 软件编译
---

## 介绍

Aseprite 是一款十分受欢迎的专业像素动画及像素艺术创作软件.支持Windows,Mac和Linux.可以从[官网](https://www.aseprite.org/) 或者[Steam](https://store.steampowered.com/app/431730/Aseprite/) 付费获取软件,但同时它是开源的，如果从源代码编译，则可以免费使用。

<!--more-->

###### 编译相关工具链接
+ 官方编译指南：[https://github.com/aseprite/aseprite/blob/master/INSTALL.md](https://github.com/aseprite/aseprite/blob/master/INSTALL.md)
+ Aseprite源码：[https://github.com/aseprite/aseprite/releases](https://github.com/aseprite/aseprite/releases)
+ Skia aseprite-m81：[https://github.com/aseprite/skia/releases](https://github.com/aseprite/skia/releases)
+ CMake：[https://cmake.org/download/](https://cmake.org/download/)
+ Ninja：[https://github.com/ninja-build/ninja/releases](https://github.com/ninja-build/ninja/releases)
+ Visual Studio Community：[https://visualstudio.microsoft.com/downloads/](https://visualstudio.microsoft.com/downloads/)
+ Aseprite汉化文件: [https://github.com/J-11/Aseprite-Simplified-Chinese](https://github.com/J-11/Aseprite-Simplified-Chinese)

## 编译

### 准备工作

* Aseprite源码,Skia aseprite-m81,CMake,Ninja,Visual Studio Community下载最新版即可
* Cmake 如下载msi包,则安装时选择 "Add Cmake to the system PATH for all user" 将其添加至环境变量;如下载zip包则需要将安装目录中的bin目录路劲添加至环境变量PATH中
* ninja 需要将安装路径添加至环境变量PATH,也可在Cmake添加环境变量后放入Cmake的bin目录下
* Visual Studio Community 安装时选择 "Workloads" 中的 "Desktop development with C++",之后在"Individual components" 中选择最新 "Windows 10 SDK" (经测试,即使在win7中选择此项同样可以成功安装Aseprite)

![工作负载(Workloads)](../Aseprite源码编译-Win/imgs/Workloads20200921141524.png)
![单个组件(Individual components)](../Aseprite源码编译-Win/imgs/Individual_components20200921141741.png)

### 编译

1. 打开cmd,配置开发人员命令行,输入命令:
``` cmd cmd命令
call "{Visual Studio Community安装目录}\Common7\Tools\VsDevCmd.bat" -arch=x64
```

2. 进行编译,编译结束后在build/bin目录即编译好后的Aseprite软件
``` cmd cmd命令
#切换至aseprite解压目录
cd /d {aseprite解压路径}

#创建build目录
mkdir build

#切换至build目录
cd build

#执行cmake命令编译
cmake -DCMAKE_BUILD_TYPE=RelWithDebInfo -DLAF_BACKEND=skia -DSKIA_DIR={Skia aseprite-m81解压目录} -DSKIA_LIBRARY_DIR={Skia aseprite-m81解压目录}\out\Release-x64 -G Ninja .. 

#ninja构建软件,会出现很多 failed / not found / warning 只要不出现error,并不影响编译结果
ninja aseprite
```
![编译完成后的build/bin目录](../Aseprite源码编译-Win/imgs/compiler_result20200921144949.png)

### 编译收尾
Aseprite运行只需要build/bin目录下的data目录及aseprite.exe,可以单独将它们拷出后删除所有相关编译工具.
![Aseprite](../Aseprite源码编译-Win/imgs/Aseprite20200921150324.png)

## 汉化
1. 在[Aseprite汉化文件](https://github.com/J-11/Aseprite-Simplified-Chinese)下载下来的文件为hanhua-1.2.23.aseprite-extension,是Aseprite的扩展文件
2. 打开Aseprite,选择Edit-preferences,之后再左侧项目中选择Extensions,在右侧选择Add Extension,找到下载的汉化文件,选中点击OK会自动进行安装,安装完成后在右侧会增加最新一条Languages Simple Chinese,此时表示插件安装成功
![preference-extensions界面](../Aseprite源码编译-Win/imgs/Aseprite_Extension20200921151346.png)
3. 接下来选中左侧General,在右侧language中选择sChinese,点击ok或者apply即可完成汉化操作.点击apply后preference并不会即时更新汉化,但此时菜单栏及其他部分已汉化,需重新打开窗口后才能生效.
![preference-General界面](../Aseprite源码编译-Win/imgs/Aseprite_General20200921151346.png)
4. 汉化后效果
![Aseprite汉化后界面](../Aseprite源码编译-Win/imgs/Aseprite_Chinese20200921153025.png)
