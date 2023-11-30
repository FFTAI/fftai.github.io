# RoCS-Client SDK (Javascript/Typescript)

The RoCS-Client SDK provides a convenient way to control your Fourier robot device. It offers a set of straightforward APIs for seamless interaction with the robot.

## Installing SDK

Install the SDK using npm:

```shell
npm install rocs-client
```

## Using the SDK


#### import sdk

First you need to import the SDK into your code

```javascript
import {Human} from 'rocs-client';   
```

#### Create a robot object

Then, you need to create a robot object in order to use this SDK

```javascript
import {Human} from 'rocs-client';  // Import Human, Car, Dog, etc

let human = new Human({host: '192.168.9.17'});
```

### Control the robot

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

#### Sample code

Here is a complete example code that demonstrates how to use this SDK to control the robot:

```javascript
import {Human} from 'rocs-client';  

let human = new Human({host: '192.168.9.17'});      // Replace host with the ip of the device you own

human.start(); // Enable remote control

setTimeout(() => {
    human.stand() // Stand up
    human.walk(0, 0.1) // Move forward at a speed of 0.1
  
    human.upper_body(arm=ArmAction.LEFT_ARM_WAVE)       // Wave left hand
    human.upper_body(arm=ArmAction.TWO_ARMS_WAVE)       // Wave hands
    human.upper_body(hand=HandAction.TREMBLE)           // Tremble fingers
  
    human.move_joint(Motor(no='1', angle=10, orientation='left'),
          Motor(no='1', angle=10, orientation='right')) // Move motor no.1 left and right by 10 degrees each
  
    //  Control system built-in state machine. In order to ensure the normal calibration and startup of the robot, it is recommended to execute subsequent commands 10 seconds after the start() command
}, 10 * 1000)
```
