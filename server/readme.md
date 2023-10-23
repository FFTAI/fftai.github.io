# Server API
![logo.jpg](../pics/logo.jpg)

## Project Introduction

The purpose of this document is to introduce the function and usage of the interface provided by the server API of the robot. By reading this document, you can learn how to use API tools such as PostMan or ApiFox and Http tools to send Http requests to control the basic behavior of the robot.

## Hardware Preparation

* Fourier GR-1 robot
* The PC that sends the control commands
* Provide a router on the same LAN

## Software Preparation

* PC Install the SSH link tool on the PC
* PC Install the interface test tool, such as PostMan or ApiFox, on a computer
* For code-only operations, install the Http and WebSocket tool packages

## Operation Procedure

* Connect to the same LAN with the robot via wifi
* The SSH tool links the bot and starts the underlying and back-end server programs
* Use the telnet command on your PC to verify that port 8001 of the robot is open
* Starts the back-end API application

## Detailed ApI Documentation

* [server_api](server_api.md)

## Curl Example