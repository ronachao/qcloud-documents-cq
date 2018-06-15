TSF Agent 是 TSF 控制模块与部署在虚拟机上的应用进行通信的 Daemon 程序。使用 TSF 部署应用之前，需要在实例上安装 TSF Agent。
<br/>
步骤如下：


1)	登录 TSF 控制台，在左侧导航栏中选择 资源管理 > 虚拟机，在实例列表上方单击【添加虚拟机】，从虚拟机列表中选择“未绑定”的虚拟机实例，单击【提交】按钮。<br/>

![](http://imgcache.tcecqpoc.fsphere.cn/image/tapd.oa.com/tfl/captures/2018-01/tapd_10130691_base64_1516193110_91.png)

<br/>
2) 使用 root 账号、密码登录目标虚拟机实例。
3) 在实例列表上方单击【安装 Agent】按钮，在 安装 Agent 页面，复制第一行命令，切换到目标虚拟机命令行上粘贴并执行。
执行结束后，复制第二行命令，切换到目标虚拟机命令行上粘贴（将命令中的 “本机 IP” 替换为虚拟机的内网 IP 地址）并执行。

![图片描述](http://imgcache.tcecqpoc.fsphere.cn/image/tapd.oa.com/tfl/captures/2018-01/tapd_10130691_base64_1516193491_71.png)

4) 完成 Agent 安装后，到 TSF 控制台的虚拟机实例列表页面刷新后，查看 Agent 安装状态。如果Agent状态显示“已安装”，说明Agent安装成功；如果Agent状态显示“未安装”，请提单咨询。


