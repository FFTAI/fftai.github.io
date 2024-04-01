# Verifying and Manual Control of RoCS Services after Installation

## Confirming Successful Installation

To confirm the successful installation of RoCS server packages, open a terminal and run the following command to check if RoCS-related packages are installed:

```shell
dpkg -l | grep rocs
```

Following output signifies a successful installation:

```shell
fftai@fftai-rocs-machine:~$ dpkg -l | grep rocs
ii  rocs-control   1.3   all     Provides support and functionality for control algorithms relevant to robotics
ii  rocs-lib          1.0   all     Installs the libraries required by RoCS
ii  rocs-svr         1.3   all     Provides export call services for robot algorithm programs
ii  rocs-webots  1.3   all     Provides a Webots simulation environment model
ii  rocs-wifi        1.0   all      Opens a hotspot for clients to connect to the same network segment as the robot
fftai@fftai-rocs-machine:~$

```

## Verifying Service Effectiveness

After completing the installation, it is essential to verify whether the automatic startup of the following services is functioning correctly.

1. Verify the Status of `rocs-wifi` Service:

```shell
sudo systemctl status rocs-wifi.service
```

2. Verify the Status of `rocs-svr` Service:

```shell
sudo systemctl status rocs-svr.service
```

## Manual Service Control

In certain situations, you may need to manually start or stop RoCS services. Follow the instructions below to perform these actions:

* Manual start the `rocs-wifi` service:

```shell
sudo systemctl start rocs-wifi.service
```

* Manual start the `rocs-svr` service:

```shell
sudo systemctl start rocs_svr.service
```

* Manual stop `rocs-wifi` service:

```shell
sudo systemctl stop rocs-wifi.service
```

* Manual stop `rocs-svr` service:

```shell
sudo systemctl stop rocs-svr.service
```

## View Service Logs

To monitor the logs of RoCS services for troubleshooting or debugging purposes, follow these steps:

* Monitor the log of `rocs-svr`:

```shell
tail -f /var/log/syslog | grep rocs
```

* Monitor the log of `rocs-control`:

```shell
tail -f ~/RoCS/server.log
```
