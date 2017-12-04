接続先Peerへのメディアチャネル接続を管理するクラスです。

## Constructor

(SDK内部の利用のみ) MediaConnectionは、`call` および `Peer.on('call')` で生成されます。

### Sample

```js
mediaConnection = peer.call('peerID', mediaStream);
```

## Members

|Name|Type|Description|
|----|----|----|
|id|string|コネクションを一意に識別するためのIDです。|
|metadata|object|任意の情報を格納するオブジェクトです。[サンプル](#)|
|open|boolean|コネクションがオープンしているかどうかを示します。|
|remoteId|string|接続先のPeerIDです。|
|peer|string|*Deprecated* 接続先のPeerIDです。remoteIdを使ってください。|

#### Sample

```js
// metadataのサンプルをここに
```

## Methods

### answer

相手からの接続要求に対してに応答します。

#### Parameters

| Name | Type | Require | Default | Description |
| --- | --- | --- | --- | --- |
| stream | MediaStream | ★ | | リモートのPeerへ送るメディアストリームです。|
| options | [answer options object](#answer-options-object) | | |応答時に付与するオプションです。帯域幅・コーデックを指定します。 |

Todo: 行きと帰りで違うことを追記

##### answer options object

| Name | Type | Required | Default | Description |
| --- | --- | --- | --- | --- |
| videoBandwidth | number | | | 映像の最大帯域幅(kbps)です。 |
| audioBandwidth | number | | | 音声の最大帯域幅(kbps)です。 |
| videoCodec | string | | | 'H264'などの映像コーデックです。 |
| audioCodec | string | | | 'PCMU'などの音声コーデックです。 |

#### Return value 

`undefined`

#### Sample

```js
// 相手から発信を受けて
peer.on('call', call => {
  call.answer(mediaStream);
});
```

### close

接続先PeerとのMediaConnectionを接続を切断します。

#### Parameters

None

#### Return value 

`undefined`

#### Fires

- Connection#event:close
(Todo: もっと良い文字に書き直す)

#### Sample

```js
call.close();
```

### replaceStream

送信しているMediaStreamを更新します。受信のみモードから双方向に切り替えできます。
また、音声のみのストリームから、音声＋映像のストリームへの変更もできます。

#### Parameters

| Name | Type | Optional | Default | Description |
| --- | --- | --- | --- | --- |
| stream | MediaStream | | | 交換対象となる新しいMediaStreamです |

#### Return value 

`undefined`

#### Sample

```js
// newStream
call.replaceStream(newStream);
```

## Events

### stream 

MediaStreamを受信したときに発生します。

|Type|Description|
|----|----|
|MediaStream|MediaStreamのインスタンスです。|

#### Sample

```js
mediaConnection.on('stream')

```

### close

MediaConnectionが切断されたときに発生します。

### removeStream

[MediaStream](https://developer.mozilla.org/en-US/docs/Web/API/MediaStream)が削除されたときに発生します。

|Type|Description|
|----|----|
|MediaStream|MediaStreamのインスタンスです。|

