# Server API
![logo.jpg](pics/logo.jpg)

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

## PostMan Example (Since PostMan does not support Websocket, it only shows Http operations)

* Download and install the PostMan tools, website to download address: https://www.postman.com/downloads/
* Open PostMan
* Enter http://[robot IP]:8001/robot/type in the URL field
* Click Send to receive the response data in Json format returned by the server API
* If you call the control command interface such as /robot/start, /robot/stand, etc., you can see that the real or simulated robot responds
![postMan.jpg](pics/down_postman.png)
![postMan.jpg](https://github.com/FFTAI/fftai.github.io/blob/Architecture/docs/server_api/pics/api%20send1.jpg)

## Apifox Specific example

* Go to the Apifox website and download it at https://apifox.com/
* Open Apifox and go to the sample project
* Http interface operation
* Create a new interface
* URL Enter http://[robot IP]:8001/robot/type, and enter the interface name
* Enter the format and parameter content of the interface entry, and save the interface
* Send the request and view the response data
* If you call the control command interface such as /robot/start, /robot/stand, etc., you can see the action of the real or simulated robot to respond
* webocket interface operation
* Add a Websocket interface
* Enter the URL and parameters
* Save interface
    * Click the link button to create a long connection
    * Send request message data
    * If you call the control command interface such as /robot/start, /robot/stand, etc., you can see the action of the real or simulated robot to respond
