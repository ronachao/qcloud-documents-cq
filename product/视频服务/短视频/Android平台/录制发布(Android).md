## 对接流程

- **短视频录制**：
  即采集摄像头画面和麦克风声音，经过图像和声音处理后，进行编码压缩最终生成期望清晰度的 MP4 文件。

- **短视频发布**：
  即将 MP4 文件上传到腾讯视频云，并获得在线观看 URL， 腾讯视频云支持视频观看的就近调度、秒开播放、动态加速 以及海外接入等要求，从而确保优质的观看体验。

![](http://imgcache.tcecqpoc.fsphere.cn/image/mc.qcloudimg.com/static/img/283c8d7fe0a5a316097ae687a2bf6c5a/image.png)

* 第一步：使用 TXUGCRecord 接口录制一段小视频，录制结束后会生成一个小视频文件（MP4）回调给客户；

* 第二步：您的 APP 向您的业务服务器申请上传签名。上传签名是 APP 将 MP4 文件上传到云平台视频分发平台的 “许可证”，为了确保安全性，这些上传签名都要求由您的业务 Server 进行签发，而不能由终端 App 生成。

* 第三步：使用 TXUGCPublish 接口发布视频，发布成功后 SDK 会将观看地址的 URL 回调给您。

## 特别注意

- APP 千万不要把计算上传签名的 SecretID 和 SecretKey 写在客户端的代码里，这两个关键信息泄露将导致安全隐患，比如恶意攻击者一旦破解 APP 获取该信息，就可以免费使用您的流量和存储服务。

- 正确的做法是在您的服务器上用  SecretID 和 SecretKey 生成一次性的上传签名然后将签名交给 APP。因为服务器一般很难被攻陷，所以安全性是可以保证的。

- 发布短视频时，请务必保证正确传递 Signature 字段，否则会发布失败；

- 对短视频录制接口 startRecord 和 stopRecord 的调用必须保证配对；

- 视频录制时长由客户您的代码来控制，基于性能考虑，为了保证良好的用户体验，建议录制时长最长不超过60秒。。


## 接口介绍 
云平台 UGC SDK 提供了相关接口用来实现短视频的录制与发布，其详细定义如下：

| 接口文件                     | 功能                       |
| ------------------------ | ------------------------ |
| `TXUGCRecord.java`       | 实现小视频的录制功能               |
| `TXUGCPublish.java`      | 实现小视频的上传发布               |
| `TXRecordCommon.java`    | 基本参数定义，包括了小视频录制回调及发布回调接口 |
| `TXUGCPartsManager.java` | 视频片段管理类，用于视频的多段录制，回删等    |
| `ITXVideoRecordListener.java` | 小视频录制回调                  |

## 对接攻略

![](http://imgcache.tcecqpoc.fsphere.cn/image/mc.qcloudimg.com/static/img/6b21b033259c1b5124648b73e88fb243/image.png)


### 1. 画面预览
TXUGCRecord（位于 TXUGCRecord.java） 负责小视频的录制功能，我们的第一个工作是先把预览功能实现。startCameraSimplePreview函数用于启动预览。由于启动预览要打开摄像头和麦克风，所以这里可能会有权限申请的提示窗。

```java
mTXCameraRecord = TXUGCRecord.getInstance(this.getApplicationContext());
mTXCameraRecord.setVideoRecordListener(this);					//设置录制回调
mVideoView = (TXCloudVideoView) findViewById(R.id.video_view);	//准备一个预览摄像头画面的
mVideoView.enableHardwareDecode(true);
TXRecordCommon.TXUGCSimpleConfig param = new TXRecordCommon.TXUGCSimpleConfig();
//param.videoQuality = TXRecordCommon.VIDEO_QUALITY_LOW;		// 360p
param.videoQuality = TXRecordCommon.VIDEO_QUALITY_MEDIUM;		// 540p
//param.videoQuality = TXRecordCommon.VIDEO_QUALITY_HIGH;		// 720p
param.isFront = true;           //是否前置摄像头，使用
param.minDuratioin = 5000;	//视频录制的最小时长ms
param.maxDuration = 60000;	//视频录制的最大时长ms
mTXCameraRecord.startCameraSimplePreview(param,mVideoView);
```

### 2. 画面特效
不管是录制前，还是录制中，您都可以使用 TXUGCRecord 里的特效开关来为视频画面添加一些特效，或者是对摄像头本身进行控制。

```java
//////////////////////////////////////////////////////////////////////////
//                      以下为 1.9.1 版本后均支持的特效
//////////////////////////////////////////////////////////////////////////
//
// 切换前后摄像头 参数 mFront 代表是否前置摄像头 默认前置
mTXCameraRecord.switchCamera(mFront);

// 设置美颜 和 美白 效果级别
// beautyDepth     : 美颜级别取值范围 0 ~ 9； 0 表示关闭 1 ~ 9值越大 效果越明显。
// whiteningDepth  : 美白级别取值范围 0 ~ 9； 0 表示关闭 1 ~ 9值越大 效果越明显。
mTXCameraRecord.setBeautyDepth(beautyDepth, whiteningDepth);

// 设置颜色滤镜：浪漫、清新、唯美、粉嫩、怀旧...
// Bitmap     : 指定滤镜用的颜色查找表。注意：一定要用png格式！！！
// demo用到的滤镜查找表图片位于RTMPAndroidDemo/app/src/main/res/drawable-xxhdpi/目录下。
// setSpecialRatio : 用于设置滤镜的效果程度，从0到1，越大滤镜效果越明显，默认取值0.5
mTXCameraRecord.setFilter(filterBitmap);
mTXCameraRecord.setSpecialRatio(0.5);
// 设置全局水印TXRect-水印相对于视频图像的归一化值，sdk内部会根据水印宽高比自动计算height
// 比如视频图像大小为（540，960） TXRect三个参数设置为0.1，0.1，0.1,
// 水印的实际像素坐标为（540 * 0.1，960 * 0.1，540 * 0.1 ，
// 540 * 0.1 * watermarkBitmap.height / watermarkBitmap.width）
setWatermark(watermarkBitmap, txRect)
// 设置绿幕文件:目前图片支持jpg/png，视频支持mp4/3gp等Android系统支持的格式
setGreenScreenFile(path, isLoop);
// 设置美颜风格：光滑，自然，朦胧
setBeautyStyle(style);

// 是否打开闪光灯 参数 mFlashOn 代表是否打开闪关灯 默认关闭
mTXCameraRecord.toggleTorch(mFlashOn);
// 获取摄像头支持的最大焦距
mTXCameraRecord.mTXCameraRecord();
// 设置焦距
mTXCameraRecord.setZoom(value);

//////////////////////////////////////////////////////////////////////////
//                      背景音相关
//////////////////////////////////////////////////////////////////////////
// 设置背景音乐播放回调接口.TXRecordCommon.ITXBGMNotify
setBGMNofify(notify);
// 播放背景音
mTXCameraRecord.playBGM(path);
// 停止播放背景音
mTXCameraRecord.stopBGM();
// 暂停播放背景音
mTXCameraRecord.pauseBGM();
// 继续播放背景音
mTXCameraRecord.resumeBGM();
// 设置麦克风的音量大小，播放背景音混音时使用，用来控制麦克风音量大小
// 音量大小,1为正常音量,建议值为0~2,如果需要调大音量可以设置更大的值.
mTXCameraRecord.setMicVolume(x);
// 设置背景音乐的音量大小，播放背景音乐混音时使用，用来控制背景音音量大小
// 音量大小,1为正常音量,建议值为0~2,如果需要调大背景音量可以设置更大的值.
setBGMVolume(x);

//////////////////////////////////////////////////////////////////////////
//                       以下为仅特权版才支持的特效
// （由于采用优图团队的知识产权，我们无法对外免费提供，需要使用特权版 SDK 才能支持）
//////////////////////////////////////////////////////////////////////////

// 设置动效贴纸 motionTmplPath 动效文件路径： 空String "" 则取消动效
mTXCameraRecord.setMotionTmp(motionTmplPath);
// 设置绿幕文件:目前图片支持jpg/png，视频支持mp4/3gp等Android系统支持的格式
mTXCameraRecord.setGreenScreenFile();
// 设置大眼效果 0~9
mTXCameraRecord.setEyeScaleLevel(eyeScaleLevel);
// 设置瘦脸效果 0~9
mTXCameraRecord.setFaceScaleLevel(faceScaleLevel);
// 设置V脸效果 0~9
mTXCameraRecord.setFaceVLevel(level)
// 设置下巴拉伸或收缩效果 0~9
mTXCameraRecord.setChinLevel(scale)
// 设置缩脸效果 0~9
mTXCameraRecord.setFaceShortLevel(level)
// 设置小鼻效果 0~9
mTXCameraRecord.setNoseSlimLevel(scale)

```


### 3. 文件录制
调用 TXUGCRecord 的 startRecord 函数即可开始录制，调用 stopRecord 函数即可结束录制，startRecord 和 stopRecord 的调用一定要配对。
```java
mTXCameraRecord.startRecord();
mTXCameraRecord.stopRecord();
```

录制的过程和结果是通过 TXRecordCommon.ITXVideoRecordListener（位于 TXRecordCommon.java 中定义）接口反馈出来的：

- onRecordProgress 用于反馈录制的进度，参数millisecond表示录制时长，单位毫秒:
```java
@optional
void onRecordProgress(long milliSecond);
```

- onRecordComplete 反馈录制的结果，TXRecordResult 的 retCode 和 descMsg 字段分别表示错误码和错误描述信息，videoPath 表示录制完成的小视频文件路径，coverImage 为自动截取的小视频第一帧画面，便于在视频发布阶段使用。
```java   
@optional
void onRecordComplete(TXRecordResult result);
```

- onRecordEvent 录制事件回调，包含事件id和事件相关的参数(key,value)格式

```java   
@optional
void onRecordEvent(final int event, final Bundle param);
```



### 4.多段录制与回删

```java
// pauseRecord 后会生成一段视频，视频可以在 TXUGCPartsManager 里面获取 
mTXCameraRecord.pauseRecord();
// 继续录制视频
mTXCameraRecord.resumeRecord();
// 获取片段管理对象
mTXCameraRecord.getPartsManager();
// 获取当前所有视频片段的总时长
mTXUGCPartsManager.getDuration();
// 获取所有视频片段路径
mTXUGCPartsManager.getPartsPathList();
// 删除最后一段视频
mTXUGCPartsManager.deleteLastPart();
// 删除指定片段视频
mTXUGCPartsManager.deletePart(index);
// 删除所有片段视频
mTXUGCPartsManager.deleteAllParts();
```

### 5. 文件预览

使用 [视频播放](/document/product/584/9373) 即可预览刚才生成的 MP4 文件，需要在调用 startPlay 时指定播放类型为 [PLAY_TYPE_LOCAL_VIDEO](/document/product/584/9373#step-3.3A-.E5.90.AF.E5.8A.A8.E6.92.AD.E6.94.BE.E5.99.A86) 。

### 6. 获取签名
要把刚才生成的 MP4 文件发布到云平台上，App 需要拿到上传文件用的短期有效上传签名，这部分有独立的文档介绍，详情请参考 [Server端集成 - 签名派发](/document/product/584/9371)。

### 7. 文件发布
TXUGCPublish（位于 TXUGCPublish.java）负责将 MP4 文件发布到云平台视频分发平台上，以确保视频观看的就近调度、秒开播放、动态加速 以及海外接入等需求。

```java
mVideoPublish = new TXUGCPublish(TCVideoPublisherActivity.this.getApplicationContext());
// 文件发布默认是采用断点续传
TXUGCPublishTypeDef.TXPublishParam param = new TXUGCPublishTypeDef.TXPublishParam();
param.signature = mCosSignature;						// 需要填写第四步中计算的上传签名
// 录制生成的视频文件路径, ITXVideoRecordListener 的 onRecordComplete 回调中可以获取
param.videoPath = mVideoPath;
// 录制生成的视频首帧预览图，ITXVideoRecordListener 的 onRecordComplete 回调中可以获取
param.coverPath = mCoverPath;
mVideoPublish.publishVideo(param);
```

发布的过程和结果是通过 TXRecordCommon.ITXVideoPublishListener（位于 TXRecordCommon.java 头文件中定义）接口反馈出来的：

- onPublishProgress 用于反馈文件发布的进度，参数 uploadBytes 表示已经上传的字节数，参数 totalBytes 表示需要上传的总字节数。
```java
void onPublishProgress(long uploadBytes, long totalBytes);
```

- onPublishComplete 用于反馈发布结果，TXPublishResult 的字段 errCode 和 descMsg 分别表示错误码和错误描述信息，videoURL表示短视频的点播地址，coverURL表示视频封面的云存储地址，videoId表示视频文件云存储Id，您可以通过这个Id调用点播 [服务端API接口](/document/product/266/1965)。
```java 
void onPublishComplete(TXPublishResult result);
```

### 8.发布结果
通过 [错误码表](/document/product/584/10176) 来确认短视频发布的结果。

如果没有错误信息返回，也没有回调。很有可能是集成出现问题，可以参考这里[集成问题](/document/product/584/11631?!preview&lang=cn#8.2-.E7.9F.AD.E8.A7.86.E9.A2.91.E5.8F.91.E5.B8.83.E9.97.AE.E9.A2.98) 
