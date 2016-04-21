# my-ros-ws
Just a repository to share and sync .rosinstall files across devices

    git clone https://github.com/moriarty/my-ros-ws ~/ros-ws-setup

If you put this repository in ~/ros-ws-setup you can copy and paste the other instructions

## Care-O-Bot 3-1 instructions

To save combile time on the Care-O-Bot, I've taken advantage of catkin workspace overlays.

### Structure and Usage

Let's assume it's been set up, and you're just a normal account user. A beginner ROS user, likely you're familiar with having two ros workspaces. The core packages you likely installed with your package manager are in ```/opt/ros/indigo``` and the catkin workspace you work in ```~/catkin_ws/src``` or ```~/indigo/src```.

We will add a new workspace into the mix. One where we require changes not yet available in the package manager, but stable enough that we don't need to ```catkin build``` them all the time. This will be located at ```/opt/ros/indigo-cob3-1-stable```.

As a user- you only need to worry about the new workspace once. After steup you can forget about the sourcing ```/opt/ros/indigo/setup.bash``` and ```/opt/ros/indigo-cob3-1-stable/setup.bash```

### Initial Setup

Assuming Clean ROS environment, ```env | grep -i ros``` should print nothing. If not use ```unset``` or edit your .bashrc and open a new session.

#### Demo User must first:

0. Start without having sourced any ROS setup files
1. Install repositories.debs
2. Source /opt/ros/indigo/setup.bash
3. Initialize stable workspace using ```wstool```
4. Configure workspace install-space and install option
5. Build workspace: this will install to /opt/ros/indigo-cob3-1-stable
6. Unset ROS variables (or logout and don't source any setup.bash)

        mkdir -p ~/indigo-cob3-1-stable
        cd ~/indigo-cob3-1-stable

    note: use the correct setup file, pc1 includes the repositories for hardware like the arm. Everyone else only needs pc2.

        wstool init src ~/ros-ws-setup/cob-stable/indigo-cob3-1-stable-pc2.rosinstall
        catkin config --init
        catkin config --install --install-space /opt/ros/indigo-cob3-1-stable
        catkin build
        logout

#### All Users must:

0. Start without having sourced any ROS setup files
1. Source the new /opt/ros/indigo-cob3-1-stable.
2. Initialize your catkin workspace with ```wstool```
3. Build the workspace. You can check the configuration first with ```catkin config```
4. Add the new devel/setup.bash to your login scripts and log & log back in.

        source /opt/ros/indigo-cob3-1-stable/setup.bash
        mkdir -p ~/indigo
        cd ~/indigo
        wstool init src ~/ros-ws-setup/cob-user/mas-domestic-robotics.rosinstall
        catkin config --init
        catkin build

    On the Care-O-Bot we're putting all of our ROS stuff into ```~/env.sh``` and sourcing that at the end of the ```.bashrc```

        vim ~/env.sh

    It should look something like this

        #!/bin/bash
        # Common Stuff
        source /etc/care-o-bot/common.bashrc
        # ROS WORKSPACE
        source $HOME/indigo/devel/setup.bash
        # ROBOT Environment (map)
        export ROBOT_ENV=brsu-c069


### Update

#### All Users

1. Use ```catkin build``` on your ```~/indigo``` workspace as normal.

#### As Demo

1. The catkin config is saved in each workspace. 
2. If you're building in the ```~/indigo``` workspace, nothing changes.
3. If you need to update something in the stable workspace:

        ~/indigo-cob3-1-stable/src

    running ```catkin build``` will use the previously set 
    ```Install Packages: True``` and ```Install Space:``` options for that workspace.

4. There is no need to source different ```setup.bash``` files


## OLD INSTRUCTIONS 

TODO: I've restructured, these can't be copied and pasted any more, need to update.

to create a catkin workspace in ~/indigo:

    mkdir -p ~/indigo
    cd ~/indigo
    source /opt/ros/indigo/setup.bash
    wstool init src ~/my-ros-ws/cob3-1-pc1.rosinstall
    wstool update

