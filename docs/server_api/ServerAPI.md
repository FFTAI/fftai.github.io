# Robot Server API

## POST Set mode

POST /robot/mode

This API is utilized to set the motion mode of a car robot. It sends a POST request to the "/robot/mode" endpoint with the specified mode value, including 4-wheel,3-wheel, and 2-wheel.

> Body Parameters

```json
{
  "host": "string",
  "port": 0,
  "mode": "string"
}
```

### Params

| Name   | Location | Type   | Required | Description            |
| ------ | -------- | ------ | -------- | ---------------------- |
| body   | body     | object | no       | none                   |
| » host | body     | string | no       | IP of the robot host   |
| » port | body     | number | no       | Port of the robot host |
| » mode | body     | string | no       | Mode to be set         |

> Response Examples

> 200 Response

```json
{}
```

### Responses

| HTTP Status Code | Meaning                                                                    | Description | Data schema |
| ---------------- | -------------------------------------------------------------------------- | ----------- | ----------- |
| 200              | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)                    | Success     | Inline      |
| 500              | [Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1) | Failure     | Inline      |

### Responses Data Schema

## POST Start robot

POST /robot/start

This API, accessible through the endpoint /robot/start, is utilized for initiating the robot. Additionally, it supports homing functionality, and the input parameter for this API is an empty JSON object ({}), signifying the absence of any required parameters.

> Body Parameters

```json
{}
```

### Params

| Name | Location | Type   | Required | Description |
| ---- | -------- | ------ | -------- | ----------- |
| body | body     | object | no       | none        |

> Response Examples

> Success

```json
{
  "code": 0,
  "msg": "ok",
  "data": {}
}
```

### Responses

| HTTP Status Code | Meaning                                                 | Description | Data schema |
| ---------------- | ------------------------------------------------------- | ----------- | ----------- |
| 200              | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | Success     | Inline      |

### Responses Data Schema

HTTP Status Code **200**

| Name   | Type    | Required | Restrictions | Title | description          |
| ------ | ------- | -------- | ------------ | ----- | -------------------- |
| » code | integer | true     | none         |       | Response status code |
| » msg  | string  | true     | none         |       | Response message     |
| » data | object  | true     | none         |       | Response data        |

## GET Get joint limit

GET /robot/joint_limit

This API is utilized to retrieve the joint limits of the robot, including the permissible range of motion for each joint. Understanding these limits is crucial for ensuring the robot's movements stay within safe and operational parameters, preventing potential damage or errors.

> Response Examples

> Success

```json
{
  "code": 0,
  "msg": "ok",
  "data": "{\"data\":{\"jointlimit\":[{\"name\":\"left_hip_roll\",\"qaMax\":0.523598775598299,\"qaMin\":-0.087266462599716,\"qdotaMax\":12.56637061435917,\"tauaMax\":82.5},{\"name\":\"left_hip_yaw\",\"qaMax\":0.392699081698724,\"qaMin\":-0.392699081698724,\"qdotaMax\":12.56637061435917,\"tauaMax\":82.5},{\"name\":\"left_hip_pitch\",\"qaMax\":0.698131700797732,\"qaMin\":-1.221730476396031,\"qdotaMax\":22.441443522143093,\"tauaMax\":200},{\"name\":\"left_knee_pitch\",\"qaMax\":2.094395102393195,\"qaMin\":-0.087266462599716,\"qdotaMax\":22.441443522143093,\"tauaMax\":200},{\"name\":\"left_ankle_pitch\",\"qaMax\":0.349065850398866,\"qaMin\":-0.698131700797732,\"qdotaMax\":17.45678317844728,\"tauaMax\":16.6},{\"name\":\"left_ankle_roll\",\"qaMax\":0.261799387799149,\"qaMin\":-0.261799387799149,\"qdotaMax\":17.45678317844728,\"tauaMax\":16.6},{\"name\":\"right_hip_roll\",\"qaMax\":0.087266462599716,\"qaMin\":-0.523598775598299,\"qdotaMax\":12.56637061435917,\"tauaMax\":82.5},{\"name\":\"right_hip_yaw\",\"qaMax\":0.392699081698724,\"qaMin\":-0.392699081698724,\"qdotaMax\":12.56637061435917,\"tauaMax\":82.5},{\"name\":\"right_hip_pitch\",\"qaMax\":0.698131700797732,\"qaMin\":-1.221730476396031,\"qdotaMax\":22.441443522143093,\"tauaMax\":100},{\"name\":\"right_knee_pitch\",\"qaMax\":2.094395102393195,\"qaMin\":-0.087266462599716,\"qdotaMax\":22.441443522143093,\"tauaMax\":100},{\"name\":\"right_ankle_pitch\",\"qaMax\":0.349065850398866,\"qaMin\":-0.698131700797732,\"qdotaMax\":17.45678317844728,\"tauaMax\":16.6},{\"name\":\"right_ankle_roll\",\"qaMax\":0.261799387799149,\"qaMin\":-0.261799387799149,\"qdotaMax\":17.45678317844728,\"tauaMax\":16.6},{\"name\":\"waist_yaw\",\"qaMax\":3.14,\"qaMin\":-3.14,\"qdotaMax\":5,\"tauaMax\":20},{\"name\":\"waist_pitch\",\"qaMax\":3.14,\"qaMin\":-3.14,\"qdotaMax\":5,\"tauaMax\":20},{\"name\":\"waist_roll\",\"qaMax\":3.14,\"qaMin\":-3.14,\"qdotaMax\":5,\"tauaMax\":20},{\"name\":\"head_yaw\",\"qaMax\":3.14,\"qaMin\":-3.14,\"qdotaMax\":5,\"tauaMax\":20},{\"name\":\"head_pitch\",\"qaMax\":3.14,\"qaMin\":-3.14,\"qdotaMax\":5,\"tauaMax\":20},{\"name\":\"head_roll\",\"qaMax\":3.14,\"qaMin\":-3.14,\"qdotaMax\":5,\"tauaMax\":20}]},\"function\":\"SonnieGetStatesLimit\"}"
}
```

### Responses

| HTTP Status Code | Meaning                                                 | Description | Data schema |
| ---------------- | ------------------------------------------------------- | ----------- | ----------- |
| 200              | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | Success     | Inline      |

### Responses Data Schema

## GET Enable state debugging mode

GET /robot/enable_states_listen

This API is utilized to instruct the robot to actively send periodic state updates. This is beneficial for real-time monitoring. To handle and process the received data, be sure to listen to the 'on_message' function.

### Params

| Name      | Location | Type    | Required | Description                                                                                                            |
| --------- | -------- | ------- | -------- | ---------------------------------------------------------------------------------------------------------------------- |
| frequence | query    | integer | no       | Monitoring frequency, where the value of it corresponds to the number of times status updates are received per second. |

> Response Examples

> Success

```json
{
  "code": 0,
  "msg": "ok",
  "data": {}
}
```

### Responses

| HTTP Status Code | Meaning                                                 | Description | Data schema |
| ---------------- | ------------------------------------------------------- | ----------- | ----------- |
| 200              | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | Success     | Inline      |

### Responses Data Schema

HTTP Status Code **200**

| Name   | Type    | Required | Restrictions | Title | description                                 |
| ------ | ------- | -------- | ------------ | ----- | ------------------------------------------- |
| » code | integer | true     | none         |       | Response code, 0 for normal, -1 for anomaly |
| » msg  | string  | true     | none         |       | Response messages                           |
| » data | string  | false    | none         |       | Response data                               |

## GET Get camera stream data

GET /control/camera

This API is utilized to fetch camera data, where the response is presented in a stream format. The front end renders the stream data using `<img src="http://127.0.0.1:8001/control/camera" width="50%">`.

> Response Examples

> 200 Response

```json
{}
```

### Responses

| HTTP Status Code | Meaning                                                 | Description | Data schema |
| ---------------- | ------------------------------------------------------- | ----------- | ----------- |
| 200              | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | Success     | Inline      |

### Responses Data Schema

## POST Stand

POST /robot/stand

This API is utilized to command the robot to assume a standing posture. Optional parameters such as 'head' and 'body' can be specified. The default input parameter is an empty JSON object ({}), indicating no specific parameters are required.

> Response Examples

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

### Responses

| HTTP Status Code | Meaning                                                 | Description | Data schema |
| ---------------- | ------------------------------------------------------- | ----------- | ----------- |
| 200              | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | Success     | Inline      |

### Responses Data Schema

HTTP Status Code **200**

| Name   | Type    | Required | Restrictions | Title | description                                      |
| ------ | ------- | -------- | ------------ | ----- | ------------------------------------------------ |
| » code | integer | true     | none         |       | Response status code. 0 for normal,1 for anomaly |
| » msg  | string  | true     | none         |       | Response error messages                          |
| » data | object  | true     | none         |       | Response data                                    |

## POST Walk

POST /robot/walk

This API is utilized to control the walking movements of the robot.

> Body Parameters

```json
{
  "velCmd": {
    "va": 1,
    "vb": 0,
    "vc": 0,
    "vx": 0.2,
    "vy": 0,
    "vz": 0
  }
}
```

### Params

| Name     | Location | Type                | Required | Description                                                   |
| -------- | -------- | ------------------- | -------- | ------------------------------------------------------------- |
| body     | body     | object              | no       | none                                                          |
| » velCmd | body     | object              | yes      | Control commands for velocity.                                |
| »» va    | body     | number(double)¦null | yes      | Not used. Do not specify or set to value 0.                   |
| »» vb    | body     | number(double)¦null | yes      | Not used. Do not specify or set to value 0.                   |
| »» vc    | body     | number(double)¦null | yes      | Left-right direction velocity, range: +-0.6, unit: m/s.       |
| »» vx    | body     | number(double)¦null | yes      | Forward-backward direction velocity, range: +-0.8, unit: m/s. |
| »» vy    | body     | number(double)¦null | yes      | Not used.                                                     |
| »» vz    | body     | number(double)¦null | yes      | Not used.                                                     |

> Response Examples

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
    "velCmd": [
      {
        "va": [
          "unallowed value 0.5"
        ]
      }
    ]
  },
  "data": {}
}
```

### Responses

| HTTP Status Code | Meaning                                                 | Description | Data schema |
| ---------------- | ------------------------------------------------------- | ----------- | ----------- |
| 200              | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | Success     | Inline      |

### Responses Data Schema

HTTP Status Code **200**

| Name   | Type    | Required | Restrictions | Title | description                                 |
| ------ | ------- | -------- | ------------ | ----- | ------------------------------------------- |
| » code | integer | true     | none         |       | Response code. 0 for normal, -1 for anomaly |
| » msg  | string  | true     | none         |       | Response messages or error messages         |
| » data | object  | true     | none         |       | Response data                               |

## GET Get joint states

GET /robot/joint_states

This API is utilized to retrieve the current joint states of the robot.This data is essential for monitoring and controlling the robot's articulation in real-time, enabling precise adjustments and ensuring the robot's overall operational status.

> Body Parameters

```json
{}
```

### Params

| Name | Location | Type   | Required | Description |
| ---- | -------- | ------ | -------- | ----------- |
| body | body     | object | no       | none        |

> Response Examples

> Success

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

### Responses

| HTTP Status Code | Meaning                                                 | Description | Data schema |
| ---------------- | ------------------------------------------------------- | ----------- | ----------- |
| 200              | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | Success     | Inline      |

### Responses Data Schema

HTTP Status Code **200**

| Name   | Type    | Required | Restrictions | Title | description                                     |
| ------ | ------- | -------- | ------------ | ----- | ----------------------------------------------- |
| » code | integer | true     | none         |       | Response code, 0 for success and -1 for failure |
| » msg  | string  | true     | none         |       | Response messages                               |
| » data | string  | true     | none         |       | Response data                                   |

## POST Power off robot

POST /robot/stop

This API is utilized to trigger an emergency stop, bringing the robot to an instantaneous and complete halt with power-off. It takes precedence over other commands.  Use this command with caution, as it results in a powered-down state of the robot. Ensure that there are no critical tasks or movements in progress before invoking this command to prevent unexpected behavior.

> Response Examples

> Success

```json
{
  "code": 0,
  "msg": "ok",
  "data": {}
}
```

### Responses

| HTTP Status Code | Meaning                                                 | Description | Data schema |
| ---------------- | ------------------------------------------------------- | ----------- | ----------- |
| 200              | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | Success     | Inline      |

### Responses Data Schema

HTTP Status Code **200**

| Name   | Type    | Required | Restrictions | Title | description                                 |
| ------ | ------- | -------- | ------------ | ----- | ------------------------------------------- |
| » code | integer | true     | none         |       | Response code, 0 for normal, -1 for anomaly |
| » msg  | string  | true     | none         |       | Response messages                           |
| » data | string  | false    | none         |       | Response data                               |

## GET Get robot type

GET /robot/type

This API is utilized to query the type of a robot when working with clusters or multiple robots. By iteratively invoking this function for each robot, you can accurately determine the type of each robot for precise control. A successful return of the message also indicates that the connection to robot is operating smoothly.

> Response Examples

> Success

```json
{
  "code": 0,
  "msg": "ok",
  "data": "human"
}
```

### Responses

| HTTP Status Code | Meaning                                                 | Description | Data schema |
| ---------------- | ------------------------------------------------------- | ----------- | ----------- |
| 200              | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | Success     | Inline      |

### Responses Data Schema

HTTP Status Code **200**

| Name   | Type    | Required | Restrictions | Title | description                                 |
| ------ | ------- | -------- | ------------ | ----- | ------------------------------------------- |
| » code | integer | true     | none         |       | Response code, 0 for normal, -1 for anomaly |
| » msg  | string  | true     | none         |       | Response messages                           |
| » data | string  | false    | none         |       | Response data                               |

## GET Disable state debugging mode

GET /robot/disable_states_listen

This API is utilized to disable state debugging mode. The robot will stop send state updates.

> Response Examples

> Success

```json
{
  "code": 0,
  "msg": "ok",
  "data": {}
}
```

### Responses

| HTTP Status Code | Meaning                                                 | Description | Data schema |
| ---------------- | ------------------------------------------------------- | ----------- | ----------- |
| 200              | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | Success     | Inline      |

### Responses Data Schema

HTTP Status Code **200**

| Name   | Type    | Required | Restrictions | Title | description                                 |
| ------ | ------- | -------- | ------------ | ----- | ------------------------------------------- |
| » code | integer | true     | none         |       | Response code, 0 for normal, -1 for anomaly |
| » msg  | string  | true     | none         |       | Response messages                           |
| » data | string  | false    | none         |       | Response data                               |

## GET Set camera availability

GET /control/camera_status

This API is invoked to configure the availability of the camera. If the response is true, you gain control over the opening and closing of the camera. If the response is false, the camera is not accessible for use.

> Response Examples

> Success

```json
{
  "code": 0,
  "msg": "ok",
  "data": true
}
```

### Responses

| HTTP Status Code | Meaning                                                 | Description | Data schema |
| ---------------- | ------------------------------------------------------- | ----------- | ----------- |
| 200              | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | Success     | Inline      |

### Responses Data Schema

HTTP Status Code **200**

| Name   | Type    | Required | Restrictions | Title | description                                             |
| ------ | ------- | -------- | ------------ | ----- | ------------------------------------------------------- |
| » code | integer | true     | none         |       | Response code, 0 for normal, -1 for anomaly             |
| » msg  | string  | true     | none         |       | Response messages                                       |
| » data | boolean | true     | none         |       | true: camera is available; false: camera is unavailable |

## GET Move head

GET /127.0.0.1:8001/ws/head

This API is utilized to control the movement of the robot's head via a long-lived WebSocket connection.

> Body Parameters

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

### Params

| Name      | Location | Type   | Required | Description                                                                                                                                                  |
| --------- | -------- | ------ | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| body      | body     | object | no       | none                                                                                                                                                         |
| » command | body     | string | yes      | Head movement                                                                                                                                                |
| » data    | body     | object | yes      | none                                                                                                                                                         |
| »» roll   | body     | number | yes      | specifies the rotation around the x-axis. Negative values turn the head to the left, and positive values turn it to the right. Range: -17.1887 to 17.1887.   |
| »» pitch  | body     | number | yes      | specifies the rotation around the y-axis. Positive values tilt the head forward, and negative values tilt it backward. Range: -17.1887 to 17.1887.           |
| »» yaw    | body     | number | yes      | specifies the rotation around the z-axis. Negative values twist the head to the left, and positive values twist it to the right. Range: -17.1887 to 17.1887. |

#### Enum

| Name      | Value |
| --------- | ----- |
| » command | head  |
| » command | move  |

> Response Examples

> 200 Response

```json
{}
```

### Responses

| HTTP Status Code | Meaning                                                 | Description | Data schema |
| ---------------- | ------------------------------------------------------- | ----------- | ----------- |
| 200              | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | Success     | Inline      |

### Responses Data Schema

## GET Get real-time states

GET /127.0.0.1:8001/ws/states

This API is called to get the real-time state data via function `SonnieGetStates`after the debugging mode is enabled.

> Response Examples

> Success

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

### Responses

| HTTP Status Code | Meaning                                                 | Description | Data schema |
| ---------------- | ------------------------------------------------------- | ----------- | ----------- |
| 200              | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | Success     | Inline      |

### Responses Data Schema

HTTP Status Code **200**

| Name               | Type     | Required | Restrictions | Title | Description                                                                                                    |
| ------------------ | -------- | -------- | ------------ | ----- | -------------------------------------------------------------------------------------------------------------- |
| » data             | object   | true     | none         |       | none                                                                                                           |
| »» states          | object   | true     | none         |       | none                                                                                                           |
| »»» basestate      | object   | true     | none         |       | Robot status data                                                                                              |
| »»»» a             | number   | true     | none         |       | Hip roll                                                                                                       |
| »»»» b             | number   | true     | none         |       | Hip Pitch                                                                                                      |
| »»»» c             | number   | true     | none         |       | Hip Yaw                                                                                                        |
| »»»» va            | number   | true     | none         |       | Not used                                                                                                       |
| »»»» vb            | number   | true     | none         |       | Not used                                                                                                       |
| »»»» vc            | number   | true     | none         |       | Not used                                                                                                       |
| »»»» vx            | number   | true     | none         |       | Forward-backward direction velocity, unit: m/s.                                                                |
| »»»» vy            | number   | true     | none         |       | Left-right direction velocity, unit: m/s.                                                                      |
| »»»» vz            | number   | true     | none         |       | Not used                                                                                                       |
| »»»» x             | number   | true     | none         |       | Base X position when standing.                                                                                 |
| »»»» y             | number   | true     | none         |       | Base y position when standing.                                                                                 |
| »»»» z             | number   | true     | none         |       | Base z position when standing.                                                                                 |
| »»» contactforce   | object   | true     | none         |       | Contact force data (not used).                                                                                 |
| »»»» fxL           | number   | true     | none         |       | Force along the X-axis for the left foot                                                                       |
| »»»» fxR           | number   | true     | none         |       | Force along the X-axis for the right foot                                                                      |
| »»»» fyL           | number   | true     | none         |       | Force along the Y-axis for the left foot                                                                       |
| »»»» fyR           | number   | true     | none         |       | Force along the Y-axis for the right foot                                                                      |
| »»»» fzL           | number   | true     | none         |       | Force along the Z-axis for the left foot                                                                       |
| »»»» fzR           | number   | true     | none         |       | Force along the Z-axis for the right foot                                                                      |
| »»»» mxL           | number   | true     | none         |       | Moment (torque) around the X-axis for left foot                                                                |
| »»»» mxR           | number   | true     | none         |       | Moment (torque) around the X-axis for right foot                                                               |
| »»»» myL           | number   | true     | none         |       | Moment (torque) around the Y-axis for left foot                                                                |
| »»»» myR           | number   | true     | none         |       | Moment (torque) around the Y-axis for right foot                                                               |
| »»»» mzL           | number   | true     | none         |       | Moment (torque) around the Z-axis for left foot                                                                |
| »»»» mzR           | number   | true     | none         |       | Moment (torque) around the Z-axis for right foot                                                               |
| »»» fsmstatename   | object   | true     | none         |       | Data related to the state machine status.                                                                      |
| »»»» currentstatus | string   | true     | none         |       | Current status, including Unknown, Start, Zero, Stand, Walk, and Stop                                          |
| »»» jointStates    | [object] | true     | none         |       | Joint state list.                                                                                              |
| »»»» name          | string   | true     | none         |       | Joint name                                                                                                     |
| »»»» qa            | number   | true     | none         |       | Actual joint angle, unit: rad.                                                                                 |
| »»»» qc            | number   | true     | none         |       | Commanded (desired) joint angle, unit: rad.                                                                    |
| »»»» qdota         | number   | true     | none         |       | Actual (measured) joint velocity, unit: rad/s                                                                  |
| »»»» qdotc         | number   | true     | none         |       | Commanded (desired) joint velocity, unit: rad/s                                                                |
| »»»» taua          | number   | true     | none         |       | Actual joint torques, unit: n.m                                                                                |
| »»»» tauc          | number   | true     | none         |       | Commanded (desired) joint torques, unit: n.m                                                                   |
| »»» stanceindex    | object   | true     | none         |       | Pose index (not used).                                                                                         |
| »» timestamp       | object   | true     | none         |       | none                                                                                                           |
| »»» nanos          | integer  | true     | none         |       | none                                                                                                           |
| »»» seconds        | string   | true     | none         |       | none                                                                                                           |
| » function         | string   | true     | none         |       | SonnieGetStates is the name of the function used to obtain the state data after the debugging mode is enabled. |

## POST Move upper body

POST /robot/upper_body

This API is called to control the upper body movements of the robot.

> Body Parameters

```json
{
  "arm_action": "HELLO",
  "hand_action": "H"
}
```

### Params

| Name          | Location | Type   | Required | Description                                                                                                                                                                                          |
| ------------- | -------- | ------ | -------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| body          | body     | object | no       | none                                                                                                                                                                                                 |
| » arm_action  | body     | string | yes      | RESET for resetting, LEFT_ARM_WAVE for waving with the left arm, TWO_ARMS_WAVE for waving with both arms, ARMS_SWING for swinging arms, HELLO for waving hello.                                      |
| » hand_action | body     | string | yes      | HALF_HANDSHAKE for a half handshake, THUMBS_UP for a thumbs-up, OPEN for an open hand, SLIGHTLY_BENT for a slightly bent hand, GRASP for grasping, TREMBLE for trembling, HANDSHAKE for a handshake. |

> Response Examples

> Success

```json
{
  "code": 0,
  "msg": "ok",
  "data": {}
}
```

### Responses

| HTTP Status Code | Meaning                                                 | Description | Data schema |
| ---------------- | ------------------------------------------------------- | ----------- | ----------- |
| 200              | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | Success     | Inline      |

### Responses Data Schema

HTTP Status Code **200**

| Name   | Type    | Required | Restrictions | Title | description                                  |
| ------ | ------- | -------- | ------------ | ----- | -------------------------------------------- |
| » code | integer | true     | none         |       | Response code, 0 for success, -1 for failure |
| » msg  | string  | true     | none         |       | Response messages                            |
| » data | object  | true     | none         |       | Response data                                |

## POST Move lower body

POST /robot/lower_body

This API is called to control the lower body movements of the robot. SQUAT for squatting, ROTATE_WAIST for rotating the waist.

> Body Parameters

```json
{
  "lower_body_mode": "enim amet id Duis"
}
```

### Params

| Name              | Location | Type   | Required | Description                                               |
| ----------------- | -------- | ------ | -------- | --------------------------------------------------------- |
| body              | body     | object | no       | none                                                      |
| » lower_body_mode | body     | string | yes      | SQUAT for squatting, ROTATE_WAIST for rotating the waist. |

> Response Examples

> Success

```json
{
  "code": 0,
  "msg": "ok",
  "data": null
}
```

### Responses

| HTTP Status Code | Meaning                                                 | Description | Data schema |
| ---------------- | ------------------------------------------------------- | ----------- | ----------- |
| 200              | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | Success     | Inline      |

### Responses Data Schema

HTTP Status Code **200**

| Name   | Type    | Required | Restrictions | Title | description                                  |
| ------ | ------- | -------- | ------------ | ----- | -------------------------------------------- |
| » code | integer | true     | none         |       | Response code, 0 for success, -1 for failure |
| » msg  | string  | true     | none         |       | Response messages                            |
| » data | null    | true     | none         |       | Response data                                |

## POST Preset head movement

POST /robot/head_action

This API is utilized to execute predefined head movements, encompassing actions such as turning the head left, right, up, and down.

> Body Parameters

```json
{
  "head_mode": "string"
}
```

### Params

| Name        | Location | Type   | Required | Description |
| ----------- | -------- | ------ | -------- | ----------- |
| body        | body     | object | no       | none        |
| » head_mode | body     | string | yes      | none        |

> Response Examples

> 200 Response

```json
{}
```

### Responses

| HTTP Status Code | Meaning                                                 | Description | Data schema |
| ---------------- | ------------------------------------------------------- | ----------- | ----------- |
| 200              | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | Success     | Inline      |

### Responses Data Schema

# Data Schema
