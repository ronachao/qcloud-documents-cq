>**注意：**
>-  本方法仅适用于容量小于 2TB 的硬盘进行分区及格式化。大于 2TB 的硬盘的分区及格式化请使用 GPT方式，可参阅 [使用 GPT 分区表分区并格式化](/doc/product/213/2043)。
>-  格式化后，数据盘中的数据将被全部清空。请在格式化之前，确保数据盘中没有数据或已对重要数据进行备份。为避免服务发生异常，格式化前请确保云服务器已停止对外服务。

## 手动格式化
请根据以下步骤对数据盘进行分区以及格式化，并挂载分区使数据盘可用。

>**注意：**
>- 执行下述命令时，请注意修改数据盘符。下文均以`vdb`为例，若是其他盘符，仅需将`vdb`替换为对应盘符即可。例如，盘符为`xvdb`，则在命令`fdisk /dev/vdb`中须替换为`fdisk /dev/xvdb`。您可使用命令`fdisk -l`查看盘符等相关信息。
>- 请确认路径为正确，若错填为`/dev/vda`,将会造成云主机崩溃。

### 步骤一：查看数据盘信息
登录 Linux 云服务器后，使用以下命令查看数据盘相关信息：
```
fdisk -l
```
>**注意：**
>若使用`df -h`命令，无法看到未分区和格式化的数据盘。

![](http://imgcache.tcecqpoc.fsphere.cn/image/mc.qcloudimg.com/static/img/00d016bf87e88a463f94561c52847b0d/47.png)
### 步骤二：数据盘分区
1. 执行以下命令对数据盘进行分区：
```
fdisk /dev/vdb
```
2. 按照界面的提示，依次键入`n`(新建分区)、`p`(新建扩展分区)、`1`(使用第1个主分区)，两次回车(使用默认配置)，`w`(保存分区表)，开始分区。

>**注意：**
>此处是以创建 1 个分区为例，开发者也可以根据自己的需求创建多个分区。

![](http://imgcache.tcecqpoc.fsphere.cn/image/mc.qcloudimg.com/static/img/fbb9742be87d5a9af0e62c4dd2e02a25/48.png)
### 步骤三：查看新分区
使用以下命令可查看新分区信息：
```
fdisk -l
```
如图，示例中新的分区 vdb1 已经创建完成。
![](http://imgcache.tcecqpoc.fsphere.cn/image/mc.qcloudimg.com/static/img/87614b99eac93c397bf42eaa76cd680e/49.png)
### 步骤四：格式化新分区
>**注意：**
>在进行分区格式化时，开发者可以自行决定文件系统的格式，如 ext2、ext3 等。示例采用`ext3`格式。

执行以下命令对新分区进行格式化：
```
mkfs.ext3 /dev/vdb1
``` 
![](http://imgcache.tcecqpoc.fsphere.cn/image/mc.qcloudimg.com/static/img/2344d2ac95607e83a09aacbb8785563f/50.png)
### 步骤五：挂载新分区
1. 执行以下命令创建 mydata 目录：
```mkdir /mydata```
2. 执行以下命令手动挂载新分区：
```mount /dev/vdb1 /mydata```
3. 最后使用以下命令查看新分区信息：
```df -h```

出现如图信息则说明挂载成功，即可以查看到数据盘了。
![](http://imgcache.tcecqpoc.fsphere.cn/image/mc.qcloudimg.com/static/img/b35b6561171d2c6d4bdc29dff7bf55b3/51.png)

### 步骤六：添加分区信息
如果希望云服务器在重启或开机时能自动挂载数据盘，必须将分区信息添加到`/etc/fstab`中。如果没有添加，则云服务器重启或开机后，都不能自动挂载数据盘。
>**注意：**
>- 请确认分区路径是否为 `/dev/vdb1`,若路径错误，将会造成云主机重启失败。
>- 添加分区信息前可使用`lsblk -f`命令查看数据盘格式。示例以`ext3`为例。 

1. 使用以下命令添加分区信息：
```
echo '/dev/vdb1 /mydata ext3 defaults 0 0' >> /etc/fstab
```
2. 使用以下命令查看分区信息：
```
cat /etc/fstab
```

出现如图信息则说明添加分区信息成功。
![](http://imgcache.tcecqpoc.fsphere.cn/image/mc.qcloudimg.com/static/img/c805b6d32a586f0d5d9300780d7164cc/52.png)



