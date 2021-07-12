
### [Click here to Chinese Version](./README-CN.md)

OS: ubuntu 18.04<br>
ROS: Melodic<br>

## 1. Install the ROS:<br>
You can go to:  http://wiki.ros.org/kinetic/Installation/Ubuntu
for how to download the ROS Kinetic version.<br>
Here we copy some of the proceed below:<br>

1. Setup your sources.list

    ```
    sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
    ```
2. Setup your keys
    ```
    sudo apt-key adv --keyserver 'hkp://keyserver.ubuntu.com:80' --recv-key C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654
    ```
3. Installation
    ```
    sudo apt-get update
    sudo apt-get install ros-melodic-desktop-full
    ```
4. Initialize rosdep
    ```
    sudo rosdep init
    rosdep update
    ```
5. Environment setup
    ```
    echo "source /opt/ros/melodic/setup.bash" >> ~/.bashrc
    source ~/.bashrc
    ```

## 2. V-rep

### 2.1 Download V-rep
You can download V-rep from the link below<br>
https://www.coppeliarobotics.com/

### 2.2 Unzip the file

### 2.3 Try to run V-rep
```
cd ${VREP_ROOT}
sh vrep.sh
```

## 3. SIMUROSOT-SPRINT
### 3.1 Download this project
#### 3.1.1 Create a workspace for the project
```
cd ~
mkdir -p vrep_ws/src
cd vrep_ws
catkin_make
```
#### 3.1.2 Move files to it
```
cd ${proj_root}
mv ./* ~/vrep_ws/src
cd ~/vrep_ws
catkin_make
```
#### 3.1.3 Change the .bashrc
```
nano ~/.bashrc
```
Add the following code to the end of the file.
```
source ~/vrep_ws/devel/setup.bash
```

### 3.2 Run the program

#### 3.2.1 Run both the server and the client on one machine

Terminal 1:
```
roscore
```
Terminal 2:
```
sh ${vrep_bin}/vrep.sh
```

After the v-rep is running, select File -> Open scene and select  ttt file of bioloid_vrep/scenes in the project.

Click the green triangle in V-rep to run the scene.

Terminal 3:<br>
run the bioloid_vrep module
```
rosrun bioloid_vrep comunication
```
if "connect successful" is printed on the screen, the operation is successful.

Terminal 4:<br>
run the bioloid_gp_master module
```
rosrun bioloid_gp_master movement.py
```
Try to enter numbers like 1 and 2 to observe the reaction in the platform.
## More to do
The given demo is really simple for beginners to start up. You can check bioloid_gp_master/src/movement.py to see how the robot is driven.

current missing functions:
1. Publish image message through ROS node
2. Client synchronization server emulation time
3. Launch the project on different machines.