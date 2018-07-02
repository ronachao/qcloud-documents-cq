LogListener 是云平台日志服务提供的日志采集 Agent，您可以安装 LogListener 实时采集日志文件。

## LogListener 系统支持

目前 LogListener 支持如下版本的 Linux 64 位操作系统

CentOS

Debian

SUSE

OpenSUSE

Ubuntu

## LogListener 使用指南

### 安装 LogListener

[点击下载 LogListener 2.1.1](http://imgcache.tcecqpoc.fsphere.cn/image/mc.qcloudimg.com/static/archive/520370e2a9e96c9bd36b5ced36ecdb83/loglistener.2.1.1.tar.gz)，将安装包解压至指定的目标目录中，在 root 下执行：

```
cd loglistener/tools;
./install.sh $(SecretId) $(SecretKey) $(region)
```

注：这里的 SecretId 与 SecretKey为您[云api秘钥](http://console.tcecqpoc.fsphere.cn/cam/capi)中的 SecretId 与 SecretKey。我们建议您使用协作者秘钥，使用前请注意授权协作者对日志服务有读写权限。region 为您所使用的**日志服务区域而非您的机器所处的区域**。服务区域编码如下：

```
shanghai - 上海
guangzhou - 广州
chengdu - 成都
beijing - 北京
```

安装脚本会通过 `rc.local`，以保证机器重起后，客户端正常拉起。

### 查看进程

您可以通过以下命令查看进程：

```
cd loglistener/tools; ./p.sh
```

正常情况下，将存在以下三个进程：

```
bin/loglistenerm -d                                                  --守护进程
bin/loglistener --conf=etc/loglistener.conf                          --主进程
bin/loglisteneru -u --conf=etc/loglistener.conf                      --更新进程

```

### 启停客户端

您可以通过以下脚本启停客户端：

```
cd loglistener/tools; ./start.sh
cd loglistener/tools; ./stop.sh
```

### 卸载 LogListener

```
cd loglistener/tools;
./uninstall
```

卸载操作将删除`rc.local`里面自动重启的工具。

## LogListener 的更新

若您的 LogListener 版本非当前最新版本，我们建议您更新至最新版本。**低于2.1.1版本的LogListener不支持日志结构化。**您可以在 `loglistener/version.txt` 中查看当前 LogListener 的版本信息。

若您的 LogListener 版本低于当前版本，但是高于2.0.0版本更新步骤如下 ：

1. 下载新的安装包
2. 在安装目录（LogListener平级目录）解压新的压缩包
3. 解压后重启 LogListener 即完成更新操作

若您的 LogListener 版本低于2.0.0手动更新步骤：

1. 停止较低版本 LogListener
2. 备份较低版本 LogListener
3. 下载并安装最新版本 LogListener 

>后续我们将支持2.0.0以上版本的LogListener自动更新，敬请期待。[低于2.0.0版本LogListener使用指南](/document/product/614/13550)

## LogListener 工作原理

LogListener 是通过文件系统的修改事件（Inotify）来感知文件的变化，采集日志。

## LogListener 相关指标与使用限制

采集延时，2秒

采集配置变更生效延时，1分钟内

日志量限制，16MB/s

日志长度限制，单条512k，如超过会跳过此512k继续采集（即本条日志会被截断入库）

最大连接数限制，1024

内存使用，正常情况最多50MB，后台服务故障时150MB

CPU 使用，5MB/s日志量下，3进程合计不超过单核20%