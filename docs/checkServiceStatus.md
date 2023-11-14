# Verifying and Manual Control of RoCS Services after Installation

## Verfiying Services Effectiveness

After completing the installation, verify whether the automatic startup of the three services is working properly. If all three are actively running, everything is functioning as expected.

### Verifying `rocs_enable_wifi` Service

```shell
sudo systemctl status rocs_enable_wifi.service
```

### Verifying `rocs_svr` Service

```shell
sudo systemctl status rocs_svr.service
```

### Verifying `rocs_model` Service

```shell
sudo systemctl status rocs_model.service
```

## Manual Start

Manually initiate the RoCS services if needed:

### Manual Start `rocs_enable_wifi` Service

```shell
sudo systemctl start rocs_enable_wifi.service
```

### Manual Start `rocs_svr` Service

```shell
sudo systemctl start rocs_svr.service
```

### Manual Start `rocs_model` Service

```shell
sudo systemctl start rocs_model.service
```

## Manual Stop

Manually stop the RoCS services if necessary:

### Manual Stop `rocs_enable_wifi` Service

```shell
sudo systemctl stop rocs_enable_wifi.service
```

### Manual Stop `rocs_svr` Service

```shell
sudo systemctl stop rocs_svr.service
```

### Manual Stop `rocs_model` Service

```shell
sudo systemctl stop rocs_model.service
```

## View Logs

Monitor the system logs for RoCS-related entries:

```shell
sudo tail -f /var/log/syslog | grep rocs
```

## Directory `sbin` Introduction

```shell
RoCS/
├── config/                  Configuration files
│ ├── cluster_master_wifi.conf   ***** Cluster mode master control WiFi information
│ ├── control_svr.conf           ***** Configuration related to algorithm control program
│ ├── password.conf              ***** Host password! Script requires sudo password, configure here
│ ├── wifi.conf                  ***** WiFi information, modify according to machine serial number
│ ├── wifi.conf.default          Default configuration for WiFi information, can be restored to default later
│ ├── human_motor_limit_list.json Humanoid robot motor limit collection
│ ├── robot.conf                 Robot configuration file, generally no need to modify, change IP if algorithm control program and software control program are on different computers
├── lib/                     Dependencies, library files, etc.
│ ├── create_ap                  Library for creating an access point
├── script/                  Script files (executed through rocs_svr)
│ ├── reboot.sh                  Reboot
│ ├── shutdown.sh                Shutdown
│ ├── sdk_ctrl_start.sh          Start algorithm control program
│ ├── sdk_ctrl_close.sh          Close algorithm control program
│ ├── sdk_ctrl_status.sh         Check algorithm control program status
│ ├── sdk_ctrl_log_view.sh       View algorithm control program logs
├── setup/                   Scripts for setting up auto-start
│ ├── setup_rocs_model.sh
│ ├── setup_rocs_svr.sh
│ ├── setup_wifi.sh
├── static/                  Static resources, store rocs software 3D model files after packaging
│ ├── index.html
├── install.sh               Environment installation script
├── rocs_svr                 Binary file for rocs software control program server
├── rocs_model               Binary file for rocs software 3D model HTTP access
├── start_up_rocs_model.sh   Script to start rocs_model
├── start_up_rocs_svr.sh     Script to start rocs_svr
├── start_up_wifi.sh         Enable access point, access point information can be modified through wifi.conf in the config directory
└── README.md (this file)
```
