## 登录小微 Skill 控制台

登录小微 Skill [控制台](http://xiaowei.qcloud.com/developer/skill-list)，单击右上角【新建技能】。

![](http://imgcache.tcecqpoc.fsphere.cn/image/mc.qcloudimg.com/static/img/93e4a3087be6cc3111d03bc8a3460730/image.png)

## 输入基本信息

 1. 输入【名称】，在【QSkill 类型】处勾选【自定义类型】，完成后单击右下角【提交】。

![](http://imgcache.tcecqpoc.fsphere.cn/image/mc.qcloudimg.com/static/img/c3af40c4f106eb179eb4c363ced3a0c2/image.png)

 2. 选择【基本配置】，填写完必要信息后单击右下角【开始配置】。

![](http://imgcache.tcecqpoc.fsphere.cn/image/mc.qcloudimg.com/static/img/364a31032144d487fc620ca112d4d219/image.png)

 3. 授权模式选择【授权码访问模式】，填写完必要信息后点击【保存】

![](http://imgcache.tcecqpoc.fsphere.cn/image/mc.qcloudimg.com/static/img/67323870ffd1a86866c9fe7585d3454d/image.png)

## 配置语言模型

 选择【语言模型】，在这个 tab 中，您可以看到 **槽位** 和 **意图** 两个选项卡，接下来我们将为您解释这两个名词的含义。

 ### 意图
 意图就是用户在说每个指令的时候，想要做的事情。例如用户说 “小微，今天天气怎么样？” 时，他的意图就是查询天气。同时查询天气这个意图包含的不仅仅是代表刚刚那一句话，而是所有相关句式的合集。

一个 Skill 里可以包含多个意图，一个意图可以包含多个关键字，这些关键字称为槽位，这部分会在后续的槽位章节说明。例如在音乐这个 Skill 里，可以包含点播、询问歌名、收藏歌曲、分享歌曲这 4 个意图。而在天气 Skill 里可以包含普通询问、下雨查询、空气质量查询这 3 个意图。意图的数量完全有 Skill 的开发者定义。

![](http://imgcache.tcecqpoc.fsphere.cn/image/mc.qcloudimg.com/static/img/69ea35693e05f662d318eab0bf6c9cef/image.jpg)

在音乐 Skill 里，用户说 “我要听周杰伦的歌” 就会被匹配到点播意图中。“这是什么歌”则会被匹配到询问歌曲名称这个意图。这意图和用户说的话中间的对应关系由各个意图里填写的句式定义，这部分会在后续的句式章节说明。

![](http://imgcache.tcecqpoc.fsphere.cn/image/mc.qcloudimg.com/static/img/0b4a5ac3783150b7b583ddf248f9c223/image.jpg)

#### 自定义意图
除了小微 Skill 开放平台预置的意图之外，其他意图需要 Skill 开发者根据自己的业务来定义，这些由开发者定义的意图成为自定义意图。

#### 内置意图
除了 Skill 各自的自定义意图外，小微平台预先训练好了一些通用的意图，供各个 Skill 使用，我们称之为内置意图。用户在任意 Skill 里说到相关的语句都会被自动分类到这些内置意图里去。
<table class="this">
<tbody>
<tr>
<th width="150"> 意图 </th>
<th width="500"> 例句 </th>
</tr>
<tr>
<td> 暂停 </td>
<td> 暂停一下；请暂停 </td>
</tr>
<tr>
<td> 继续 </td>
<td> 继续播；请继续 </td>
</tr>
<tr>
<td> 退出 </td>
<td> 结束；停止播放 </td>
</tr>
<tr>
<td> 帮助 </td>
<td> 我要怎么说; 如何使用 </td>
</tr>
<tr>
<td> 上一个 </td>
<td> 上一首；上一段 </td>
</tr>
<tr>
<td> 下一个 </td>
<td> 下一首；下一段 </td>
</tr>
<tr>
<td> 顺序播放 </td>
<td> 按列表播放；按顺序播放 </td>
</tr>
<tr>
<td> 随机播放 </td>
<td> 播放随机；随机 </td>
</tr>
<tr>
<td> 单曲循环 </td>
<td> 只听这一首；单曲循环播放 </td>
</tr>
<tr>
<td> 重播 </td>
<td> 你说什么；再说一遍 </td>
</tr>
<tr>
<td> 从头开始 </td>
<td> 重头开始播放；重新开始 </td>
</tr>
<tr>
<td> 是 </td>
<td> 是的；确定 </td>
</tr>
<tr>
<td> 否 </td>
<td> 不是；取消 </td>
</tr>
</tbody>
</table>

注意：

* 如果你的 Skill 没有启用 Audio Player，有 3 个内置意图是你的 Skill 必须支持的，分别是：退出、帮助、重播。
* 如果你的 Skill 启用的了 Audio Player，除了上述 3 个内置意图外，还必须支持这些：暂停、继续、顺序播放、随机播放、单曲循环、上一个、下一个。

 ### 槽位

 某些意图里会包含和意图强相关的关键字，这些关键字称为 **槽位**，例如点播意图可以包含歌手名槽位。

一个意图里可以包含多个槽位，例如查询天气的意图必须包含时间和地点两个关键字才能完成，也就是包含了时间和地点这两个槽位。当然时间我们可以默认是当前时间，地点我们可以根据设备的位置获得，所以这两个槽位是非必须的槽位，用户可以不提供。

但是如果用户要发送 QQ 消息，发送的对象会是一个必须的槽位，如果用户不提供发送的对象，这个任务将无法完成。您可以在小微 Skill 平台上设置某个意图是否必须，被设置成必须的槽位如果用户没有提供，我们会自动反问用户槽位内容。

#### 内置槽位类型
内置槽位类型是小微预置的槽位类型，不需要开发者填写槽位的值，这些槽位类型我们会逐步扩充。

目前小微包含的内置槽位类型如下：
<table class="this">
<tbody>
<tr>
<th> 槽位类型 </th>
<th> 名称 </th>
<th> 例子 </th>
</tr>
<tr>
<td>T.LOC_CITY</td>
<td> 城市名 </td>
<td> 北京；夏威夷 </td>
</tr>
<tr>
<td>T.LOC_CHINA_CITY	</td>
<td> 中国城市名 </td>
<td> 上海；夏威夷 </td>
</tr>
<tr>
<td>T.LOC_FORTIGN_CITY</td>
<td> 外国城市名 </td>
<td> 洛杉矶；斯德哥尔摩 </td>
</tr>
<tr>
<td>T.LOC_COUNTRY</td>
<td> 国家名 </td>
<td> 中国；美利坚合众国 </td>
</tr>
<tr>
<td>T.LOC_PROVINCE</td>
<td> 省名 </td>
<td> 广东省；福建省 </td>
</tr>
<tr>
<td>T.LOC_TOWN</td>
<td> 城镇名 </td>
<td> 深圳市；广州市 </td>
</tr>
</tbody>
</table>

#### 自定义槽位类型
除了我们内置的槽位类型，很多 Skill 需要额外的槽位类型，例如星座建议的 Skill 需要一个槽位类型是星座名。这时候开发者可以新建一个自定义的槽位类型，名字由开发者自定义，比如 “constellation” ，同时需要在平台上配置该槽位类型的所有值。


注意，新建槽位类型时，一定要把这个类型所有可能的值都填写全，避免意图识别的错误。槽位类型的命名仅能使用英文、数字和下划线。在新建槽位时，只需要在槽位类型栏目选择 “constellation” 就可以使用到刚刚新建的槽位类型。

## 开启测试训练

 选择【测试训练】，在【是否开启测试训练】勾选。

 ![](http://imgcache.tcecqpoc.fsphere.cn/image/mc.qcloudimg.com/static/img/3d0a0daa425291b8b43681eee60784d4/image.png)

## 发布 Skill

 选择【发布】，填写发布内容信息，完成后选择【保存配置】可以保存本次填写的信息，【提交审核】可以将本次填写的信息提交给我们审核，资料审核通过后便可以发布。

![](http://imgcache.tcecqpoc.fsphere.cn/image/mc.qcloudimg.com/static/img/2f9e2fb3a62f07d099f267ef4ed6688c/image.png)
