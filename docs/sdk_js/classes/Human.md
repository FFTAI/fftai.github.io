[gros-client](../readme.md) / [Exports](../modules.md) / Human

# Class: Human

GR-1人形机器人对象

在你需要连接GR-1人形机器人的时候，你可以创建一个new Human()对象！ 这将会在后台连接到人形的控制系统，并提供对应的控制函数和状态监听！

## Hierarchy

- `RobotBase`

  ↳ **`Human`**

## Table of contents

### Constructors

- [constructor](Human.md#constructor)

### Properties

- [camera](Human.md#camera)
- [system](Human.md#system)

### Methods

- [disable\_debug\_state](Human.md#disable_debug_state)
- [enable\_debug\_state](Human.md#enable_debug_state)
- [get\_joint\_limit](Human.md#get_joint_limit)
- [get\_joint\_states](Human.md#get_joint_states)
- [head](Human.md#head)
- [on\_close](Human.md#on_close)
- [on\_connected](Human.md#on_connected)
- [on\_error](Human.md#on_error)
- [on\_message](Human.md#on_message)
- [stand](Human.md#stand)
- [start](Human.md#start)
- [stop](Human.md#stop)
- [walk](Human.md#walk)

## Constructors

### constructor

• **new Human**(`option?`)

#### Parameters

| Name | Type |
| :------ | :------ |
| `option?` | `ConnectOption` |

#### Overrides

RobotBase.constructor

#### Defined in

[lib/robot/human.ts:10](https://github.com/FFTAI/gros_client_js/blob/bc9e358/lib/robot/human.ts#L10)

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

### disable\_debug\_state

▸ **disable_debug_state**(): `Promise`<`any`\>

关闭state调试模式

#### Returns

`Promise`<`any`\>

return

#### Defined in

[lib/robot/human.ts:74](https://github.com/FFTAI/gros_client_js/blob/bc9e358/lib/robot/human.ts#L74)

___

### enable\_debug\_state

▸ **enable_debug_state**(`frequence?`): `Promise`<`any`\>

开启state调试模式
触发该函数将会在后台触发GR-01人形设备主动发送状态值的指令，因此对应的你需要监听on_message函数进行处理\

#### Parameters

| Name | Type | Default value | Description |
| :------ | :------ | :------ | :------ |
| `frequence` | `number` | `1` | 频率 (整数) |

#### Returns

`Promise`<`any`\>

return

#### Defined in

[lib/robot/human.ts:60](https://github.com/FFTAI/gros_client_js/blob/bc9e358/lib/robot/human.ts#L60)

___

### get\_joint\_limit

▸ **get_joint_limit**(): `Promise`<`any`\>

获取关节限位

#### Returns

`Promise`<`any`\>

return

#### Defined in

[lib/robot/human.ts:34](https://github.com/FFTAI/gros_client_js/blob/bc9e358/lib/robot/human.ts#L34)

___

### get\_joint\_states

▸ **get_joint_states**(): `Promise`<`any`\>

获取关节状态

#### Returns

`Promise`<`any`\>

return

#### Defined in

[lib/robot/human.ts:46](https://github.com/FFTAI/gros_client_js/blob/bc9e358/lib/robot/human.ts#L46)

___

### head

▸ **head**(`roll`, `pitch`, `yaw`): `void`

控制GR-01人形头部运动 (该请求维持了长链接的方式进行发送)

#### Parameters

| Name | Type | Description |
| :------ | :------ | :------ |
| `roll` | `number` | （翻滚角）：描述围绕x轴旋转的角度，左转头为负，向右转为正，范围（-17.1887-17.1887） |
| `pitch` | `number` | （俯仰角）：描述围绕y轴旋转的角度。前点头为正，后点头为负，范围（-17.1887-17.1887） |
| `yaw` | `number` | （偏航角）：描述围绕z轴旋转的角度。左扭头为负，右扭头为正，范围（-17.1887-17.1887） |

#### Returns

`void`

#### Defined in

[lib/robot/human.ts:104](https://github.com/FFTAI/gros_client_js/blob/bc9e358/lib/robot/human.ts#L104)

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

### stand

▸ **stand**(): `Promise`<`any`\>

GR-01人形设备将会原地站立

当进行了start之后如果你想对GR-01人形设备进行指令控制，你同样需要调用该函数让其位置stand的模式。
如果是在行走过程中需要停止，你同样可以调用该函数进行stand

#### Returns

`Promise`<`any`\>

return

#### Defined in

[lib/robot/human.ts:22](https://github.com/FFTAI/gros_client_js/blob/bc9e358/lib/robot/human.ts#L22)

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

___

### walk

▸ **walk**(`angle`, `speed`): `void`

控制GR-01人形设备行走 (该请求维持了长链接的方式进行发送)

#### Parameters

| Name | Type | Description |
| :------ | :------ | :------ |
| `angle` | `number` | 角度 控制方向，取值范围为正负45度。向左为正，向右为负！(浮点数8位) |
| `speed` | `number` | 速度 控制前后，取值范围为正负0.8。向前为正，向后为负！(浮点数8位) |

#### Returns

`void`

#### Defined in

[lib/robot/human.ts:87](https://github.com/FFTAI/gros_client_js/blob/bc9e358/lib/robot/human.ts#L87)
