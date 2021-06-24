# ROS environment

- Install ROS distro: Ros Melodic  
- install catkin_tools
- Install Moveit (if not installed by default)


# Useful ROS commnads

 - After creating a workspace
    
        catkin init
    You should init a workspace (catkin init), or ensure that you are in the folder that you original created.
- sdsds

        rosdep install -y --from-paths . --ignore-src --rosdistro melodic

- Install dependency of all packages in the workspace

        rosdep install --from-paths src --ignore-src -r -y 

- Different option

        rosdep install --from-paths src --ignore-src -y 

- build ROS pckages
    
        catkin build
    or

        catkin_make 

- Source the workspace paths. (After catkin build!!!!!!!!!!!!!!!)   
        
        source devel/setup.bash  

    Source the workspace paths

        source ./devel/setup.bash 
 
- To add directly a workspace to the bashrc from the command line
    
        echo 'source ~/ws_moveit/devel/setup.bash' >> ~/.bashrc  

- To code the bashrc file in vscode

        code ~/.bashrc

- To check the toolset that is currently in use. 
  
        catkin config

- To switch to catkin build, run first

        catkin clean -bdy

- To kill ROS

        killall -9 roscore # kill ros
        killall -9 rosmaster # kill ros
        rosnode kill -a

# Messages and topics

- To get info from a topic so sensor_msgs.msg import JointState can be use
        
        rostopic info /joint_states 
- To get structure of the topic message

        rosmsg show sensor_msgs/JointState 


## define a namespace in the command line but best to do with a lauch file:
export ROS_NAMESPACE=/iiwa

# Moveit

- To launch moveit assistance

        roslaunch moveit_setup_assistant setup_assistant.launch

# Usefull commandas to update and upgrade ROS packages if something doesn't work

    sudo apt-get update 
    sudo apt-get upgrade 

# Install joint_state_publisher_GUI in melodic

    sudo apt update

Install the package

    sudo apt install ros-melodic-joint-state-publisher-gui

# Convert xacro to urdf

    rosrun xacro xacro --inorder model.urdf.xacro > model.urdf # convert xacro to urdf ROS kinetic OK
    rosrun xacro xacro irb120_3_58.xacro > abb_irb120.urdf # ROS Melodic OK
    rosrun xacro xacro --inorder -o abb_irb120.urdf irb120_3_58_macro.xacro # Kinetic ok