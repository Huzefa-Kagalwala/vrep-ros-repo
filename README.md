# VREP-ROS-Scenes
## Connecting V-REP and ROS

### STEP 1: Getting the repository running:
- The V-REP ROS bridge used here has been developed by the Inria Lagadic team. You can go to the following link to access the repository for this plugin [V-Rep ROS Bridge](https://github.com/lagadic/vrep_ros_bridge), if you want to take a look for yourself.
- First you will need to install ROS on your system. You can install ROS Kinetic [here](http://wiki.ros.org/kinetic/Installation/Ubuntu)
- This plugin supports only prior versions of CoppeliaSim (i.e. V-REP versions 3.6.2 and earlier). So, you must use the V-REP version provided here, as there some changes made to the install files also to make it run with the bridge.
- Clone this repository into the `/src` folder of your catkin_ws and delete the `build` and `devel` folders of your catkin workspace. Move the V-REP folder to your `home` folder in your system. Change the name of the `vrep_ros` folder to `vrep_ros_bridge`
- Now run `catkin_make`. After this, build the packagae again using the following command:
`catkin_make --pkg vrep_ros_bridge --cmake-args -DCMAKE_BUILD_TYPE=RelWithDebInfo`
- Open the file bashrc: `gedit ~/.bashrc` in the end of the file add:

`export VREP_ROOT_DIR=/ChangeWithyourPathToVrep/
export ROS_PACKAGE_PATH=${ROS_PACKAGE_PATH}:/path_to_catkin_ws/catkin_ws/src
source /opt/ros/kinetic/setup.bash
source /path_to_catkin_ws/catkin_ws/devel/setup.bash`

and then source this .bashrc file.
- The file libv_repExtRosBridge.so has to be in the V-Rep installation folder in order to be loaded. What we will do is to create a symbolic link to it. Go via terminal to the installation folder of V-Rep and type: `ln -s /YOUR_CATKIN_WS_PATH/devel/lib/libv_repExtRosBridge.so`, where `YOUR_CATKIN_WS_PATH/` is the path to reach your catkin_ws.
- We need to create a link pointing to the file compiledRosPlugins/libv_repExtRos.so in the V-REP root folder. Go via terminal to the installation folder of V-Rep and type: `ln -s compiledRosPlugins/libv_repExtRos.so`

### STEP 2: Running some scene in V-REP
- Download this [scene](https://github.com/jokla/vrep_car_simulation)
- Install `jstest-gtk` to test your joystick using `$ sudo apt-get install jstest-gtk`
- Follow [this](http://wiki.ros.org/joy/Tutorials/ConfiguringALinuxJoystick) tutorial to configure your joystick. (Just change the ROS package name to kinetic in this tutorial, it will run fine).
- Run `roscore` in the terminal. Start V-REP from another terminal and open the scene provided. In another terminal run the joystick node using `roslaunch teleop_twist_joy teleop-ps4.launch`.
- You can move the red car by keeping L1 pressed and after that use the two thumbsticks to apply a linear velocity (right thumbstick - up and down) and angular velocity (right thumbstick - left and right).
- The video of the scene working using a joystick has been provided [here](https://clemson.sharepoint.com/teams/ARMLab/Shared%20Documents/Forms/AllItems.aspx)
