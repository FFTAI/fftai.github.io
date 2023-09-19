[gros-client](README.md) / Exports

# gros-client

## Table of contents

### Enumerations

- [CarMod](enums/CarMod.md)

### Classes

- [Camera](classes/Camera.md)
- [Car](classes/Car.md)
- [Human](classes/Human.md)
- [System](classes/System.md)

### Functions

- [get\_robot\_type](modules.md#get_robot_type)

## Functions

### get\_robot\_type

▸ **get_robot_type**(`option?`): `Promise`<`AxiosResponse`<`any`, `any`\>\>

获取Robot类型

当你使用群集或者多设备的时候 你可以遍历调用该接口依次从设备上读取类型，以便于您做出准确的控制

#### Parameters

| Name | Type | Description |
| :------ | :------ | :------ |
| `option?` | `ConnectOption` | 连接对象，默认连接127.0.0.1:8001 请根据需要修改{host: str, port: number} |

#### Returns

`Promise`<`AxiosResponse`<`any`, `any`\>\>

#### Defined in

[index.ts:16](https://github.com/FFTAI/gros_client_js/blob/bc9e358/index.ts#L16)
