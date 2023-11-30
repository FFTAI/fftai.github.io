# RoCS-Client SDK (python)

## Overview

This example (RoCS Client SDK) is suitable for you already have a robot device provided by Fourier!
This example can be used to control the robot.
It provides a set of simple APIs that allow you to easily interact with the robot.

## Quick Start

### Installation

```shell
pip install rocs_client 

# If you encounter network delay, you can choose to install from Tsinghua source 
# pip install -i https://pypi.tuna.tsinghua.edu.cn/simple rocs_client
```

### Usage

#### Import sdk

First, you need to import this SDK in your Python code

```python
import rocs_client   # Import root
```

#### Create a robot object

Then, you need to create a robot object in order to use this SDK

```python
from rocs_client import Human  # Import Human as needed, similarly there are Car, Dog, etc.

human = Human(host='192.168.12.1')
```

### Control the Robot

You can use the following methods to control the robot:

- start(): Zero/Start control
- stop(): Emergency stop (will stop with power off)
- exit(): Exit robot control
- stand(): Stand in place
- walk(angle, speed): Control the robot to move, walk
  - angle(float): Angle controls direction, range is plus or minus 45 degrees. Left is positive, right is negative! (Floating point number with 8 digits)
  - speed(float): Speed controls forward and backward, range is plus or minus 0.8. Forward is positive, backward is negative! (Floating point number with 8 digits)
- head(roll, pitch, yaw): Control GR-01 humanoid head movement
  - roll(float): roll (roll angle): describes the angle of rotation around the x-axis, left turn head is negative, right turn is positive, range (-17.1887-17.1887)
  - pitch(float): pitch (pitch angle): describes the angle of rotation around the y-axis. Nodding forward is positive, nodding backward is negative, range (-17.1887-17.1887)
  - yaw(float): yaw (yaw angle): describes the angle of rotation around the z-axis. Turning left head is negative, turning right head is positive, range (-17.1887-17.1887)
- move_joint(*motor): Move joint (variable length parameter, can control multiple joints at the same time, delay estimate 2ms)
  - motor(Motor): Joint object, can get corresponding joint mapping relationship and parameter number through human.motor_limits
- upper_body(arm_action, hand_action): Upper limb preset command
  - arm_action(ArmAction): Arm preset command enumeration
  - hand_action(HandAction): Hand preset command enumeration

### Sample Code

Below is a complete sample code that demonstrates how to use this SDK to control a robot:

```python
import time
from rocs_client import Human
from rocs_client.robot.human import ArmAction, HandAction, Motor

human = Human(host='192.168.9.17') # Please replace host with the ip of your device
human.start() # Start remote control
time.sleep(10) # Control system built-in state machine. To ensure normal calibration and startup of the robot, it is recommended to execute subsequent instructions after start() instruction for 10s

human.stand() # Stand up
human.walk(0, 0.1) # Move forward at a speed of 0.1

human.upper_body(arm=ArmAction.LEFT_ARM_WAVE)       # Wave left hand
human.upper_body(arm=ArmAction.TWO_ARMS_WAVE)       # Wave hands
human.upper_body(hand=HandAction.TREMBLE)           # Tremble fingers

human.move_joint(Motor(no='1', angle=10, orientation='left'), 
                 Motor(no='1', angle=10, orientation='right')) # Move motor no.1 left and right by 10 degrees each

```
