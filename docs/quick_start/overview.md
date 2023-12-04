# Overview

RoCS serves as the core engine responsible for executing algorithmic control logic. 
It plays a crucial role in receiving commands from `Control App` or `SDK control programs`. The server adopts a layered structure, comprising three key components:

1. **Control Logic Component `rocs_svr`:** RoCS Server executes algorithmic control programs, managing intricate robot movements and actions to ensure the accurate execution of user-defined tasks.
2. **Communication Component `rocs_enable_wifi`:** ensures the robot can effectively connect to the network and achieve functionalities such as remote control and data transmission.
3. **3D model Component `rocs_model`:** delivers 3D model information of the robot and offers the capability to better comprehend and visualize the external appearance and structural details of the robot throughout the development process.

Next, we'll guide you through the [quick installation and use of RoCS](quick_start/installation.md)