# droneslam
Fred's and Valli's past-time coding excercises


# Setup instructions
Original guide at https://dev.px4.io/v1.9.0/en/simulation/ros_interface.html
The guide fails to mention that you have to (of course) download PX4's flightstack and build it,
but we will cover it here :)

If you don't have the "future" module for Python, install it with
>pip3 install --user future


You also might have to install ROSdep for Python apparently...
> sudo apt install python3-rosdep2

Download the installation script for ROS-Gazebo-PX4-mavros at: 
>https://raw.githubusercontent.com/PX4/Devguide/v1.9.0/build_scripts/ubuntu_sim_ros_melodic.sh

and run the script with
> source ubuntu_sim_ros_melodic.sh

That script should take a while and install everything necessary to run everything related to this repository except the python packages in requirements.txt

Note:
ROS Melodic is installed with Gazebo9 by default.
Your catkin (ROS build system) workspace is created at ~/catkin_ws/.

Now to the PX4 build instructions. It's easiest to just have the Firmware folder inside your repos
but the "correct" way to do it is to "link" it as a sub-repository in Git, but I've had problems with that in the past.
So you'll have to clone this repos, and inside it we will install have the Firmware folder. The Git doesn't know anything about the Firmware folder and it's ignored in .gitignore.


