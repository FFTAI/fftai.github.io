# Welcome to RoCS Server API documentation


# Robot

> v1.0.0

Base URLs:

* <a href="http://127.0.0.1:8001">Development environment: http://127.0.0.1:8001</a>

# Robot

## POST human 

POST /robot/start

Control instruction: The robot returns to the zero interface, entered as {} a json object without any parameters

> Body request parameters

```json
{}
```

###  Request Parameters

|Name|Position|Type|Mandatory|Description|
|---|---|---|---|---|
|body|body|object| No |none|

> Description

> Success

```json
{
  "code": 0,
  "msg": "ok",
  "data": {}
}
```

### Return the result

|Status Code|Status Code Meaning|Description|Data Model|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|success|Inline|

### Return the data structure

Status Code **200**

|Name|Type|Mandatory|Constraints|Name|Description|
|---|---|---|---|---|---|
|» code|integer|true|none||Return Status code|
|» msg|string|true|none||Return information|
|» data|object|true|none||Return data|

## POST human stand

POST /robot/stand

Control instruction: Standing interface, you can choose to input head and body parameters when standing, the default entry is {} a json object without any parameters can be

> Body Request parameter

```json
{}
```

### Request parameters

| Name | Location | Type | Mandatory | Description |
|---|---|---|---|---|
|body|body|object| No |none|
|» body|body|object¦null| Yes |body parameters|
|»» x|body|integer| Yes | Center of gravity X-axis (range:+-0.03)|
|»» y|body|integer| Yes | Center of gravity Y-axis (range:+-0.03)|
|»» z|body|integer| Yes | Center of gravity Z-axis (range:+-0.03)|
|»» a|body|integer| Yes |Lumbar X-axis deviation (range:+-0.04)|
|»» b|body|integer| Yes |Lumbar Y-axis deviation (range:+-0.04)|
|»» c|body|integer| Yes |Lumbar Z-axis deviation (range:+-0.03)|
|» head|body|object¦null| Yes |head parameter|
|»» a|body|integer| Yes |Head X axis, left and right tilt (range:+-0.03)|
|»» b|body|integer| Yes |Head Y axis, left and right tilt (range:+-0.03)|
|»» c|body|integer| Yes |Head Z axis, left and right tilt (range:+-0.03)|

> Return example

> Success

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

### Return the result

|Status Code|Status Code Meaning| Description |Data Model|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Success|Inline|

### Return data structure

Status Code **200**

|Name|Type|Mandatory|Restriction|Description|
|---|---|---|---|---|---|
|» code|integer|true|none||Return status code 0-Success、1-error|
|» msg|string|true|none||Return exception message|
|» data|object|true|none||Return data|



## Get the state of the joint when it starts

GET /robot/joint_states

Obtain the status of the robot starting joint

> Body parameter

```json
{}
```

### Request parameters

|Name|Location|Type|Mandatory|Description|
|---|---|---|---|---|
|body|body|object| No |none|

> Return examples

> Successs

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

### Return the result

|Status Code|Status Code Meaning|Description|Data Model|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Success|Inline|

### Return data structure

Status Code **200**

|Name|Type|Mandatory|Constraints|
|---|---|---|---|---|---|
|» code|integer|true|none||response code，0-success，-1-error|
|» msg|string|true|none||response imformation|
|» data|string|true|none||response data|

## GET the range of motion of the robot joint

GET /robot/joint_limit

Robot joint range of motion query

> Return examples

> Success

```json
{
  "code": 0,
  "msg": "ok",
  "data": "{\"data\":{\"jointlimit\":[{\"name\":\"left_hip_roll\",\"qaMax\":0.523598775598299,\"qaMin\":-0.087266462599716,\"qdotaMax\":12.56637061435917,\"tauaMax\":82.5},{\"name\":\"left_hip_yaw\",\"qaMax\":0.392699081698724,\"qaMin\":-0.392699081698724,\"qdotaMax\":12.56637061435917,\"tauaMax\":82.5},{\"name\":\"left_hip_pitch\",\"qaMax\":0.698131700797732,\"qaMin\":-1.221730476396031,\"qdotaMax\":22.441443522143093,\"tauaMax\":200},{\"name\":\"left_knee_pitch\",\"qaMax\":2.094395102393195,\"qaMin\":-0.087266462599716,\"qdotaMax\":22.441443522143093,\"tauaMax\":200},{\"name\":\"left_ankle_pitch\",\"qaMax\":0.349065850398866,\"qaMin\":-0.698131700797732,\"qdotaMax\":17.45678317844728,\"tauaMax\":16.6},{\"name\":\"left_ankle_roll\",\"qaMax\":0.261799387799149,\"qaMin\":-0.261799387799149,\"qdotaMax\":17.45678317844728,\"tauaMax\":16.6},{\"name\":\"right_hip_roll\",\"qaMax\":0.087266462599716,\"qaMin\":-0.523598775598299,\"qdotaMax\":12.56637061435917,\"tauaMax\":82.5},{\"name\":\"right_hip_yaw\",\"qaMax\":0.392699081698724,\"qaMin\":-0.392699081698724,\"qdotaMax\":12.56637061435917,\"tauaMax\":82.5},{\"name\":\"right_hip_pitch\",\"qaMax\":0.698131700797732,\"qaMin\":-1.221730476396031,\"qdotaMax\":22.441443522143093,\"tauaMax\":100},{\"name\":\"right_knee_pitch\",\"qaMax\":2.094395102393195,\"qaMin\":-0.087266462599716,\"qdotaMax\":22.441443522143093,\"tauaMax\":100},{\"name\":\"right_ankle_pitch\",\"qaMax\":0.349065850398866,\"qaMin\":-0.698131700797732,\"qdotaMax\":17.45678317844728,\"tauaMax\":16.6},{\"name\":\"right_ankle_roll\",\"qaMax\":0.261799387799149,\"qaMin\":-0.261799387799149,\"qdotaMax\":17.45678317844728,\"tauaMax\":16.6},{\"name\":\"waist_yaw\",\"qaMax\":3.14,\"qaMin\":-3.14,\"qdotaMax\":5,\"tauaMax\":20},{\"name\":\"waist_pitch\",\"qaMax\":3.14,\"qaMin\":-3.14,\"qdotaMax\":5,\"tauaMax\":20},{\"name\":\"waist_roll\",\"qaMax\":3.14,\"qaMin\":-3.14,\"qdotaMax\":5,\"tauaMax\":20},{\"name\":\"head_yaw\",\"qaMax\":3.14,\"qaMin\":-3.14,\"qdotaMax\":5,\"tauaMax\":20},{\"name\":\"head_pitch\",\"qaMax\":3.14,\"qaMin\":-3.14,\"qdotaMax\":5,\"tauaMax\":20},{\"name\":\"head_roll\",\"qaMax\":3.14,\"qaMin\":-3.14,\"qdotaMax\":5,\"tauaMax\":20}]},\"function\":\"SonnieGetStatesLimit\"}"
}
```

### Return the result

|Status Code|Status Code Meaning|Description|Data Model|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Success|Inline|

### Return data structure

## POST Robot power-off interface

POST /robot/stop

Control commands: Commands take precedence over other commands! The power will stop. Please trigger in case of emergency

> Return example

> Success

```json
{
  "code": 0,
  "msg": "ok",
  "data": {}
}
```

### Return the result

|Status Code|Status Code Meaning|Description|Data Model|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Success|Inline|

### Return data structure

 Status Code **200**

|ame|Type|Mandatory|Restriction|Description|
|---|---|---|---|---|---|
|» code|integer|true|none||response code，0-success，-1-error|
|» msg|string|true|none||response information|
|» data|string|false|none||response information|

## GET Get the robot category

GET /robot/type

> Return to example

> Success

```json
{
  "code": 0,
  "msg": "ok",
  "data": "human"
}
```

### Return the result

|Status Code|Status Code Meaning|Description|Data Model|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Success|Inline|

### Return data structure

Status Code **200**

|Name|Type|Mandatory|Restriction|Description|
|---|---|---|---|---|---|
|» code|integer|true|none||response code，0-success，-1-error|
|» msg|string|true|none||response code|
|» data|string|false|none||response code|

## GET Enables real-time monitoring of the robot

GET /robot/enable_states_listen

Turn on robot status monitoring

### Request parameters

|Name|Location|Type|Mandatory|Description|
|---|---|---|---|---|
|frequence|query|integer| No |Listening frequency frequence indicates the number of status updates received per second|

> Return examples

> Successs

```json
{
  "code": 0,
  "msg": "ok",
  "data": {}
}
```

### Return the result

|Status Code|Status Code Meaning|Description|Data Model|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|success|Inline|

### Return data structure

Status Code **200**

|Name|Type|Mandatory|Restriction|Description|
|---|---|---|---|---|---|
|» code|integer|true|none||response code，0-success，-1-error|
|» msg|string|true|none||response imformation|
|» data|string|false|none||response imformation|

## GET Turn off the monitoring robot real-time status

GET /robot/disable_states_listen

> Return examples

> Successs

```json
{
  "code": 0,
  "msg": "ok",
  "data": {}
}
```

### Return the result

|Status Code|Status Code Meaning|Description|Data Model|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|success|Inline|

### Return data structure

Status Code **200**

|Name|Type|Mandatory|Restriction|Description|
|---|---|---|---|---|---|
|» code|integer|true|none||response code，0-success，-1-error|
|» msg|string|true|none||response imformation|
|» data|string|false|none||response imformation|

## GET Whether the camera can be turned on

GET /control/camera_status

> Return examples

> Successs

```json
{
  "code": 0,
  "msg": "ok",
  "data": true
}
```

### Return the result

|Status Code|Status Code Meaning|Description|Data Model|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|success|Inline|

### Return data structure

Status Code **200**

|Name|Type|Mandatory|Restriction|Description|
|---|---|---|---|---|---|
|» code|integer|true|none||response code，0-success，-1-error|
|» msg|string|true|none||response imformation|
|» data|boolean|true|none||true- The camera can be turned on. false- The camera cannot be turned on|

## GET Get camera data

GET /control/camera

Obtain camera data, response format for streaming data, front end with``<img src="http://127.0.0.1:8001/control/camera" width="50%">``receiving display

> Return examples

> 200 Response

```json
{}
```

### Return the result

|Status Code|Status Code Meaning|Description|Data Model|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|success|Inline|

### Return data structure

## websocket move order

URL:
>ws://127.0.0.1:8001/ws

Control instruction: The websocket long connection sends the move instruction

> Body request parameters


```json
{
  "command": "move",
  "data": {
    "angle": 0,
    "speed": 0.1
  }
}
```

### Request parameters

|Name|Location|Type|Mandatory|Description|
|---|---|---|---|---|
|body|body|object| No |none|
|» command|body|string| Yes |1 head motion 2 move|
|» data|body|object| Yes |none|
|»» speed|body|number| Yes |Before and after the speed control, the value ranges from plus to minus 0.8. Forward is positive, backward is negative! (floating point number 8 bits)|
|»» angle|body|number| Yes |Angle Control direction. The value ranges from plus to minus 45 degrees. Left is positive, right is negative! (floating point number 8 bits)|

#### enumerated value

|Stats|Value|
|---|---|
|» command|head|
|» command|move|

> Return examples

> 200 Response

```json
{}
```

### Return the result

|Status Code|Status Code Meaning|Description|Data Model|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|success|Inline|

### Return data structure

## websocket head command

URL:
>ws /127.0.0.1:8001/ws

Control instruction: websocket long connection sends header instruction

> Body Request parameters

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

### Request parameters

|Name|Location|Type|Mandatory|Description|
|---|---|---|---|---|
|body|body|object| No |none|
|» command|body|string| Yes |head|
|» data|body|object| Yes |none|
|»» roll|body|number| Yes |roll: Describes the Angle of rotation around the X-axis, negative for left heads, positive for right, range (-17.1887-17.1887)|
|»» pitch|body|number| Yes |pitch: Describes the Angle of rotation around the Y-axis. The front nod is positive, the back nod is negative, the range is (-17.1887-17.1887)|
|»» yaw|body|number| Yes |yaw: Describes the Angle of rotation around the z axis. The left torsion head is negative, the right torsion head is positive, and the range is (-17.1887-17.1887)|

#### enumerated value

|Stats|Value|
|---|---|
|» command|head|
|» command|move|

> Return examples

> 200 Response

```json
{}
```

### Return the result

|Status Code|Status Code Meaning|Description|Data Model|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|success|Inline|

### Return data structure

## websocket gets real-time status

URL:
>ws://127.0.0.1:8001/ws

websocket long connection listening to obtain real-time status

> Return examples

> Successs

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

### Return the result

|Status Code|Status Code Meaning|Description|Data Model|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|success|Inline|

### Return data structure

Status Code **200**

|Name|Location|Type|Mandatory|Description|
|---|---|---|---|---|
|» data|object|true|none||none|
|»» states|object|true|none||none|
|»»» basestate|object|true|none||Robot state data|
|»»»» a|number|true|none||hip roll|
|»»»» b|number|true|none||hip Pitch|
|»»»» c|number|true|none||hip Yaw|
|»»»» va|number|true|none||not use|
|»»»» vb|number|true|none||not use|
|»»»» vc|number|true|none||not use|
|»»»» vx|number|true|none||Speed in the forward direction, in m/s|
|»»»» vy|number|true|none||Velocity in the left and right directions, in m/s|
|»»»» vz|number|true|none||not use|
|»»»» x|number|true|none||base  X，X position when standing|
|»»»» y|number|true|none||base  Y，Y position when standing|
|»»»» z|number|true|none||base  Z，Z position when standing|
|»»» contactforce|object|true|none||contact force data not use|
|»»»» fxL|number|true|none||Left foot contact force|
|»»»» fxR|number|true|none||Left foot contact force|
|»»»» fyL|number|true|none||Left foot contact force|
|»»»» fyR|number|true|none||Left foot contact force|
|»»»» fzL|number|true|none||Left foot contact force|
|»»»» fzR|number|true|none||Left foot contact force|
|»»»» mxL|number|true|none||Left foot contact force|
|»»»» mxR|number|true|none||Left foot contact force|
|»»»» myL|number|true|none||Left foot contact force|
|»»»» myR|number|true|none||Left foot contact force|
|»»»» mzL|number|true|none||Left foot contact force|
|»»»» mzR|number|true|none||Left foot contact force|
|»»» fsmstatename|object|true|none||Data about the state of the state machine|
|»»»» currentstatus|string|true|none||Current state Unknown、Start、Zero、Stand、Walk、Stop|
|»»» jointStates|[object]|true|none||Joint status list|
|»»»» name|string|true|none||Joint name|
|»»»» qa|number|true|none||Actual joint Angle, unit: rad|
|»»»» qc|number|true|none||Desired joint velocity in rad|
|»»»» qdota|number|true|none||Real joint velocity in rad/s (radians per second)|
|»»»» qdotc|number|true|none||Desired joint velocity in rad/s (radians per second)|
|»»»» taua|number|true|none||Real torque, unit :n\*m|
|»»»» tauc|number|true|none||Desired joint torque, unit:n\*m|
|»»» stanceindex|object|true|none||Attitude index not use|
|»» timestamp|object|true|none||none|
|»»» nanos|integer|true|none||none|
|»»» seconds|string|true|none||none|
|» function|string|true|none||SonnieGetStates|

# Data model

