# Overview

The SDK library serves as a crucial component for applications aiming to exercise command over the GR-1, retrieve sensor data, and set up payload services. This quickstart guide offers a step-by-step walkthrough to assist you in installing the necessary SDK libraries (both in Python and JavaScript/TypeScript) and running basic programs for GR-1 control.

The SDK can be executed in either a virtual environment or on a physical robot:

# Extended Development Through Virtual Environment Webots

 To set up a virtual development environment, you need to:

- Install the RoCS server dependencies and server binaries.
- Install the webots software.
- Start RoCS server service.
- Lauch the webots and load GR-1 model file.
- Lauch the client SDK to control the GR-1.

### Installing Server Environment Dependencies and RoCS Server Binary

Use either of the following commands in your terminal to install the server dependencies and RoCS Server binaries:

**Option 1: Using curl:**

```
curl -o- https://raw.githubusercontent.com/FFTAI/rocs_server/v1.3.0/install.sh | bash

```

**Option 2: Using weget:**

```
wget -qO- <https://raw.githubusercontent.com/FFTAI/rocs_server/v1.3.0/install.sh> | bash
```

### Installing Webots

Follow these steps to set up the virtual robot environment using Webots:

1. Open a terminal and run the following command to download the webots installation package:

```
wget https://github.com/cyberbotics/webots/releases/download/R2023b/webots_2023b_amd64.deb
```

2. Run command ``sudo dpkg -i webots_2023b_amd64.deb`` to install the package.

### Starting the RoCS Server

Open a terminal, run the following command:

```
cd ~/.rocs_server1.3.0/sbin
bash start_up_rocs_svr.sh
```

After running these commands, the server service will be active, allowing the client SDK to send control commands to the virtual robot.

!> Ensure that the server is successfully started before attempting to interact with the virtual robot using the client SDK.

### Loading Webots Model

1. Open a terminal and run the `webots`command to start Webots.
2. Navigate to `File` -> `Open World`.
3. Select the world file located at `.rocs_server/bin/webots/webotsim/worlds/SonnyV4.wbt`.

# Extended Development Through Physical GR-1 Robot

To develop with a physical robot, you need to:

1. Get familiar with the robot operation, see [Operation Instruction](operationinstruction.md) part for details.
2. Modify configuration information.

```
sbin/
├── config/
├──── control_svr.conf        ***** Configuration for algorithm control program (path to the binary executable in bin/real). Modify accordingly if your file differs.
├──── password.conf           ***** Host password! Script requires sudo privileges, and the password is configured here.
├──── wifi.conf               ***** Wifi information (sets up the host as an access point with a wifi network for control. Note that this is optional; if you have another method for communication within the same network, you can ignore this setting).
```

!> We recommend carefully reading the README file in the sbin directory and then modifying the corresponding configuration information (modify according to your actual situation).

3.Compile and install the Runtime Environment for real machine.

```
cd sbin
bash install.sh
```

4. Power on GR-1 and explore.

   Congratulations on completing the installation with the above steps! You are now ready to initiate your robot experience using our SDK or the Android APK to control Fourier GR1.
