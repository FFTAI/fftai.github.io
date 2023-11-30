# About RoCS Server Introduction

## rocs_svr


The `rocs_svr` essentially serves as the bridge between the upper computer and the lower computer. It handles commands originating from the upper computer, which can be a Control APP user interface or SDK control programs. Its primary function is to process these commands and transmit control instructions to the lower computer using underlying communication protocols. This intricate communication mechanism enables the achievement of precise control over the robot's movements.


**Startup Configuration**: By executing the `install_env.sh` script during the initial setup, you can configure the system for the first time. After running this script in a network-connected state, the system will establish three startup items: `rocs_svr`, `rocs_model`, and `rocs_enable_wifi`.


**Manual Operations**: Several manual operation commands are provided, such as starting, stopping, and restarting the `rocs_svr` service. These commands can be executed using the corresponding `systemctl` commands to manually manage the status of `rocs_svr`.


## rocs_model


The `rocs_model` serves as a crucial component within the RoCS system, specializing in the external synchronization of 3D robot model information. Its primary function is to meticulously replicate the robot's coordinates and position, delivering a visually appealing user interface through the HTTP service.


Within the `rocs_model`, real-time position coordinate data is continuously monitored via remote monitoring. This information is then utilized to render the model through a websocket, a high-performance real-time communication method. This dynamic interaction serves as a valuable resource for developers, offering an intuitive insight into the current state of the robot and significantly enhancing control and monitoring efficiency.


Throughout the development process, `rocs_model` assumes a pivotal role by facilitating the implementation of the robot's visual representation. This includes external features and structural aspects, providing developers with a comprehensive understanding of the robot's status, movement, and task execution.


The `RoCS_model` is a vital tool for developers in robotics, offering profound insights into the robot's appearance and structure. This enhances the development process by providing a valuable visual representation for monitoring and understanding the robot's behavior and functionality.


## rocs_enable_wifi


`rocs_enable_wifi` is a crucial component within the RoCS system, tasked with managing and configuring the robot's Wi-Fi connection. Here's a detailed overview of its functionalities:


**Wi-Fi Connection Management:** The primary role of `rocs_enable_wifi` is to oversee the robot's Wi-Fi connection, encompassing the configuration and activation of Wi-Fi functionality. Through this component, users can set wireless network parameters, ensuring the robot can seamlessly connect to the specified Wi-Fi network.


**Hotspot Functionality Activation:** In addition to connecting to external Wi-Fi networks, `rocs_enable_wifi` also supports activating hotspot functionality. This means the robot can establish an independent Wi-Fi hotspot, allowing other devices to connect to the robot, facilitating local data transfer and control.


**Flexibility and Customization:** Through the configuration file `wifi.conf`, users can flexibly adjust Wi-Fi information based on the robot's serial number, adapting to different usage scenarios and network environments. This provides a level of customization, allowing users to fine-tune Wi-Fi settings according to specific requirements.


`rocs_enable_wifi` plays a pivotal role in the RoCS system, ensuring the robot can effectively connect to the network and achieve functionalities such as remote control and data transmission.


