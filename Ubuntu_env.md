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

- Install pip:

        sudo apt install python-pip
- Install numpy: 

        pip install numpy
- Install PyBullet
- Install PyTorch

        pip3 install torchvision


# Networking:

# setup VPN in ubuntu - AMRC
https://www.sheffield.ac.uk/it-services/vpn/linux

- Get your machine IP address, open a new terminal and type
        
        hostname -I


# Remote PC file access with SSHFS

1. First create a directory in the local PC (e.g.) (if done - no need to do it again)
                
        mkdir remote_agv

2. Next do the mounting on local pc like: sshfs remote_pc_user_name@remote_pc_IP:/home /home/ukaea/remote_agv. (e.g. use this one)

        sshfs nvidia@192.168.5.160:/home /home/ukaea/remote_agv

3. if mountpoint is not empty use:

        sshfs -o nonempty nvidia@192.168.5.160:/home /home/ukaea/remote_agv

4. Then enter remote PC password (e.g.):

        nvidia
        ukaea2021

5. To desmount before disconecting the remote machine
        
        sudo umount -l /home/ukaea/remote_agv

6. To kill sshf

        killall sshfs


# Share internet between local and a remote PC with SSH

- cd to share_net location (fisrt make sure to have the "share_net" file)

        sudo ./share_net enp1s0 wlx1cbfce3a256c
        sudo ./share_net to_XXXXX from_XXXXX
        ssh nvidia@192.168.5.160 
        ping www.google.com

## Explanation
1. Download the script called: "share_net"  
- the content of the script is:

        #!/bin/bash
        TO=$1
        SOURCE=$2

        echo 1 >  /proc/sys/net/ipv4/ip_forward
        iptables -A FORWARD -i $TO -o $SOURCE -j ACCEPT
        iptables -A FORWARD -i $SOURCE -o $TO -m state --state ESTABLISHED,RELATED  -j ACCEPT
        iptables -t nat -A POSTROUTING -o $SOURCE -j MASQUERADE

2. make the share_net script file executable if it isn't already:

        sudo chmod +x share_net

3. The script has two arguments: The network interface that has internet access and the interface that you need to share internet with. 
  - In your case, it sounds like this is wlan0 and eth0 respectively. Use ifconfig to confirm. 
  - You only need to execute the script once per boot on you Ubuntu machine: sudo ./share_net wlan0 eth0
4. Now ssh into the jetson and assign the gateway address as your Ubuntu PC's ethernet interface address  

        ssh nvidia@192.168.5.160 
        
        sudo vim /etc/network/interfaces

5. You should see an entry for the Jetson's eth0 interface. Define a gateway in this entry:     

        auto eth0
        iface eth0 inet static
        address 192.168.5.160
        netmask 255.255.255.0
        gateway 192.168.5.XXX

6. Replace XXX with the last byte of the ethernet IP address on your Ubuntu PC.
7. Save and exit that file then power cycle the robot. Once the robot boots back up. Remote into the Jetson and try to ping www.google.com.


# other

Sudo gedit /etc/hosts # something ??????