P2P接続およびルーム接続機能を操作するためのクラスです。

## コンストラクタ


```js
const peer = new Peer({
    key:   "<YOUR-API-KEY>"
    debug: 3,
});
```

### パラメータ

#### 案1: List表示

- id
    - Optional: True
    - Description: ユーザのPeer IDです。
    - Type: String
- options
    - Optional: False
    - Description 接続に関するパラメータを指定するオプションです。
    - Type: Object
        - key
            - Type: String
            - Optional: False
            - Description: SkyWayのAPIキーです。
        - debug
            - Type: number
            - Optional: True
            - Default: 0
            - Description: ログレベル： NONE:0、 ERROR:1、 WARN:2、 FULL:3 から選択できます。
        - config
            - Type: Object
            - Optional: True 
            - Default: config.defaultConfig
            - Description: RTCPeerConnectionに渡されるオブジェクトです。
        - turn
            - Type: boolean
            - Optional: True
            - Default: True
            - Description: SkyWayで提供するTURNを使うかどうかのフラグです。
        - credential
            - Description
            - Optional: True
            - Type: Object
                - timestamp
                    - Optional: True
                    - Description: 現在のUNIXタイムスタンプです。
                    - Type: number

#### 案2: Table表示(JSDoc同様、ただし生HTML)

<table class="params">
   <thead>
      <tr>
         <th>Name</th>
         <th>Type</th>
         <th>Attributes</th>
         <th class="last">Description</th>
      </tr>
   </thead>
   <tbody>
      <tr>
         <td class="name"><code>id</code></td>
         <td class="type">
            <span class="param-type">string</span>
         </td>
         <td class="attributes">
            &lt;optional><br>
         </td>
         <td class="description last">
            <span class="jp">ユーザーのPeer IDです。</span>
         </td>
      </tr>
      <tr>
         <td class="name"><code>options</code></td>
         <td class="type">
            <span class="param-type">Object</span>
         </td>
         <td class="attributes">
         </td>
         <td class="description last">
            <span class="jp">接続に関するパラメータを指定するオプションです。</span>
            <h6>Properties</h6>
            <table class="params">
               <thead>
                  <tr>
                     <th>Name</th>
                     <th>Type</th>
                     <th>Attributes</th>
                     <th>Default</th>
                     <th class="last">Description</th>
                  </tr>
               </thead>
               <tbody>
                  <tr>
                     <td class="name"><code>key</code></td>
                     <td class="type">
                        <span class="param-type">string</span>
                     </td>
                     <td class="attributes">
                     </td>
                     <td class="default">
                     </td>
                     <td class="description last">
                        <span class="jp">SkyWayのAPIキーです。</span>
                     </td>
                  </tr>
                  <tr>
                     <td class="name"><code>debug</code></td>
                     <td class="type">
                        <span class="param-type">number</span>
                     </td>
                     <td class="attributes">
                        &lt;optional><br>
                     </td>
                     <td class="default">
                        0
                     </td>
                     <td class="description last">
                        <span class="jp">ログレベル： NONE:0、 ERROR:1、 WARN:2、 FULL:3 から選択できます。</span>
                     </td>
                  </tr>
                  <tr>
                     <td class="name"><code>config</code></td>
                     <td class="type">
                        <span class="param-type">object</span>
                     </td>
                     <td class="attributes">
                        &lt;optional><br>
                     </td>
                     <td class="default">
                        config.defaultConfig
                     </td>
                     <td class="description last">
                        <span class="jp">RTCPeerConnectionに渡されるオブジェクトです。</span>
                     </td>
                  </tr>
                  <tr>
                     <td class="name"><code>turn</code></td>
                     <td class="type">
                        <span class="param-type">boolean</span>
                     </td>
                     <td class="attributes">
                        &lt;optional><br>
                     </td>
                     <td class="default">
                        true
                     </td>
                     <td class="description last">
                        <span class="jp">SkyWayで提供するTURNを使うかどうかのフラグです。</span>
                     </td>
                  </tr>
                  <tr>
                     <td class="name"><code>credential</code></td>
                     <td class="type">
                        <span class="param-type">object</span>
                     </td>
                     <td class="attributes">
                        &lt;optional><br>
                     </td>
                     <td class="default">
                     </td>
                     <td class="description last">
                        <span class="jp">Peerを認証するためのクレデンシャルです。次のプロパティを含みます。</span>
                        <h6>Properties</h6>
                        <table class="params">
                           <thead>
                              <tr>
                                 <th>Name</th>
                                 <th>Type</th>
                                 <th>Attributes</th>
                                 <th class="last">Description</th>
                              </tr>
                           </thead>
                           <tbody>
                              <tr>
                                 <td class="name"><code>timestamp</code></td>
                                 <td class="type">
                                    <span class="param-type">number</span>
                                 </td>
                                 <td class="attributes">
                                    &lt;optional><br>
                                 </td>
                                 <td class="description last">
                                    <span class="jp">現在のUNIXタイムスタンプです。</span>
                                 </td>
                              </tr>
                              <tr>
                                 <td class="name"><code>ttl</code></td>
                                 <td class="type">
                                    <span class="param-type">number</span>
                                 </td>
                                 <td class="attributes">
                                    &lt;optional><br>
                                 </td>
                                 <td class="description last">
                                    <span class="jp">Time to live(ttl)。タイムスタンプ + ttl の時間でクレデンシャルが失効します。</span>
                                 </td>
                              </tr>
                              <tr>
                                 <td class="name"><code>authToken</code></td>
                                 <td class="type">
                                    <span class="param-type">string</span>
                                 </td>
                                 <td class="attributes">
                                    &lt;optional><br>
                                 </td>
                                 <td class="description last">
                                    <span class="jp">HMACを利用して生成する認証用トークンです。</span>
                                 </td>
                              </tr>
                           </tbody>
                        </table>
                     </td>
                  </tr>
               </tbody>
            </table>
         </td>
      </tr>
   </tbody>
</table>

## Members

|Name|Type|Description|
|:---|:---|:---|
|connections|Object|全てのコネクションを保持するオブジェクトです。|
|id|string|ユーザーが指定したPeer ID、もしくはサーバが生成したPeer IDです。|
|open|boolean|シグナリングサーバへの接続状況を保持します。|
|rooms|object|全てのルームを保持するオブジェクトです。|

## Methods

### call

指定したPeerにメディアチャネルで接続して、MediaConnectionを作成します。 オプションを指定することで、帯域幅・コーデックを指定できます。

```js
const call = peer.call("DestPeerID", localStream);
```

#### パラメータ

<table class="params">
   <thead>
      <tr>
         <th>Name</th>
         <th>Type</th>
         <th>Attributes</th>
         <th class="last">Description</th>
      </tr>
   </thead>
   <tbody>
      <tr>
         <td class="name"><code>peerId</code></td>
         <td class="type">
            <span class="param-type">string</span>
         </td>
         <td class="attributes">
         </td>
         <td class="description last">
            <span class="jp">接続先のPeer IDです。</span>
         </td>
      </tr>
      <tr>
         <td class="name"><code>stream</code></td>
         <td class="type">
            <span class="param-type">MediaStream</span>
         </td>
         <td class="attributes">
            &lt;optional&gt;<br>
         </td>
         <td class="description last">
            <span class="jp">リモートのPeerへ送るメディアストリームです。</span>
            <span class="jp">設定されていない場合は、受信のみモードで発信します。</span>
         </td>
      </tr>
      <tr>
         <td class="name"><code>options</code></td>
         <td class="type">
            <span class="param-type">object</span>
         </td>
         <td class="attributes">
            &lt;optional&gt;<br>
         </td>
         <td class="description last">
            <span class="jp">発信時に付与するオプションです。帯域幅・コーデックを指定します。</span>
            <h6>Properties</h6>
            <table class="params">
               <thead>
                  <tr>
                     <th>Name</th>
                     <th>Type</th>
                     <th>Attributes</th>
                     <th class="last">Description</th>
                  </tr>
               </thead>
               <tbody>
                  <tr>
                     <td class="name"><code>label</code></td>
                     <td class="type">
                        <span class="param-type">string</span>
                     </td>
                     <td class="attributes">
                        &lt;optional&gt;<br>
                     </td>
                     <td class="description last">
                        <span class="jp">接続先のPeer IDを識別するのに利用するラベルです。</span>
                     </td>
                  </tr>
                  <tr>
                     <td class="name"><code>videoBandwidth</code></td>
                     <td class="type">
                        <span class="param-type">number</span>
                     </td>
                     <td class="attributes">
                        &lt;optional&gt;<br>
                     </td>
                     <td class="description last">
                            <span class="jp">映像の最大帯域幅(kbps)です。</span>
                     </td>
                  </tr>
                  <tr>
                     <td class="name"><code>audioBandwidth</code></td>
                     <td class="type">
                        <span class="param-type">number</span>
                     </td>
                     <td class="attributes">
                        &lt;optional&gt;<br>
                     </td>
                     <td class="description last">
                        <span class="jp">音声の最大帯域幅(kbps)です。</span>
                     </td>
                  </tr>
                  <tr>
                     <td class="name"><code>videoCodec</code></td>
                     <td class="type">
                        <span class="param-type">string</span>
                     </td>
                     <td class="attributes">
                        &lt;optional&gt;<br>
                     </td>
                     <td class="description last">
                        <span class="jp">'H264'などの映像コーデックです。</span>
                     </td>
                  </tr>
                  <tr>
                     <td class="name"><code>audioCodec</code></td>
                     <td class="type">
                        <span class="param-type">string</span>
                     </td>
                     <td class="attributes">
                        &lt;optional&gt;<br>
                     </td>
                     <td class="description last">
                        <span class="jp">'PCMU'などの音声コーデックです。</span>
                     </td>
                  </tr>
               </tbody>
            </table>
         </td>
      </tr>
   </tbody>
</table>

#### 戻り値

[MediaConnection]()のインスタンス

### connect

...


## Events

