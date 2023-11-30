# Overview

This section guides you through utilizing the client SDK for GR-1 robot development.

The SDK is versatile, supporting execution in both virtual environments and on physical robots:

# Extended Development Through Virtual Environment Webots

To establish a virtual development environment, follow these steps:

## Initial Setup (First-time Users)

If this is your first time running the development environment, complete the following steps before proceeding with the setup:

* [Installing Server Environment Dependencies and RoCS Server Binary](https://fftai.github.io/#/quickstart?id=installing-server-environment-dependencies-and-rocs-server-binary)
* [Installing Webots](https://fftai.github.io/#/quickstart?id=installing-webots)

## Setting Up the Virtual Environment

Once the initial setup is complete, proceed with the following steps:

* [Starting the RoCS Server](https://fftai.github.io/#/quickstart?id=starting-the-rocs-server)
* [Loading Webots Model](https://fftai.github.io/#/quickstart?id=loading-webots-model)
* [Lauching Client SDK](https://fftai.github.io/#/quickstart?id=lauching-client-sdk)

### Installing Server Environment Dependencies and RoCS Server Binary

Use either of the following commands in your terminal to install the server dependencies and RoCS Server binaries:

**Option 1: Using curl:**

```shell
curl -o- https://raw.githubusercontent.com/FFTAI/rocs_server/v1.3.0/install.sh | bash

```

**Option 2: Using weget:**

```shell
wget -qO- <https://raw.githubusercontent.com/FFTAI/rocs_server/v1.3.0/install.sh> | bash
```

### Installing Webots

Follow these steps to set up the virtual robot environment using Webots:

1. Open a terminal and run the following command to download the webots installation package:

```shell
wget https://github.com/cyberbotics/webots/releases/download/R2023b/webots_2023b_amd64.deb
```

2. Run command ``sudo dpkg -i webots_2023b_amd64.deb`` to install the package.

!> Webots is a robot simulation software developed by Cyberbotics，which is used for simulating and testing the behavior of robots in a virtual environment before deploying them in the physical world. Webots provides a library of pre-built robot models representing a wide variety of robots. It incorporates a powerful physics engine that simulates realistic interactions between robots and their environments. It supports programming interfaces in several languages (C, C++, Python, Java) for developing and controlling robot behaviors. For more information on Webots, you can refer to its official documentation: [Webots +User Guide](https://www.cyberbotics.com/doc/guide/index).

### Starting the RoCS Server

Open a terminal, run the following command:

```shell
cd ~/.rocs_server1.3.0/sbin
bash start_up_rocs_svr.sh
```

After running these commands, the server service will be active, allowing the client SDK to send control commands to the virtual robot.

!> Ensure that the server is successfully started before attempting to interact with the virtual robot using the client SDK.

### Loading Webots Model

1. Open a terminal and run the `webots`command to start Webots GUI interface.
2. Navigate to `File` -> `Open World`.
3. Select the world file located at `.rocs_server/bin/webots/webotsim/worlds/SonnyV4.wbt`.

!> If the model cannot be shown, attempt to restore the layout by navigating to Tools -> Restore Layout.

### Lauching Client SDK

You can choose either Python Client SDK or JavaScript/TypeScript Client SDK to control the robot.

#### Using Python Client SDK

1. Install the Python Client SDK package:

```shell
pip install rocs_client

```

!> If you're experiencing network delays, you have the option to install from the Tsinghua source. Just use the following command: `pip install -i https://pypi.tuna.tsinghua.edu.cn/simple rocs_client`

2. Import the SDK to your Python code.

```Python
import rocs_client   # Import RoCS Client module
```

3. Create a robot object.

```Python
human = Human(host='192.168.9.17') 
```

!> RoCS supports three types of robots: dog, car, human. The above statement creates an instance of the `Human` class and assigns it to the variable `human`.  The `Human` class includes functionalities related to communication and interaction with the GR-1 robot at the specified IP address.

!> The host parameter is set to the IP address '192.168.12.1', which you should change to the actual IP of PC that your virtual robot runs on. For details, see **GR-1 as a WiFi client** in [Network Choice](https://fftai.github.io/#/networking?id=network-choice) section.

4. Control the Robot.

   You can use the following methods of the `human` class to control the robot:

   * `start()`: initiates or resets control.
   * `stop()`: triggers an emergency stop (halts with power off).
   * `exit()`: ends robot control session.
   * `stand()`: commands the robot to stand in place.
   * `walk(angle, speed)`: guides the robot in movement.

     * `angle(float)`: controls direction with a range of plus or minus 45 degrees. Positive for left, negative for right. The value is an 8-digit floating-point number.
     * `speed(float)`: manages forward and backward movement with a range of plus or minus 0.8. Positive for forward, negative for backward. The value is an 8-digit floating-point number.
   * `head(roll, pitch, yaw)`:  directs the GR-1 robot's head movements.

     * `roll(float)`: controls the roll angle (rotation around the x-axis). Negative for left, positive for right, within the range of (-17.1887-17.1887).
     * `pitch(float)`: adjusts the pitch angle (rotation around the y-axis). Positive for nodding forward, negative for nodding backward, within the range of (-17.1887-17.1887).
     * `yaw(float)`: manages the yaw angle (rotation around the z-axis). Negative for turning left, positive for turning right, within the range of (-17.1887-17.1887).
   * `move_joint(*motor)`: moves joints (variable length parameter, capable of controlling multiple joints simultaneously, estimated delay 2ms).

     * `motor(Motor)`: joint object, provides joint mapping relationships and parameter numbers through `human.motor_limits`.
   * `upper_body(arm_action, hand_action)`: executes preset commands for the upper limbs.

     * `arm_action(ArmAction)`: enumeration for arm preset commands.
     * `hand_action(HandAction)`: enumeration for hand preset commands.

##### Example Code

Here's an example code snippet showcasing the utilization of the Python Client SDK for robot control:

```Python
import time

from rocs_client import Human

from rocs_client.robot.human import ArmAction, HandAction, Motor

# Connect to your robot using its IP address
human = Human(host='192.168.9.17') # Replace '192.168.9.17' with your robot's actual IP

# Activate remote control for the robot
human.start() 

# Wait for 10 seconds to ensure the robot's control system stabilizes after initiating the remote control command start().
time.sleep(10) 

# Instruct the robot to stand up
human.stand() 

# Move the robot forward at a speed of 0.1
human.walk(0, 0.1) 

# Gesture: Wave the left hand
human.upper_body(arm=ArmAction.LEFT_ARM_WAVE)   

# Gesture: Wave both hands
human.upper_body(arm=ArmAction.TWO_ARMS_WAVE)   

# Gesture: Tremble the fingers
human.upper_body(hand=HandAction.TREMBLE)   

# Move motor no.1 left and right by 10 degrees each
human.move_joint(Motor(no='1', angle=10, orientation='left'), 

                 Motor(no='1', angle=10, orientation='right')) 

```

#### Using JavaScript/TypeScript Client SDK

1. Install the JavaScript/TypeScript Client SDK using npm:

```shell
npm install rocs-client
```

2. Import the SDK to your JavaScript/TypeScript code.

```javascript
import {Human} from 'rocs-client';   // import human class of RoCS client module
```

3. Create a robot object.

```javascript
let human = new Human({host: '192.168.9.17'}); //create an instance of the Human class and assigns it to the variable human
```

4. Control the robot.

   You can use the following methods of the `human` class to control the robot:

   * `start()`: initiates or resets control.
   * `stop()`: triggers an emergency stop (halts with power off).
   * `exit()`: ends robot control session.
   * `stand()`: commands the robot to stand in place.
   * `walk(angle, speed)`: guides the robot in movement.

     * `angle(float)`: controls direction with a range of plus or minus 45 degrees. Positive for left, negative for right. The value is an 8-digit floating-point number.
     * `speed(float)`: manages forward and backward movement with a range of plus or minus 0.8. Positive for forward, negative for backward. The value is an 8-digit floating-point number.
   * `head(roll, pitch, yaw)`: directs the GR-1 robot's head movements.

     * `roll(float)`: controls the roll angle (rotation around the x-axis). Negative for left, positive for right, within the range of (-17.1887-17.1887).
     * `pitch(float)`: adjusts the pitch angle (rotation around the y-axis). Positive for nodding forward, negative for nodding backward, within the range of (-17.1887-17.1887).
     * `yaw(float)`: manages the yaw angle (rotation around the z-axis). Negative for turning left, positive for turning right, within the range of (-17.1887-17.1887).
   * `move_joint(*motor)`: moves joints (variable length parameter, capable of controlling multiple joints simultaneously, estimated delay 2ms).

     * `motor(Motor)`: joint object, provides joint mapping relationships and parameter numbers through `human.motor_limits`.
   * `upper_body(arm_action, hand_action)`: executes preset commands for the upper limbs.

     * `arm_action(ArmAction)`: enumeration for arm preset commands.
     * `hand_action(HandAction)`: enumeration for hand preset commands.

##### Example code

Here's an example code snippet showcasing the utilization of the JavaScript/TypeScript Client SDK for robot control:

```Javascript/TypeScript
// Import Human class from the 'rocs-client' library
import {Human} from'rocs-client';  

// Create an instance of the Human class with the specified robot IP
let human = newHuman({host:'192.168.9.17'});      // Replace '192.168.9.17' with your robot's actual IP

// Enable remote control for the robot
human.start(); 

// After a brief delay, execute a sequence of actions
setTimeout(() => {
    // Make the robot stand up
    human.stand() 
    // Move the robot forward at a speed of 0.1
    human.walk(0, 0.1) 
    // Wave left hand
    human.upper_body(arm=ArmAction.LEFT_ARM_WAVE)   
    // Wave both hands
    human.upper_body(arm=ArmAction.TWO_ARMS_WAVE)   
    // Tremble the fingers
    human.upper_body(hand=HandAction.TREMBLE)   
  
    //Move motor no.1 left and right by 10 degrees each
    human.move_joint(Motor(no='1', angle=10, orientation='left'),

          Motor(no='1', angle=10, orientation='right')) 

  

    //  Control system built-in state machine to ensure the normal robot calibration and startup. It is recommended to execute subsequent commands 10 seconds after the start() command.

}, 10*1000)

```

# Extended Development Through Physical GR-1 Robot

## Initial Setup (First-time Users)

If this is your first time running the development environment, complete the following steps before proceeding with the setup:

1. Familiarize yourself with the robot's operation. Refer to [Operation Instruction](../concepts/operation_instruction.md) for details.
2. Install Server Environment Dependencies and RoCS Server Binary.

   Use either of the following commands in your terminal to install the server dependencies and RoCS Server binaries:

   **Option 1: Using curl:**

   ```shell
   curl -o- https://raw.githubusercontent.com/FFTAI/rocs_server/v1.3.0/install.sh | bash

   ```

   **Option 2: Using weget:**

   ```shell
   wget -qO- <https://raw.githubusercontent.com/FFTAI/rocs_server/v1.3.0/install.sh> | bash
   ```
3. Modify configuration information under the `sbin` folder.

```
sbin/
├── config/
├──── control_svr.conf        ***** Configuration for algorithm control program (path to the binary executable in bin/real). Modify accordingly if your file differs.
├──── password.conf           ***** Host password! Script requires sudo privileges, and the password is configured here.
├──── wifi.conf               ***** Wifi information (sets up the host as an access point with a wifi network for control. Note that this is optional; if you have another method for communication within the same network, you can ignore this setting).
```

!> We recommend carefully reading the README file in the sbin directory and then modifying the corresponding configuration information (modify according to your actual situation).

4. Run the following commands in a terminal to compile and install the runtime environment for real machine.

```shell
cd sbin
bash install.sh
```

!> Upon completion of these steps, your host machine will integrate three system services: `rocs_svr`, `rocs_model`, and `rocs_enable_wifi`, which are configured to automatic startup during system boot.

## Start Development

Once the initial setup is complete, simply power on the GR-1 and start your Client SDK or Control APP; you're ready to go because the three system services: `rocs_svr`, `rocs_model`, and `rocs_enable_wifi`, are already configured to automatically start during system boot, as mentioned above.

!> For the use of the Client SDKs, see [Lauching Client SDK](https://fftai.github.io/#/quickstart?id=lauching-client-sdk) for details. For the use of Control APP, see [Remote Control App User Guide](https://fftai.github.io/#/rocsappoperation?id=remote-control-app-user-guide) for reference.
