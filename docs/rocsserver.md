# RoCS Server Reference Guide

## **System Requirements**

* A PC  with at least a 2 GHz dual core CPU clock speed and 2 GB of RAM is a minimum requirement.
* Operating system: Ubuntu Long Term Support (LTS) releases, including versions 22.04 and 20.04.
* An NVIDIA or AMD OpenGL (minimum version 3.3) capable graphics adapter with at least 512 MB of RAM is required.

## Installation

The RoCS server can be installed fully automatically via bash script. You can download the bach script either using `curl` or `wget`.

### Script for RoCS Server Installation using `curl`

```
curl -o- <https://raw.githubusercontent.com/FFTAI/rocs_server/v1.3.0/install.sh> | bash
```

This script utilizes `curl` to download and execute the installation script for the "rocs_server" from a specific GitHub repository and version (v1.3.0).

* **curl**: Command-line tool for making HTTP requests. It's used here to download content from a URL.
* **-o-**: Option instructs curl to write the downloaded content to standard output (usually the console).
* [https://raw.githubusercontent.com/FFTAI/rocs_server/v1.3.0/install.sh](https://raw.githubusercontent.com/FFTAI/rocs_server/v1.3.0/install.sh): URL of the installation script on GitHub. curl fetches the content from this URL.
* **|**: Pipe operator. It takes the output (script content fetched by curl) and passes it as input to the next command.
* **bash**: Command that executes the content received from curl as a Bash script. It essentially runs the installation script.

### Script for RoCS Server Installation using `wget`

```
wget -qO- <https://raw.githubusercontent.com/FFTAI/rocs_server/v1.3.0/install.sh> | bash
```

This command uses `wget` to download and execute the installation script for the "rocs_server" from a specific GitHub repository and version (v1.3.0).

* **wget:** A command-line utility for non-interactive downloading of files from the web.
* **-qO-:** Options for `wget`.

  * `-q:` Quiet mode, which suppresses output.
  * `-O-:` Specifies where to write the downloaded content; `-` indicates standard output.
* **[https://raw.githubusercontent.com/FFTAI/rocs_server/v1.3.0/install.sh](https://raw.githubusercontent.com/FFTAI/rocs_server/v1.3.0/install.sh):** URL of the installation script on GitHub. `wget` fetches the content from this URL.
* **|:** Pipe operator. It takes the output (script content fetched by `wget`) and passes it as input to the next command.
* **bash:** Command that executes the content received from `wget` as a Bash script. It essentially runs the installation script.

### Introduction to the Installation Script `install.sh`

```

# !/bin/bash

set -e

git clone -b v1.3.0 [https://github.com/FFTAI/rocs_server.git](https://github.com/FFTAI/rocs_server.git) ~/.rocs_server1.3.0

cd ~/.rocs_server1.3.0/lib
sh install.sh

cd ~/.rocs_server1.3.0
rm -rf ./bin*
wget [https://github.com/FFTAI/rocs_server/releases/download/v1.3.0/bin.zip](https://github.com/FFTAI/rocs_server/releases/download/v1.3.0/bin.zip)
unzip bin.zip

cd ~/.rocs_server1.3.0
rm -rf ./sbin*
wget [https://github.com/FFTAI/rocs_server/releases/download/v1.3.0/sbin.zip](https://github.com/FFTAI/rocs_server/releases/download/v1.3.0/sbin.zip)
unzip sbin.zip

```

This Bash script performs the following actions:

1. **Clone repository:** It clones the `rocs_server` repository from GitHub, specifically the `v1.3.0` branch, into the `~/.rocs_server1.3.0` directory in your home folder.
2. **Install dependencies:** It navigates to the `.rocs_server1.3.0/lib` directory and executes the `install.sh` script. This script handles the installation of dependencies and other necessary setup tasks.
3. **Download and extract bin.zip:** It returns to the `.rocs_server1.3.0` directory, removes all files and directories starting with `bin`, and then uses `wget` to download a compressed file named `bin.zip`. Finally, it extracts the contents of `bin.zip`.
4. **Download and extract sbin.zip:** Similarly, it returns to the `.rocs_server1.3.0` directory, removes all files and directories starting with `sbin`, and uses `wget` to download a compressed file named `sbin.zip`. It then extracts the contents of `sbin.zip`.

The `set -e` at the beginning ensures that the script exits immediately if any command returns a non-zero exit status, indicating an error during execution. This helps to detect and respond to errors promptly during script execution.

### Introduction to the `lib` folder

The lib folder includes three libraries which are installed via the auto bash script `install.sh` under the lib folder.

This script automates the process of updating system packages, installing necessary development tools and libraries, setting up a working path, building, and installing specific libraries (eigen, qpOASES, rbdl), and configuring the system to recognize the newly installed libraries:

```
sudo apt update -y
sudo apt upgrade -y
sudo apt --fix-broken install -y
sudo apt install cmake -y
sudo apt install libeigen3-dev -y
sudo apt install build-essential -y
sudo apt install cmake-curses-gui -y
sudo apt install libunittest++-dev -y
sudo apt install qtbase5-dev -y

WORK_PATH=$(pwd)
echo "current_file: $WORK_PATH/$FILE_NAME"
echo "   WORK_PATH: $WORK_PATH"

sudo rm -rf $WORK_PATH/eigen/build
mkdir -p $WORK_PATH/eigen/build
cd $WORK_PATH/eigen/build
cmake ..
make
sudo make install
sudo rm -rf $WORK_PATH/eigen/build

sudo rm -rf $WORK_PATH/qpOASES/build
mkdir -p $WORK_PATH/qpOASES/build
cd $WORK_PATH/qpOASES/build
cmake ..
make
sudo make install
sudo rm -rf $WORK_PATH/qpOASES/build

sudo rm -rf $WORK_PATH/rbdl/build
sudo rm -rf /usr/bin/librbdl.*
sudo rm -rf /usr/local/include/rbdl
mkdir -p $WORK_PATH/rbdl/build
cd $WORK_PATH/rbdl/build
cmake ..
make
sudo make install
sudo cp -f librbdl.* /usr/bin/

sudo ldconfig
```
