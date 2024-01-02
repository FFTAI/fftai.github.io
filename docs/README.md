# What it is

> Where precision fuses with robotic mastery.

The Robot Control System, abbreviated as RoCS, is an advanced software framework designed for precise management and control of robots. It is the upper computer of the whole Fourier robot  software system which includes both upper computer and lower computer.

RoCS empowers robots with exceptional control and functionality. Here's a brief overview:

## Features

* **High Precision Control:** RoCS excels in various tasks, be it in industrial automation, medical surgery, or other domains, thanks to its precise control of robotic systems.
* **Layered Architecture:** It employs a modular architecture, making maintenance and scalability a breeze. This simplifies development and integration, enhancing system maintainability.
* **User-Friendly Interface:** RoCS provides a user-friendly graphical interface (Control App) that expedites the development process, allowing developers to interact with and monitor robotic systems seamlessly.
* **Open Source:** Part of RoCS (Client SDK) is open source, fostering community engagement and driving innovation by offering flexibility and customization opportunities.
* **Efficient Data Transmission:** RoCS's Server API ensures efficient and secure data transfer through HTTP and WebSocket protocols, crucial for real-time control and monitoring.
* **Comprehensive Functionality:** RoCS offers a wide range of functionalities, including sound and video processing, motion algorithms, hardware control, and more, making it suitable for diverse robotic application domains.
* **Integration:** RoCS effectively integrates various components within its layered structure, making it a comprehensive robotic control system capable of meeting diverse application needs.

## Lower Computer

The lower computer, acting as the equivalent of the cerebellum in human physiology, specializes in motion control, handling motor control, motion algorithms, hardware driver management, and other critical functions essential for the robot's movement and stability.

## Upper Computer

The upper computer is dedicated to data exchange and executing specific logic applications. It manages tasks such as receiving and playing audio, real-time transmission of video streams, dispatching precise instructions to hardware components, and continuous monitoring of the robot's operational status.

## Components of RoCS

RoCS consists of three components:

* **Control App (User Graphic Application)**

  An intuitive graphical application for developers to reference and interact with.
* **Client SDK (Client Interface)**

  Facilitates interaction with the Robot Control System, encouraging the development of customized applications.
* **Server API (Server Interface)**

  Acts as a conduit between the lower computer and the external world, ensuring efficient and secure data exchange. It leverages HTTP and WebSocket protocols for communcation. Due to efficiency and security concerns, it is not open-sourced.

## RoCS Architecture

The RoCS architecture offers precise control and management of robotic systems through network-based communication, connecting the terminal with the three layers of the system.

![](concepts/static/about_rocs.png)

* **Bottom Layer - Motion Library**

  * The Motion Library, at the bottom layer, handles core functions related to motion control and operational control.
  * It encompasses motor control, motion algorithms, and operational control, ensuring precise and coordinated robot movements.
* **Middle Layer - Body**

  * The middle layer, known as the Body, represents the physical embodiment of the robot and is responsible for various aspects of its operation.
  * Components for head interaction, joint control, upper limb dexterity, hand environmental awareness, and proprioception contribute to the robot's physical capabilities and sensory perception.
* **Upper Layer**

  * The uppermost layer is versatile and dynamic, incorporating advanced functionalities such as graphical programming, cluster control, avatar control, and embodied intelligence.
  * This layer enables higher-level tasks, including human-robot interaction, decision-making, and intelligent behaviors.

For more information, see the [Quick Start](quick_start/overview.md) section.
