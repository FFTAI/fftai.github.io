# Overview

The configuration of RoCS for simulation environment involves:

* [Setting Up RoCS Server](quick_start/setup_for_simulated_robot?id=setting-up-rocs-server)
* [Loading Webots Model](quick_start/setup_for_simulated_robot?id=loading-webots-model)
* [Controlling Robot Using Client SDK](quick_start/setup_for_simulated_robot?id=controlling-robot-using-client-sdk)

# Setting Up RoCS Server

## System Requirements

Before proceeding with the RoCS Server installation, ensure that your system meets the following requirements:

* A PC with a minimum dual-core CPU clock speed of 2 GHz and 2 GB of RAM.
* Operating system: Ubuntu Long Term Support (LTS) releases, including versions 22.04 and 20.04.
* An NVIDIA or AMD OpenGL-capable graphics adapter with a minimum version of 3.3 and at least 512 MB of RAM.

## Installing RoCS Server Dependencies and Binaries

Use either of the following commands in your terminal to install the server dependencies and RoCS Server binaries:

**Option 1:**

```shell
wget -qO- https://raw.githubusercontent.com/FFTAI/rocs_server/main/install.sh | bash
```

**Option 2:**

```shell
curl -o- https://raw.githubusercontent.com/FFTAI/rocs_server/main/install.sh | bash
```

---

## Verifying Installation

To confirm the successful installation of RoCS server packages, open a terminal and run the following command to check if RoCS-related packages are installed:

```shell
dpkg -l | grep rocs
```

Following output signifies a successful installation:

```shell
fftai@fftai-rocs-machine:~$ dpkg -l | grep rocs
ii  rocs-control   1.3   all     Provides support and functionality for control algorithms relevant to robotics
ii  rocs-lib          1.0   all     Installs the libraries required by RoCS
ii  rocs-svr         1.3   all     Provides export call services for robot algorithm programs
ii  rocs-webots  1.3   all     Provides a Webots simulation environment model
ii  rocs-wifi        1.0   all      Opens a hotspot for clients to connect to the same network segment as the robot
fftai@fftai-rocs-machine:~$

```

## Introduciton to Installed Server Packages

### rocs-control

`rocs-control` is the core component of the RoCS system, and we provide a binary file that operates within the '~/RoCS' directory of the embedded robot computer. If you need to fine-tune and customize configuration settings, which may include PID, mass, filtering, and other parameters of the robot, you can achieve this by manually editing the configuration file. This approach allows for precise control of the robot's behavior.

### rocs-lib

`rocs-libs` are the libraries that the RoCS system relies on. It provides essential features to:

* Conduct rigid body dynamics computations, facilitating precise modeling of the robot's physical movements.
* Tackle quadratic programming (QP) problems efficiently, enabling the robot's control system to address complex optimization tasks.
* Perform various linear algebra operations, serving as the mathematical foundation for critical robot functionalities.

### rocs-svr

The `rocs-svr` essentially serves as the bridge between the upper computer and the lower computer. It is automatially started as a service during booting. It handles commands originating from the upper computer, which can be a Control APP user interface or SDK control programs. Its primary function is to process these commands and transmit control instructions to the lower computer using underlying communication protocols. This intricate communication mechanism enables the achievement of precise control over the robot's movements.

### rocs-webots

`rocs-webots` is a simulation environment based on Webots, an open source robot simulation application from Cyberbotics. Prior to interacting directly with the robot, we strongly recommend that you gain familiarity with its operation and usage by first experiencing it within the Webots simulation environment. This simulation environment faithfully replicates the motion characteristics and structure of the robot, making it an essential preliminary step. This pacakge is installed only for the simulation environment.

### rocs-wifi

`rocs-wifi` is a crucial component in the RoCS system, responsible for managing and configuring the robot's Wi-Fi connection, including configuring and activating Wi-Fi functionalities. Through this component, it ensures a seamless connection to the Wi-Fi network where the robot is located. It is automatially started as a service during booting.

## Verifying Service Effectiveness

Following two services have been configured for automatic startup during the boot process. After the installation is finished, it's crucial to confirm that these services indeed start automatically as intended.

1. Verify the Status of `rocs-wifi` Service:

```shell
sudo systemctl status rocs-wifi.service
```

2. Verify the Status of `rocs-svr` Service:

```shell
sudo systemctl status rocs-svr.service
```

## Manual Service Control

In certain situations, you may need to manually start or stop RoCS services. Follow the instructions below to perform these actions:

* Manual start the `rocs-wifi` service:

```shell
sudo systemctl start rocs-wifi.service
```

* Manual start the `rocs-svr` service:

```shell
sudo systemctl start rocs_svr.service
```

* Manual stop `rocs-wifi` service:

```shell
sudo systemctl stop rocs-wifi.service
```

* Manual stop `rocs-svr` service:

```shell
sudo systemctl stop rocs-svr.service
```

## View Service Logs

To monitor the logs of RoCS services for troubleshooting or debugging purposes, follow these steps:

* Monitor the log of `rocs-svr`:

```shell
tail -f /var/log/syslog | grep rocs
```

* Monitor the log of `rocs-control`:

```shell
tail -f ~/RoCS/server.log
```

!> Userful Tip: Open a terminal and run the command `tail -f /var/log/syslog | grep rocs` to monitor the server log in real time. Keeping the terminal window always on top can provide a convenient way to stay updated.

# Loading Webots Model

1. Open a terminal and run the `webots` command to start Webots GUI interface.
2. Navigate to `File` -> `Open World`.
3. Select the world file located at `～/RoCS/webots/worlds/SonnyV4.wbt`.

!> If the model cannot be shown, attempt to restore the layout by navigating to Tools -> Restore Layout.


# Controlling Robot Using Client SDK

Use either [Python SDK](quick_start/setup_for_physical_robot?id=setting-up-python-client-sdk) or [JavaScript/TypeScript SDK](quick_start/setup_for_physical_robot?id=setting-up-javascripttypescript-client-sdk) to control the robot.
