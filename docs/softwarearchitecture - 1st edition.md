# Software Architecture

Software architecture enables the functionality of the robot by providing a structured and organized framework that effectively manages the various aspects of the robot's operation. Here's how each layer of the architecture contributes to the robot's functionality:

![1698819486264](image/README/1698819486264.png)

The control of robotic system is through a network-based communication framework. This system ensures smooth interaction with the robot and empowers operators to issue commands while receiving real-time feedback. The supported communication protocols are `HTTP `and `WebSocket`. Any client, whether it's implemented in `Node.js` or `Python`, can be utilized as long as it supports these two protocols to establish communication with the three system layers. Furthermore, a joystick terminal running the Control APP can also be employed for this purpose.

Overall, this three-layered architecture is designed to create a balanced system. The Bottom Layer handles fundamental control, the Middle Layer provides the physical capabilities and sensory perception, and the Upper Layer adds advanced functionality and intelligence. This architecture enables the robot to perform tasks, interact with humans, and adapt to a wide range of applications and environments, making it a versatile and functional robotic system.

## Bottom Layer - Motion Library

### Core Motion Control

- This layer ensures that the robot's fundamental motion control, including motor control and low-level operational control, is handled accurately. This is crucial for controlling the robot's movement, which is fundamental to its operation.

### Motion Algorithms

- The use of motion algorithms within this layer ensures that the robot can execute precise and coordinated movements. These algorithms help the robot navigate its environment and interact with objects or humans effectively.

### Operational Control

- Operational control functions ensure that the robot's basic operational aspects are managed efficiently, such as power management, self-calibration, and diagnostics. This is essential for the robot's overall reliability and performance.

## Middle Layer - Body

### Physical Representation

- The Body layer represents the physical embodiment of the robot, encompassing its structural components. It is responsible for various physical aspects, such as head interaction, joint control, hand Dexterity, environmental Awareness, and proprioception.

### Head Interaction

- This component provides sensory perception, allowing the robot to interact with its environment through vision, hearing, or other sensory modalities.

### Joint Control

- Joint control contributes to the robot's mobility and flexibility, enabling it to perform various physical tasks and movements.

### Hand Dexterity

- This aspect enhances the robot's ability to manipulate objects and interact with the environment in a precise and controlled manner.

### Environmental Awareness

- Environmental awareness ensures that the robot can interact with objects safely and adapt to its surroundings.

### Proprioception

- Proprioception enables the robot to have self-awareness of its body and movements, which is vital for executing tasks effectively and avoiding collisions.

## Upper Layer

The Upper Layer provides a dynamic and versatile framework that includes advanced functionalities, such as graphical programming, cluster control, avatar control, and embodied intelligence.

### Graphical Programming

- Graphical programming tools simplify customization and programming, making it easier for developers and users to define robot behaviors and tasks.

### Cluster Control

- The ability to control multiple robots as a cluster enhances the robot's capabilities for collaborative and coordinated tasks.

### Avatar Control

- This feature can allow remote operation by a human user, enabling teleoperation or remote supervision.

### Embodied Intelligence

- Embodied intelligence empowers the robot to exhibit intelligent behaviors and adapt to changing situations, enhancing its autonomy and problem-solving abilities.
