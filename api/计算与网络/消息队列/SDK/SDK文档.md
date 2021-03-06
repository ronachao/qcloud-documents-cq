## CMQ SDK 使用说明文档
为了方便开发者更好地使用 CMQ 的 SDK，云平台提供以下使用说明文档：

[Java (Windows)](http://cmqsdk-10016717.cos.myqcloud.com/JAVA%20SDK%20%E5%BC%80%E5%8F%91%E6%8C%87%E5%8D%97%28windows%29.pdf)

[Python (Linux)](http://cmqsdk-10016717.cos.myqcloud.com/python%20SDK%20%E5%BC%80%E5%8F%91%E6%8C%87%E5%8D%97%28linux%29.pdf)

[PHP (Linux)](http://cmqsdk-10016717.cos.myqcloud.com/PHP%20SDK%20%E5%BC%80%E5%8F%91%E6%8C%87%E5%8D%97%28linux%29%20.pdf)

[C++ (Linux)](http://cmqsdk-10016717.cos.myqcloud.com/C%2B%2BSDK%20%E5%BC%80%E5%8F%91%E6%8C%87%E5%8D%97%28linux%29.pdf)

## 示例：JAVA SDK 使用简介(Windows)

### 环境依赖
请确保已经安装了JDK环境，若未安装请前往 Oracle 官网下载[JDK 安装包](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)并安装；

### CMQ Java SDK 下载与配置
#### 云 API 密钥使用说明
使用 Java SDK 时，首先需要用户的云 API 密钥，云 API 密钥是对用户身份的合法性验证。获取云 API 密钥的方法如下：登录[云平台控制台](http://console.tcecqpoc.fsphere.cn/)，选择【云产品】-【云 API 密钥】选项
![](http://imgcache.tcecqpoc.fsphere.cn/image/mc.qcloudimg.com/static/img/b04d51df61bc4e9259dcee293981b644/5.png)

用户可在此新建新的云 API 密钥或使用现有密钥。点击密钥 ID 进入详情页获取使用的密钥 secretId 和对应的 secretKey。
![](http://imgcache.tcecqpoc.fsphere.cn/image/mc.qcloudimg.com/static/img/47b2cf18add4d32a867f115fffb6af48/2.png)

#### endpoint 说明
endpoint 是使用 CMQ 服务的访问地址，同时 endpoint 中也包含了使用的协议，endpoint的格式如下：

- 内网：<font style="color:red">http:// cmq-queue-region.api.tencentyun.com</font>
- 外网：<font style="color:red">http(s)://cmq-queue-region.api.qcloud.com</font>


#### region 说明
region 需要使用具体地域进行替换，有如下三个地区：gz(广州)，sh(上海)，bj(北京)。划分不同地域有助于不同地域的用户就近选择，提供更好的服务。公共参数中的 region 值要与域名的 region 值保持一致，如果出现不一致的情况，以域名的 region 值为准，将请求发往域名 region 所指定的地域。

#### 内外网区别
如果业务进程也部署在云平台的 CVM 子机上，强烈建议使用同地域的内网endpoint：
1) 同地域内网的时延更低；
2) 目前消息队列对于公网下行流量是要收取流量费用的，用内网可以节省这部分的费用。

外网域名请求既支持http，也支持https。内网请求仅支持http。举个例子：如果使用云平台北京地区的云主机，那么建议请求北京地域的endpoint，这样可以取得较低的时延，同时使用内网可以减少使用费用。因此选用的 endpoint 为`http://cmq-queue-bj.api.tencentyun.com`。

#### JAVA SDK下载
下载最新版[CMQ Java SDK](http://cmqsdk-10016717.cos.myqcloud.com/qc_cmq_java_sdk_V1.0.1.zip)，或选择下载[jar包](http://cmqsdk-10016717.cos.myqcloud.com/cmq.jar)。

如果使用java源码，直接将源码包含在代码目录下：
![](http://imgcache.tcecqpoc.fsphere.cn/image/mc.qcloudimg.com/static/img/997a2dcd9ebddadae8d0fcc17ac185a2/3.png)

如果使用jar包，请在项目【property】对话框-【Java Build Path】-【Libraries】中加入cmq.jar包。
![](http://imgcache.tcecqpoc.fsphere.cn/image/mc.qcloudimg.com/static/img/48efa6b553e9023b8bb94d631892d6d2/4.png)

添加jar包之后，目录如下：
![](http://imgcache.tcecqpoc.fsphere.cn/image/mc.qcloudimg.com/static/img/a025253000b587bc35eca6bc1904d81c/6.png)

添加完毕后，就可以运行程序了。如果有错误返回，请参考官网[错误码说明](/doc/api/431/5903)排查问题。

### 使用 CMQ JAVA SDK

下面的代码也是 Java SDK 中的sample，从创建队列、获取队列属性、发送消息、接收消息、删除消息、删除队列等操作演示了整个消息队列操作的全过程。

```
	import com.qcloud.cmq.*; 
	import java.lang.*;
	import java.util.ArrayList;
	import java.util.List;
	public class 
	{
	public static void main(String[] args) {
	String secretId="";
	String secretKey="";
	String endpoint = "http://cmq-queue-gz.api.qcloud.com";
	String path = "/v2/index.php";
	String method = "POST";
	
    try
    {
		Account account = new Account(endpoint,secretId, secretKey);
		
	
		account.deleteQueue("queue-test10");
		System.out.println("---------------create queue ...---------------");
		QueueMeta meta = new QueueMeta();
		meta.pollingWaitSeconds = 10;
		meta.visibilityTimeout = 10;
		meta.maxMsgSize = 65536;
		meta.msgRetentionSeconds = 345600;
		account.createQueue("queue-test10",meta);
		System.out.println("queue-test10 created");
		account.createQueue("queue-test11",meta);
		System.out.println("queue-test11 created");
		account.createQueue("queue-test12",meta);
		System.out.println("queue-test12 created");
		
		System.out.println("---------------list queue ...---------------");
		ArrayList<String> vtQueue = new ArrayList<String>();
		int totalCount = account.listQueue("",-1,-1,vtQueue);
		System.out.println("totalCount:" + totalCount);
		for(int i=0;i<vtQueue.size();i++)
		{
			System.out.println("queueName:" + vtQueue.get(i));
		}
		
		System.out.println("---------------delete queue ...---------------");
		account.deleteQueue("queue-test11");
		System.out.println("queue-test11 deleted");
		account.deleteQueue("queue-test12");
		System.out.println("queue-test12 deleted");

		System.out.println("--------------- queue[queue-test10] ---------------");
		Queue queue = account.getQueue("queue-test10");
		
		System.out.println("---------------set queue attributes ...---------------");
		QueueMeta meta1 = new QueueMeta();
		meta1.pollingWaitSeconds = 20;
		queue.setQueueAttributes(meta1);
		System.out.println("pollingWaitSeconds=20 set");
		
		System.out.println("---------------get queue attributes ...---------------");
		QueueMeta meta2 = queue.getQueueAttributes();
		System.out.println("maxMsgHeapNum:" + meta2.maxMsgHeapNum);
		System.out.println("pollingWaitSeconds:" + meta2.pollingWaitSeconds);
		System.out.println("visibilityTimeout:" + meta2.visibilityTimeout);
		System.out.println("maxMsgSize:" + meta2.maxMsgSize);
		System.out.println("createTime:" + meta2.createTime);
		System.out.println("lastModifyTime:" + meta2.lastModifyTime);
		System.out.println("activeMsgNum:" + meta2.activeMsgNum);
		System.out.println("inactiveMsgNum:" + meta2.inactiveMsgNum);
		
		System.out.println("---------------send message ...---------------");
		String msgId = queue.sendMessage("hello world,this is cmq sdk for java");
		System.out.println("[hello world,this is cmq sdk for java] sent");
		
		System.out.println("---------------recv message ...---------------");
		Message msg = queue.receiveMessage(10);
		
		System.out.println("msgId:" + msg.msgId);
		System.out.println("msgBody:" + msg.msgBody);
		System.out.println("receiptHandle:" + msg.receiptHandle);
		System.out.println("enqueueTime:" + msg.enqueueTime);
		System.out.println("nextVisibleTime:" + msg.nextVisibleTime);
		System.out.println("firstDequeueTime:" + msg.firstDequeueTime);
		System.out.println("dequeueCount:" + msg.dequeueCount);
		
		System.out.println("---------------delete message ...---------------");
		queue.deleteMessage(msg.receiptHandle);
		System.out.println("receiptHandle:" + msg.receiptHandle +" deleted");
		
		System.out.println("---------------batch send message ...---------------");
		ArrayList<String> vtMsgBody = new ArrayList<String>();
		String msgBody = "hello world,this is cmq sdk for java 1";
		vtMsgBody.add(msgBody);
		msgBody = "hello world,this is cmq sdk for java 2";
		vtMsgBody.add(msgBody);
		msgBody = "hello world,this is cmq sdk for java 3";
		vtMsgBody.add(msgBody);
		List<String> vtMsgId = queue.batchSendMessage(vtMsgBody);
		for(int i=0;i<vtMsgBody.size();i++)
			System.out.println("[" + vtMsgBody.get(i) + "] sent");	
		for(int i=0;i<vtMsgId.size();i++)
			System.out.println("msgId:" + vtMsgId.get(i));
		
		ArrayList<String> vtReceiptHandle = new ArrayList<String>();
		System.out.println("---------------batch recv message ...---------------");
		List<Message> msgList = queue.batchReceiveMessage(10,10);
		System.out.println("recv msg count:" + msgList.size());
		for(int i=0;i<msgList.size();i++)
		{
			Message msg1 = msgList.get(i);
			System.out.println("msgId:" + msg1.msgId);
			System.out.println("msgBody:" + msg1.msgBody);
			System.out.println("receiptHandle:" + msg1.receiptHandle);
			System.out.println("enqueueTime:" + msg1.enqueueTime);
			System.out.println("nextVisibleTime:" + msg1.nextVisibleTime);
			System.out.println("firstDequeueTime:" + msg1.firstDequeueTime);
			System.out.println("dequeueCount:" + msg1.dequeueCount);
			
			vtReceiptHandle.add(msg1.receiptHandle);
		}
		
		queue.batchDeleteMessage(vtReceiptHandle);
		System.out.println("---------------batch delete message ...---------------");
		for(int i=0;i<vtReceiptHandle.size();i++)
			System.out.println("receiptHandle:" + vtReceiptHandle.get(i) + " deleted");

    }
    catch(CMQServerException e1){
        System.out.println("Server Exception, " + e1.toString());
    } catch(CMQClientException e2){
        System.out.println("Client Exception, " + e2.toString());
    }
	catch (Exception e) {
			System.out.println("error..." + e.toString());
	}
	}
	} 
```
