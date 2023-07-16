# Fast-Drone-250 on Arm
## OpenCV报错
+ 报错信息：Project 'cv_bridge' specifies 'usr/include/opencv' as an include dir, which is not found
+ 报错原因：由于Nvidia jetpack将OpenCV文件夹命名为OpenCV4，导致编译的时候找不到
+ 找到报错文件，即cv_bridgeconfig.cmake，搜索"/usr/include/opencv"，并改为"/usr/include/opencv4"
## realsense报错
+ 报错原因：realsense在x86平台和在arm平台上安装方法不一致，arm平台的安装方式如下：

1.编译安装realsense
```
#编译realsense
sudo apt install -y cmake git 
sudo apt-get install -y libusb-1.0-0-dev pkg-config
sudo apt-get install -y libglfw3-dev libgl1-mesa-dev libglu1-mesa-dev
sudo apt-get install openssl libssl-dev

cd ~/librealsense
mkdir build
cd build
rm -rf *
cmake ../ -DFORCE_RSUSB_BACKEND=ON -DBUILD_PYTHON_BINDINGS:bool=true -DPYTHON_EXECUTABLE=/usr/bin/python3
make -j6
sudo make install
```

+ 加入环境变量

`export PYTHONPATH=$PYTHONPATH:/usr/local/lib:/usr/local/lib/python3.6/pyrealsense2
`

2.安装ROS+realsense环境
```
sudo apt-get install ros-melodic-realsense2-camera
sudo apt-get install ros-melodic-realsense2-description

```
