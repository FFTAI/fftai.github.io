# src.gros_client.robot package

## Submodules

## src.gros_client.robot.car module

### *class* src.gros_client.robot.car.Car(ssl: bool = False, host: str = '127.0.0.1', port: int = 8001, on_connected: Callable = None, on_message: Callable = None, on_close: Callable = None, on_error: Callable = None)

Bases: [`RobotBase`](#src.gros_client.robot.robot_base.RobotBase)

Car对象

在你需要连接Car的时候，你可以创建一个Car()对象！ 这将会在后台连接到控制系统，并提供对应的控制函数和状态监听！

Args:

> - ssl(bool):  是否开启ssl认证。默认 False
> - host(str):  car的网络IP
> - port(int):  car的控制服务的PORT
> - on_connected(Callable):  该监听将会在car连接成功时触发
> - on_message(Callable): 该监听将会在car发送系统状态时候触发，你可能需要监听该回掉处理你的逻辑
> - on_close(Callable): 该监听将会在car连接关闭时触发
> - on_error(Callable): 该监听将会在car发生错误时触发

#### \_\_init_\_(ssl: bool = False, host: str = '127.0.0.1', port: int = 8001, on_connected: Callable = None, on_message: Callable = None, on_close: Callable = None, on_error: Callable = None)

#### move(angle: float, speed: float)

控制Car行走

`该请求维持了长链接的方式进行发送`

Args:

> - angle(float): 角度 控制方向，取值范围为正负45度。向左为正，向右为负！(浮点数8位)
> - speed(float): 速度 控制前后，取值范围为正负500。向前为正，向后为负！(浮点数8位)

#### set_mode(mod: [Mod](#src.gros_client.robot.car.Mod))

设置小车的模式

完成后小车将在对应模式下运动，包括 4轮 3轮 2轮

Args:

> - mod(Mod): 模式对象定义

### *class* src.gros_client.robot.car.Mod(value, names=None, \*, module=None, qualname=None, type=None, start=1, boundary=None)

Bases: `Enum`

对应car set_mode函数的参数

#### MOD_2_WHEEL *= 'WHEEL_2'*

#### MOD_3_WHEEL *= 'WHEEL_3'*

#### MOD_4_WHEEL *= 'WHEEL_4'*

## src.gros_client.robot.human module

### *class* src.gros_client.robot.human.Human(ssl: bool = False, host: str = '127.0.0.1', port: int = 8001, on_connected: Callable = None, on_message: Callable = None, on_close: Callable = None, on_error: Callable = None)

Bases: [`RobotBase`](#src.gros_client.robot.robot_base.RobotBase)

GR-1人形机器人对象

在你需要连接GR-1人形机器人的时候，你可以创建一个Human()对象！ 这将会在后台连接到人形的控制系统，并提供对应的控制函数和状态监听！

Args:

> - ssl(bool):  是否开启ssl认证。默认 False
> - host(str):  GR-01人形设备的网络IP
> - port(int):  GR-01人形设备的控制服务的PORT
> - on_connected(Callable):  该监听将会在GR-01人形设备连接成功时触发
> - on_message(Callable): 该监听将会在GR-01人形设备发送系统状态时候触发，你可能需要监听该回掉处理你的逻辑
> - on_close(Callable): 该监听将会在GR-01人形设备连接关闭时触发
> - on_error(Callable): 该监听将会在GR-01人形设备发生错误时触发

#### \_\_init_\_(ssl: bool = False, host: str = '127.0.0.1', port: int = 8001, on_connected: Callable = None, on_message: Callable = None, on_close: Callable = None, on_error: Callable = None)

#### disable_debug_state()

关闭state调试模式

#### enable_debug_state(frequence: int = 1)

开启state调试模式

触发该函数将会在后台触发GR-01人形设备主动发送状态值的指令，因此对应的你需要监听on_message函数进行处理

Args:

> frequence(int): 频率

Returns:

> data (dict): 响应数据

> > - log (dict): 日志信息
> >   > - logBuffer (list): 日志缓冲区
> >   >   > - log (str): 日志内容
> > - states (dict): 关节状态数据
> >   > - basestate (dict): 机器人状态数据
> >   >   > - a (float): hip roll
> >   >   > - b (float): hip Pitch
> >   >   > - c (float): hip Yaw
> >   >   > - va (float): not use
> >   >   > - vb (float): not use
> >   >   > - vc (float): not use
> >   >   > - vx (float): 前进方向速度，单位m/s
> >   >   > - vy (float): 左右方向速度，单位m/s
> >   >   > - vz (float): not use
> >   >   > - x (float): base  X，站立时X位置
> >   >   > - y (float): base  Y，站立时Y位置
> >   >   > - z (float): base  Z，站立时Z位置
> >   > - fsmstatename (dict): 有关状态机状态的数据
> >   >   > - currentstatus (str): 当前状态 Unknown、Start、Zero、Stand、Walk、Stop
> >   > - jointStates (list): 关节状态列表
> >   >   > - name (str): 关节名称
> >   >   > - qa (float): 真实的关节角度，单位：rad（弧度）
> >   >   > - qdota (float): 真实的关节速度，单位：rad/s（弧度/秒）
> >   >   > - taua (float): 真实的扭矩，单位:n\*m
> >   >   > - qc (float): 期望的关节速度，单位：rad
> >   >   > - qdotc (float): 期望的关节速度，单位：rad/s（弧度/秒）
> >   >   > - tauc (float): 期望的关节扭矩，单位：unit:n\*m
> >   > - stanceindex (dict): 姿态索引 not use
> >   > - contactforce (dict): 接触力数据 not use
> >   >   > - fxL (float): 左脚接触力
> >   >   > - fyL (float): 左脚接触力
> >   >   > - fzL (float): 左脚接触力
> >   >   > - mxL (float): 左脚接触力
> >   >   > - myL (float): 左脚接触力
> >   >   > - mzL (float): 左脚接触力
> >   >   > - fxR (float): 右脚接触力
> >   >   > - fyR (float): 右脚接触力
> >   >   > - fzR (float): 右脚接触力
> >   >   > - mxR (float): 右脚接触力
> >   >   > - myR (float): 右脚接触力
> >   >   > - mzR (float): 右脚接触力
> > - timestamp (dict): 时间戳
> >   > - nanos (int):
> >   > - seconds (str):

> function (str): 接口名

Example:

```json
{
    "data": {
        "states": {
            "basestate": {
                "a": -0.00008816774229518624,
                "b": -0.0031777816310660227,
                "c": 0,
                "va": -3.2955695877132929e-9,
                "vb": -6.542262024864478e-7,
                "vc": 2.0403557796187139e-8,
                "vx": 0,
                "vy": 0,
                "vz": 0,
                "x": 0,
                "y": 0,
                "z": 0
            },
            "contactforce": {
                "fxL": 0,
                "fxR": 6,
                "fyL": 1,
                "fyR": 7,
                "fzL": 2,
                "fzR": 8,
                "mxL": 3,
                "mxR": 9,
                "myL": 4,
                "myR": 10,
                "mzL": 5,
                "mzR": 11
            },
            "fsmstatename": {
                "currentstatus": "Start"
            },
            "jointStates": [
                {
                    "name": "left_hip_roll",
                    "qa": -0.000002967348844382189,
                    "qc": -4.195799309522971e-9,
                    "qdota": -1.2811068419807388e-8,
                    "qdotc": -2.5650460977039419e-9,
                    "taua": 0.00000421397498061693,
                    "tauc": 0.00000421397498061693
                },
                {
                    "name": "left_hip_yaw",
                    "qa": 1.1561011056000389e-7,
                    "qc": 5.763118985802831e-10,
                    "qdota": 5.413053331490085e-10,
                    "qdotc": -1.998095673038479e-9,
                    "taua": -5.607576848879348e-7,
                    "tauc": -5.607576848879348e-7
                },
                {
                    "name": "left_hip_pitch",
                    "qa": 0.00004391517501779261,
                    "qc": 1.515751869369811e-8,
                    "qdota": 1.9014878092501132e-7,
                    "qdotc": -4.227869290635517e-8,
                    "taua": -0.000007239519592483131,
                    "tauc": -0.000007239519592483131
                },
                {
                    "name": "left_knee_pitch",
                    "qa": 0.00004577103623661791,
                    "qc": 1.825644254205245e-8,
                    "qdota": 1.9871683938840232e-7,
                    "qdotc": -1.3400628221563269e-7,
                    "taua": -0.000004188456587918816,
                    "tauc": -0.000004188456587918816
                },
                {
                    "name": "left_ankle_pitch",
                    "qa": 0.0000515945298803933,
                    "qc": 2.2981673142499234e-8,
                    "qdota": 2.242746827673787e-7,
                    "qdotc": -2.258893072672217e-7,
                    "taua": -7.153918887352573e-8,
                    "tauc": -7.153918887352573e-8
                },
                {
                    "name": "left_ankle_roll",
                    "qa": 6.419495520105573e-7,
                    "qc": 3.706374175342285e-11,
                    "qdota": 2.794181899265958e-9,
                    "qdotc": -5.949285977052194e-9,
                    "taua": 1.093729550329863e-10,
                    "tauc": 1.093729550329863e-10
                },
                {
                    "name": "right_hip_roll",
                    "qa": 0.0000028389355052439439,
                    "qc": 4.865708590789946e-9,
                    "qdota": 1.2246925191446977e-8,
                    "qdotc": -3.962174546204988e-9,
                    "taua": -0.000004837825973754749,
                    "tauc": -0.000004837825973754749
                },
                {
                    "name": "right_hip_yaw",
                    "qa": -4.364693140246345e-7,
                    "qc": 6.000702384094449e-10,
                    "qdota": -1.8497568931031923e-9,
                    "qdotc": -1.7781221204499439e-9,
                    "taua": -5.867529228984824e-7,
                    "tauc": -5.867529228984824e-7
                },
                {
                    "name": "right_hip_pitch",
                    "qa": 0.000045113585488131829,
                    "qc": 2.367752787246051e-8,
                    "qdota": 1.950714297088208e-7,
                    "qdotc": -6.520824184784889e-8,
                    "taua": -0.000011320537478692172,
                    "tauc": -0.000011320537478692172
                },
                {
                    "name": "right_knee_pitch",
                    "qa": 0.0000479437468878189,
                    "qc": 2.324249646390596e-8,
                    "qdota": 2.0757655546078694e-7,
                    "qdotc": -1.4486023522267125e-7,
                    "taua": -0.00000557281564261239,
                    "tauc": -0.00000557281564261239
                },
                {
                    "name": "right_ankle_pitch",
                    "qa": 0.00005468652781599774,
                    "qc": 2.4630029782206445e-8,
                    "qdota": 2.3684484798495586e-7,
                    "qdotc": -2.2533190930925487e-7,
                    "taua": -7.817536142908409e-8,
                    "tauc": -7.817536142908409e-8
                },
                {
                    "name": "right_ankle_roll",
                    "qa": -1.4411157156501987e-7,
                    "qc": 8.786951464767337e-11,
                    "qdota": -6.347293532005193e-10,
                    "qdotc": -6.275949957243541e-9,
                    "taua": 5.977234519649815e-11,
                    "tauc": 5.977234519649815e-11
                },
                {
                    "name": "waist_yaw",
                    "qa": 2.7287197903010758e-10,
                    "qc": -1.9509172839224989e-10,
                    "qdota": 2.182983232727597e-7,
                    "qdotc": -1.5630533392766103e-7,
                    "taua": -0.000003249343357926737,
                    "tauc": -0.0000017639729379187398
                },
                {
                    "name": "waist_pitch",
                    "qa": -1.1411541437762108e-8,
                    "qc": -5.783273072262379e-9,
                    "qdota": -5.121972652033971e-13,
                    "qdotc": 3.810219915783962e-8,
                    "taua": 0.000011505459672511687,
                    "tauc": 0.000005496170595926694
                },
                {
                    "name": "waist_roll",
                    "qa": -1.302909426086466e-8,
                    "qc": -6.480917136286735e-9,
                    "qdota": -3.6044103175709825e-13,
                    "qdotc": -4.3982596326637839e-10,
                    "taua": 0.000013027709577777855,
                    "tauc": 0.000006483935166648911
                },
                {
                    "name": "head_yaw",
                    "qa": 0,
                    "qc": 0,
                    "qdota": 0,
                    "qdotc": 0,
                    "taua": 0,
                    "tauc": 0
                },
                {
                    "name": "head_pitch",
                    "qa": 0,
                    "qc": 0,
                    "qdota": 0,
                    "qdotc": 0,
                    "taua": 0,
                    "tauc": 0
                },
                {
                    "name": "head_roll",
                    "qa": 0,
                    "qc": 0,
                    "qdota": 0,
                    "qdotc": 0,
                    "taua": 0,
                    "tauc": 0
                }
            ],
            "stanceindex": {}
        },
        "timestamp": {
            "nanos": 2,
            "seconds": "1"
        }
    },
    "function": "SonnieGetStates"
}
```

#### get_joint_limit()

获取关节限位
Args:

> None

Returns:

> result(Dict):

> > - code (int): 返回码，0-表示成功，-1-表示失败
> > - msg (str): 返回消息，ok表示正常，失败返回错误信息
> > - data (dict): 数据对象，包含具体数据
> >   > - data (list): 关节限制列表，每个元素是一个字典
> >   >   > - name (str): 关节名称
> >   >   > - qdotaMax (float): 关节最大速度，单位：rad/s
> >   >   > - qaMax (float): 关节最大弧度，单位：rad
> >   >   > - qaMin (float): 关节最小角度，单位：rad
> >   >   > - tauaMax (float): 最大扭矩，单位：n\*m
> >   > - function (str): 函数名称

Example:

```json
{
    "code": 0,
    "msg": "ok",
    "data": {
        "data": {
            "jointlimit": [
                {
                    "name": "left_hip_roll",
                    "qaMax": 0.523598775598299,
                    "qaMin": -0.087266462599716,
                    "qdotaMax": 12.56637061435917,
                    "tauaMax": 82.5
                },
                {
                    "name": "left_hip_yaw",
                    "qaMax": 0.392699081698724,
                    "qaMin": -0.392699081698724,
                    "qdotaMax": 12.56637061435917,
                    "tauaMax": 82.5
                },
                {
                    "name": "left_hip_pitch",
                    "qaMax": 0.698131700797732,
                    "qaMin": -1.221730476396031,
                    "qdotaMax": 22.441443522143093,
                    "tauaMax": 200
                },
                {
                    "name": "left_knee_pitch",
                    "qaMax": 2.094395102393195,
                    "qaMin": -0.087266462599716,
                    "qdotaMax": 22.441443522143093,
                    "tauaMax": 200
                }

            ]
        },
        "function": "SonnieGetStatesLimit"
    }
}
```

#### get_joint_states()

获取关节状态

Returns:

> Dict: 返回数据包含以下字段:

> - code (int): 状态码，0 表示正常，-1 表示异常
> - msg (str): 状态信息，”ok” 表示正常
> - data (dict): 响应数据，包含以下字段：
>   > - data (dict): 状态数据，包含以下字段：
>   >   > - bodyandlegstate (dict): 身体和腿部状态，包含以下字段：
>   >   >   > - currentstatus (str): 当前状态，”StartComplete” 表示启动完成
>   >   >   > - log (dict): 日志信息，包含以下字段：
>   >   >   >   > - logBuffer (list): 日志缓冲区，包含以下字段：
>   >   >   >   >   > - log (str): 日志内容，”GRPC system state response init complete” 表示 GRPC 系统状态响应初始化完成
>   >   > - leftarmstate (dict): 左侧手臂状态，包含以下字段：
>   >   >   > - armstatus (str): 手臂状态，”Swing” 表示摆臂模式
>   >   > - rightarmstate (dict): 右侧手臂状态，包含以下字段：
>   >   >   > - armstatus (str): 手臂状态，”Swing” 表示摆臂模式
>   > - function (str): 调用该接口的函数名，”SonnieGetSystemStates” 表示获取系统状态接口

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

#### head(roll: float, pitch: float, yaw: float)

控制GR-01人形头部运动

`该请求维持了长链接的方式进行发送`

Args:

> - roll(float): roll（翻滚角）：描述围绕x轴旋转的角度，左转头为负，向右转为正，范围（-17.1887-17.1887）
> - pitch(float): pitch（俯仰角）：描述围绕y轴旋转的角度。前点头为正，后点头为负，范围（-17.1887-17.1887）
> - yaw(float): yaw（偏航角）：描述围绕z轴旋转的角度。左扭头为负，右扭头为正，范围（-17.1887-17.1887）

#### stand()

GR-01人形设备将会原地站立

当进行了start之后如果你想对GR-01人形设备进行指令控制，你同样需要调用该函数让其位置stand的模式。如果是在行走过程中需要停止，你同样可以调用该函数进行stand

Returns:

> result(Dict): return一个结果集 {code: 0, msg: ‘ok’}  or  {code: -1, msg: $ERR_MSG}

#### walk(angle: float, speed: float)

控制GR-01人形设备行走

`该请求维持了长链接的方式进行发送`

Args:

> - angle(float): 角度 控制方向，取值范围为正负45度。向左为正，向右为负！(浮点数8位)
> - speed(float): 速度 控制前后，取值范围为正负0.8。向前为正，向后为负！(浮点数8位)

## src.gros_client.robot.robot_base module

### *class* src.gros_client.robot.robot_base.RobotBase(ssl: bool = False, host: str = '127.0.0.1', port: int = 8001, on_connected: Callable = None, on_message: Callable = None, on_close: Callable = None, on_error: Callable = None)

Bases: `object`

Robot 基类

实例化的时候会通过websocket连接到对应设备的控制端口！

#### \_\_init_\_(ssl: bool = False, host: str = '127.0.0.1', port: int = 8001, on_connected: Callable = None, on_message: Callable = None, on_close: Callable = None, on_error: Callable = None)

#### exit()

端口Robot链接

#### start()

启动 : 重置/归零/对设备初始状态的校准/

当你想要控制Robot设备的时候，你的第一个指令

#### stop()

停止

`该命令优先于其他命令! 会掉电停止。请在紧急情况下触发`

## Module contents
