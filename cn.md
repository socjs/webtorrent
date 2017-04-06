WebTorrent是用于 Node.js 和浏览器的流 torrent 客户端，完全使用 JavaScript 编写。WebTorrent 是个轻量级，快速的开源 BT 客户端，拥有非常棒的用户体验。

在 node.js 中，模块只是简单的 torrent 客户端，使用 TCP 和 UDP 来和其他 torrent 客户端进行通讯。

在浏览器中，WebTorrent 使用 WebRTC  (数据通道)进行点对点的传输，无需任何浏览器插件，扩展或者安装。注意：在浏览器上，WebTorrent 不 支持 UDP/TCP 点对点传输。

WebTorrent Desktop 连接 BitTorrent 和WebTorrent 端点。

![Network](https://webtorrent.io/img/network.png)

## 特性

- Node.js &浏览器的 BT 客户端 (相同的 npm 包)
- 速度非常快
- 可同时，高效的下载多个 torrents
- 纯 Javascript (无原生依赖)
- 像 streams 一样表示文件
- 支持高级 BT 客户端特性
  - magnet uri 支持，通过 [ut_metadata](https://github.com/feross/ut_metadata)
  - 点发现 ，通过 [dht](https://github.com/feross/bittorrent-dht) , [tracker](https://github.com/feross/bittorrent-tracker) 和 [ut_pex](https://github.com/fisch0920/ut_pex)
  - [协议扩展 api](https://github.com/feross/bittorrent-protocol#extension-api)，添加新扩展
- 完整的测试套件 (完全支持离线运行，非常可靠快速)


仅浏览器支持的特性：

- WebRTC 数据通道
- P2P 网络
- 流视频 torrent 为 <video> 标签 ( webm (vp8, vp9) 或者 mp4 (h.264) )
- 支持 Chrome, Firefox 和 Opera


仅 NodeJS 支持的特性：

- 支持 AirPlay , Chromecast , VLC player 流和其他设备/播放器

## 示例

浏览器下载文件：

```js
var WebTorrent = require('webtorrent')

var client = new WebTorrent()
var magnetURI = '...'

client.add(magnetURI, function (torrent) {
  // Got torrent metadata!
  console.log('Client is downloading:', torrent.infoHash)

  torrent.files.forEach(function (file) {
    // Display the file by appending it to the DOM. Supports video, audio, images, and
    // more. Specify a container element (CSS selector or reference to DOM node).
    file.appendTo('body')
  })
})
```

浏览器发送文件：

```js
var dragDrop = require('drag-drop')
var WebTorrent = require('webtorrent')

var client = new WebTorrent()

// When user drops files on the browser, create a new torrent and start seeding it!
dragDrop('body', function (files) {
  client.seed(files, function (torrent) {
    console.log('Client is seeding:', torrent.infoHash)
  })
})
```

WebTorrent 遵循 MIT 开源授权协议。
