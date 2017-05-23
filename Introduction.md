# HTML5视频直播技术浅析

[TOC]

## 1.主流技术介绍



目前视频直播技术的主流方案有：

1. RTMP（Real Time Messaging Protocol）
2. HLS（HTTP Live Streaming）
3. HTTP-FLV（FLV  over HTTP）
4. MPEG-DASH（HTTP动态自适应流媒体）
5. MSE（Media Source Extension）
6. WebSocket

### RTMP

目前主流 直播平台使用的技术，该协议基于TCP协议，链接稳定，不丢包。延迟较低，大约在10秒以。目前有秒级的RTMP直播解决方案DyncRTMPLiveClient。

由于RTMP是Adobe公司的私有协议，所以在PC端需要借助Flash才能支持。移动端上也需要借助第三方框架，如 FFMpeg ,IJKPlayer和 VLC 等。同时服务器需要支持RTMP协议。

所以，由于协议限制，网页直播无法使用RTMP技术。

### HLS

HLS（HTTP Live Streaming）是苹果公司制定的基于HTTP协议的流媒体传输协议。由于是基于HTTP协议，所以兼容性较好，IOS和安卓都原生支持。原理是将直播流文件分片，通过HTTP协议不断地进行传输，然后实时地播放出来。缺点是延时也比较高，延时与视频流的分片长度有关。

### HTTP-FLV

HTTP-FLV与RTMP类似，都是以FLV文件作为直播流的格式，但相比于RTMP省去了一些协议交互时间，握手方式更加简单，并且HTTP可拓展的功能更多。

HTTP-FLV的HTTP请求没有content-length字段，所以会返回一个无限大的HTTP流的文件，直到服务器和客户端之间的Socket连接断开为止。

FLV流封装简单，相比RTMP实现成本更低。

HTML5虽然不能原生支持HTTP-FLV，但是目前已经有第三框架（flv.js）通过解包封包的方法变为HTML5支持的格式播放出来。

### MPEG-DASH

DASH（Dynamic Adaptive Streaming over HTTP）基于HTTP的动态自适应流媒体传输标准，其制定的目的是为了建立一个统一的流媒体协议标准。其标准建立的较晚，目前应用的并不广泛。其原理也是将视频切分成小片，相比RTMP和HTTP-FLV，具有较高的延迟。

其原理是将视频切割成协议支持的格式，并用MPD文件索引。客户端首先请求mpd文件，根据请求到的mpd文件，就可以知道链接所对应的视频的信息。

其协议内容比较复杂，并且兼容微软的SmoothStreaming和苹果的HLS。

### MSE



