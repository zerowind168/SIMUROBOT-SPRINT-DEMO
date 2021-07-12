操作系统：Ubuntu18.04<br>
ROS版本：Melodic<br>

## 1. ROS的安装:<br>
可以访问 http://wiki.ros.org/kinetic/Installation/Ubuntu 链接来找到如何下载Melodic版本的ROS<br>
下面是部分教程<br>

1. 配置 sources.list
    ```
    sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
    ```
2. 设置 keys
    ```
    sudo apt-key adv --keyserver 'hkp://keyserver.ubuntu.com:80' --recv-key C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654
    ```
3. 安装ROS
    ```
    sudo apt-get update
    sudo apt-get install ros-melodic-desktop-full
    ```
4. rosdep的初始化
    ```
    sudo rosdep init
    rosdep update
    ```
5. bash环境的配置
    ```
    echo "source /opt/ros/melodic/setup.bash" >> ~/.bashrc
    source ~/.bashrc
    ```

## 2. V-rep

### 2.1 下载 V-rep
V-rep的官方地址如下<br>
https://www.coppeliarobotics.com/

### 2.2 解压文件

### 2.3 尝试运行V-rep
```
cd ${VREP_ROOT}
sh vrep.sh
```

## 3. SIMUROSOT-SPRINT
### 3.1 下载本工程
#### 3.1.1 创建一个ROS的工作空间
```
cd ~
mkdir -p vrep_ws/src
cd vrep_ws
catkin_make
```
#### 3.1.2 把文件移动到工作空间
```
cd ${proj_root}
mv ./* ~/vrep_ws/src
cd ~/vrep_ws
catkin_make
```
#### 3.1.3 更改bash配置
```
nano ~/.bashrc
```
把下面的代码加到最后一行
```
source ~/vrep_ws/devel/setup.bash
```

### 3.2 项目的运行

#### 3.2.1 单主机运行
共需要四个终端

终端一：
```
roscore
```

终端二：
```
sh ${vrep_bin}/vrep.sh
```

V-rep运行成功后，依次点击File -> Open scene 然后选择bioloid_vrep/scenes里面的ttt文件

点击绿色三角形来运行场景。

终端三：
运行bioloid_vrep模块
```
rosrun bioloid_vrep communication
```
如果屏幕打印了"connect successful"，则操作成功

终端四：
运行bioloid_gp_master模块
```
rosrun bioloid_gp_master movement.py
```
Try to enter numbers like 1 and 2 to observe the reaction in the platform.

## 后续工作
给定的demo足够简单，初学者可以简单地上手。
bioloid_gp_master/src/movement.py里面描述了机器人是如何被驱动的。
