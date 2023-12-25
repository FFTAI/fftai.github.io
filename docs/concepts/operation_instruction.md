# Overview

This section is to guide you through the process of setting up and operating the Fourier Robot. Since the robot is delivered fully assembled, we will focus on the initial setup and basic operation.

[Inspecting Robot before Power-on](#Inspecting-Robot-before-Power-on)

# Initial Setup and Powering on

## Unpacking the Robot

!> Due to the substantial weight and intricate design of the robot, it is crucial to engage at least two individuals in the unboxing process. This collaborative effort ensures safe and secure handling, minimizing the risk of potential damage caused by pinching or accidental dropping.

To begin, carefully follow these steps:

1. Begin by extracting the robot from its packaging box.
2. Verify the items against the provided packing list.

| Items              | Quantity | Comments                                   |
| :----------------- | :------- | ------------------------------------------ |
| **Standard Items** |          |                                            |
| Robot              | 1        |                                            |
| Power Adapter      | 1        |                                            |
| Remote Controller  | 1        |                                            |
| User Manual        | 1        |                                            |
| Certification      | 1        |                                            |
| Calibration Tools  | 15       |                                            |
| Extension Dock     | 1        |                                            |
| **Optional Items** |          |                                            |
| Protective Lift    | 1        | If required, kindly purchase it separately |

3. Remove protective coverings to prepare the robot for use.

## Charging

Before the initial use, it's essential to ensure that the robot, Remote Controller, and protective lift (if purchased) are fully charged using the provided chargers.

`<a id="Inspecting-Robot-before-Power-on"></a>`

## Preparation Before Power on

### Environmental Inspection

The environment should meet the following criteria:

* The ground must be level and non-slippery to prevent accidental movements or falls.
* Avoid operating the robot on uneven, steep, muddy, loose, or slippery surfaces to prevent malfunctions or accidents.
* A minimum of 4 meters of free space around the robot is recommended to ensure a safe operating area and to accommodate the robot's range of motion.

![](static/1698656074242.png ":size=80%")

### Robot Inspection

Prior to use, perform a comprehensive check of the robot:

* Ensure the robot is properly fastened to the protective lift.
* Inspect for any loose or damaged parts that could hinder the robot's smooth and unobstructed movement.
* Check that the robot's battery and the battery of any connected mobile devices have sufficient power for the operation.
* Remove the calibration pin, if present, to allow for proper movement.

![](static/1698657344119.png ":size=80%")

### Initial Positioning

Before activating the robot, it's critical to set it to its initial pose. This includes:

1. Align shoulder slots.
2. Keep the arms hanging straight down with the palms facing inward.
3. Ensure a 10 cm interval between palms and hips.
4. Ensure that the robot stands pright.
5. The robot should bow down while keeping the waist upright, which facilitates a stable startup.

![](static/1698658681237.png ":size=80%")

## Powering on Robot

1. Long press actuator power-on button.
2. Press embedded computer power-on button.
3. Release Emergence Stop switch.

!> The Emergency Stop switch should be released only after the initial pose has been set. Once released, maintain the pose for at least 5 seconds to ensure stability.

![](static/poweron.png ":size=80%")

!>Observe the robot's indicator light; a steady breathing blink pattern indicates that the robot is starting up normally.

![](static/1698661268810.png ":size=30%")

## Connecting Control APP to Robot

The robot creates a Wi-Fi hotspot that the Control APP needs to connect to. Once the connection is successful, the Control APP will indicate a "Connected" status.

For details, see [Connecting to Robot](demo_app/connnecting_to_robot).

## **Initiating Control Software**

To start the motion control, you need to click `Startup` in the Control APP interface.


## Landing Robot

1. Ensure that the robot is fastened to the protective lift.
2. Click **Initial** to make the robot to initial state.
3. Lower the robot with the lift of the protective lift and ensure the robot's feet stably contact with the ground.
4. Click **Stand** in the remote controller.

## Controlling Robot

1. Power on the remote controller and connect to the robot's Wi-Fi.
2. Operate the remote controller to control the motion of the robot.

   ![1703237619698](image/operation_instruction/1703237619698.png)

## Halting Robot Motion

Following two approaches are used to halt the motion of the robot:

* Press the **Stand** button on the remote controller.
* Press down the E-stop button in case of danger or any emergency situation.

 !>E-stop will cut off the power supply of the robot and risk of data loss.

## Powering off Robot

1. Fasten the robot to the protective lift.
2. Press the E-stop button.
3. Press the actuator power button to power off the actuator.
4. Connect the robot to the monitor.
5. Kill the processes of the control software and then power off the robot host through the desktop terminal.

### Connecting robot to monitor

1. Power on the router.
2. Connect monitor to Type-C interface through the extension dock.

![](static/1698657743472.png)
