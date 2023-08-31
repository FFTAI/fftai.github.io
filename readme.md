# 机器人遥控系统 GROS

![](pics/gr1half.png)

`机器人遥控系统`负责机器人的整体遥控功能。分为三个部分：`控制App`（用户图形应用），`前端`（客户端接口），`后端`（服务器接口）。`控制App`运行在终端上（电脑或手机）是用户图形应用，通过集成`前端`访问`后端`。`后端`运行在机器人上，负责转发机器人的运动命令和传感器数据等。拓扑图如下：  
![](pics/v0.1_1.png)


## 后端
[后端api文档](https://fftai-gros.github.io/doc-svr/index.html)  

## 前端
[javascript版代码](https://github.com/FFTAI/gros_client_js)  
[javascript版文档](https://fftai-gros.github.io/doc-js/classes/Robot.html)  
[python版代码](https://github.com/FFTAI/gros_client_py)

## 控制App
[代码](https://github.com/FFTAI/gros_app)  


## 历史版本
[v0.1 发布描述](v0.1.md)