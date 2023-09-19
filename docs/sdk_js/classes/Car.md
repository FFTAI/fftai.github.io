[gros-client](../readme.md) / [Exports](../modules.md) / Car

# Class: Car

Car对象

在你需要连接Car的时候，你可以创建一个new Car()对象！ 这将会在后台连接到控制系统，并提供对应的控制函数和状态监听！

## Hierarchy

- `RobotBase`

  ↳ **`Car`**

## Table of contents

### Constructors

- [constructor](Car.md#constructor)

### Properties

- [camera](Car.md#camera)
- [system](Car.md#system)

### Methods

- [move](Car.md#move)
- [on\_close](Car.md#on_close)
- [on\_connected](Car.md#on_connected)
- [on\_error](Car.md#on_error)
- [on\_message](Car.md#on_message)
- [set\_mode](Car.md#set_mode)
- [start](Car.md#start)
- [stop](Car.md#stop)

## Constructors

### constructor

• **new Car**(`option?`)

#### Parameters

| Name | Type |
| :------ | :------ |
| `option?` | `ConnectOption` |

#### Overrides

RobotBase.constructor

#### Defined in

[lib/robot/car.ts:28](https://github.com/FFTAI/gros_client_js/blob/bc9e358/lib/robot/car.ts#L28)

## Properties

### camera

• `Readonly` **camera**: `undefined` \| [`Camera`](Camera.md)

相机

#### Inherited from

RobotBase.camera

#### Defined in

[lib/robot/robot_base.ts:34](https://github.com/FFTAI/gros_client_js/blob/bc9e358/lib/robot/robot_base.ts#L34)

___

### system

• `Readonly` **system**: [`System`](System.md)

系统控制

#### Inherited from

RobotBase.system

#### Defined in

[lib/robot/robot_base.ts:38](https://github.com/FFTAI/gros_client_js/blob/bc9e358/lib/robot/robot_base.ts#L38)

## Methods

### move

▸ **move**(`angle`, `speed`): `void`

控制Car移动 (该请求维持了长链接的方式进行发送)

#### Parameters

| Name | Type | Description |
| :------ | :------ | :------ |
| `angle` | `number` | 角度 控制方向，取值范围为正负45度。向左为正，向右为负！(浮点数8位) |
| `speed` | `number` | 速度 控制前后，取值范围为正负500。向前为正，向后为负！(浮点数8位) |

#### Returns

`void`

#### Defined in

[lib/robot/car.ts:59](https://github.com/FFTAI/gros_client_js/blob/bc9e358/lib/robot/car.ts#L59)

___

### on\_close

▸ **on_close**(`listener`): `void`

event: 该监听将会在Robot设备连接关闭时触发

#### Parameters

| Name | Type | Description |
| :------ | :------ | :------ |
| `listener` | () => `void` | 无参回调，你可以再次进行资源回收等类似的操作 |

#### Returns

`void`

#### Inherited from

RobotBase.on\_close

#### Defined in

[lib/robot/robot_base.ts:134](https://github.com/FFTAI/gros_client_js/blob/bc9e358/lib/robot/robot_base.ts#L134)

___

### on\_connected

▸ **on_connected**(`listener`): `void`

event : 该监听将会在Robot设备连接成功时触发

#### Parameters

| Name | Type | Description |
| :------ | :------ | :------ |
| `listener` | () => `void` | 无参回调, 你可以在确认后执行你的业务逻辑 |

#### Returns

`void`

#### Inherited from

RobotBase.on\_connected

#### Defined in

[lib/robot/robot_base.ts:125](https://github.com/FFTAI/gros_client_js/blob/bc9e358/lib/robot/robot_base.ts#L125)

___

### on\_error

▸ **on_error**(`listener`): `void`

event: 该监听将会在Robot设备发送错误时触发

#### Parameters

| Name | Type | Description |
| :------ | :------ | :------ |
| `listener` | (`err`: `Error`) => `void` | 会将错误信息回调 |

#### Returns

`void`

#### Inherited from

RobotBase.on\_error

#### Defined in

[lib/robot/robot_base.ts:143](https://github.com/FFTAI/gros_client_js/blob/bc9e358/lib/robot/robot_base.ts#L143)

___

### on\_message

▸ **on_message**(`listener`): `void`

该监听将会在Robot设备主动广播消息时触发

#### Parameters

| Name | Type | Description |
| :------ | :------ | :------ |
| `listener` | (`data`: `any`) => `void` | ，你可能需要监听该回调处理你的逻辑 |

#### Returns

`void`

#### Inherited from

RobotBase.on\_message

#### Defined in

[lib/robot/robot_base.ts:152](https://github.com/FFTAI/gros_client_js/blob/bc9e358/lib/robot/robot_base.ts#L152)

___

### set\_mode

▸ **set_mode**(`mod`): `Promise`<`any`\>

设置小车运动模式

完成后小车将在对应模式下运动，包括 4轮 3轮 2轮

#### Parameters

| Name | Type | Description |
| :------ | :------ | :------ |
| `mod` | [`CarMod`](../enums/CarMod.md) | 模式对象定义 |

#### Returns

`Promise`<`any`\>

return

#### Defined in

[lib/robot/car.ts:41](https://github.com/FFTAI/gros_client_js/blob/bc9e358/lib/robot/car.ts#L41)

___

### start

▸ **start**(): `Promise`<`any`\>

启动 : 重置/归零/对设备初始状态的校准

当你想要控制Robot设备的时候，你的第一个指令

#### Returns

`Promise`<`any`\>

#### Inherited from

RobotBase.start

#### Defined in

[lib/robot/robot_base.ts:100](https://github.com/FFTAI/gros_client_js/blob/bc9e358/lib/robot/robot_base.ts#L100)

___

### stop

▸ **stop**(): `Promise`<`any`\>

停止

该命令优先于其他命令! 会掉电停止。请在紧急情况下触发

#### Returns

`Promise`<`any`\>

#### Inherited from

RobotBase.stop

#### Defined in

[lib/robot/robot_base.ts:112](https://github.com/FFTAI/gros_client_js/blob/bc9e358/lib/robot/robot_base.ts#L112)
