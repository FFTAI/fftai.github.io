# RoCS Server Installation Guide

## System Requirements

Before proceeding with the RoCS Server installation, ensure that your system meets the following requirements:

* A PC with a minimum dual-core CPU clock speed of 2 GHz and 2 GB of RAM.
* Operating system: Ubuntu Long Term Support (LTS) releases, including versions 22.04 and 20.04.
* An NVIDIA or AMD OpenGL-capable graphics adapter with a minimum version of 3.3 and at least 512 MB of RAM.

## Quick Installation

Use either of the following commands in your terminal to install the server dependencies and RoCS Server binaries:

**Option 1:**

```shell
wget -qO- https://raw.githubusercontent.com/FFTAI/rocs_server/main/install.sh | bash
```

**Option 2:**

```shell
curl -o- https://raw.githubusercontent.com/FFTAI/rocs_server/main/install.sh | bash
```

---

## Running in a simulation environment (Webots)

### I. Downloading Webots

1. Execute script for quick installation

```shell
wget https://github.com/cyberbotics/webots/releases/download/R2023b/webots_2023b_amd64.deb
sudo dpkg -i webots_2023b_amd64.deb
```

2. Alternatively, you can download your preferred desktop distribution from the official website by visiting [cyberbotics](https://www.cyberbotics.com).

### II. Loading Webots model

1. Open Webots
2. `file` -> `open world` -> `～/RoCS/webots/worlds/SonnyV4.wbt`

### III. Controlling Robot using Client SDK

1. Install Client SDK for corresponding language: [Python](https://pypi.org/project/rocs-client) 或 [JavaScript/TypeScript](https://www.npmjs.com/package/rocs-client).
2. You can see the corresponding sample code on the introduction page of SDK, and manipulate it through the SDK sample code

---

## Running on real machines

### I. Modifying Configuration Information

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
