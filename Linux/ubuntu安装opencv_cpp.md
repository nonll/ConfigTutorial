# ubuntu安装opencv_c++

## 1. 安装依赖
1. 安装g++, cmake, make, wget, unzip，若已安装，此步跳过

``` bash
sudo apt install -y g++
sudo apt install -y cmake
sudo apt install -y make
sudo apt install -y wget unzip

```
2. 安装opencv依赖的库

``` bash
sudo apt-get install build-essential libgtk2.0-dev libgtk-3-dev libavcodec-dev libavformat-dev libjpeg-dev libswscale-dev libtiff5-dev

```
3. 安装一些可选的库

``` bash
# python3支持（首次安装了python的库，但make报错了，之后删了这两个库，若不使用python，建议不安装）
sudo apt install python3-dev python3-numpy
# streamer支持
sudo apt install libgstreamer-plugins-base1.0-dev libgstreamer1.0-dev
# 可选的依赖
sudo apt install libpng-dev libopenexr-dev libtiff-dev libwebp-dev

```

## 2. 下载OpenCV 4.5.0源文件

> 可以在官网下载相应版本的OpenCV，主要有Source和GitHub两种方式下载。

1. Source：https://opencv.org/releases/
2. GitHub下载

``` bash
# 安装4.5.0版本
wget -O opencv.zip https://github.com/opencv/opencv/archive/4.7.0.zip
# 安装最新版本
wget -O opencv.zip https://github.com/opencv/opencv/archive/master.zip
# 解压
unzip -d opencv opencv.zip
```

## 3.  Cmake配置和编译OpenCV

1. 进入到下载好的opencv目录中，新建并进入目录build
``` bash
cd opencv
mkdir build
cd build
```
2. make配置opencv
`cmake -D CMAKE_BUILD_TYPE=Release -D OPENCV_GENERATE_PKGCONFIG=YES ..`

> 说明：
-D OPENCV_GENERATE_PKGCONFIG=YES
OpenCV4以上默认不使用pkg-config，该编译选项开启生成opencv4.pc文件，支持pkg-config功能

3. 用make进行编译
`make -j8`

> 说明：
-j8中的8指同时使用8个进程，可以根据电脑的进程数调整此值

4. 用make进行安装

`sudo make install`

> 默认安装路径为：
``` bash
/usr/local/bin - executable files
/usr/local/lib - libraries (.so)
/usr/local/cmake/opencv4 - cmake package
/usr/local/include/opencv4 - headers
/usr/local/share/opencv4 - other files (e.g. trained cascades in XML format)
```

## 4.  环境配置
1.  配置pkg-config环境
>opencv4.pc文件的默认路径：/usr/local/lib/pkgconfig/opencv4.pc
若此目录下没有，可以使用以下命令搜索：
`sudo find / -iname opencv4.pc`

将路径加入到PKG_CONFIG_PATH（用vim打开）：
`sudo vim /etc/profile.d/pkgconfig.sh`

在文件后面加入下面一行：
`export PKG_CONFIG_PATH=/usr/local/lib/pkgconfig:$PKG_CONFIG_PATH`

保存并退出后激活：
vim保存退出的方式->输入:wq 然后回车

``` bash
# 激活
source /etc/profile
# 用以下命令验证是否成功：
pkg-config --libs opencv4
# ❯ pkg-config --libs opencv4  出现以下信息
#-L/usr/local/lib -lopencv_gapi -lopencv_highgui -lopencv_ml -lopencv_objdetect -lopencv_photo -lopencv_stitching -lopencv_video -lopencv_calib3d -lopencv_features2d -lopencv_dnn -lopencv_flann -lopencv_videoio -lopencv_imgcodecs -lopencv_imgproc -lopencv_core
```

2.  配置动态库环境
``` bash
# 打开文件（可能为空文件）：
sudo vim /etc/ld.so.conf.d/opencv4.conf
# 在该文件末尾加上OpenCV的lib路径，保存退出：
/usr/local/lib
#使配置的路径生效：
sudo ldconfig
```

## 5.  测试OpenCV
cd 到/opencv/samples/cpp/example_cmake目录下，依次执行以下命令：

``` bash
cmake .
make
./opencv_example
```

该测试需要电脑有摄像头，若启动摄像头看到了画面，说明安装成功；若未启动摄像头，但出现`Hello OpenCV`显示，也安装成功

## 6. 用Cmake构建C++项目调用OpenCV
下面简单构建一个显示图片的C++程序

1. 在桌面新建文件夹ImageShow

2. 进入该文件夹，打开终端，输入：
` vi main.cpp `

3. 打开main.cpp，输入如下代码：

``` cpp
#include <iostream>
#include <opencv2/core.hpp>
#include <opencv2/highgui.hpp>
using namespace cv;
using namespace std;
int main(int argc, char** argv )
{

    if ( argc != 2 )
    {
        cout<<"usage: DisplayImage.out <Image_Path>\n";
        return -1;
    }
    Mat image;
    image = imread( argv[1], 1 );
    if ( !image.data )
    {
        cout<<"No image data \n";
        return -1;
    }
    namedWindow("Display Image", WINDOW_AUTOSIZE );
    imshow("Display Image", image);
    waitKey(0);
    return 0;
}
```

4. 终端输入
`vi CMakeLists.txt`

5. 打开CMakeLists.txt，输入如下代码：

``` cmake
# cmake needs this line
cmake_minimum_required(VERSION 3.1)

# Define project name
project(ImageShow)

# Find OpenCV, you may need to set OpenCV_DIR variable
# to the absolute path to the directory containing OpenCVConfig.cmake file
# via the command line or GUI
find_package(OpenCV REQUIRED)

# Enable C++11
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED TRUE)

# Declare the executable target built from your sources
add_executable(ImageShow main.cpp)

# Link your application with OpenCV libraries
target_link_libraries(ImageShow PRIVATE ${OpenCV_LIBS})
```
6. 在该文件夹下加入一张名为flower.jpg的图片，用于测试

7. 在终端依次输入如下代码，构建并运行程序：

``` bash
cmake .
make
./ImageShow flower.jpg
```

8. 成功运行, 会显示该图片

## 7. 问题
1. make时的一些报错：
> C++这个fatal error的解决方式：扩大虚拟机内存
> 两个make的error：卸载python3-dev和python3-numpy

2. cmake重新编译的方法：
>删除build文件夹下的文件CMakeCache.txt，重新编译即可
`rm CMakeCache.txt`

3.  一些教程配置动态库环境改的是/etc/bash.bashrc
>参考链接：https://blog.csdn.net/smile_from_2015/article/details/80058351
该链接对这个问题有详细的解释

## 8. 参考文章
https://blog.csdn.net/smile_from_2015/article/details/80058351
https://blog.csdn.net/weixin_44554475/article/details/109767632
https://blog.csdn.net/weixin_43118645/article/details/113920231