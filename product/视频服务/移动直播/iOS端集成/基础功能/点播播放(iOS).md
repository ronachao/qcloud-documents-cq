## 基础知识
本文主要介绍视频云 SDK 的点播播放功能，在此之前，先了解如下一些基本知识会大有裨益：

- **直播和点播**
<font color='blue'>直播（LIVE）</font> 的视频源是主播实时推送的。因此，主播停止推送后，播放端的画面也会随即停止，而且由于是实时直播，所以播放器在播直播 URL 的时候是没有进度条的。

 <font color='blue'>点播（VOD）</font> 的视频源是云端的一个视频文件，只要未被从云端移除，视频就可以随时播放， 播放中您可以通过进度条控制播放位置，腾讯视频和优酷土豆等视频网站上的视频观看就是典型的点播场景。

- **协议的支持**
 通常使用的点播协议如下，现在比较流行的是HLS(以“http”打头，以“.m3u8”结尾)的点播地址：
![](http://imgcache.tcecqpoc.fsphere.cn/image/mc.qcloudimg.com/static/img/4b42a00bb7ce2f58f362f35397734177/image.jpg)

## 特别说明
视频云 SDK  <font color='red'>**不会对**</font> 播放地址的来源做限制，即您可以用它来播放云平台或非云平台的播放地址。但视频云 SDK 中的播放器只支持 FLV 、RTMP 和 HLS（m3u8）三种格式的直播地址，以及 MP4、 HLS（m3u8）和 FLV 三种格式的点播地址。

## 对接攻略

### step 1: 创建Player
视频云 SDK 中的 TXVodPlayer 模块负责实现点播播放功能。

```objectivec
TXVodPlayer *_txVodPlayer = [[TXVodPlayer alloc] init];
[_txVodPlayer setupVideoWidget:_myView insertIndex:0]
```

### step 2: 渲染View
接下来我们要给播放器的视频画面找个地方来显示，iOS系统中使用 view 作为基本的界面渲染单位，所以您只需要准备一个 view 并调整好布局就可以了。

```objectivec
[_txVodPlayer setupVideoWidget:_myView insertIndex:0]
```

内部原理上讲，播放器并不是直接把画面渲染到您提供的 view （示例代码中的 \_myView）上，而是在这个view之上创建一个用于OpenGL渲染的子视图（subView）。

如果您要调整渲染画面的大小，只需要调整你所常见的 view 的大小和位置即可，SDK 会让视频画面跟着您的 view 的大小和位置进行实时的调整。

![](http://imgcache.tcecqpoc.fsphere.cn/image/mccdn.qcloud.com/static/img/75b41bd0e9d8a6c2ec8406dc706de503/image.png)
 
> **如何做动画？**
> 针对view做动画是比较自由的，不过请注意此处动画所修改的目标属性应该是 <font color='red'>transform</font> 属性而不是 frame 属性。
```objectivec
  [UIView animateWithDuration:0.5 animations:^{
            _myView.transform = CGAffineTransformMakeScale(0.3, 0.3); //缩小1/3
        }];
```

### step 3: 启动播放
TXVodPlayer支持两种播放模式，您可以根据需要自行选择
1. 通过url方式
TXVodPlayer 内部会自动识别播放协议，您只需要将您的播放 URL 传给 startPlay 函数即可。
```objectivec
NSString* url = @"http://1252463788.vod2.myqcloud.com/xxxxx/v.f20.mp4";
[_txVodPlayer startPlay:url ];
```
2. 通过fileId方式
```objectivec
TXPlayerAuthParams *p = [TXPlayerAuthParams new];
p.appId = 1252463788;
p.fileId = @"4564972819220421305";
[_txVodPlayer startPlayWithParams:p];
```
在[点播视频管理](http://console.tcecqpoc.fsphere.cn/video/videolist) 找到对应的文件。点开后在右侧视频详情中，可以看到appId和fileId。

![视频管理](http://imgcache.tcecqpoc.fsphere.cn/image/mc.qcloudimg.com/static/img/fcad44c3392b229f3a53d5f8b2c52961/image.png)

通过fileId方式播放，播放器会向后台请求真实的播放地址。如果此时网络异常或fileId不存在，则会收到`PLAY_ERR_GET_PLAYINFO_FAIL`事件，反之收到`PLAY_EVT_GET_PLAYINFO_SUCC`表示请求成功。

### step 4: 画面调整

- **view：大小和位置**
如需修改画面的大小及位置，直接调整 setupVideoWidget 的参数 view 的大小和位置，SDK 会让视频画面跟着您的 view 的大小和位置进行实时的调整。

- **setRenderMode：铺满or适应**

| 可选值 | 含义  |
|---------|---------|
| RENDER_MODE_FILL_SCREEN | 将图像等比例铺满整个屏幕，多余部分裁剪掉，此模式下画面不会留黑边，但可能因为部分区域被裁剪而显示不全。 | 
| RENDER_MODE_FILL_EDGE | 将图像等比例缩放，适配最长边，缩放后的宽和高都不会超过显示区域，居中显示，画面可能会留有黑边。 | 

- **setRenderRotation：画面旋转**

| 可选值 | 含义  |
|---------|---------|
| HOME_ORIENTATION_RIGHT | home在右边 | 
| HOME_ORIENTATION_DOWN | home在下面 | 
| HOME_ORIENTATION_LEFT | home在左边 | 
| HOME_ORIENTATION_UP | home在上面 | 

![](http://imgcache.tcecqpoc.fsphere.cn/image/mc.qcloudimg.com/static/img/ef948faaf1d62e8ae69e3fe94ab433dc/image.png)


### step 5: 播放控制
```objectivec
// 调整进度
[_txVodPlayer seek:slider.value];
// 暂停播放
[_txVodPlayer pause];
// 恢复播放
[_txVodPlayer resume];
```

### step 6: 结束播放
结束播放时，如果要推出当前的UI界面，要记得用 <font color='red'>** removeVideoWidget **</font> 销毁view控件，否则会产生内存泄露或闪屏问题。

```objectivec
// 停止播放
[_txVodPlayer stopPlay];
[_txVodPlayer removeVideoWidget]; // 记得销毁view控件
```

### step 7: 屏幕截图
通过调用 **snapshot** 您可以截取当前视频为一帧画面，此功能只会截取当前直播流的视频画面，如果您需要截取当前的整个 UI 界面，请调用 iOS 的系统 API 来实现。

![](http://imgcache.tcecqpoc.fsphere.cn/image/mc.qcloudimg.com/static/img/f63830d29c16ce90d8bdc7440623b0be/image.jpg)

### step 8: 变速播放
点播播放器支持变速播放，通过接口`setRate`设置点播播放速率来完成，支持快速与慢速播放，如0.5X、1.0X、1.2X、2X等。

![](http://imgcache.tcecqpoc.fsphere.cn/image/mc.qcloudimg.com/static/img/8666305d62167cfb7c1e670d14fbd689/image.png)

 ```objectivec
//设置1.2倍速播放
[_txVodPlayer setRate:1.2]; 
// ...
//开始播放
[_txVodPlayer startPlay:url];
```

### step 9: 本地缓存 [UGC版本暂不支持]
在短视频播放场景中，视频文件的本地缓存是很刚需的一个特性，对于普通用户而言，一个已经看过的视频再次观看时，不应该再消耗一次流量。

- **格式支持**
SDK 支持 HLS(m3u8) 和 MP4 两种常见点播格式的缓存功能。

- **何时开启?**
SDK 并不默认开启缓存功能，对于用户回看率不高的场景，也并不推荐您开启此功能。

- **如何开启？**
开启此功能需要配置两个参数：本地缓存目录及需要缓存的视频个数。

```objectivec
TXVodPlayConfig _config = [[TXVodPlayConfig alloc] init];

// 设置缓存路径
_config.cacheFolderPath = 
[NSSearchPathForDirectoriesInDomains(NSDocumentDirectory, NSUserDomainMask, YES) objectAtIndex:0];

// 设置最多缓存多少个文件，避免缓存太多数据
_config.maxCacheItems = 10;

[_txVodPlayer setConfig: _config]; 
// ...
//开始播放
[_txVodPlayer startPlay:playUrl];                            
```

### step 10: 预加载
在短视频播放场景中，预加载功能对于流畅的观看体验很有帮助：在观看当前视频的同时，在后台加载即将要播放的下一个视频URL，这样一来，当用户真正切换到下一个视频时，已经不需要从头开始加载了，而是可以做到立刻播放。

这就是视频播放中无缝切换的背后技术支撑，您可以使用 TXVodPlayer 中的 isAutoPlay 开关来实现这个功能，具体做法如下：

![](http://imgcache.tcecqpoc.fsphere.cn/image/mc.qcloudimg.com/static/img/7331417ebbdfe6306fe96f4b76c8d0ad/image.jpg)

```objectivec
// 播放视频A: 如果将 isAutoPlay 设置为 YES， 那么 startPlay 调用会立刻开始视频的加载和播放
NSString* url_A = @"http://1252463788.vod2.myqcloud.com/xxxxx/v.f10.mp4";
_player_A.isAutoPlay = YES;
[_player_A startPlay:url_A];

// 在播放视频 A 的同时，预加载视频 B，做法是将 isAutoPlay 设置为 NO
NSString* url_B = @"http://1252463788.vod2.myqcloud.com/xxxxx/v.f20.mp4";
_player_B.isAutoPlay = NO;
[_player_B startPlay:url_B];
```

等到视频 A 播放结束，自动（或者用户手动切换到）视频B时，调用 resume 函数即可实现立刻播放。
```objectivec
-(void) onPlayEvent:(TXVodPlayer *)player event:(int)EvtID withParam:(NSDictionary*)param
{
    // 在视频 A 播放结束的时候，直接启动视频 B 的播放，可以做到无缝切换
    if (EvtID == PLAY_EVT_PLAY_END) {
			[_player_A stopPlay];
			[_player_B setupVideoWidget:mVideoContainer insertIndex:0];
			[_player_B resume];
		}
}
```

### step 11: 贴片广告
autoPlay 还可以用来做贴片广告功能，由于设置了 autoPlay 为 NO 之后，播放器会立刻加载但又不会立刻播放，因此可以在此时展示贴片广告，等广告播放结束，在使用 resume 函数立即开始视频的播放。

### step 12: 加密播放 [UGC版本暂不支持]
视频加密方案主要用于在线教育等需要对视频版权进行保护的场景。如果要对您的视频资源进行加密保护，就不仅仅需要在播放器上做改造，还需要对视频源本身进行加密转码，亦需要您的后台和终端研发工程师都参与其中。在 [视频加密解决方案](/document/product/266/9638) 中您会了解到全部细节内容。

目前 TXVodPlayer 也是支持加密播放的，您可以使用通过 [URL](/document/product/266/9638#.E8.A7.86.E9.A2.91.E6.92.AD.E6.94.BE.E6.96.B9.E6.A1.881.EF.BC.9A.E9.80.9A.E8.BF.87querystring.E4.BC.A0.E9.80.92.E8.BA.AB.E4.BB.BD.E8.AE.A4.E8.AF.81.E4.BF.A1.E6.81.AF) 携带身份认证信息的方案，该种方案下 SDK 的调用方式跟普通情况没有什么区别。 您也可以使用 [Cookie](/document/product/266/9638#.E8.A7.86.E9.A2.91.E6.92.AD.E6.94.BE.E6.96.B9.E6.A1.882.EF.BC.9A.E9.80.9A.E8.BF.87cookie.E4.BC.A0.E9.80.92.E8.BA.AB.E4.BB.BD.E8.AE.A4.E8.AF.81.E4.BF.A1.E6.81.AF) 携带身份认证信息的方案，该种方案下，需要您通过 TXVodPlayConfig 中的 headers 字段设置 cookie 信息于 http 请求头中。

### step 13: HTTP-REF [UGC版本暂不支持]
TXVodPlayConfig 中的 headers 可以用来设置 http 请求头，比如常用的防止 URL 被到处拷贝的 Referer 字段（云平台可以提供更加安全的签名防盗链方案），以及用于验证客户端身份信息的 Cookie 字段。

### step 14: 硬件加速
对于蓝光级别（1080p）的画质，简单采用软件解码的方式很难获得较为流畅的播放体验，所以如果您的场景是以游戏直播为主，一般都推荐开启硬件加速。

软解和硬解的切换需要在切换之前先**stopPlay**，切换之后再**startPlay**，否则会产生比较严重的花屏问题。

```objectivec
  [_txVodPlayer stopPlay];
  _txVodPlayer.enableHWAcceleration = YES;
  [_txVodPlayer startPlay:_flvUrl type:_type];
```

### step 15: 多码率文件 [UGC版本暂不支持]
SDK支持hls的多码率格式，方便用户切换不同码率的播放流。在收到PLAY_EVT_PLAY_BEGIN事件后，可以通过下面方法获取多码率数组
```objectivec
NSArray *bitrates = [_txVodPlayer supportedBitrates]; //获取多码率数组
```

在播放过程中，可以随时通过`-[TXVodPlayer setBitrateIndex:]`切换码率。切换过程中，会重新拉取另一条流的数据，因此会有稍许卡顿。SDK针对云平台的多码率文件做过优化，可以做到切换无卡顿。

## 进度展示

点播进度分为两个指标：**加载进度** 和 **播放进度**，SDK 目前是以事件通知的方式将这两个进度实时通知出来的。

您可以为 TXVodPlayer 对象绑定一个 **TXVodPlayListener** 监听器，进度通知会通过 **PLAY_EVT_PLAY_PROGRESS** 事件回调到您的应用程序，该事件的附加信息中即包含上述两个进度指标。

![](http://imgcache.tcecqpoc.fsphere.cn/image/mc.qcloudimg.com/static/img/6ac5e2fe87e642e6c2e6342d72464f4a/image.png)

```objectivec
-(void) onPlayEvent:(int)EvtID withParam:(NSDictionary*)param {
    if (EvtID == PLAY_EVT_PLAY_PROGRESS) {
		    // 加载进度, 单位是秒
		    float playable = [param[EVT_PLAYABLE_DURATION] floatValue];
				[_loadProgressBar setValue:playable];
				
		    // 播放进度, 单位是秒
		    float progress = [param[EVT_PLAY_PROGRESS] floatValue];
				[_seekProgressBar setValue:progress];
				
			// 视频总长, 单位是秒
			float duration = [param[EVT_PLAY_DURATION] floatValue];
			// 可以用于设置时长显示等等
	}
}
```
如果点播播放场景需要获取到毫秒级别的时间戳来加载字幕，您需要用到以下回调。
```objective
-(void) onPlayEvent:(int)EvtID withParam:(NSDictionary*)param {
    if (EvtID == PLAY_EVT_PLAY_PROGRESS) {
		    // 加载进度, 单位是毫秒
		    float playable_ms = [param[EVT_PLAYABLE_DURATION_MS] floatValue];
				[_loadProgressBar setValue:playable];
				
		    // 播放进度, 单位是毫秒
		    float progress_ms = [param[EVT_PLAY_PROGRESS_MS] floatValue];
				[_seekProgressBar setValue:progress];
				
			// 视频总长, 单位是毫秒
			float duration_ms = [param[EVT_PLAY_DURATION_MS] floatValue];
			// 可以用于设置时长显示等等
	}
}
```




## 事件监听
除了 PROGRESS 进度信息，SDK 还会通过 onPlayEvent（事件通知） 和 onNetStatus（状态反馈）同步给您的应用程序很多其它的信息：

### 1. 播放事件
| 事件ID               |   数值  |  含义说明                 |   
| :-------------------  |:-------- |  :------------------------ | 
|PLAY_EVT_PLAY_BEGIN    |  2004|  视频播放开始，如果有转菊花什么的这个时候该停了 | 
|PLAY_EVT_PLAY_PROGRESS |  2005|  视频播放进度，会通知当前播放进度、加载进度 和总体时长     | 
|PLAY_EVT_PLAY_LOADING	|  2007|  视频播放loading，如果能够恢复，之后会有BEGIN事件|  

### 2. 结束事件
| 事件ID                 |    数值  |  含义说明                |   
| :-------------------  |:-------- |  :------------------------ | 
|PLAY_EVT_PLAY_END      |  2006|  视频播放结束   | 
|PLAY_ERR_NET_DISCONNECT |  -2301  |  网络断连,且经多次重连亦不能恢复,更多重试请自行重启播放 | 
|PLAY_ERR_HLS_KEY		| -2305 | HLS解密key获取失败 |

### 3. 警告事件
如下的这些事件您可以不用关心，它只是用来告知您 SDK 内部的一些事件。

| 事件ID                 |    数值  |  含义说明                    |   
| :-------------------  |:-------- |  :------------------------ | 
| PLAY_WARNING_VIDEO_DECODE_FAIL   |  2101  | 当前视频帧解码失败  |
| PLAY_WARNING_AUDIO_DECODE_FAIL   |  2102  | 当前音频帧解码失败  |
| PLAY_WARNING_RECONNECT           |  2103  | 网络断连, 已启动自动重连 (重连超过三次就直接抛送 PLAY_ERR_NET_DISCONNECT 了) |
| PLAY_WARNING_RECV_DATA_LAG       |  2104  | 网络来包不稳：可能是下行带宽不足，或由于主播端出流不均匀|
| PLAY_WARNING_VIDEO_PLAY_LAG      |  2105  | 当前视频播放出现卡顿|
| PLAY_WARNING_HW_ACCELERATION_FAIL|  2106  | 硬解启动失败，采用软解   |
| PLAY_WARNING_VIDEO_DISCONTINUITY |  2107  | 当前视频帧不连续，可能丢帧|
| PLAY_WARNING_DNS_FAIL            |  3001  | RTMP-DNS解析失败（仅播放RTMP地址时会抛送）|
| PLAY_WARNING_SEVER_CONN_FAIL     |  3002  | RTMP服务器连接失败（仅播放RTMP地址时会抛送）|
| PLAY_WARNING_SHAKE_FAIL          |  3003  | RTMP服务器握手失败（仅播放RTMP地址时会抛送）|

### 4. 连接事件
此外还有几个连接服务器的事件，主要用于测定和统计服务器连接时间，您也无需关心：

| 事件ID                     |    数值  |  含义说明                    |   
| :-----------------------  |:-------- |  :------------------------ | 
| PLAY_EVT_CONNECT_SUCC     |  2001    | 已经连接服务器                |
| PLAY_EVT_RTMP_STREAM_BEGIN|  2002    | 已经连接服务器，开始拉流（仅播放RTMP地址时会抛送） |
| PLAY_EVT_RCV_FIRST_I_FRAME|  2003    | 网络接收到首个可渲染的视频数据包(IDR)  |

### 5. 分辨率事件
以下事件用于获取画面变化信息，您也无需关心：

| 事件ID                     |    数值  |  含义说明                    |   
| :-----------------------  |:-------- |  :------------------------ | 
| PLAY_EVT_CHANGE_RESOLUTION|  2009    | 视频分辨率改变               |
| PLAY_EVT_CHANGE_ROATION	|  2011    | MP4视频旋转角度 |


## 视频宽高 
**视频的宽高（分辨率）是多少？**
站在 SDK 的角度，如果只是拿到一个 URL 字符串，它是回答不出这个问题的。要知道视频画面的宽和高各是多少个 pixel, SDK 需要先访问云端服务器，直到加载到足够能够分析出视频画面大小的信息才行，所以对于视频信息而言，SDK 也只能以通知的方式告知您的应用程序。 

 **onNetStatus** 通知每秒都会被触发一次，目的是实时反馈当前的推流器状态，它就像汽车的仪表盘，可以告知您目前SDK内部的一些具体情况，以便您能对当前网络状况和视频信息等有所了解。
  
|   评估参数                   |  含义说明                   |   
| :------------------------  |  :------------------------ | 
| NET_STATUS_CPU_USAGE     | 当前瞬时CPU使用率 | 
| **NET_STATUS_VIDEO_WIDTH**  | 视频分辨率 - 宽 |
| **NET_STATUS_VIDEO_HEIGHT**| 视频分辨率 - 高 |
|	NET_STATUS_NET_SPEED     | 当前的网络数据接收速度 |
|	NET_STATUS_VIDEO_FPS     | 当前流媒体的视频帧率    |
|	NET_STATUS_VIDEO_BITRATE | 当前流媒体的视频码率，单位 kbps|
|	NET_STATUS_AUDIO_BITRATE | 当前流媒体的音频码率，单位 kbps|
|	NET_STATUS_CACHE_SIZE    | 缓冲区（jitterbuffer）大小，缓冲区当前长度为 0，说明离卡顿就不远了|
| NET_STATUS_SERVER_IP | 连接的服务器IP | 

## 视频信息
如果通过fileId方式播放且请求成功，SDK会将一些请求信息通知到上层。您需要在收到`PLAY_EVT_GET_PLAYINFO_SUCC`事件后，解析param中的信息。

|   视频信息                   |  含义说明                   |   
| :------------------------  |  :------------------------ | 
| EVT_PLAY_COVER_URL     | 视频封面地址 | 
| EVT_PLAY_URL  | 视频播放地址 |
| EVT_PLAY_DURATION | 视频时长 |
