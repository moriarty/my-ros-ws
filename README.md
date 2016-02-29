# my-ros-ws
Just a repository to share and sync .rosinstall files across devices

    git clone https://github.com/moriarty/my-ros-ws ~/my-ros-ws

to create a catkin workspace in ~/indigo:

    mkdir -p ~/indigo
    cd ~/indigo
    source /opt/ros/indigo/setup.bash
    wstool init src ~/my-ros-ws/cob3-1-pc1.rosinstall
    wstool update

