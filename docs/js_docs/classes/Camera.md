[gros-client](../README.md) / [Exports](../modules.md) / Camera

# Class: Camera

相机

 用于获取视频流状态和视频流

## Table of contents

### Constructors

- [constructor](Camera.md#constructor)

### Properties

- [videoStreamStatus](Camera.md#videostreamstatus)
- [videoStreamUrl](Camera.md#videostreamurl)

## Constructors

### constructor

• **new Camera**(`baseurl`)

#### Parameters

| Name | Type |
| :------ | :------ |
| `baseurl` | `string` |

#### Defined in

[lib/common/camera.ts:19](https://github.com/FFTAI/gros_client_js/blob/6341ea8/lib/common/camera.ts#L19)

## Properties

### videoStreamStatus

• **videoStreamStatus**: `boolean` = `false`

视频流状态 True OR False

#### Defined in

[lib/common/camera.ts:17](https://github.com/FFTAI/gros_client_js/blob/6341ea8/lib/common/camera.ts#L17)

___

### videoStreamUrl

• **videoStreamUrl**: `undefined` \| `string`

视频流地址。如果相机开启状态为false 则该字段为 undefined

#### Defined in

[lib/common/camera.ts:13](https://github.com/FFTAI/gros_client_js/blob/6341ea8/lib/common/camera.ts#L13)
