## 1 Nginx HTTPS双向认证配置指南

以第三方开发者域名`http://www.example.com`为例。

### 1.1 情况1：第三方开发者已有权威第三方签发的证书

1. 开发者准备权威第三方为`www.example.com`签发的证书`www.example.com.crt`和派发的私钥`www.example.com.key`；注意必须是权威的第三方机构（如天威、globalsign等）签发的证书；
1. 云平台给开发者后台提供用于验证请求方（腾讯）证书的CA证书[TencentQQAuthCA.crt](http://share.weiyun.com/7d86303625fda66998bcc46f79320503)；
2. 参照[Nginx HTTPS双向认证配置参考](#2-nginx-https.E5.8F.8C.E5.90.91.E8.AE.A4.E8.AF.81.E9.85.8D.E7.BD.AE.E5.8F.82.E8.80.83)进行配置。
	
### 1.2 情况2：第三方开发者向云平台申请为域名签发证书

1. 第三方开发者向云平台提供开发者后台域名，例如`www.example.com`；
1. 云平台给开发者后台域名`www.example.com`签发证书和私钥，`www.example.com.crt`和`www.example.com.key`；
1. 同时云平台给开发者后台提供用于验证请求方（腾讯）证书的CA证书[TencentQQAuthCA.crt](http://share.weiyun.com/7d86303625fda66998bcc46f79320503)；
2. 参照[Nginx HTTPS双向认证配置参考](#2-nginx-https.E5.8F.8C.E5.90.91.E8.AE.A4.E8.AF.81.E9.85.8D.E7.BD.AE.E5.8F.82.E8.80.83)进行配置。
	
## 2 Nginx HTTPS双向认证配置参考

将`www.example.com.crt`、`www.example.com.key`和`TencentQQAuthCA.crt`拷贝到Nginx的安装目录的conf文件夹下。修改nginx.conf配置文件，参考配置如下。

```
server {
    listen 443 ssl;
    ssl_protocols TLSv1 TLSv1.1;

    server_name            www.example.com;      #域名
    ssl_certificate        www.example.com.crt;  #腾讯给第三方签发的证书
    ssl_certificate_key    www.example.com.key;  #和证书配对的私钥

    ssl_verify_client on;  #验证请求来源
    ssl_client_certificate TencentQQAuthCA.crt;  #腾讯认证的CA证书
	
    location / {
        root   html;
        index  index.html index.htm;
    }
}
```