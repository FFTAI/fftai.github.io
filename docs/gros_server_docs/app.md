# app package

## Submodules

## app.api module

### *async* app.api.camera()

打开摄像头

Args:

> - None

Returns:

> - type (StreamingResponse): io流数据

### *async* app.api.camera_open()

摄像头是否可以打开

Args:

> - None

Returns:

> - type (bool): True-可以打开，False-不可以打开

### *async* app.api.get_type()

获取设备类型

Args:

> - None

Returns:

> - type (str): 机器人类别

### *async* app.api.human_enable_states_listen()

关闭state

Args:

> - None

Returns:

> - result(Dict):
>   > - code (int): 返回码，0-表示成功，-1-表示失败
>   > - msg (str): 返回消息，ok表示正常，失败返回错误信息
>   > - data (dict): 数据对象，包含具体数据

### *async* app.api.human_stand()

人形站立

Args:

> - None

Returns:

> - result(Dict):
>   > - code (int): 返回码，0-表示成功，-1-表示失败
>   > - msg (str): 返回消息，ok表示正常，失败返回错误信息
>   > - data (dict): 数据对象，包含具体数据

### *async* app.api.human_state_limit()

获取机器人关节可活动范围

Args:

> - None

Returns:

> - result(Dict):
>   > - code (int): 返回码，0-表示成功，-1-表示失败
>   > - msg (str): 返回消息，ok表示正常，失败返回错误信息
>   > - data (dict): 数据对象，包含具体数据
>   >   > - data (list): 关节限制列表，每个元素是一个字典
>   >   >   > - name (str): 关节名称
>   >   >   > - qdotaMax (float): 关节最大速度，单位：rad/s
>   >   >   > - qaMax (float): 关节最大弧度，单位：rad
>   >   >   > - qaMin (float): 关节最小角度，单位：rad
>   >   >   > - tauaMax (float): 最大扭矩，单位：n\*m
>   >   > - function (str): 函数名称

Example:

> ```json
> {
>     "code": 0,
>     "msg": "ok",
>     "data": {
>         "data": {
>             "jointlimit": [
>                 {
>                     "name": "left_hip_roll",
>                     "qaMax": 0.523598775598299,
>                     "qaMin": -0.087266462599716,
>                     "qdotaMax": 12.56637061435917,
>                     "tauaMax": 82.5
>                 },
>                 {
>                     "name": "left_hip_yaw",
>                     "qaMax": 0.392699081698724,
>                     "qaMin": -0.392699081698724,
>                     "qdotaMax": 12.56637061435917,
>                     "tauaMax": 82.5
>                 },
>                 {
>                     "name": "left_hip_pitch",
>                     "qaMax": 0.698131700797732,
>                     "qaMin": -1.221730476396031,
>                     "qdotaMax": 22.441443522143093,
>                     "tauaMax": 200
>                 },
>                 {
>                     "name": "left_knee_pitch",
>                     "qaMax": 2.094395102393195,
>                     "qaMin": -0.087266462599716,
>                     "qdotaMax": 22.441443522143093,
>                     "tauaMax": 200
>                 }
>             ]
>         },
>         "function": "SonnieGetStatesLimit"
>     }
> }
> ```

### *async* app.api.human_system_states()

获取关节状态

Args:

> - None

Returns:

> - result(Dict):
>   > - code (int): 状态码，0 表示正常，-1 表示异常
>   > - msg (str): 状态信息，”ok” 表示正常
>   > - data (dict): 响应数据，包含以下字段：
>   >   > - data (dict): 状态数据，包含以下字段：
>   >   >   > - bodyandlegstate (dict): 身体和腿部状态，包含以下字段：
>   >   >   >   > - currentstatus (str): 当前状态，”StartComplete” 表示启动完成
>   >   >   >   > - log (dict): 日志信息，包含以下字段：
>   >   >   >   >   > - logBuffer (list): 日志缓冲区，包含以下字段：
>   >   >   >   >   >   > - log (str): 日志内容，”GRPC system state response init complete” 表示 GRPC 系统状态响应初始化完成
>   >   >   > - leftarmstate (dict): 左侧手臂状态，包含以下字段：
>   >   >   >   > - armstatus (str): 手臂状态，”Swing” 表示摆臂模式
>   >   >   > - rightarmstate (dict): 右侧手臂状态，包含以下字段：
>   >   >   >   > - armstatus (str): 手臂状态，”Swing” 表示摆臂模式
>   >   > - function (str): 调用该接口的函数名，”SonnieGetSystemStates” 表示获取系统状态接口

Example:

```json
{
    "code": 0,
    "msg": "ok",
    "data": {
        "data": {
            "bodyandlegstate": {
                "currentstatus": "StartComplete",
                "log": {
                    "logBuffer": [
                        {
                            "log": "GRPC system state response init complete"
                        }
                    ]
                }
            },
            "leftarmstate": {
                "armstatus": "Swing"
            },
            "rightarmstate": {
                "armstatus": "Swing"
            }
        },
        "function": "SonnieGetSystemStates"
    }
}
```

### *async* app.api.robot_start()

设备启动

Args:

> - None

Returns:

> - result(Dict):
>   > - code (int): 返回码，0-表示成功，-1-表示失败
>   > - msg (str): 返回消息，ok表示正常，失败返回错误信息
>   > - data (dict): 数据对象，包含具体数据

### *async* app.api.robot_stop()

停止

`该命令优先于其他命令! 会掉电停止。请在紧急情况下触发`

Args:

> - None

Returns:

> - result(Dict):
>   > - code (int): 返回码，0-表示成功，-1-表示失败
>   > - msg (str): 返回消息，ok表示正常，失败返回错误信息
>   > - data (dict): 数据对象，包含具体数据

### *async* app.api.socket_endpoint(ws: WebSocket)

socket 处理器

Args:
: ws(WebSocket):  websocket 对象

### *async* app.api.socket_handle(ws: WebSocket, message_json: dict[str, any])

### *async* app.api.validate_receive(msg_text: str)

## app.api_param module

## app.apis module

## app.device_hub module

### *class* app.device_hub.DeviceHub

Bases: `object`

#### *property* camera*: [Camera](robotics.common.md#robotics.common.camera.Camera)*

#### *property* network*: [Network](system.md#system.network.Network)*

#### *property* robot*: [Robotic](robotics.base.md#robotics.base.robotic.Robotic)*

#### *property* system*: [System](system.md#system.system.System)*

## app.run module

### app.run.main()

## app.strategy_context module

## app.websocket_schema module

## Module contents
