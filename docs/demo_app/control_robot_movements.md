# Controlling Robot Movements

The RoCS Control App provides users with intuitive controls to command various movements of the robot, allowing for a dynamic and interactive experience.

Following topics are covered:

- [Controlling Robot Movements](#controlling-robot-movements)
  - [Stand Motion](#stand-motion)
  - [Gait Motion](#gait-motion)
  - [Stationary Motion](#stationary-motion)
  - [Grasping Motion](#grasping-motion)

!> All motions should be executed with the prerequisite that the robot has been properly landed. This implies that the robot is already in its initial state and is standing independently. For how to land the robot, refer to section [Landing Robot](concepts/operation_instruction?id=landing-robot).

## Stand Motion

In `Stand` mode, the robot maintains a static standing posture, suitable for scenarios requiring a stationary robot presence. This mode is useful for applications where a consistent and non-mobile robot presence is needed.

To engage the robot in `Stand` mode:

1. Click `Stand` to make the robot stand up.

!> The robot's position will be automatically checked against the calibrated pose when transition from the `initial` state to `Stand`. If the robot's posture falls outside the acceptable range, the `Stand` button will become unavailable, and the following prompt will be displayed.

  ![1704768021321](image/control_robot_movements/1704768021321.png)

2. The robot will maintain a static standing position until instructed otherwise.

!> Avoid keeping robot in the stand position for an extended period, as it can cause damage to ankle actuators due to overloading.

## Gait Motion

In Gait motion mode, users can command the robot to move in different directions, including forward, backward, left, and right. This mode offers a dynamic and directional approach, enabling users to navigate the robot seamlessly.

To control the robot in `Gait`motion mode:

1. Select a desired `Gait` motion.

   ![1702625084624](image/control_robot_movements/1702625084624.png)
2. Use the intuitive controls, such as a joystick or touchscreen, to direct the robot's movements.
3. Experiment with variations in speed and direction to suit specific scenarios.

## Stationary Motion

Stationary motion mode provides control over the robot's movements while it remains in a fixed position. This mode is ideal for showcasing dynamic actions without changing the robot's location.

To control the robot in Stationary motion mode:

1. Select a desired `Stationary` motion.

   ![1702625005544](image/control_robot_movements/1702625005544.png)
2. Utilize the controls to prompt on-the-spot movements, allowing for dynamic action demonstrations.

## Grasping Motion

Grasping motion mode introduces a specialized mode for controlling the robot's end effector grasping actions. This mode is designed for tasks involving object manipulation, adding a unique capability to the robot.

To control the robot in Grasping motion mode:

1. Select a desired `Grasping` motion.

   ![1702625405510](image/control_robot_movements/1702625405510.png)
2. Use the controls to command the robot's end effector, allowing for precise grasping actions.

Understanding these distinct motion modes empowers users to command the robot effectively, whether it's navigating a space, demonstrating actions, maintaining a static posture, or engaging in intricate object manipulation tasks. Experimenting with different modes and controls enhances the user experience, offering versatility in robotic interactions.
