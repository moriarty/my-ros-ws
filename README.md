# my-ros-ws
Just a repository to share and sync .rosinstall files across devices

    git clone https://github.com/moriarty/my-ros-ws ~/my-ros-ws

## Care-O-Bot 3-1 instructions

To save combile time on the Care-O-Bot, I've taken advantage of catkin workspace overlays.

### Structure and Usage

Let's assume it's been set up, and you're just a normal account user. A beginner ROS user, likely you're familiar with having two ros workspaces. The core packages you likely installed with your package manager are in ```/opt/ros/indigo``` and the catkin workspace you work in ```~/catkin_ws/src``` or ```~/indigo/src```.

We will add a new workspace into the mix. One where we require changes not yet available in the package manager, but stable enough that we don't need to ```catkin build``` them all the time. This will be located at ```/opt/ros/indigo-cob3-1-stable```.

As a user- you only need to worry about the new workspace once. After steup you can forget about the sourcing ```/opt/ros/indigo/setup.bash``` and ```/opt/ros/indigo-cob3-1-stable/setup.bash```

### Initial Setup

Assuming Clean ROS environment, ```env | grep -i ros``` should print nothing. If not use ```unset``` or edit your .bashrc and open a new session.

#### Demo User must first:

1. Install repositories.debs
2. Source /opt/ros/indigo/setup.bash
3. Initialize stable workspace using ```wstool```
4. Configure workspace install-space and install option
5. Build workspace: this will install to /opt/ros/indigo-cob3-1-stable
6. Unset ROS variables (or logout and don't source any setup.bash)

#### All Users must:


1. Source the new /opt/ros/indigo-cob3-1-stable.
2. Initialize your catkin workspace with ```wstool```
3. Build the workspace. You can check the configuration first with ```catkin config```
4. Add the new devel/setup.bash to your login scripts and log & log back in.

### Update

#### All Users

1. Use ```catkin build``` on your ```~/indigo``` workspace as normal.

#### As Demo

1. The catkin config is saved in each workspace, if you change something in the ```~/indigo-cob3-1-stable``` running ```catkin build``` will use the previously set ```Install Packages: True``` and ```Install Space:``` options.
2. If you're building in the ```~/indigo``` workspace, nothing changes.
3. There is no need to source different ```setup.bash``` files


## OLD INSTRUCTIONS 

TODO: I've restructured, these can't be copied and pasted any more, need to update.

to create a catkin workspace in ~/indigo:

    mkdir -p ~/indigo
    cd ~/indigo
    source /opt/ros/indigo/setup.bash
    wstool init src ~/my-ros-ws/cob3-1-pc1.rosinstall
    wstool update

