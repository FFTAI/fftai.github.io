# Overview

The SDK library serves as a crucial component for applications aiming to exercise command over the GR-1, retrieve sensor data, and set up payload services. This quickstart guide offers a step-by-step walkthrough to assist you in installing the necessary SDK libraries (both in Python and JavaScript/TypeScript) and running basic programs for GR-1 control.

The SDK can be executed in either a virtual environment or on a physical robot:

# Extended Development Through Virtual Environment Webots

 To set up a virtual development environment, you need to:

* [Installing Server Environment Dependencies and RoCS Server Binary](http://localhost:3000/#/quickstart?id=installing-server-environment-dependencies-and-rocs-server-binary)
* [Installing Webots](http://localhost:3000/#/quickstart?id=installing-webots)
* [Starting the RoCS Server](http://localhost:3000/#/quickstart?id=starting-the-rocs-server)
* [Loading Webots Model](http://localhost:3000/#/quickstart?id=loading-webots-model)
* [Lauching Client SDK](http://localhost:3000/#/quickstart?id=lauching-client-sdk)

## Installing Server Environment Dependencies and RoCS Server Binary

Use either of the following commands in your terminal to install the server dependencies and RoCS Server binaries:

**Option 1: Using curl:**

```shell
curl -o- https://raw.githubusercontent.com/FFTAI/rocs_server/v1.3.0/install.sh | bash

```

**Option 2: Using weget:**

```shell
wget -qO- <https://raw.githubusercontent.com/FFTAI/rocs_server/v1.3.0/install.sh> | bash
```

## Installing Webots

Follow these steps to set up the virtual robot environment using Webots:

1. Open a terminal and run the following command to download the webots installation package:

```shell
wget https://github.com/cyberbotics/webots/releases/download/R2023b/webots_2023b_amd64.deb
```

2. Run command ``sudo dpkg -i webots_2023b_amd64.deb`` to install the package.

!> Webots is a robot simulation software developed by Cyberbotics，which is used for simulating and testing the behavior of robots in a virtual environment before deploying them in the physical world. Webots provides a library of pre-built robot models representing a wide variety of robots. It incorporates a powerful physics engine that simulates realistic interactions between robots and their environments. It supports programming interfaces in several languages (C, C++, Python, Java) for developing and controlling robot behaviors. For more information on Webots, you can refer to its official documentation: [Webots User Guide](https://www.cyberbotics.com/doc/guide/index).

## Starting the RoCS Server

Open a terminal, run the following command:

```shell
cd ~/.rocs_server1.3.0/sbin
bash start_up_rocs_svr.sh
```

After running these commands, the server service will be active, allowing the client SDK to send control commands to the virtual robot.

!> Ensure that the server is successfully started before attempting to interact with the virtual robot using the client SDK.

## Loading Webots Model

1. Open a terminal and run the `webots`command to start Webots GUI interface.
2. Navigate to `File` -> `Open World`.
3. Select the world file located at `.rocs_server/bin/webots/webotsim/worlds/SonnyV4.wbt`.

!> If the model cannot be shown, attempt to restore the layout by navigating to Tools -> Restore Layout.

## Lauching Client SDK

You can choose either Python Client SDK or JavaScript/TypeScript Client SDK to control the robot.

### Using Python Client SDK

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

!> The host parameter is set to the IP address '192.168.12.1', which you should change to the actual IP of PC that your virtual robot runs on. For details, see **GR-1 as a WiFi client** in [Network Choice](http://localhost:3000/#/networking?id=network-choice) section.

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

#### Example Code

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

### Using JavaScript/TypeScript Client SDK

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

#### Example code

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

To develop with a physical robot, you need to:

1. Get familiar with the robot operation, see [Operation Instruction](operationinstruction.md) for details.
2. Installing Server Environment Dependencies and RoCS Server Binary.

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

4. Power on GR-1 and explore.

   After completing the above actions, congratulations, you have successfully installed!

   Now, you can begin your robot experience using our provided SDK or Android APK to control Fourier GR1.

!> For the use of the Client SDKs, see [Lauching Client SDK](http://localhost:3000/#/quickstart?id=lauching-client-sdk) for details. For the use of Control APP, see [Remote Control App User Guide](http://localhost:3000/#/rocsappoperation?id=remote-control-app-user-guide) for reference.
