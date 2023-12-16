# RoCS Server Installation Guide


## System Environment

* A PC  with at least a 2 GHz dual core CPU clock speed and 2 GB of RAM is a minimum requirement.
* Operating system: Ubuntu Long Term Support (LTS) releases, including versions 22.04 and 20.04.
* An NVIDIA or AMD OpenGL (minimum version 3.3) capable graphics adapter with at least 512 MB of RAM is required.


## Quick installation 

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

### II. Load Webots model 
1. Open Webots
2. `file` -> `open world` -> `～/RoCS/webots/worlds/SonnyV4.wbt`

### III. Control model 
1. Install Client SDK for corresponding language : [Python](https://pypi.org/project/rocs-client/)或[JavaScript/TypeScript]().
2. You can see the corresponding sample code on the introduction page of SDK, and manipulate it through the SDK sample code 

## Running on real machines 

### I. Modifying Configuration Information 
Firstly, we suggest that you carefully read the sbin readme file and modify the corresponding configuration information (which needs to be modified according to the actual situation)
```markdown
/usr/local/bin/rocs-svr/
├── config/                                     Configuration files
│ ├── application.conf                               ***** Configuration file, may need modification
│ ├── human_motor_limit_list.json                    ***** Robot joint limit information
```

### II. Power on, start and experience 

**After completing the above actions, congratulations on completing the installation!**

Now you can start your robot experience through our SDK or Android Apk control program - Fourier GR1!


## Portal

### Documentation
[RoCS platform Doc](http://fftai.github.io/)   
[Python SDK Doc](https://fftai.github.io/rocs_client_py/index.html)  
[javascript SDK Doc](https://fftai.github.io/rocs_client_js/index.html)  

### Control App
[Fourier GR1.apk](https://github.com/FFTAI/rocs_app/releases/download/v1.1/ROCS-App-1.1.30.apk)
