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

### send

接続先のPeerにデータを送信します。シリアライズ方法が'binary'である場合は、送信前に分割します。

#### Parameters

| Name | Type | Optional | Default | Description |
| --- | --- | --- | --- | --- |
| data | *| | | 接続先のPeerに送るデータです。|

Todo: 行きと帰りで違うことを追記

#### Return value 

`undefined`

#### Sample

```js
dataConnection.send('sample');
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
|MediaStream|(現行のドキュメントバグでは？)|
