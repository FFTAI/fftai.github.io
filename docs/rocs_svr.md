# rocs_svr Introduction

The `control_svr` of Robotics Control System (RoCS), is the server component responsible for executing the algorithmic control logic within the system. Acting as a crucial element, it handles commands originating from the upper computer, which can be a Control APP user interface or SDK control programs. Its primary function is to process these commands and transmit control instructions to the lower computer using underlying communication protocols. This intricate communication mechanism enables the achievement of precise control over the robot's movements. The `control_svr` essentially serves as the bridge between the upper computer and the lower computer, facilitating the seamless execution of algorithmic control in the RoCS framework.


**control_svr.conf**: The file `control_svr.conf` serves as the configuration file for adjusting parameters related to the algorithmic control program. Within this file, you can customize and fine-tune the behavior of the algorithmic control program to meet the specific requirements of your application.

**Startup Configuration**: By executing the `install_env.sh` script during the initial setup, you can configure the system for the first time. After running this script in a network-connected state, the system will establish three startup items: `rocs_svr`, `rocs_model`, and `rocs_enable_wifi`. Notably, `rocs_svr` corresponds to `control_svr`, ensuring that the algorithm control program server starts automatically with the system to guarantee seamless functionality.

**Manual Operations**: Several manual operation commands are provided, such as starting, stopping, and restarting the algorithm control program server. These commands can be executed using the corresponding `systemctl` commands to manually manage the state of the algorithmic control program.
