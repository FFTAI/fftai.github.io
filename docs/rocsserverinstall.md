# RoCS Server Installation Guide

## System Requirements

* A PC  with at least a 2 GHz dual core CPU clock speed and 2 GB of RAM is a minimum requirement.
* Operating system: Ubuntu Long Term Support (LTS) releases, including versions 22.04 and 20.04.
* An NVIDIA or AMD OpenGL (minimum version 3.3) capable graphics adapter with at least 512 MB of RAM is required.

## Installation 

Install the environment information and executable files that ROCS depends on (choose one of two)

```shell
wget -qO- https://raw.githubusercontent.com/FFTAI/rocs_server/main/install.sh | bash
```

```shell
curl -o- https://raw.githubusercontent.com/FFTAI/rocs_server/main/install.sh | bash
```

## Running in a simulation environment (Webots)

### I. Downloading Webots

1. Execute script for quick installation 
```shell
wget https://github.com/cyberbotics/webots/releases/download/R2023b/webots_2023b_amd64.deb

sudo dpkg -i webots_2023b_amd64.deb
```

2. Alternatively, you can visit [cyberbotics](https://www.cyberbotics.com) Download your preferred desktop distribution from the official website 


### II. Launch SDK control program 
```shell
cd ~/.rocs_server/sbin
bash start_up_rocs_svr.sh
```

### III. Load Webots model 
1. Open Webots
2. `file` -> `open world` -> `～/.rocs_server/bin/webots/worlds/SonnyV4.wbt`

### IV. Control model 
1. Install Client SDK for corresponding language : [Python](https://pypi.org/project/rocs-client/)或[JavaScript/TypeScript]().
2. You can see the corresponding sample code on the introduction page of SDK, and manipulate it through the SDK sample code 

## Running on real machines 

### I. Modifying Configuration Information 
Firstly, we suggest that you carefully read the sbin readme file and modify the corresponding configuration information (which needs to be modified according to the actual situation)
```markdown
sbin/
├── config/                                     Configuration files
│ ├── application.conf                               ***** Configuration file, may need modification
│ ├── human_motor_limit_list.json                    ***** Robot joint limit information
```

### II. Compiling and installing the real machine runtime environment
After the execution is completed, your host will add three system services and set them as bootable and rocs_svr, rocs_model, rocs_enable_wifi
```shell
cd sbin
bash install.sh
```

### III. Power on, start and experience 

**After completing the above actions, congratulations on completing the installation!**

Now you can start your robot experience through our SDK or Android Apk control program - Fourier GR1!
