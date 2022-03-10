# API渗透测试

## 1、API概念

API：Application Programming Interface，即应用程序编程接口。接口就是一个位于复杂系统之上并且能简化你的任务，它就像一个中间人让你不需要了解详细的所有细节。那我们今天要讲的Web API就是这么一类东西。像谷歌搜索系统，它提供了搜索接口，简化了你的搜索任务。再像用户登录页面，我们只需要调用我们的登录接口，我们就可以达到登录系统的目的。

### **接口分类**

目前接口（API）主要分为 WEB 接口、TCP 接口、其他特定接口。

| 接口分类     | 描述                                                         | 传输方式                      | 备注                         |
| ------------ | ------------------------------------------------------------ | ----------------------------- | ---------------------------- |
| **Web API**  | Web API 主要是基于HTTP 协议提供方服务，常见的有 webservice、restAPI 等 | 互联网                        | 主要为互联网用 户提供 服务。 |
| **TCP/DUP**  | TCP socket 主要基于有二进制传输、java                        | 互联网 加密、内部专线、VPN 等 | 主要为特定少                 |
| **其他接口** | 主要为私有的、非标准                                         | 互联网、专 线、VPN            | 主要为特殊对象以及客户端     |
|              |                                                              |                               |                              |



## 2、**常见接口测试工具**

### **1.1 SOAP UI API 测试工具**

SoapUI 是一个开源测试工具，通过 soap/http 来检查、调用、实现 Web Service 的功能/负载/符合性测试。SOAP 包含接口功能测试、接口负载测试、接口安全测试等。支持主流的接口协议，比如 REST API 等，SoapUI 允许任何人轻松地开发作为自己最喜欢的功能插件。

> 下载地址：https://www.soapui.org/
>
>  教程：https://www.cnblogs.com/test-my/p/6269089.html

### **1.2 Postman API 测试工具**

 Postman 是一个很强大的 API 调试、Http 请求的工具，支持用户发送任何类型的 HTTP 请求，例如 GET，POST，HEAD，PUT、DELETE等，并且可以允许任意的参数和 Headers。支持不同的认证机制，包括 Basic Auth，Digest Auth，OAuth 1.0，OAuth 2.0

> 下载地址：https://www.getpostman.com/apps
>
> 教程：https://blog.csdn.net/weixin_39190897/article/details/106129738



### **1.3 SocketTool TCP/UDP 测试工具**

SocketTool 是常见的 TCP/UDP 测试工具，支持 socket 传输。

> https://blog.csdn.net/oShiShuiNianHua1234/article/details/79257353

- 常见的浏览器插件

  - Chrome Restlet Client

  - ```
    - Firefox RESTClient
    ```

## 3、**测试方法**

### Web API 测试

主要参考常规 web 测试，使用 burpsuite、 fiddler、Firefox-hackbar 插件等集成安全测试工具对 API 接口进行分析、测试。

###  Sockket API 测试

使用 SocketTool 等 socket 数据包测试工具，以及开发接口的公司使用的专用测试工具或者自己编写的测试脚本进行分析、测试。使用 wireshark 进行数据包流量分析。 

### 其他接口测试（接近研究性质）

主要使用 wireshark、SocketTool、自主编写的测试（FUZZ）脚本等进行测试。

### 如何查找

**1：如何查找
**　　把以下目录直接增加到字典中，

```
/swagger/
/api/swagger/
/swagger/ui/
/api/swagger/ui/
/swagger-ui.html
/api/swagger-ui.html
/user/swagger-ui.html
/swagger/ui/
/api/swagger/ui/
/libs/swaggerui/
/api/swaggerui/
/swagger-resources/configuration/ui/
/swagger-resources/configuration/security/
```

### 找 Webservice 接口

- Google hacking
  - inurl:jws?wsdl
  - inurl:asmx?wsdl
  - inurl:aspx?wsdl
  - inurl:ascx?wsdl
  - inurl:ashx?wsdl
  - inurl:dll?wsdl
  - inurl:exe?wsdl
  - inurl:php?wsdl
  - inurl:pl?wsdl
  - inurl:?wsdl
  - filetype:jws
  - filetype:asmx
  - filetype:ascx
  - filetype:aspx
  - filetype:ashx
  - filetype:dll
  - filetype:exe
  - filetype:php
  - filetype:pl
  - filetype:wsdl wsdl

　　

1-1：根据返回状态码判断是否存在

1-2：通过js查找在网站的config等关键词js文件中查找

## 4 常见 API 相关漏洞



![Picture1](https://img-blog.csdnimg.cn/img_convert/9970bca50e2ac420a9875e1bfa2122cd.png)

#### 3.1 逻辑越权类

本质上可以说是不安全的直接对象引用，可以通过修改可猜测的参数获取不同参数下的响应结果。参数可以是用户名、用户 ID，连续的数字，变形的连续数字（各种编码或哈希），通过直接修改参数值完成越权的操作。

示例：

- https://wooyun.shuimugan.com/bug/view?bug_no=189225
- https://wooyun.shuimugan.com/bug/view?bug_no=150462
- https://wooyun.shuimugan.com/bug/view?bug_no=140374
- https://wooyun.shuimugan.com/bug/view?bug_no=106709

#### 3.2 输入控制类

XXE，Restful API 的注入漏洞，XSS，溢出，特殊字符的处理。

示例：

- https://wooyun.shuimugan.com/bug/view?bug_no=211103
- https://wooyun.shuimugan.com/bug/view?bug_no=132270
- https://wooyun.shuimugan.com/bug/view?bug_no=8714

#### 3.3 接口滥用

没有请求频率限制导致的各种爆破和遍历，如短信验证码爆破、登录爆破、手机号遍历、身份证遍历等。

示例：

- https://wooyun.shuimugan.com/bug/view?bug_no=141419
- https://wooyun.shuimugan.com/bug/view?bug_no=66571
- https://wooyun.shuimugan.com/bug/view?bug_no=36058
- https://wooyun.shuimugan.com/bug/view?bug_no=147334

#### 3.4 信息泄露

包括越权导致的信息泄露、畸形请求导致的报错响应。

示例：

- https://wooyun.shuimugan.com/bug/view?bug_no=171313
- https://wooyun.shuimugan.com/bug/view?bug_no=160095
- https://wooyun.shuimugan.com/bug/view?bug_no=127457

#### 3.5 HTTP 响应头控制

关于响应头：

- 发送 `X-Content-Type-Options: nosniff` 头。
- 发送 `X-Frame-Options: deny` 头。
- 发送 `Content-Security-Policy: default-src 'none'` 头。
- 删除指纹头 - `X-Powered-By`, `Server`, `X-AspNet-Version` 等等。
- 在响应中强制使用 `content-type`。

#### 3.6 服务端配置漏洞

如服务端版本信息泄露，或服务端程序本身存在漏洞等。

## 4 API 安全加固

根据上面讲的测试方法，一般需要做好：

1. 认证和授权控制
2. 用户输入控制
3. 接口请求频率的限制
4. 输出控制
5. 添加安全响应头参数

## Postman实操

1. 你可以关闭 Postman 中的证书验证。 在 General 设置选项卡下面有一个 SSL 认证验证选项。 设置为 关掉（Off），将使 Postman 忽略任何证书问题，包括 Burp Suite 的 PortSwigger CA 。

2. 你可以将你的Burp Suite CA 设置到系统信任存储。 具体的设置细节和平台有关系。

   Postman界面如下

   ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200514221322594.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl8zOTE5MDg5Nw==,size_16,color_FFFFFF,t_70)

   ### GET请求

   直接看一个Get请求类型的API接口测试实例，以下是接口开发文档对接口参数的具体描述：

   ![在这里插入图片描述](https://img-blog.csdnimg.cn/2020051422063039.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl8zOTE5MDg5Nw==,size_16,color_FFFFFF,t_70)

   Postman新建请求后直接发送以下接口测试请求：

   ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200514220901546.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl8zOTE5MDg5Nw==,size_16,color_FFFFFF,t_70)

   【注意】对于GET请求，可以直接点击Params，输入多个参数名称及value（键对值），即可自动添加在URL链接上，如下图所示：

   ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200514222258785.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl8zOTE5MDg5Nw==,size_16,color_FFFFFF,t_70)

   关于接口开发文档，测试过程中可以找开发人员要，格式参考：API接口文档。http://szdbf.rtb56.com/usercenter/manager/api_doc.aspx

   【注意】进行API接口安全测试时，一般不需要安全人员自己构造数据包， 客户会提供一个测试demo程序（HTML网页形式的），demo中已包含所有功能已经构造好的数据包，只需在页面上直接改请求参数内容然后点发送即可。因为客户自己的测试人员平时做业务功能测试时，也都是有现成的测试 demo的，不可能在Postman中一个一个手动构造请求去测试。

   ### Post请求

   同样直接看一个Post请求类型的API接口测试实例，以下是接口开发文档对接口参数的具体描述：

   ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200514221123224.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl8zOTE5MDg5Nw==,size_16,color_FFFFFF,t_70)Postman新建请求后直接发送以下接口测试请求：

   ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200514221204569.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl8zOTE5MDg5Nw==,size_16,color_FFFFFF,t_70)【注意】上述请求头是根据请求参数的形式自动生成的。请求头中的Content-Type与请求参数的格式之间是有关联关系，比如：

   ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200514222701872.png)

   添加请求头
   对于某些API接口，可能需要添加特定的请求头信息进行身份认证才能进行访问，比如 Sign、Token、Cookie、Authorization 等。在Postman中可直接通过 Headers 添加（以下实例的sign值为“用户名+密码”的32位MD5值）：、

   ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200514223951613.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl8zOTE5MDg5Nw==,size_16,color_FFFFFF,t_70)

   或者使用专门的 Authorization 模块进行添加：

   ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200514224128297.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl8zOTE5MDg5Nw==,size_16,color_FFFFFF,t_70)图示的几种身份认证方式简述如下：

   | 认证方式     | 简述                                     |
   | ------------ | ---------------------------------------- |
   | No Auth      | 即不需要认证，这是默认选中的             |
   | Bearer Toker | 填写Token进行验证                        |
   | Basic Auth   | 输入用户名和密码，直接明文发送数据       |
   | Digest Auth  | 摘要认证，在基本身份认证上面扩展了安全性 |
   | OAuth 2.0    | 一个开放授权协议，详情参见理解OAuth 2.0  |

   这里补充下摘要认证方式：消息摘要式身份认证在基本身份认证上面扩展了安全性，服务器为每一个连接生成一个唯一的随机数，客户端用这个随机数对密码进行MD5加密，然后返回服务器，服务器也用这个随机数对密码进行加密，然后和客户端传送过来的加密数据进行比较,如果一致就返回结果。

## 参考文章

https://blog.csdn.net/weixin_39190897/article/details/106129738

https://www.cnblogs.com/anbuxuan/p/13826186.html

https://xz.aliyun.com/t/2412

https://blog.csdn.net/bloodzero_new/article/details/112479328



ewogICAgImFsZyI6ICJub25lIiwKICAgICJ0eXAiOiAiSldUIgp9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.