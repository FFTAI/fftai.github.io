# Overview

The server is already installed in the embedded robot computer before delivery. To configure RoCS environment for physical robot, you only need to:

* [Modifying Configuration File](#modifying-configuration-file)
* [Setting Up Python Client SDK](quick_start/setup_for_physical_robot?id=setting-up-python-client-sdk) or [Setting Up Javascript/TypeScript SDK](quick_start/setup_for_physical_robot?id=setting-up-javascripttypescript-client-sdk)

# Modifying Configuration File

!> Reminder: This operation involves operating the robot. Be sure to familarize yourself with the basic operations through reading the [Operation Instruction](concepts/operation_instruction.md) section and remember to adhere to safety guidelines and recommendations throughout the process.

Prior to the initial use of the robot, you need to modify the configuration file `application.conf` according to your actual situation.

To do this:

1. Connect a monitor to the embedded robot computer via the robot Type C interface.
2. Navigate to the directory `/user/local/bin/rocs-svr` to access and make the necessary modifications.

```markdown
/usr/local/bin/rocs-svr/
├── config/                                     Configuration files
│ ├── application.conf                               ***** Configuration file, may need modification
│ ├── human_motor_limit_list.json                    ***** Robot joint limit information
```

3. Restart the embedded robot computer to make the modifications take effect.

# Setting Up Python Client SDK

!> We presume that you have already installed and configured both `Python` and `pip` correctly. If not, please consult the appropriate resources for guidance on their installation. The recommended Python versions are 3.8 and above.

## Installing Python Client SDK

The RoCS Client Python packages can be easily installed or upgraded from PyPI with the following command.

```shell
pip install rocs_client 
```

## Verifying the Installation

Run the following command to verify the installation:

**Windows Users**:

```shell
python -m pip list | findstr rocs-client
```

**Linux Users**:

```shell
python -m pip list | grep rocs-client
```

The following output signifies a successful installation.

```shell
C:\Users\Fourier>python -m pip list | findstr rocs-client
rocs-client        1.3.3
```

## Using Python Client SDK

1. Import the SDK to your Python code.

```Python
import rocs_client   # Import the RoCS Client module
```

2. Create a humanoid robot object.

```Python
from rocs_client import Human  # Import Human class, which represents behaviors of a humanoid robot.

human = Human(host='192.168.12.1')  # Replace the IP with actual IP of your device.

```

!> RoCS supports three types of robots: dog, car and human. The above statement creates an instance of the `Human` class and assigns it to the variable `human`.  The `Human` class includes functionalities related to communication and interaction with the GR humanoid robot at the specified IP address.

3. Control the robot.

   You can use the following methods of the `human` class to control the robot:

   * `_control_svr_start()`: turns on the robot.
   * `_control_svr_status()`: checks the current operational status of the robot.
   * `_control_svr_log_view()`: checks logs related to the robot's operations. It provides insights into the robot's runtime activities and events.
   * `_control_svr_close()`: initiates the process of shutting down the robot.
   * `stop()`: triggers an emergency stop (halts with power off).
   * `exit()`: ends robot control session.
   * `stand()`: commands the robot to stand in place.
   * `walk(angle, speed)`: guides the robot in movement.

     * `angle(float)`: controls direction with a range of plus or minus 45 degrees. Positive for left, negative for right. The value is an 8-digit floating-point number.
     * `speed(float)`: manages forward and backward movement with a range of plus or minus 0.8. Positive for forward, negative for backward. The value is an 8-digit floating-point number.
   * `head(roll, pitch, yaw)`:  directs the GR robot's head movements.

     * `roll(float)`: controls the roll angle (rotation around the x-axis). Negative for left, positive for right, within the range of (-17.1887-17.1887).
     * `pitch(float)`: adjusts the pitch angle (rotation around the y-axis). Positive for nodding forward, negative for nodding backward, within the range of (-17.1887-17.1887).
     * `yaw(float)`: manages the yaw angle (rotation around the z-axis). Negative for turning left, positive for turning right, within the range of (-17.1887-17.1887).
   * `move_joint(*motor)`: moves joints (variable length parameter, capable of controlling multiple joints simultaneously, estimated delay 2ms).

     * `motor(Motor)`: joint object, provides joint mapping relationships and parameter numbers through `human.motor_limits`.
   * `upper_body(arm_action, hand_action)`: executes preset commands for the upper limbs.

     * `arm_action(ArmAction)`: enumeration for arm preset commands.
     * `hand_action(HandAction)`: enumeration for hand preset commands.

## Example Code

Here's an example code snippet showcasing the utilization of the Python Client SDK for robot control:

### Code for Controlling Whole Robot (rocs_client>=1.0)

!> The version of the RoCS Client should be version 1.0 or higher for this example. Run command `pip show rocs_client` in a terminal to check the version of the installed package.

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

### Code for Controlling Motors (rocs_client>=1.3.3)

```python
import math
import threading
import time
import unittest

from rocs_client import Motor

motor = Motor(host="192.168.137.210")

arm_motor = motor.limits[0:17] if len(motor.limits) > 18 else []
clamping_jaw = motor.limits[17:19] if len(motor.limits) > 20 else []
dexterous_hand = motor.limits[19:31] if len(motor.limits) > 32 else []

print(f'arm_motor: {arm_motor}')
print(f'clamping_jaw: {clamping_jaw}')
print(f'dexterous_hand: {dexterous_hand}')

motors = arm_motor + clamping_jaw


def set_pds_flag():
    """ Enable the switch/flag for setting pd parameters """
    for item in motors:
        motor.set_motor_pd_flag(item['no'], item['orientation'])
    motor.exit()


def set_pds():
    """ Set pd parameters """
    for item in motors:
        motor.set_motor_pd(item['no'], item['orientation'], 0.36, 0.042)
    motor.exit()


def smooth_move_motor_with_differential(no, orientation, target_angle, offset=0.05, interval=0.004):
    """
    Use differential to move the motor smoothly
    Args:
        no: Number of the motor to be operated
        orientation: Orientation of the motor to be operated
        target_angle: Angle of motion
        offset: The Angle of each move
        interval: Interval of differential
    """
    if int(no) > 8:
        print('Motor number greater than 8 is not supported.')
        return

    def wait_target_done(rel_tol=2):
        while True:
            try:
                p = motor.get_motor_pvc(no, orientation)['data']['position']
                if math.isclose(p, target_angle, rel_tol=rel_tol):
                    break
            except Exception as e:
                print(f'wait_target_done err: {e}')

    while True:
        try:
            result = motor.get_motor_pvc(no, orientation)
            current_position = result['data']['position']
            if current_position is not None:
                break
        except Exception as e:
            print(f'current_position err: {e}')

    target_position = target_angle
    cycle = abs(int((target_position - current_position) / offset))

    for i in range(0, cycle):
        if target_position > current_position:
            current_position += offset
        else:
            current_position -= offset
        motor.move_motor(no, orientation, current_position)
        time.sleep(interval)
    wait_target_done()


def enable_all():
    """ Enable All Motors """
    for item in motors:
        motor.enable_motor(item['no'], item['orientation'])
    time.sleep(1)


def disable_all(offset=1, interval=0.015):
    """Disable All Motors """

    def _disable_left():
        for i in range((len(motors) - 1), -1, -1):
            item = motors[i]
            if item['orientation'] == 'left':
                smooth_move_motor_with_differential(item['no'], item['orientation'], 0, offset, interval)

        for i in range((len(motors) - 1), -1, -1):
            item = motors[i]
            if item['orientation'] == 'left':
                motor.disable_motor(item['no'], item['orientation'])

    def _disable_right():
        for i in range((len(motors) - 1), -1, -1):
            item = motors[i]
            if item['orientation'] != 'left':
                smooth_move_motor_with_differential(item['no'], item['orientation'], 0, offset=1.5, interval=0.02)

        for i in range((len(motors) - 1), -1, -1):
            item = motors[i]
            if item['orientation'] != 'left':
                motor.disable_motor(item['no'], item['orientation'])

    time.sleep(2)

    t_left = threading.Thread(target=_disable_left)
    t_right = threading.Thread(target=_disable_right)
    t_left.start(), t_right.start()
    t_left.join(), t_right.join()
    motor.exit()


class TestHumanMotor(unittest.TestCase):

    def test_set_pd_flag(self):
        """ Enable the switch/flag for setting pd parameters """
        set_pds_flag()

    def test_set_pd(self):
        """ Set pd parameters """
        set_pds()

    def test_enable_motors(self):
        """ Enable All Motors """
        enable_all()

    def test_disable_motors(self):
        """ Disable All Motors """
        disable_all()

    def test_get_pvc(self):
        """ Obtain the specified motor information """
        print(f"test_get_pvc {motor.get_motor_pvc('0', 'yaw')}")
        motor.exit()

    def test_action_sample(self):
        """
        This is a sample action

        When initially controlling a motor individually, it is strongly recommended to run this function for testing.

        If the motor moves smoothly and predictably, explore slightly more complex actions.

        However, if the motor becomes unresponsive or behaves unexpectedly, fine-tune the P and D parameters.

        If the robotic arm's movements are smooth and stable, build more advanced programming on this foundation.

        To coordinate multiple joints for simultaneous motion, consider using the `threading` approach for control.
        Additional examples provide specific details.   
  
  
        """



        enable_all()
        smooth_move_motor_with_differential('2', 'left', -20)
        smooth_move_motor_with_differential('3', 'left', -40)
        # disable_all()
```

### Code for Controlling Hands (rocs_client>=1.3.3)

```python
from rocs_client import Motor

motor = Motor(host="192.168.12.1")


def test_enable_hand():
    """Enabling hand"""
    motor.enable_hand()
    motor.exit()


def test_disable_hand():
    """ Disabled hand """
    motor.disable_hand()
    motor.exit()


def test_get_hand_position():
    """ Obtain Hand Position"""
    print(f'test_get_hand_position:  {motor.get_hand_position()}')


test_enable_hand()

angle = 500
motor.move_motor('11', 'left', angle)
motor.move_motor('12', 'left', angle)
motor.move_motor('13', 'left', angle)
motor.move_motor('14', 'left', angle)

motor.move_motor('11', 'right', angle)
motor.move_motor('12', 'right', angle)
motor.move_motor('13', 'right', angle)
motor.move_motor('14', 'right', angle)
motor.exit()

```

### Additional Test Cases

Addtional test cases can be found in [Test Cases](https://github.com/FFTAI/rocs_client_py/tree/main/test).

# Setting Up JavaScript/TypeScript Client SDK

Prior to the setup, install Node.js and npm:

* Download and install Node.js from [nodejs.org](https://nodejs.org/).
* npm (Node Package Manager) comes bundled with Node.js.
* Verify installation by running `node -v` and `npm -v` in your terminal.

## Installing JavaScript/TypeScript SDK

The RoCS JavaScript/TypeScript Client packages can be easily installed or upgraded with the following command.

```shell
npm install rocs-client
```

## Verifying the Installation

Run the following command to verify the installation:

```shell
npm list rocs-client
```

**T**he following output signifies a successful installation.

```shell
C:\Users\Fourier>npm list rocs-client
Fourier@ C:\Users\Fourier
`-- rocs-client@1.1.0
```

## Using JavaScript/TypeScript SDK

1. Import the SDK to your JavaScript/TypeScript code.

```javascript
import {Human} from 'rocs-client';   // import human class of RoCS client module
```

3. Create a robot object.

```javascript
import {Human} from 'rocs-client';  // Import Human, Car, Dog, etc

let human = new Human({host: '192.168.9.17'}); // Please replace host with the ip of your device

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
   * `head(roll, pitch, yaw)`: directs the GR robot's head movements.

     * `roll(float)`: controls the roll angle (rotation around the x-axis). Negative for left, positive for right, within the range of (-17.1887-17.1887).
     * `pitch(float)`: adjusts the pitch angle (rotation around the y-axis). Positive for nodding forward, negative for nodding backward, within the range of (-17.1887-17.1887).
     * `yaw(float)`: manages the yaw angle (rotation around the z-axis). Negative for turning left, positive for turning right, within the range of (-17.1887-17.1887).
   * `move_joint(*motor)`: moves joints (variable length parameter, capable of controlling multiple joints simultaneously, estimated delay 2ms).

     * `motor(Motor)`: joint object, provides joint mapping relationships and parameter numbers through `human.motor_limits`.
   * `upper_body(arm_action, hand_action)`: executes preset commands for the upper limbs.

     * `arm_action(ArmAction)`: enumeration for arm preset commands.
     * `hand_action(HandAction)`: enumeration for hand preset commands.

## Example code

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
