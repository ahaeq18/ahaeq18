# 啊哈，域名

www.example.com真正的域名是www.example.com.root，简写为www.example.com.。因为，根域名.root对于所有域名都是一样的，所以平时是省略的。

根域名的下一级，叫做”顶级域名”（top-level domain，缩写为TLD），比如.com、.net；再下一级叫做”次级域名”（second-level domain，缩写为SLD），比如www.example.com里面的.example，这一级域名是用户可以注册的；再下一级是主机名（host），比如www.example.com里面的www，又称为"三级域名"，这是用户在自己的域里面为服务器分配的名称，是用户可以任意分配的。

总结一下，域名的层级结构如下。

主机名.次级域名.顶级域名.根域名
host.sld.tld.root

[设置CNAME域名解析](https://help.aliyun.com/document_detail/205660.html)

> A记录域名解析

A记录域名解析又称IP指向，您可以设置子域名并指向到自己的目标主机IP上，从而实现通过域名找到指定IP。应用型负载均衡ALB默认对外提供公网IP访问，如需通过域名访问主机，可以配置A记录域名解析，具体实现方案如下图所示：

![image](https://user-images.githubusercontent.com/101488791/164894754-6e69b71a-ba11-4624-837c-94ed71314a90.png)

> CNAME域名解析

CNAME域名解析又称别名解析，您可以设置子域名并指向到其他域名，从而实现将一个域名指向另一个域名。应用型负载均衡ALB默认对外提供域名访问，如果通过其他域名访问请配置CNAME域名解析，具体实现方案如下图所示：

![image](https://user-images.githubusercontent.com/101488791/164894738-bdc3f87d-1287-40cf-8f2e-9f3a6adc7066.png)

## [深入理解内容分发网络 CDN](https://hexingxing.cn/deep-understanding-of-content-delivery-network-cdn/)

![image](https://user-images.githubusercontent.com/101488791/158043621-7519167b-fab4-4dfd-a638-b24fab539edf.png)
![image](https://user-images.githubusercontent.com/101488791/158043623-1a2d84ed-3a64-436d-92db-81bfeb58fc6f.png)
> 以上为阿里云 CDN 的产品架构图，由调度系统、链路质量系统、缓存系统和支撑系统这四大系统组成。假设您的加速域名为 www.a.com，接入 CDN 开始加速服务后，当终端用户在北京发起 HTTP 请求时，处理流程如上图所示。

CDN 是一个加速网站静态文件的服务，通过向阿里云、腾讯云、百度云等服务商配置 CDN 参数及 CNAME 调用方式来加速网站访问服务，阿里云等服务商主要将源站文件自动缓存分发到自己的 CDN 节点，使网站访问者连接到最近的 CDN 节点，让用户就近访问最近范围分布的节点内容，以达到加速访问和承载源站服务器的压力的效果。

开通 CDN 服务后，你可以应用于以下主要场景：
1. 最开始是应用于网站的小文件缓存，如图片、CSS、JS 等；
2. 后来还针对下载站而涉及的大文件下载服务，如应用更新、手机 ROM 升级、应用程序包下载等；
3. 再后来应用于音视频网站点播服务，如影视、教育、新闻类视频网站及短视频网站和音频类网站等；
4. 如今的 CDN 服务已覆盖以上列举的静态加速方案，以及动态网站文件 .jsp .asp .php 和视频直播等领域。

[附录 CDN 的关键词条]()

源站
源站是指运行用户业务应用的 Web 服务提供方。源站可用来处理和响应用户请求，当边缘节点没有缓存用户请求的内容时，节点会返回源站获取资源数据并返回给用户。阿里云 CDN 的源站可以是 OSS 域名、IP、源站域名或函数计算域名。

边缘节点
边缘节点是 CDN 用于缓存源站资源，以便快速响应不同地域用户请求的网络节点。在阿里云 CDN 的帮助文档中，边缘节点、CDN 节点、Cache 节点、缓存节点、加速节点、阿里云节点等都指阿里云 CDN 的边缘节点。

加速域名
域名（Domain Name）又称网域，是由一串用点分隔的名字组成的 Internet 上某一台计算机或计算机组的名称，用于在数据传输时标识计算机的电子方位（有时也指地理位置）。

加速域名是指接入 CDN，用于加速源站的域名，也是您最终暴露给终端用户访问的域名。CDN 通过加速域名将源站资源缓存到 CDN 加速节点，实现资源访问加速。例如，您使用 www.example.com 域名接入阿里云 CDN，那么加速域名就是 www.example.com。在阿里云 CDN 的帮助文档中，加速域名通常被简写为域名。

CNAME 记录
CNAME（Canonical Name）记录即别名记录，用来把一个域名解析成另一个域名，再由另一个域名提供源站服务。

例如，您在一台服务器上存放了很多资料，使用 docs.example.com 访问服务器上的资源，但又希望通过 documents.example.com 也能访问，您可以在您的 DNS 解析服务商添加一条 CNAME 记录，将 documents.example.com 指向 docs.example.com，所有访问 documents.example.com 的请求都会被转发到 docs.example.com。

CNAME 域名
在 CDN 控制台添加加速域名后，系统会给对应的域名分配一个.kunlun*.com 形式的 CNAME 域名。您需要在您的 DNS 解析服务商处添加一条 CNAME 记录，将加速域名指向 CNAME 域名。记录生效后域名解析就正式转向 CDN 服务，该域名所有的请求都将转向 CDN 的边缘节点，达到加速效果。

静态内容（静态资源）
静态内容是指用户多次请求某一资源，响应返回的数据都是相同的内容。例如图片、视频、网站中的文件（HTML、CSS、JS）、软件安装包、APK 文件、压缩包文件等。

CDN 通过加速域名将源站的静态资源缓存到 CDN 遍布全球的加速节点上，供用户就近访问，实现资源访问加速。

动态内容（动态资源）
动态内容是指用户多次请求某一资源，响应返回的数据可能是不同的内容。例如网站中的文件（ASP、JSP、PHP、PERL、CGI）、API 接口、数据库交互请求等。

DNS
DNS（Domain Name System）即域名解析服务，可以将域名转换成网络可以识别的 IP 地址。人们习惯记忆域名，但机器间互相只识别 IP 地址。域名与 IP 地址之间是一一对应的，它们之间的转换工作称为域名解析，域名解析需要由专门的域名解析服务器来完成，整个过程自动进行。例如，您上网时输入的 www.baidu.com 会自动转换成 220.181.112.143。

SSL/TLS
SSL（Secure Sockets Layer）即安全套接字协议，SSL 协议位于 TCP/IP 协议与各种应用层协议之间，可以有效协助 Internet 上的应用软件提升通讯时的资料完整性及安全性。IETF 将 SSL 标准化后名称被改为 TLS（Transport Layer Security），即传输层安全协议，因此通常将两者并称为 SSL/TLS。

回源
当用户通过浏览器发送请求时，如果 CDN 节点未缓存请求的资源或缓存资源已到期，此时会回源站获取资源并返回给用户，该过程被称为回源。

回源 HOST
回源 HOST 即回源域名，当源站服务器上提供多个域名服务时，CDN 节点回源时在源站访问的具体站点域名。示例如下：
-示例 1：源站是域名。
源站为 www.a.com，回源 HOST 为 www.b.com，实际回源是请求到 www.a.com 解析到的 IP，即对应的主机上的站点 www.b.com。

-示例 2：源站是 IP。
源站为 1.1.1.1，回源 HOST 为 www.b.com，实际回源的是 1.1.1.1 对应的主机上的站点 www.b.com。

回源协议
回源协议指 CDN 节点回源时使用的协议，与客户端访问资源时使用的协议相同。例如，当客户端使用 HTTPS 方式请求未缓存在 CDN 节点上的资源时，CDN 节点会使用相同的 HTTPS 方式回源站获取资源。

## [刺客雇佣网站](https://www.theguardian.com/lifeandstyle/2021/dec/17/bob-innes-rent-a-hitman-assassin-services-website)

![image](https://user-images.githubusercontent.com/101488791/158043691-c81f0c03-4488-4f9a-a6b0-b0660b8ab608.png)

2005年，一个美国大学生购买了 [rentahitman.com](https://rentahitman.com/) 这个域名，意为"雇佣刺客"，打算囤积起来，将来以更高的价格卖掉。

几年以后，他意外收到一个陌生女人的来信，要求帮忙干掉她的三个亲戚，防止他们夺取她父亲的遗产。他觉得太荒谬了，就没有回信。但是，那个女人又发来第二封电子邮件，还提供了姓名、地址等详细信息。他查了一下，发现这个女人正因为其他案件被通缉，就把这些信息提交给警方。

事后他想到，因为这个域名，他可能拯救了三个人的生命。这个网站因此是有意义的，值得认真运作，他就重新制作了网页，使它看上去就像一个真的能雇佣刺客的网站（上图），可以点进去访问。截止2021年，他已经把几百条线索转交警方，他说自己可能挽救了近150人。


## 参考

![Alt](https://repobeats.axiom.co/api/embed/ac9751b512bd3a52343f3d40af691e485e193712.svg "Repobeats analytics image")
