# Overview


**rocs_server** is the core engine for executing algorithmic control logic. It plays a crucial role in receiving commands from "Control App" or "SDK control programs". The server adopts a layered structure, including the following key components: 

1. **Control Logic Component `rocs-svr`:** Used to execute algorithmic control programs, managing complex robot movements and actions to ensure accurate execution of user-defined tasks. 

2. **Communication Component `rocs-wifi`:** This component ensures that the robot can connect to the network effectively and realize functions such as remote control and data transmission. 

3. **`rocs-control` / `rocs-webots`:** This corresponds to the motion control program in a real or simulation environment, which is the key to specific motion capabilities and behaviors.


Next, we'll guide you through the [quick installation and use of RoCS](quick_start/installation.md)