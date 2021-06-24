# ROS_Cheatsheet

## Setup Ubuntu environment 
- Linux version: Ubuntu 18.04
- Update ubuntu:

        sudo apt update && sudo apt upgrade -y
- Check upgradable packages

        apt list --upgradable
- Update package information

        sudo apt-get update
- Upgrade packages on system and fix broken packages in the process

        sudo apt-get -f dist-upgrade
- Only fix broken packages

        sudo apt-get -f install
- To install a package from a directory
        
        sudo apt-get install [include here path to file]



- ROS distro: Ros Melodic  
- install catkin_tools
- Install Moveit (if not installed by default)
- Install Vscode
- Get Vscode extentions
  - Pylance 
  - ROS
  - git
  - gitgraph
  - 3D viewer
  - URDF
  - vscode-icons
  - Yaml

- Install pip:

        sudo apt install python-pip
- Install numpy: 

        pip install numpy
- Install PyBullet
- Install PyTorch

# Useful ROS commnads

        catkin init # after creating a workspace
        catkin build

# Networking:

- Get your machine IP address, open a new terminal and        type
        
        hostname -I