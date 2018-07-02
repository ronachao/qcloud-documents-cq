## 1. ImSDK集成

本节主要介绍如何创建一个应用，并集成ImSDK。

### 1.1 支持版本

ImSDK.framework 支持iOS 7.0 及以上系统。

### 1.2 下载ImSDK

从 [官网](/product/im.html#sdk) 下载ImSDK开发包，主要包括：ImSDK.framework、IMCore.framework、TLSSDK.framework、QALSDK.framework。各个包的说明如下：

必选SDK：**必须是一个版本成套使用，不同版本不可混用**

* ImSDK.framework 		IM接口SDK
* QALSDK.framework		网络SDK
* TLSSDK.framework		登录SDK

可选SDK：

* IMCore.framework		IM核心功能
  * 如果使用IM聊天必须加入，如果只用登录功能（如只使用音视频的情况，可不加入）
  * 如果不加入IMCore.framework，使用时需 #import "ImSDK/ImSDKSimple.h"，不要包含其他头文件，否则可能会引起编译错误
* IMSDKBugly.framework	Crash上报功能
 * 如无特殊需要，推荐使用，在控制台页面可以查看Crash率等信息
 * 如果不加入此SDK，需要调用 [TIMManager sharedInstance] disableCrashReport]; 禁用功能

其他SDK：

* QALHttpSDK.framework		网络透传SDK
 * 只有用到网络透传功能时使用

### 1.3 创建应用

创建一个新工程，填入工程名，这里以IMDemo为例：

![](http://avc.qcloud.com/wiki2.0/im/imgs/20150928013356_56054.jpg)
![](http://avc.qcloud.com/wiki2.0/im/imgs/20150928013638_56711.jpg)

### 1.4 集成ImSDK

选中IMDemo的Target，在General面板中的Linked Frameworks and Libraries添加依赖库。

![](http://avc.qcloud.com/wiki2.0/im/imgs/20150928013833_31715.jpg)

需要添加的依赖库有：

```
CoreTelephony.framework
SystemConfiguration.framework
libc++.dylib
libstdc++.6.dylib
libz.dylib
libsqlite3.dylib
ImSDK.framework
IMCore.framework
TLSSDK.framework
QALSDK.framework
IMSDKBugly.framework
```

其中 ImSDK.framework、IMCore.framework、TLSSDK.framework、QALSDK.framework 为步骤1.1.1下载的SDK，其余均为系统内置库。另外**需要在Build Setting中Other Linker Flags添加-ObjC**。

### 1.5 功能开发

在调用代码中引入ImSDK.framework头文件ImSDK.h，根据后续章节的开发指引进行功能的开发。其中函数调用顺序可参见（1.2.2 调用顺序介绍）。

## 2. ImSDK 基本概念

会话：ImSDK中会话(Conversation)分为两种，一种是C2C会话，表示单聊情况自己与对方建立的对话，读取消息和发送消息都是通过会话完成；另一种是群会话，表示群聊情况下，群内成员组成的会话，群会话内发送消息群成员都可接收到。

如下图所示，一个会话表示与一个好友的对话：

![](http://imgcache.tcecqpoc.fsphere.cn/image/mccdn.qcloud.com/static/img/6a12c1ea947e7b36a7abe25e55c33608/image.jpg)

消息：ImSDK中消息(Message)表示要发送给对方的内容，消息包括若干属性，如是否自己已读，是否已经发送成功，发送人帐号，消息产生时间等；一条消息由若干Elem组合而成，每种Elem可以是文本、图片、表情等等，消息支持多种Elem组合发送。

![](http://avc.qcloud.com/wiki2.0/im/imgs/20150928014948_11392.png)

群组Id：群组Id唯一标识一个群，由后台生成，创建群组时返回。

### 2.1 ImSDK对象简介

iOS ImSDK 对象主要分为通讯管理器，会话、消息，群管理，具体的含义参见下表：

对象 | 介绍 | 功能
---|---|---
TIMManager | 管理器类，负责基本的SDK操作 | 初始化登录、注销、创建会话等
TIMConversation | 会话，负责会话相关操作 | 如发送消息，获取会话消息缓存，获取未读计数等
TIMMessage | 消息 | 包括文本、图片等不同类型消息
TIMGroupManager | 群管理器 | 负责创建群，增删成员，以及修改群资料等
TIMFriendshipManager | 资料关系链管理 | 负责获取、修改好友资料和关系链信息


### 2.2 调用顺序介绍

ImSDK调用API需要遵循以下顺序，其余辅助方法需要在登录成功后调用。

步骤 | 对应函数 | 说明
---|---|---
初始化 | TIMManager : setMessageListener | 设置消息回调
初始化 | TIMManager : setConnListener | 设置链接通知回调
初始化 | TIMManager : initSdk | 初始化SDK
登录 | TIMManager : login | 登录
消息收发 | TIMManager : getConversation | 获取会话
消息收发 | TIMConversation : sendMessage | 发送消息
群组管理 | TIMGroupManager | 群组管理
资料关系链 | TIMFriendshipManager | 资料关系链管理
注销 | TIMManager : logout | 注销（用户可选）

