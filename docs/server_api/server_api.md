# 欢迎来到 GROS 服务器 API 文档


# Robot

> v1.0.0

Base URLs:

* <a href="http://127.0.0.1:8001">开发环境: http://127.0.0.1:8001</a>

# Robot

## POST human回零

POST /robot/start

机器人回零接口，入参为{}一个没有任何参数的json对象

> Body 请求参数

```json
{}
```

### 请求参数

|名称|位置|类型|必选|说明|
|---|---|---|---|---|
|body|body|object| 否 |none|

> 返回示例

> 成功

```json
{
  "code": 0,
  "msg": "ok",
  "data": {}
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» code|integer|true|none||返回状态码|
|» msg|string|true|none||返回信息|
|» data|object|true|none||返回数据|

## POST human站立

POST /robot/stand

站立接口，站立时可以选择输入head和身体body参数，默认入参为{}一个没有任何参数的json对象即可

> Body 请求参数

```json
{}
```

### 请求参数

|名称|位置|类型|必选|说明|
|---|---|---|---|---|
|body|body|object| 否 |none|
|» body|body|object¦null| 是 |body参数|
|»» x|body|integer| 是 |重心x轴（范围:+-0.03）|
|»» y|body|integer| 是 |重心y轴（范围:+-0.03）|
|»» z|body|integer| 是 |重心z轴（范围:+-0.03）|
|»» a|body|integer| 是 |腰部x轴偏向（范围:+-0.04）|
|»» b|body|integer| 是 |腰部y轴偏向（范围:+-0.04）|
|»» c|body|integer| 是 |腰部z轴偏向（范围:+-0.03）|
|» head|body|object¦null| 是 |head参数|
|»» a|body|integer| 是 |头部x轴、左右倾斜（范围:+-0.03）|
|»» b|body|integer| 是 |头部y轴、前后倾斜（范围:+-0.03）|
|»» c|body|integer| 是 |头部z轴、直立旋转（范围:+-0.03）|

> 返回示例

> 成功

```json
{
  "code": 0,
  "msg": "ok",
  "data": {}
}
```

```json
{
  "code": -1,
  "msg": {
    "head": [
      {
        "a": [
          "max value is 0.03"
        ]
      }
    ]
  },
  "data": {}
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» code|integer|true|none||返回状态码0-正常、1-异常|
|» msg|string|true|none||返回异常信息|
|» data|object|true|none||返回数据|



## GET 获取关节启动时状态

GET /robot/joint_states

获取机器人启动关节状态

> Body 请求参数

```json
{}
```

### 请求参数

|名称|位置|类型|必选|说明|
|---|---|---|---|---|
|body|body|object| 否 |none|

> 返回示例

> 成功

```json
null
```

```json
{
  "code": 0,
  "msg": "ok",
  "data": "{\"data\":{\"bodyandlegstate\":{\"currentstatus\":\"StartComplete\",\"log\":{\"logBuffer\":[{\"log\":\"GRPC system state response init complete\"}]}},\"leftarmstate\":{\"armstatus\":\"Swing\"},\"rightarmstate\":{\"armstatus\":\"Swing\"}},\"function\":\"SonnieGetSystemStates\"}"
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» code|integer|true|none||响应码0-成功，-1-失败|
|» msg|string|true|none||响应信息|
|» data|string|true|none||响应数据|

## GET 获取机器人关节可活动范围

GET /robot/joint_limit

机器人关节活动范围查询

> 返回示例

> 成功

```json
{
  "code": 0,
  "msg": "ok",
  "data": "{\"data\":{\"jointlimit\":[{\"name\":\"left_hip_roll\",\"qaMax\":0.523598775598299,\"qaMin\":-0.087266462599716,\"qdotaMax\":12.56637061435917,\"tauaMax\":82.5},{\"name\":\"left_hip_yaw\",\"qaMax\":0.392699081698724,\"qaMin\":-0.392699081698724,\"qdotaMax\":12.56637061435917,\"tauaMax\":82.5},{\"name\":\"left_hip_pitch\",\"qaMax\":0.698131700797732,\"qaMin\":-1.221730476396031,\"qdotaMax\":22.441443522143093,\"tauaMax\":200},{\"name\":\"left_knee_pitch\",\"qaMax\":2.094395102393195,\"qaMin\":-0.087266462599716,\"qdotaMax\":22.441443522143093,\"tauaMax\":200},{\"name\":\"left_ankle_pitch\",\"qaMax\":0.349065850398866,\"qaMin\":-0.698131700797732,\"qdotaMax\":17.45678317844728,\"tauaMax\":16.6},{\"name\":\"left_ankle_roll\",\"qaMax\":0.261799387799149,\"qaMin\":-0.261799387799149,\"qdotaMax\":17.45678317844728,\"tauaMax\":16.6},{\"name\":\"right_hip_roll\",\"qaMax\":0.087266462599716,\"qaMin\":-0.523598775598299,\"qdotaMax\":12.56637061435917,\"tauaMax\":82.5},{\"name\":\"right_hip_yaw\",\"qaMax\":0.392699081698724,\"qaMin\":-0.392699081698724,\"qdotaMax\":12.56637061435917,\"tauaMax\":82.5},{\"name\":\"right_hip_pitch\",\"qaMax\":0.698131700797732,\"qaMin\":-1.221730476396031,\"qdotaMax\":22.441443522143093,\"tauaMax\":100},{\"name\":\"right_knee_pitch\",\"qaMax\":2.094395102393195,\"qaMin\":-0.087266462599716,\"qdotaMax\":22.441443522143093,\"tauaMax\":100},{\"name\":\"right_ankle_pitch\",\"qaMax\":0.349065850398866,\"qaMin\":-0.698131700797732,\"qdotaMax\":17.45678317844728,\"tauaMax\":16.6},{\"name\":\"right_ankle_roll\",\"qaMax\":0.261799387799149,\"qaMin\":-0.261799387799149,\"qdotaMax\":17.45678317844728,\"tauaMax\":16.6},{\"name\":\"waist_yaw\",\"qaMax\":3.14,\"qaMin\":-3.14,\"qdotaMax\":5,\"tauaMax\":20},{\"name\":\"waist_pitch\",\"qaMax\":3.14,\"qaMin\":-3.14,\"qdotaMax\":5,\"tauaMax\":20},{\"name\":\"waist_roll\",\"qaMax\":3.14,\"qaMin\":-3.14,\"qdotaMax\":5,\"tauaMax\":20},{\"name\":\"head_yaw\",\"qaMax\":3.14,\"qaMin\":-3.14,\"qdotaMax\":5,\"tauaMax\":20},{\"name\":\"head_pitch\",\"qaMax\":3.14,\"qaMin\":-3.14,\"qdotaMax\":5,\"tauaMax\":20},{\"name\":\"head_roll\",\"qaMax\":3.14,\"qaMin\":-3.14,\"qdotaMax\":5,\"tauaMax\":20}]},\"function\":\"SonnieGetStatesLimit\"}"
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|Inline|

### 返回数据结构

## POST 机器人断电接口

POST /robot/stop

命令优先于其他命令! 会掉电停止。请在紧急情况下触发

> 返回示例

> 成功

```json
{
  "code": 0,
  "msg": "ok",
  "data": {}
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» code|integer|true|none||响应码，0-正常，-1-异常|
|» msg|string|true|none||响应信息|
|» data|string|false|none||响应信息|

## GET 获取机器人类别

GET /robot/type

> 返回示例

> 成功

```json
{
  "code": 0,
  "msg": "ok",
  "data": "human"
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» code|integer|true|none||响应码，0-正常，-1-异常|
|» msg|string|true|none||响应信息|
|» data|string|false|none||响应信息|

## GET 开启监听机器人实时状态

GET /robot/enable_states_listen

开启机器人状态监听

### 请求参数

|名称|位置|类型|必选|说明|
|---|---|---|---|---|
|frequence|query|integer| 否 |监听频率，frequence对应一秒接收状态更新次数|

> 返回示例

> 成功

```json
{
  "code": 0,
  "msg": "ok",
  "data": {}
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» code|integer|true|none||响应码，0-正常，-1-异常|
|» msg|string|true|none||响应信息|
|» data|string|false|none||响应信息|

## GET 关闭监听机器人实时状态

GET /robot/disable_states_listen

> 返回示例

> 成功

```json
{
  "code": 0,
  "msg": "ok",
  "data": {}
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» code|integer|true|none||响应码，0-正常，-1-异常|
|» msg|string|true|none||响应信息|
|» data|string|false|none||响应信息|

## GET 摄像头是否可以打开

GET /control/camera_status

> 返回示例

> 成功

```json
{
  "code": 0,
  "msg": "ok",
  "data": true
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» code|integer|true|none||响应码，0-正常，-1-异常|
|» msg|string|true|none||响应信息|
|» data|boolean|true|none||true-可以打开摄像头，false-不可以打开|

## GET 获取摄像头数据

GET /control/camera

获取摄像头数据，响应格式为流式数据，前端用``<img src="http://127.0.0.1:8001/control/camera" width="50%">``接收展示

> 返回示例

> 200 Response

```json
{}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|Inline|

### 返回数据结构

## websocket move指令

URL:
>ws://127.0.0.1:8001/ws

websocket长连接发送move指令

> Body 请求参数

```json
{
  "command": "move",
  "data": {
    "angle": 0,
    "speed": 0.1
  }
}
```

### 请求参数

|名称|位置|类型|必选|说明|
|---|---|---|---|---|
|body|body|object| 否 |none|
|» command|body|string| 是 |1、head-头运动、2-move行走指令|
|» data|body|object| 是 |none|
|»» speed|body|number| 是 |速度 控制前后，取值范围为正负0.8。向前为正，向后为负！(浮点数8位)|
|»» angle|body|number| 是 |角度 控制方向，取值范围为正负45度。向左为正，向右为负！(浮点数8位)|

#### 枚举值

|属性|值|
|---|---|
|» command|head|
|» command|move|

> 返回示例

> 200 Response

```json
{}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|Inline|

### 返回数据结构

## websocket head指令

URL:
>ws /127.0.0.1:8001/ws

websocket长连接发送头部指令

> Body 请求参数

```json
{
  "command": "head",
  "data": {
    "roll": 0,
    "pitch": 0,
    "yaw": 0
  }
}
```

### 请求参数

|名称|位置|类型|必选|说明|
|---|---|---|---|---|
|body|body|object| 否 |none|
|» command|body|string| 是 |head|
|» data|body|object| 是 |none|
|»» roll|body|number| 是 |roll（翻滚角）：描述围绕x轴旋转的角度，左转头为负，向右转为正，范围（-17.1887-17.1887）|
|»» pitch|body|number| 是 |pitch（俯仰角）：描述围绕y轴旋转的角度。前点头为正，后点头为负，范围（-17.1887-17.1887）|
|»» yaw|body|number| 是 |yaw（偏航角）：描述围绕z轴旋转的角度。左扭头为负，右扭头为正，范围（-17.1887-17.1887）|

#### 枚举值

|属性|值|
|---|---|
|» command|head|
|» command|move|

> 返回示例

> 200 Response

```json
{}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|Inline|

### 返回数据结构

## websocket 获取实时状态

URL:
>ws://127.0.0.1:8001/ws

websocket长连接监听获取实时状态

> 返回示例

> 成功

```json
{
  "data": {
    "states": {
      "basestate": {
        "a": -0.00008816774229518624,
        "b": -0.0031777816310660225,
        "c": 0,
        "va": -3.2955695877132928e-9,
        "vb": -6.542262024864478e-7,
        "vc": 2.0403557796187137e-8,
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
          "qdota": -1.2811068419807387e-8,
          "qdotc": -2.5650460977039418e-9,
          "taua": 0.00000421397498061693,
          "tauc": 0.00000421397498061693
        },
        {
          "name": "left_hip_yaw",
          "qa": 1.1561011056000388e-7,
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
          "qdotc": -1.3400628221563268e-7,
          "taua": -0.000004188456587918816,
          "tauc": -0.000004188456587918816
        },
        {
          "name": "left_ankle_pitch",
          "qa": 0.0000515945298803933,
          "qc": 2.2981673142499233e-8,
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
          "qa": 0.0000028389355052439438,
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
          "qa": 0.000045113585488131827,
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
          "qdotc": -1.4486023522267124e-7,
          "taua": -0.00000557281564261239,
          "tauc": -0.00000557281564261239
        },
        {
          "name": "right_ankle_pitch",
          "qa": 0.00005468652781599774,
          "qc": 2.4630029782206444e-8,
          "qdota": 2.3684484798495585e-7,
          "qdotc": -2.2533190930925486e-7,
          "taua": -7.817536142908408e-8,
          "tauc": -7.817536142908408e-8
        },
        {
          "name": "right_ankle_roll",
          "qa": -1.4411157156501986e-7,
          "qc": 8.786951464767337e-11,
          "qdota": -6.347293532005193e-10,
          "qdotc": -6.275949957243541e-9,
          "taua": 5.977234519649814e-11,
          "tauc": 5.977234519649814e-11
        },
        {
          "name": "waist_yaw",
          "qa": 2.7287197903010756e-10,
          "qc": -1.9509172839224988e-10,
          "qdota": 2.182983232727597e-7,
          "qdotc": -1.5630533392766102e-7,
          "taua": -0.000003249343357926737,
          "tauc": -0.0000017639729379187397
        },
        {
          "name": "waist_pitch",
          "qa": -1.1411541437762108e-8,
          "qc": -5.783273072262379e-9,
          "qdota": -5.121972652033971e-13,
          "qdotc": 3.810219915783962e-8,
          "taua": 0.000011505459672511686,
          "tauc": 0.000005496170595926694
        },
        {
          "name": "waist_roll",
          "qa": -1.302909426086466e-8,
          "qc": -6.480917136286735e-9,
          "qdota": -3.6044103175709823e-13,
          "qdotc": -4.3982596326637837e-10,
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

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» data|object|true|none||none|
|»» states|object|true|none||none|
|»»» basestate|object|true|none||机器人状态数据|
|»»»» a|number|true|none||hip roll|
|»»»» b|number|true|none||hip Pitch|
|»»»» c|number|true|none||hip Yaw|
|»»»» va|number|true|none||not use|
|»»»» vb|number|true|none||not use|
|»»»» vc|number|true|none||not use|
|»»»» vx|number|true|none||前进方向速度，单位m/s|
|»»»» vy|number|true|none||左右方向速度，单位m/s|
|»»»» vz|number|true|none||not use|
|»»»» x|number|true|none||base  X，站立时X位置|
|»»»» y|number|true|none||base  Y，站立时Y位置|
|»»»» z|number|true|none||base  Z，站立时Z位置|
|»»» contactforce|object|true|none||接触力数据 not use|
|»»»» fxL|number|true|none||左脚接触力|
|»»»» fxR|number|true|none||左脚接触力|
|»»»» fyL|number|true|none||左脚接触力|
|»»»» fyR|number|true|none||左脚接触力|
|»»»» fzL|number|true|none||左脚接触力|
|»»»» fzR|number|true|none||左脚接触力|
|»»»» mxL|number|true|none||左脚接触力|
|»»»» mxR|number|true|none||左脚接触力|
|»»»» myL|number|true|none||左脚接触力|
|»»»» myR|number|true|none||左脚接触力|
|»»»» mzL|number|true|none||左脚接触力|
|»»»» mzR|number|true|none||左脚接触力|
|»»» fsmstatename|object|true|none||有关状态机状态的数据|
|»»»» currentstatus|string|true|none||当前状态 Unknown、Start、Zero、Stand、Walk、Stop|
|»»» jointStates|[object]|true|none||关节状态列表|
|»»»» name|string|true|none||关节名称|
|»»»» qa|number|true|none||真实的关节角度，单位：rad（弧度）|
|»»»» qc|number|true|none||期望的关节速度，单位：rad|
|»»»» qdota|number|true|none||真实的关节速度，单位：rad/s（弧度/秒）|
|»»»» qdotc|number|true|none||期望的关节速度，单位：rad/s（弧度/秒）|
|»»»» taua|number|true|none||真实的扭矩，单位:n\*m|
|»»»» tauc|number|true|none||期望的关节扭矩，单位：unit:n\*m|
|»»» stanceindex|object|true|none||姿态索引 not use|
|»» timestamp|object|true|none||none|
|»»» nanos|integer|true|none||none|
|»»» seconds|string|true|none||none|
|» function|string|true|none||SonnieGetStates|

# 数据模型

