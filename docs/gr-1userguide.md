# Concepts

This documentation is intended to guide you for the extended development of GR-1 based on the SDKs provided.

Two approaches are provided to control and develop the GR-1 robot:

* Through virtual environment Webots
* Through physical robot

For the development using virtual environment, refer to [Extended Development Through Virtual Environment Webots](#extended-development-through-virtual-environment-webots).

For the development using physical robot, refer to [Extended Development Through Physical GR-1 Robot](#extended-development-through-physical-gr-1-robot).

# Fourier GR-1

Fourier GR-1 is a general-purpose humanoid robot. It is composed of up to 40 FSA joints, which can provide 230 N.m peak joint torque. The whole body controll algorithm enables 44 full-body degrees of freedom.

Its human-like agility and motion kinematics, such as:

* Straight leg walking
* Fast walking
* Agile obstacle evasion
* Steady slope ascending and descending
* Resilient impact disturbance response
* Human-robot collaboration in task execution

makes it a potential carrier for the next-generation "Embodied AI", which would combine AI technology with physical robots to provide controllable, perceptible, interactive, and mobile entities.

The Fourier GR-1 offers scalability for validating various AI models and algorithms, with significant potential in industrial, rehabilitation, home, and research applications.

![1698383000820](image/readme/1698383000820.png)

## GR-1 Specifications

| Mechanical    |                                      |
| ------------- | ------------------------------------ |
| Standing size | 1650 x 515 x 320 mm                  |
| Arm span      | 1680 mm                              |
| Net weight    | ≈ 55 kg                              |
| Materials     | Aluminum alloy, engineering plastics |

| Electrical           |         |
| -------------------- | ------- |
| Power supply voltage | 46.2 V  |
| Max.  power          | ≈ 550 W |

| Performance              |                                      |
| ------------------------ | ------------------------------------ |
| Walk speed               | 5 km/h                               |
| Single hand payload      | ≈ 3 kg                               |
| Basic computing capacity | 7-13700h 6P+8E 20 threads 1.6/5.0GHz |

| Joint                 |                                                                                                                                                                                                                                                                                                                                                                           |
| --------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Total joint actuators | 44                                                                                                                                                                                                                                                                                                                                                                        |
| FSA actuators         | 32                                                                                                                                                                                                                                                                                                                                                                        |
| Maximum joint torque  | 230 N.m                                                                                                                                                                                                                                                                                                                                                                   |
| Operating voltage     | 12 - 60 V                                                                                                                                                                                                                                                                                                                                                                 |
| Rated voltage         | 46 V                                                                                                                                                                                                                                                                                                                                                                      |
| Max. current          | 40 A                                                                                                                                                                                                                                                                                                                                                                      |
| Joint motions         | Head: forward, backward, left, right, roll<br />Shoulder: forward, backward, left, right, roll<br />Wrist: forward, backward, left, right, roll<br />Hip: flexion and extension, inward/outward roll, side swing<br />Anckle: flexion and extension, side swing<br />Knee: flexion and extension<br />Waist: forward, backward, left, right, roll<br />Finger: grip, hold |
| Complied standards    | GB 17625.1-2012，GB 4943.1-2011，GB/T 9254-2008                                                                                                                                                                                                                                                                                                                           |

| Sensor       |           |
| :----------- | --------- |
| Depth camera | Realsense |
| IMU          | √         |

| Battery and adapter     |                    |
| :---------------------- | ------------------ |
| Battery capacity        | 483 Wh             |
| Battery type            | Lithium battery    |
| Battery nominal voltage | 40 V               |
| Charging limit voltage  | 46 V               |
| Rated capacity          | 5.2Ah 112.3Wh      |
| Cruise duration         | ≈ 60 min           |
| Walk cruise duration    | ≈ 45 min           |
| Full charge             | 315 min            |
| Adapter input           | 100-240 V, 50/60Hz |
| Adapter output          | MAX. 46 V, 2 A     |

| Operating system and connections |                                                                       |
| :------------------------------- | --------------------------------------------------------------------- |
| OS                               | Ubuntu18.04+ROS 2                                                     |
| External interfaces              | HDMIx1，Type-C x 3(fast charge，USB，peripheral extension ports)      |
| Wireless connection              | Wi-Fi，EEE 80211a/b/g/n/ac, bluetooth 4.2                             |
| Host                             | ASUS 13th Generation - Dawn X MINI Commercial and Home Office Desktop |
| Model                            | PN64171RZ                                                             |
| CPU                              | I7 13700H                                                             |
| Memory                           | 16 G                                                                  |
| SSD                              | 512 G                                                                 |

## Operation Instruction

#### Before power-on

Do the following steps before powering on the robot:

1. Inspect robot.  

   Ensure that the robot is fastened to the support stand.  
   Ensure that the batteries of robot and the support stand are fully chareged.  
   Ensure that the robot components moves smoothly.

   ![1698657344119](image/README/1698657344119.png)
2. Inspect environment.  

   Ensure that there is a 4-meter clearance around the robot and that the ground is level and dry.

   ![1698656074242](image/README/1698656074242.png)
3. Connect robot to monitor.  

   Power on the router.  
   Connect monitor to Type-C interface through the extension dock.  

   ![1698657743472](image/README/1698657743472.png)
4. Prepare arms for calibration.  

   Align shoulder grooves.  
   Keep the arms hanging straight down with the palms facing inward.  
   Ensure a 10 cm interval between palms and hips.  
   Ensure that the robot stands upright.  

   ![1698658681237](image/README/1698658681237.png)

### Powering on Robot

1. Press actuator power-on button.
2. Press robot host power-on button.
3. Release e-stop switch.

   ![1698659185945](image/README/1698659185945.png)
4. Initialize robot arms and legs through desktop terminal.  

   Enter the following command to calibrate arms.  

   ```
   $sh arm .sh
   ```

   Enter the following command to calibrate legs.  

   ```
   $sh leg.sh
   ```

!>The robot has started successfullly if the indicator lights of actuators and robot host flash regularly.

   ![1698661268810](image/README/1698661268810.png)

### Connecting Remote Controller to Robot

1. Switch on the remote controller and open the **System Settings** interface.
2. Input the Wi-Fi account and password specified on the back of the robot.

![1698736555432](image/README/1698736555432.png)

31. Click **Connect** .

!> A success prompt will be given when the connection succeeds.

### Landing Robot

1. Ensure that the robot is fastened to the support stand.
2. Click **Initial** to make the robot to initial state.
   ![1698744141867](image/README/1698744141867.png)
3. Lower the robot with the lift of the support stand and ensure the robot's feet stably contact with the ground.  
4. Click **Stand** in the remote controller.

![1698744210172](image/README/1698744210172.png)

### Controlling Robot

1. Power on the remote controller and connect to the robot's Wi-Fi.
2. Operate the remote controller to control the motion of the robot.  
  
   Use left handler to move the robot.
   Use right handler to control the vision field.

   ![1698744913325](image/README/1698744913325.png)

### Pausing Robot Motion

Following two approaches are used to pause the motion of the robot:

* Press the **Stand** button on the remote controller.
* Press down the E-stop button in case of danger or any emergency situation.
  
 !>E-stop will cut off the power supply of the robot and risk of data loss.

### Powering off Robot

1. Fasten the robot to the supoort stand.
2. Press the E-stop button.
3. Press the actuator power button to power off the actuator.
4. Connect the robot to the monitor.
5. Kill the processes of the control software and then power off the robot host through the desktop terminal.

   ![1698745650898](image/README/1698745650898.png)
