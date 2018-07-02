
## Paymemt 概述

### 简介

Payment 是 MobileLine 的移动支付服务，给用户提供微信支付与手 Q 支付两种支付渠道，支持 Android 和 iOS 两大主流智能手机平台，开发者可以在移动应用中调起微信和手 Q 来完成支付。

> **注意：**
> 这里的微信支付和手 Q 支付都是指的其 App 支付模式。

### 交易流程

应用 App 在支付时，首先需要通过应用 Server 调用 Payment Server 统一下单接口，然后用获取的订单信息来初始化 Payment 支付请求并唤起支付，后续流程均由 Payment SDK 完成，支付完成后会返回支付的结果信息。最终支付成功后，应用后台会收到 Payment 后台服务的通知。整个支付过程如下：

![支付过程](http://tacimg-1253960454.cos.ap-guangzhou.myqcloud.com/guides/payment/payment%E6%95%B4%E4%BD%93%E6%B5%81%E7%A8%8B.png)

> Payment Server 回调地址即为控制台上配置的回调地址，应用 Server 需要根据实际情况来按格式进行返回。

### 名词解释

|名词|解释|
|:--:|:--|
|应用 App| 您自己的 App，用于集成我们的 MobileLine Payment 服务|
|应用 Server|您自己的 Server，需要在该 Server 上配置下单、通知回调等服务|
|Payment SDK|即 MobileLine Payment SDK，您可以通过 Gradle，或者本地方式来集成|
|Payment Server|即 MobileLine Payment 服务端|
|支付渠道|这里指的是微信支付和 QQ 支付，需要您自己去申请和配置相关渠道信息|

## Payment 接入

下面将按步骤详细介绍如何接入我们的 Payment 服务，主要分为如下几步：

### 1. 创建 MobileLine 应用

如果您还没有自己的 MobileLine 应用，那么您首先需要在控制台上 [创建项目](/document/product/666/14836)，创建好项目后，请在该项目下 [创建 MoblieLine 应用](/document/product/666/14835)，创建应用时，**请按照控制台指引配置您自己的应用 APP**。

### 2. 配置应用 Server

应用 Server 指的是您自己业务的服务端，使用 Payment 服务时，您必须至少在应用 Server 上部署**统一下单**和**支付成功回调**两个接口，其他如查询订单信息、退货等接口您可以根据自己的需要自行配置，服务端配置请参见 [Payment 后台服务配置](/document/product/666/14600)。

### 3. 配置支付渠道

支付渠道包括微信支付和 QQ 支付两个渠道，您需要自己在微信开放平台或者腾讯开放平台上申请渠道信息，然后在控制台上进行配置，支付渠道配置请参见 [Payment 支付渠道配置指引](/document/product/666/14599)。

### 4. 接入 Payment SDK

配置好支付渠道后，您需要将 Payment SDK 集成到应用中，具体步骤请参见 [Payment Android 集成指南](/document/product/666/14593) 和 [Payment IOS 集成指南](/document/product/666/14614)。

### 5. 使用 Payment SDK 发起支付

至此，您已经完成了整个 Payment 服务的配置，现在您可以使用 Payment SDK 来发起支付了，详情请参见 [Payment Android 编程手册](/document/product/666/14594) 和 [Payment IOS 编程手册](/document/product/666/14613)。

### 6. 沙箱联调和发布上线

Payment 支持沙箱和线上两种环境，在您未发布到线上环境前，应用默认的是沙箱环境，这两种环境分布在不同的 Payment 服务器上，请根据您自己应用的实际情况，合理的使用相应的环境。

#### 沙箱环境

Payment 的默认环境，主要用于调试，在这个环境下，支付成功后，Payment Server 会回调控制台上设置的沙箱回调地址。

#### 线上环境

当您的应用调试成功后，请您将应用发布上线，上线后，Payment Server 会在您支付成功后回调控制台上设置的主回调地址或者备回调地址，如何发布上线请参考 Payment 控制台使用手册的 [配置参数](/document/product/666/14838) 部分。



