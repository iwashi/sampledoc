P2P接続およびルーム接続機能を操作するためのクラスです。

## Constructor

### Parameter

|Name|Type|Required|Default|Description|
|----|----|----|----|----|
|id|string|||ユーザのPeer IDです。|
|options|[options object](options-object)|✔||接続に関するパラメータを指定するオプションです。|

#### options object

|Name|Type|Required|Default|Description|
|----|----|----|----|----|
|key|string|✔||SkyWayのAPIキーです。|
|debug|number|||ログレベル： NONE:0、 ERROR:1、 WARN:2、 FULL:3 から選択できます。|
|turn|boolean|||SkyWayで提供するTURNを使うかどうかのフラグです。|
|credential|[credential object](#credential-object)|||Peerを認証するためのクレデンシャルです。次のプロパティを含みます。|
|config|RTCConfiguration object||[RTCConfiguration object](#rtcconfiguration-object)|[応用] [RTCPeerConnectionに渡されるオブジェクト](https://w3c.github.io/webrtc-pc/#rtcconfiguration-dictionary)です。|

#### credential object

|Name|Type|Required|Default|Description|
|----|----|----|----|----|
|timestamp|number|||現在のUNIXタイムスタンプです。|
|ttl|string|||Time to live(ttl)。タイムスタンプ + ttl の時間でクレデンシャルが失効します。|
|authToken|string||Default|HMACを利用して生成する認証用トークンです。|

#### RTCConfiguration object

```js
const defaultConfig = {
  iceServers: [{
    urls: 'stun:stun.webrtc.ecl.ntt.com:3478',
    url:  'stun:stun.webrtc.ecl.ntt.com:3478',
  }],
  iceTransportPolicy: 'all',
};
```
### Sample

```js
const peer = new Peer({
    key:   "<YOUR-API-KEY>"
    debug: 3,
});
```

## Members

|Name|Type|Description|
|----|----|----|
|connections|Object|全てのコネクションを保持するオブジェクトです。|
|id|string|ユーザーが指定したPeer ID、もしくはサーバが生成したPeer IDです。|
|open|boolean|シグナリングサーバへの接続状況を保持します。|
|rooms|object|全てのルームを保持するオブジェクトです。|

## Methods

### call

指定したPeerにメディアチャネルで接続して、MediaConnectionを作成します。 オプションを指定することで、帯域幅・コーデックを指定できます。


#### Parameters

| Name | Type | Required | Default | Description |
| --- | --- | --- | --- | --- |
| peerId | string | ✔ | | 接続先のPeer IDです。 |
| stream | MediaStream | | | リモートのPeerへ送るメディアストリームです。 設定されていない場合は、受信のみモードで発信します。 |
| options | [call options object](#call-options-object) | | |発信時に付与するオプションです。帯域幅・コーデックを指定します。 |

##### call options object

| Name | Type | Required | Default | Description |
| --- | --- | --- | --- | --- |
| label | string | | | 接続先のPeer IDを識別するのに利用するラベルです。 |
| videoBandwidth | number | | | 映像の最大帯域幅(kbps)です。 |
| audioBandwidth | number | | | 音声の最大帯域幅(kbps)です。 |
| videoCodec | string | | | 'H264'などの映像コーデックです。 |
| audioCodec | string | | | 'PCMU'などの音声コーデックです。 |
| videoReceiveEnabled | boolean | | | 映像を受信のみで使う場合のフラグです。|
| audioReceiveEnabled | boolean | | | 音声を受信のみで使う場合のフラグです。|

#### Return value 

[MediaConnection]()のインスタンス

#### Sample

```js
const call = peer.call('peerID', localStream);
```

### connect

指定したPeerにデータチャネルで接続して、DataConnectionインスタンスを生成します。

#### Parameters

| Name | Type | Required | Description |
| --- | --- | --- | --- |
| peerId | string | ✔ |   接続先のPeer IDです。|
| options | [connect options object](#connect-options-object) | | 接続時に付与するオプションです。 |

##### connect options object

| Name | Type | Required | Description |
| --- | --- | --- | --- |
| label | string | | 接続先のPeer IDを識別するのに利用するラベルです。 |
| metadata | string | | コネクションに関連付けされるメタデータで、コネクションを開始したpeerに渡されます。 |
| serialization | string | | 送信時のシリアライズ方法を指定します。'binary'、'json'、'none'のいずれか、となります。 |
| dcInit | [RTCDataChannelInit Object](https://www.w3.org/TR/webrtc/#dom-rtcdatachannelinit) | | DataChannel利用時に信頼性の有無を指定するためのオプションです。デフォルトでは信頼性有で動作します。なお、chromeは、`maxPacketLifetime` の代わりに、`maxRetransmitTime` を利用します。 |

#### Return value 

DataConnectionのインスタンス

#### Sample

```js
// 単にDataChannelを接続する場合(デフォルトで信頼性有り)
peer.connect('peerId');

// 信頼性無モードでDataChannelを接続する場合
peer.connect('peerId', {
  dcInit: {
    // 最大2回、再送する
    maxRetransmits: 2,
  },
});
```

### destroy

全てのコネクションを閉じ、シグナリングサーバへの接続を切断します。

#### Parameters

None

#### Return value 

`undefined`

#### Sample

```js
TBD
```

### disconnect

シグナリングサーバへの接続を閉じ、disconnectedイベントを送出します。

#### Parameters

None

#### Return value 

`undefined`

#### Sample

```js
TBD
```

### joinRoom

メッシュ接続のルーム、またはSFU接続のルームに参加します。

#### Parameters

| Name | Type | Rquired| Default | Description |
| --- | --- | --- | --- | --- |
| roomName | string | ✔ | | 参加先のルームの名前です。|
| roomOptions | [roomOptions object](#roomoptions-object) | | 接続時に選択・付与するオプションです。|

##### roomOptions object

| Name | Type | Required | Default | Description |
| --- | --- | --- | --- | --- |
| mode | string | | 'mesh' | 'sfu'または'mesh'を指定します。 |
| stream | MediaStream | | | ユーザーが送信するメディアストリームです。 |
| videoBandwidth | number | | | 映像の最大帯域幅(kbps)です。メッシュ接続のみ使用可能です。 |
| audioBandwidth | number | | | 音声の最大帯域幅(kbps)です。 メッシュ接続のみ使用可能です。|
| videoCodec | string | | | 'H264'などの映像コーデックです。 メッシュ接続のみ使用可能です。|
| audioCodec | string | | | 'PCMU'などの音声コーデックです。メッシュ接続のみ使用可能です。 |
| videoReceiveEnabled | boolean | | | 映像を受信のみで使う場合のフラグです。メッシュ接続のみ使用可能です。 |
| audioReceiveEnabled | boolean | | | 音声を受信のみで使う場合のフラグです。メッシュ接続のみ使用可能です。 |

#### Return value 

SFURoomまたはMeshRoomのインスタンス

#### Sample

```js
// Mesh接続を利用する場合
const room = peer.joinRoom("roomName", {
  mode: 'mesh', 
  stream: localStream,
});
```

```js
// SFU接続を利用する場合
const room = peer.joinRoom("roomName", {
  mode: 'sfu', 
  stream: localStream,
});
```

### listAllPeers

REST APIを利用して、APIキーに紐づくPeerID一覧を取得します。

#### Parameters

None

#### Return value 

`undefined`

#### Sample

```js
TBD
```

### updateCredential

TTLを延長するための更新リクエストの送付します。

#### Parameters

| Name | Type | Required | Default | Description |
| --- | --- | --- | --- | --- |
| mode | [credential object](#credential-object)| ✔ | |   ユーザー側で作成する新しいクレデンシャルです。 |

##### newCredential object

|Name|Type|Optional|Default|Description|
|----|----|----|----|----|
|timestamp|number|✔||現在のUNIXタイムスタンプです。|
|ttl|string|✔||Time to live(ttl)。タイムスタンプ + ttl の時間でクレデンシャルが失効します。|
|authToken|string|✔|Default|HMACを利用して生成する認証用トークンです。|

#### Return value 

`undefined`

#### Sample

```js
TBD
```

## Events

### open

シグナリングサーバへ正常に接続できたときのイベントです。

|Type|Description|
|----|----|
|string|Peer ID|

#### Sample

```js
peer.on('open', id => {
  console.log(id);
})
```

### call

接続先のPeerからMediaChannelの接続を受信したときのイベントです。

|Type|Description|
|----|----|
|MediaConnection|MediaConnectionのインスタンスです。|

### close

Peerに対する全ての接続を終了したときのイベントです。

### connection

接続先のPeerからDataChannelの接続を受信したときのイベントです。

|Type|Description|
|----|----|
|DataConnection|DataConnectionのインスタンスです。|

### disconnected

シグナリングサーバから切断したときのイベントです。

|Type|Description|
|----|----|
|string|Peer ID|

### expiresin

|Type|Description|
|----|----|
|number|クレデンシャルが失効するまでの時間(秒)です。|

### error

エラーが発生した場合のイベントです。

|Type|Description|
|----|----|
|room-error|ルーム名が指定されていません|
||ルームタイプが異なります。(メッシュルームとして作成した部屋に、SFUルーム指定で参加した場合)|
||SFU機能が該当のAPIキーでDisabledです。利用するには、Dashboardからenableにしてください。|
||不明なエラーが発生しました。少し待って、リトライしてください。|
||ルームログ取得時にエラーが発生しました。少し待って、リトライしてください。|
|authentication|指定されたクレデンシャルを用いた認証に失敗しました。|
|permission|該当のルームの利用が許可されてません。|
|list-error|APIキーのREST APIが許可されてません。|
|disconnected|SkyWayのシグナリングサーバに接続されていません。|
|socket-error|SkyWayのシグナリングサーバとの接続が失われました。|
|invalid-id|IDが不正です。|
|invalid-key|APIキーが無効です。|
|server-error|SkyWayのシグナリングサーバからPeer一覧を取得できませんでした。|
|TBDサーバ側のエラー色々|TBD(サーバ側のメッセージから起こす必要があるので後で)|

#### Sample

```js
// 仮にRoom名を指定せずにjoinRoomを呼んだ場合
peer.on('error', error => {
  console.log(`${error.type}: ${error.message}`);
  // => room-error: Room name must be defined.
});
```