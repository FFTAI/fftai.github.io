# rocs_svr Introduction

The `rocs_svr` essentially serves as the bridge between the upper computer and the lower computer. It handles commands originating from the upper computer, which can be a Control APP user interface or SDK control programs. Its primary function is to process these commands and transmit control instructions to the lower computer using underlying communication protocols. This intricate communication mechanism enables the achievement of precise control over the robot's movements. 

**Startup Configuration**: By executing the `install_env.sh` script during the initial setup, you can configure the system for the first time. After running this script in a network-connected state, the system will establish three startup items: `rocs_svr`, `rocs_model`, and `rocs_enable_wifi`. 

**Manual Operations**: Several manual operation commands are provided, such as starting, stopping, and restarting the `rocs_svr` service. These commands can be executed using the corresponding `systemctl` commands to manually manage the status of `rocs_svr`.
