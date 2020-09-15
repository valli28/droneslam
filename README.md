# droneslam
Fred's and Valli's past-time coding excercises


# Setup instructions
Original guide at https://dev.px4.io/v1.9.0/en/simulation/ros_interface.html
The guide fails to mention that you have to (of course) download PX4's flightstack and build it,
but we will cover it here :)

If you don't have the "future" module for Python, install it with
>pip3 install --user future


You also might have to install ROSdep for Python apparently...
> sudo apt install python-rosdep2
And I had to perform this also, so you might as well do it as well:
> sudo apt-get install python-rosdep python-rosinstall-generator python-vcstool python-rosinstall build-essential


Download the installation script for ROS-Gazebo-PX4-mavros at: 
>https://raw.githubusercontent.com/PX4/Devguide/v1.9.0/build_scripts/ubuntu_sim_ros_melodic.sh

and run the script with
>source ubuntu_sim_ros_melodic.sh

If your build fails at some point or the PX4 flight stack doesn't install by itself, then try to cd into catkin_ws/src and do:
>git clone https://github.com/PX4/Firmware.git

Also remember to clean your build (if it fails) with:
>catkin clean

That script should take a while and install everything necessary to run everything related to this repository except the python packages in requirements.txt

Note:
ROS Melodic is installed with Gazebo9 by default.
Your catkin (ROS build system) workspace is created at ~/catkin_ws/.

Now to the PX4 build instructions. It's easiest to just have the Firmware folder inside your repos
but the "correct" way to do it is to "link" it as a sub-repository in Git, but I've had problems with that in the past.
So you'll have to clone this repos, and inside it we will install have the Firmware folder. The Git doesn't know anything about the Firmware folder and it's ignored in .gitignore.


# PX4 stuff
Even though some of the shit above fails, most of the things that are necessary are installed such as ROS and Gazebo are fine. Mavros and Mavlink might be another story... let's see.

First clone PX4's firmware and then do all this:
>git clone https://github.com/PX4/Firmware.git
>cd <Firmware_clone>
>DONT_RUN=1 make px4_sitl_default gazebo
>source ~/catkin_ws/devel/setup.bash    # (optional)
>source Tools/setup_gazebo.bash $(pwd) $(pwd)/build/px4_sitl_default
>export ROS_PACKAGE_PATH=$ROS_PACKAGE_PATH:$(pwd)
>export ROS_PACKAGE_PATH=$ROS_PACKAGE_PATH:$(pwd)/Tools/sitl_gazebo
>roslaunch px4 posix_sitl.launch

If the above steps fail... then I don't know what went wrong for you.

Now ROS is running at the same time as Gazebo and PX4. Let's see if we can do some magic to our workspace. 
This link explains roughly how to implement an "offboard" node that we can use to control our drone. 
https://darienmt.com/autonomous-flight/2018/11/25/px4-sitl-ros-example.html
and the first important things here are: 
>sudo apt-get install ros-melodic-mavros-msgs
>sudo apt-get install ros-melodic-mavros ros-melodic-mavros-extras

Now let's make the package. While in the "root" folder of our workspace, make a src folder
>mkdir src
>cd src
Create a catkin package with the following messages
>catkin_create_pkg offb std_msgs roscpp geometry_msgs mavros_msgs

