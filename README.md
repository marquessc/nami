# NAMI：专为微信小程序服务端开发而生
*面向前端开发人员的后端逻辑中间件*

## 什么是NAMI
微信小程序的前端框架，官方命名为MINA；那我们的非官方后端就呼应一下，姑且命名为NAMI（纳米）。<br/>
NAMI提供了一个小程序服务端所需**所有**服务的支持，**包括但不仅限于处理request请求、接收和处理websocket、与微信服务端交互并维护access_token、处理微信服务端登录鉴权、发送模板消息、接收微信支付事件**，等等。<br/>
<br/>
对于小应用：你只需要找一台电脑（无论windows、mac还是linux），一台云虚拟机，甚至一个docker实例，就可以安装NAMI；NAMI提供了一整套完整的小程序后端解决方案，替你包揽有关小程序后端开发的所有问题。<br/>
<br/>
对于大应用：可能小程序只是你整个IT架构的其中一部分；可能你还需要考虑负载均衡，考虑多实例部署，考虑缓存；NAMI可以作为一个纯粹的JAVA开源框架，简化你的JAVA开发，帮你更高效解决与小程序有关的问题。<br/>

更多精美介绍（感谢公司前端小伙伴做的页面）：[http://riversoft.com.cn/nami.html](http://riversoft.com.cn/nami.html)

## NAMI受众
### 前端开发工程师
不需了解JAVA、PHP或其他后端语言；<br/>
不需要安装TOMCAT，不需要LAMP；<br/>
用你**最熟悉的javascript语言编写后端逻辑**，用命令式的语句直接操作数据库，调用微信后台服务（**你试过用javascript发送模板消息吗？**）

### 专注于业务实现，而不想纠结于技术的小程序后端开发者
也许你是有经验的JAVA或PHP程序员，但是leader给你开发小程序的时间不多了；<br/>
面对着**鉴权登录、支付、模板消息、用unionid打通服务号**，看着微信官方文档的**access token心跳维持、加密解密**，你头都大了；<br/>
也许你更擅长需求建模、业务逻辑开发，但不想纠结于技术细节；<br/>
NAMI采用脚本式开发，**只要会写if（判断）会写for-each（循环）**，你的问题都可以快速高效解决。

### JAVA程序员
NAMI采用纯粹的JAVA语言开发，拥有清晰的封装和外部API；<br/>
NAMI内置动态脚本引擎，对微信官方服务端API进行全封装；<br/>
NAMI**也可以成为你JAVA项目的其中一个开源独立JAR包**，帮你更高效快速解决问题。

## NAMI特性
- 可直接运行于任意主流IAAS或PAAS或docker容器,如阿里云、网易蜂巢
- 内置JDK,内置tomcat,支持跨平台(windows/linux/macOS)
- 内置https解决方案，快速申请免费证书并自动维持永久生效
- javaEE技术架构，成熟的横向扩展方案，支持高并发、高可用系统需求，能支持大型/超大型系统
- 傻瓜化脚本开发模式,只关注业务逻辑,不纠结技术实现
- 支持javascript,groovy,java语言开发业务逻辑,总有一款合你意
- 微信API封装,消息、支付、鉴权简单实现

## NAMI关键模块
- 简洁的request门面
- 配置化websocket
- 内置脚本逻辑引擎(可选语言：groovy/javascript/el)
- 全量微信API封装
- 解压即可运行的容器式封装
- 小程序文件上传下载体系封装
- 内置的https解决方案封装

## 一个例子
1. 前端发起一个request
![](http://i.imgur.com/j1qXYf7.png)
前端源码：

```javascript
    //==================NAMI HELLO WORLD begin =================
    //第一个NAMI小程序调用
    wx.request({
      url: 'http://localhost:8080/request/hello.js',
      data: {
        a : 'hello',
        b : 2
      },
      method: 'GET', // OPTIONS, GET, HEAD, POST, PUT, DELETE, TRACE, CONNECT
      // header: {}, // 设置请求的 header
      success: function(res){
        // success
      },
      fail: function() {
        // fail
      },
      complete: function(res) {
        // complete
        console.log("调用完成");
        console.log(res.data);
      }
    })
    //==================NAMI HELLO WORLD end =================
```

2. 启动NAMI后,在request目录中增加脚本
![](http://i.imgur.com/MCEv7r4.png)
<br/>
![](http://i.imgur.com/HTvnQMU.png)
<br/>
后端源码：

```javascript
//definde
function main() {
	var a = request.getString("a") || 'none';
	var b = request.getInteger("b") || 0;

	return {
		a : a,
		b : b
	}
}

// invoke
main();
```

3. 前端回调结果
![](http://i.imgur.com/29RPWnK.png)

## 系列文章
- [NAMI来了！第一个NAMI小程序Hello World！(含视频)](http://mp.weixin.qq.com/s?__biz=MzI2MDE0MjA5MQ==&mid=2247483828&idx=1&sn=cf997d92abd1783b5746bc6ac5afe646&chksm=ea6f64d0dd18edc61b4fcc158c91c342b4ad75891bb083dabc2777946808157da56e3846790a&scene=18#wechat_redirect)
- [NAMI来了！五分钟让微信小程序接上数据库（含视频）](http://mp.weixin.qq.com/s?__biz=MzI2MDE0MjA5MQ==&mid=2247483854&idx=1&sn=5c80bf25dbbbc7637c758929bf5d237d&chksm=ea6f64aadd18edbc6bf84be857711886f072d01c5bd07804befeb77e82e7283569187c1fb178#rd)

## 如何打包
用maven构建，根目录执行：
```
mvn clean install
```
打包结果在/package/target/nami-package.zip

## 开发团队
- woden
<br/>
BPMT微信快速开发平台核心开发
<br/>
微信公众号: **全栈生姜头** 
<br/>
![](http://i.imgur.com/bfh9QVR.jpg)

- borball
<br/>
开源项目微信JavaSDK([https://github.com/borball/weixin-sdk](https://github.com/borball/weixin-sdk "微信SDK"))发起人
<br/>
BPMT快速开发平台核心开发




## 团队招募
> 有意向者可在“全栈生姜头”公众号留言，也可以邮件给我（github资料有邮箱地址）
> 支持（欢迎）远程开发，直接在github上面开发；
> 磨合期先自己fork项目然后push request给我；
> 磨合期之后我会添加到collaborators；

1. 前端工程师招募（1-2名）
	1. 负责NAMI小程序端（前端）框架封装；
	2. 负责NAMI小程序端（前端）DEMO开发；
	3. 可获得“生姜头”小程序账号开发者/体验者资格（一起尝鲜吧~）；
	4. 跟着NAMI项目一起到处活动；

2. 测试工程师（1-2名）
	1. 参与NAMI测试，设计test case；
	2. 开发基于NAMI的各类DEMO；
	3. 可获得“生姜头”小程序账号开发者/体验者资格（一起尝鲜吧~）；
	4. 跟着NAMI项目一起到处活动；

