# RoCS Server Introduction

The `rocs_server` covers the entire communication process and capabilities related to robot control. To simplify the installation and utilization, we offer five .deb packages specifically designed for the Ubuntu AMD64 operating system. These packages expedite the installation of the RoCS Server, streamlining your experience with robot control.

## rocs-lib

`rocs-libs` are the libraries that the RoCS system relies on. It provides essential features to:

* Conduct rigid body dynamics computations, facilitating precise modeling of the robot's physical movements.
* Tackle quadratic programming (QP) problems efficiently, enabling the robot's control system to address complex optimization tasks.
* Perform various linear algebra operations, serving as the mathematical foundation for critical robot functionalities.

## rocs-svr

The `rocs-svr` essentially serves as the bridge between the upper computer and the lower computer. It handles commands originating from the upper computer, which can be a Control APP user interface or SDK control programs. Its primary function is to process these commands and transmit control instructions to the lower computer using underlying communication protocols. This intricate communication mechanism enables the achievement of precise control over the robot's movements.

## rocs-wifi

`rocs-wifi` is a crucial component in the RoCS system, responsible for managing and configuring the robot's Wi-Fi connection, including configuring and activating Wi-Fi functionalities. Through this component, it ensures a seamless connection to the Wi-Fi network where the robot is located.

## rocs-webots

`rocs-webots` is a simulation environment based on Webots, an open source robot simulation application from Cyberbotics. Prior to interacting directly with the robot, we strongly recommend that you gain familiarity with its operation and usage by first experiencing it within the Webots simulation environment. This simulation environment faithfully replicates the motion characteristics and structure of the robot, making it an essential preliminary step.

## rocs-control

`rocs-control` is the core component of the RoCS system, and we provide a binary file that operates within the '~/RoCS' directory of the embedded robot computer. If you need to fine-tune and customize configuration settings, which may include PID, mass, filtering, and other parameters of the robot, you can achieve this by manually editing the configuration file. This approach allows for precise control of the robot's behavior.
