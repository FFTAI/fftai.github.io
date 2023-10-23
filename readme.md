# Robot Control System (RoCS)

In general, our softwares are divided into two parts: the upper computer and the lower computer.
* The lower computer is like the cerebellum in humans, mainly responsible for motion control related tasks such as motor driving, motion algorithms, hardware drivers, etc.
* The upper computer mainly focuses on data transmission and a small amount of logic applications. For example, receiving and playing sound, video stream transmission, sending instructions, receiving status, etc.

The **Robot Control System** is responsible for the overall monitoring and remote control functions of the robot. It is divided into three layers:
**Control App** (user graphic application), **Client SDK** (client interface), **Server API** (server interface).

* **Server API** runs on the robot and is a thin data forwarding layer. It uses `http` and `websocket` protocols to forward external commands to the lower computer and various data from the robot to the outside. Although it runs inside the robot, this layer is also part of the upper computer. It is the interface between the lower computer and the outside world. Because this time it is just a forwarding layer, and considering efficiency and other users' security, it has not been open-sourced.
* **Client SDK** can use any tool (as long as it supports `http` and `websocket` protocols) to access the **Server API**. But for developers' convenience, we provide the **Client SDK**, which encapsulates the **Server API**, providing a more friendly interface. Developers can directly use the corresponding language's **Client SDK** to develop their own applications. This layer is open-source.
* **Control App** runs on terminals outside of the robot body (computers or mobile phones) and is a user graphic application. The purpose of the **Control App** is not to provide a complete consumer-oriented application, but to make all functions into a comprehensive example for developers' reference. Developers can refer to the code of the **Control App** to develop their own applications. This layer is also open-source.

All upper computer software together is called `RoCS`, which stands for:
**Ro**bot **C**ontrol **S**ystem

![](pics/logo.jpg)  

---
![](rocs_com.png)

## Contents
[About GR-1](contents/about_gr_1.md)  
[Quick Start](contents/quick_start.md)  
[Software Architecture](contents/soft_arc.md)  
[Remote Application](contents/app/readme.md)  
[Autonomous Control](contents/auto_ctrl.md)  
[Embody](contents/embody.md)  
[Motion Library](contents/motion_lib.md)  

## SDKs
[Javascript SDK](https://github.com/FFTAI/rocs_client_js/blob/main/README.md)   
[Python SDK](https://github.com/FFTAI/rocs_client_py/blob/main/README.md)  

## Server
[Server API](server/readme.md)  

## Release Notes
[v1.1 notes](release/v1.1.md)  
[v0.2 notes](release/v0.2.md)  
[v0.1 notes](release/v0.1.md)  
