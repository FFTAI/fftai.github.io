# About RoCS Server Introduction

The rocs_server covers the entire communication process and capabilities of robot control. For ease of use and installation, we provide 5 .deb packages based on the Ubuntu AMD64 operating system, which will allow you to quickly and efficiently complete the installation and use of the rocs_server, so that you can focus more on manipulating the robot.

## rocs-lib

`rocs-libs` are the library files that our entire robot operating system relies on. We have packaged them to avoid the tedious process of you needing to download, decompress, and compile them.

## rocs-svr

The `rocs-svr` essentially serves as the bridge between the upper computer and the lower computer. It handles commands originating from the upper computer, which can be a Control APP user interface or SDK control programs. Its primary function is to process these commands and transmit control instructions to the lower computer using underlying communication protocols. This intricate communication mechanism enables the achievement of precise control over the robot's movements.

## rocs-wifi

`rocs-wifi` is a crucial component in the RoCS system, responsible for managing and configuring the robot's Wi-Fi connection, including configuring and activating Wi-Fi functions. Through this component, it ensures that you can seamlessly connect to the Wi-Fi network where the robot is located.

## rocs-webots

`rocs-webots` is a simulation environment provided by us based on Webots! Perhaps before you access the robot, in order to better familiarize yourself with the operation and use of the robot, we strongly recommend that you first experience it in the Webots simulation environment. The simulation environment accurately reproduces the motion characteristics and structure of the robot, which will be a very important step.

## rocs-control

`rocs-control` is the core part of our robot control program, and we provide a binary file that runs in the '～/RoCS' directory of the robot host. If you need to adjust and modify configuration items, including but not limited to the PID, mass, filtering and other parameters of the robot, you can achieve this by manually modifying the configuration file. This can help you control the robot more accurately.

