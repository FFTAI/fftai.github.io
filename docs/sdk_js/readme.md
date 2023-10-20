gros-client / [Exports](modules.md)

# Fourier Universal Robot System - Client SDK (Javascript/Typescript)
![](pics/banner.jpeg)

* [Source Code](https://github.com/FFTAI/gros_client_js.git)
* [Document](modules.md)

## Overview
This example (RoCS Client SDK) applies to the robot equipment that you already have provided by Fourier, through which you can control the robot. It provides a set of simple apis that allow you to easily interact with robots.

## Course

| Version number | Author | Date | Description | Quick preview |
|-----|--------|--------|------------------------------|--------------------------------------------|
| 0.1 | Fourier Software Department  | 2023.8 | 1. Project approval <br/>2. Confirm the infrastructure       | [0.1 Description](https://fftai.github.io/v0.1.html) |
| 0.2 | Fourier Software Department  | 2023.9 | 1. Control module, system module<br/>2. specific coding | [0.2 Description](https://fftai.github.io/v0.2.html) |

## Quick Start

### Install

```shell
npm install gros-client
```

### How to use
#### import sdk
First you need to import the SDK into your code

```javascript
import {Human} from 'gros-client';   
```
#### Create a robot object
Then, you need to create a robot object in order to use this SDK

```javascript
import {Human} from 'gros-client';  // Import Human, Car, Dog, etc

let human = new Human({host: '192.168.9.17'});
```

### Control the robot
You can use the following methods to control the robot:

- start(): return to zero or enables the control
- stop(): emergency stop(will be powered off)
- exit(): exit robot control
- stand(): stand in place
- walk(angle, speed): control the robot to move and walk
    - angle(float): indicate the Angle control direction. The value ranges from plus to minus 45 degrees. Left is positive, right is negative! (floating point 8 bits)
    - speed(float): before or after the speed control. The value ranges from plus to minus 0.8. Forward is positive, backward is negative! (floating point 8 bits)
- head(roll, pitch, yaw): control the human head motion of GR-01
    - roll(float): describe the Angle of rotation around the X-axis, left head is negative, right becomes positive, range (-17.1887-17.1887)
    - pitch(float): describe the Angle of rotation around the Y-axis. Front nod is positive, back nod is negative, range (-17.1887-17.1887)
    - yaw(float): describe the Angle of rotation around the z axis. Left torsion is negative, right torsion is positive, range (-17.1887-17.1887)
#### Sample code
Here is a complete example code that demonstrates how to use this SDK to control the robot:

```javascript
import {Human} from 'gros-client';  

let human = new Human({host: '192.168.9.17'});      // Replace host with the ip of the device you own

human.start(); // Enable remote control

setTimeout(() => {
    human.stand() // Stand
    human.walk(0, 0.1) // Move forward at a speed of 0.1
    
    //  Control system built-in state machine. In order to ensure the normal calibration and startup of the robot, it is recommended to execute subsequent commands 10 seconds after the start() command
}, 10 * 1000)
```
