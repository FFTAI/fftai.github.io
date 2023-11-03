
# RoCS Server Installation Guide

**In a Virtual Environment (Webots)**

To set up the RoCS (Robotics Control System) server in a virtual environment using Webots, follow these steps:

## Downloading Webots

1. Download Webots 2023b from the official website at [https://www.cyberbotics.com/](https://www.cyberbotics.com/).
2. Save the downloaded Webots file to the `rocs_server/` folder.
3. Rename the Webots file to `webots_2023b_amd64.deb` if it has a different name.

## Downloading RoCS Binary

1. Download the `bin.zip` and `lib.zip` files from the [RoCS server release page](https://github.com/FFTAI/rocs_server/releases/tag/v1.1.0).
2. Unzip the downloaded files into the `rocs_server/` folder.
3. Ensure that your directory structure matches the following:

```
rocs_server/
├── bin/
│   ├── joystick/
│   ├── sdk/
│   └── webots/
├── lib/
│   ├── eigen/
│   ├── qpOASES/
│   └── rbdl/
├── install_RoCS.sh
├── README.md (this file)
└── webots_2023b_amd64.deb
```

## Installing the Server Environments and Dependencies

Open your terminal and run the following command:

```shell
sh install_RoCS.sh
```

## Starting the RoCS Server

### 1. Load Webots Model

1. Launch Webots.
2. Navigate to `File` -> `Open World`.
3. Select the world file located at `rocs_server/bin/webots/webotsim/worlds/SonnyV4.wbt`.

### 2. Start the RoCS Server

In your terminal, run the following command:

```
sh start_RoCS_server_sdk.sh
```

## Using the Remote App

To operate RoCS with a Remote App, adhere to these instructions:

1. **Download the Remote App**: On your Windows computer, obtain the Remote App from [this link](https://github.com/FFTAI/gros_app/releases).

2. **Installation**: Double-click the downloaded file to install and launch the Remote App.

## Joystick Control

Directly control RoCS using an Xbox Joystick. Connect the Joystick to your computer via USB and execute the following command in your terminal:

```shell
sh start_RoCS_server_jotstick.sh
```
