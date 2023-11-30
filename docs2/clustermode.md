
# **Cluster Mode in RoCS**

Cluster mode in RoCS refers to a specific operational configuration where multiple robotic systems, usually termed as nodes or robots, operate in a synchronized and coordinated manner under the control of a central main control robot. This mode is designed to enhance the capabilities and efficiency of robotic systems, particularly in scenarios where a collective effort or coordination among multiple robots is required.

## Key Aspects of Cluster Mode:

**Network Connectivity:**

* In cluster mode, all robots are interconnected through a network, allowing seamless communication and data exchange.

**Main Control Machine:**

* One robot is designated as the main control robot, often referred to as the "master" or "main controller." This robot takes on a central role in managing and coordinating the activities of the entire cluster.

**Distributed Operation:**

* Each robot in the cluster can operate independently, contributing to the collective tasks assigned to the robotic system. The robots work together in a distributed fashion to achieve common goals.

**Synchronization:**

* The main control robot is responsible for ensuring synchronization among all robots in the cluster. This synchronization is crucial for maintaining consistency in movements, actions, and overall behavior.

**Parallel Processing:**

* Cluster mode enables parallel processing, allowing multiple robots to perform tasks simultaneously. This can significantly enhance the overall speed and efficiency of the robotic system.

## Cluster Mode in RoCS Architecture:

* **Control App (User Graphic Application):**
  * The Control App, serving as a graphical application for external terminals, plays a crucial role in overseeing and managing the cluster. It provides a comprehensive reference for developers, facilitating interaction with the robotic systems.
* **Client SDK (Client Interface):**
  * The Client SDK serves as the client-side interface, enabling developers to interact with the Robot Control System. It offers a streamlined mechanism for accessing the Server API, encouraging the development of customized applications for cluster management.
* **Server API (Server Interface):**
  * Operating within the robot, the Server API functions as a lightweight data forwarding layer. It leverages HTTP and WebSocket protocols for efficient data transmission between the main control machine and individual machines in the cluster.

## Use Cases for Cluster Mode:

* **Collaborative Tasks:**
  * Cluster mode is beneficial for scenarios where multiple robots need to collaborate on a task, such as moving objects collectively or coordinating in a complex environment.
* **Increased Efficiency:**
  * The parallel processing capabilities of cluster mode enhance the overall efficiency of robotic operations, especially in situations that require simultaneous actions.
* **Scalability:**
  * As additional robots are added to the cluster, the system remains scalable, allowing for the expansion of capabilities without a significant impact on performance.



Cluster mode in RoCS provides a powerful framework for orchestrating the actions of multiple robotic systems, fostering collaboration, and enabling efficient parallel processing to tackle complex tasks.

!> Please be advised that the cluster mode in RoCS is a specialized service provided exclusively by our expert team. Due to the intricate nature of the configuration, this process requires vendor expertise. Customers are kindly requested to contact our support team for tailored cluster mode customization, as it involves aligning the system with specific robotic functionalities and ensuring optimal performance.
