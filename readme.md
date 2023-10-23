# 机器人控制系统 RoCS

总体来讲，软件系统分为两大部分：上位机 和 下位机。  
* 下位机相当于人类的小脑，主要负责运动控制相关。如电机驱动，运动算法，硬件驱动等。  
* 上位机则重点负责数据传输和少量逻辑应用。比如声音的接受播放，视频流传输，发送指令，接受状态等等。

**机器人控制系统**负责机器人的整体监视遥控功能。分为三个层：
**控制App**（用户图形应用），**前端SDK**（客户端接口），**后端API**（服务器接口）。
* **后端API** 运行在机器人上，是一个很薄的数据转发层，他通过`http`加`websocket`协议，将外界指令转达给下位机，将机器人的各种数据，转发到外部。虽然运行在机器人里，但本层也属于上位机的一部分，它是下位机和外界的接口。因为本次只是一个转发层，且考虑到效率和其他用户的安全性，所以没有开源。
* **前端SDK** 外界可以使用任何工具（只要支持`http`加`websocket`协议）访问**后端API**。但是为了开发者方便，我们提供了**前端SDK**，它是对**后端API**的封装，提供了更加友好的接口，开发者可以直接使用相应语言的**前端SDK**来开发自己的应用。本层是开源的。
* **控制App** 运行在机器人本体以外的终端上（电脑或手机），是用户图形应用。**控制App** 的目的并不是为了提供一个完整的面向消费者的应用，而是将所有功能，做成一个全面的实例，为开发者提供参考。开发者可以参考**控制App**的代码，来开发自己的应用。本层也是开源的。

所有上位机软件在一起，这个整体叫`RoCS`，意思是：
![](pics/logo.jpg)
Robot Control System

---
![](rocs_com.png)

## Contents
[About GR-1]()  
[Networking]()  
[Software Architecture]()  
[Simulation Environment Setup]()  
[Remote Application]()  
[Autonomous Control]()  
[Embody]()  
[Motion Library]()  
## SDKs
[javascript SDK](sdks/sdk_js/readme.md)   
[python SDK](sdks/sdk_py/readme.md)  
## Server
[Server API](docs/server_api/readme.md)
## Release Notes
[v0.1 notes](release/v0.1.md)
[v0.2 notes](release/v0.2.md)
![v1.0 notes](release/v1.1.md)
