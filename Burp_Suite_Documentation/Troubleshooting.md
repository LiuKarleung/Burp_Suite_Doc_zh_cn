# 故障排除

如果你是新手 且对于 Burp 存在一些问题，请首先阅读 Burp Suite 的入门的帮助，并按照其说明操作。如果帮助中未能提到解决方案，那么下面的问题和解决方案可能会帮助你。

1. Burp 不能运行.  
	首先确定您已[安装了适当版本的Java](Getting_Started/Launching_Burp.md)。 然后[从命令行启动 Burp](Getting_Started/Launching_Burp.md)。查看出现在命令行上的任何错误消息或其他输出的内容，这些内容可能会包含无法启动的主要原因。

2. 我得到一个错误消息说NoClassDefFoundError。  
	从命令行运行 Burp 时，请确保已包含```-jar```参数，后跟 Burp JAR 文件的位置。 如果还是有问题，请检查您的命令是否启动了正确的 Java 版本。 运行命令```java -version```，该命令会返回当前安装的 Java的版本，请确认正在运行的版本是 1.6 或更高版本。如果您安装了更高版本的Java，但是旧版本仍在执行，请将"java"的环境变量替换为系统上正确的 java 可执行文件的绝对路径。如果仍然有问题，您安装的 Java 可能已损坏，请重新安装 Java，然后重试。  
	如果在尝试使用 Burp Extender 插件启动 Burp 时收到此错误消息，请检查 BurpExtender 类是否在 burp 包中声明，并且扩展程序的 JAR 文件存在于 burp 的文件夹中。

3. 我解压缩了Burp JAR文件。 接下来该做什么？  
	您不需要解压缩 Burp 的 JAR 文件。 这可能是因为您的计算机将 .JAR 文件扩展名与某些解压软件相关联。您可以将此关联更改为用Java 去运行，或这，您可以从命令行启动Burp(这也是我们推荐的方式)。

4. 我的浏览器无法发出任何请求。  
	如果您的浏览器总是在等待且未显示出任何实际的内容，请尝试以下操作步骤来解决该问题。在每个步骤完成之后，请检查问题是否依然存在，如问题依然存在，您可以继续执行下一步以排除问题。
	- 首先运行 Burp，然后转到 Porxy 选项卡的 Intercept 子选项卡。 如果在这里能够看到 HTTP 请求，那么您可以尝试关闭拦截（单击"Intercept is on"按钮切换侦听状态）。此时，您的浏览器应该可以正常的工作。有关使用 Burp Proxy 的基础知识的更多帮助，请参阅[Burp Proxy 入门](../Proxy/Getting_Started.md)
	- 尝试使用您的浏览器访问其他网站（最好是较为知名的网站）。如果能够访问，那么问题可能与您要访问网站有关。
	- 转到 Proxy 选项卡的 Options 子选项卡。 在 "代理侦听器(Proxy Listeners)" 这里的表应至少显示一个条目，并且 Running 是选中的。 如果未选中，请单击以选中。 如果无法选中该框，并且 "Alerts" 选项卡显示 “无法启动代理服务(Failed to start proxy service)” 消息，则表示 Burp 无法监听指定的端口。这通常是因为端口正在被另一个程序使用。回到刚才的表中，选择表中的项目，单击 "编辑(Edit)" 按钮，将端口号(Bind to port)更改为其他端口号。 单击 "确定(OK)" ，然后看看现在是否可以启用侦听器。您可以先查询下您的计算机有那些端口可用，从中选择一个端口号进行配置。 然后在浏览器的代理配置这里使用新的端口号以更新浏览器的代理配置。
	- 检查您的浏览器的代理设置是否配置正确，检查是否与 Burp 中正在运行的代理侦听器上配置的IP地址和端口号是否相同（在 Burp 的默认设置中，这是IP地址为 127.0.0.1 端口为 8080，可能与您的 Burp 的配置不同）。相关的详细信息，请参阅[配置浏览器](Getting_Started/Configuring_Your_Browser.md)。
	- 在 Burp 中，转到 User Options 选项卡的 Connections 子选项卡。 在 "上游代理服务器(Upstream Proxy Servers)" 这部分查看是否配置了上游代理，如果是，请确认上游代理可用。
	- 从浏览器发出更多请求（例如，刷新几次）。 在 "警报(Alerts)" 选项卡中查看是否有新的提示。 如果有的话，那么这些信息可能指示问题的主要原因。
	- 转到 Burp 菜单，并为所有选项选择 "恢复默认值(Restore defaults)" 。 然后关闭浏览器并重新启动 Burp。然后检查 Burp 及浏览器是否可以正常使用。
5. Burp 没有拦截到任何东西。  
	在Burp中，转到 代理(Proxy) 选项卡的 历史记录(HTTP history) 子选项卡。从浏览器发出更多请求(例如刷新几次)，查看代理历史记录中是否显示出了新的条目。如果可以显示出，那么说明 Burp 正在处理您的浏览器流量，但未显示任何拦截消息。转到 拦截(Intercept)选项卡，并启用拦截器(单击 "拦截已关闭(Intercept is off)" 按钮以切换拦截状态)。然后转到 代理选项(Proxy -> Options) 选项卡，找到 "截取客户端请求(Intercept Client Requests)" 和 "拦截服务器响应(Intercept Server Responses)" ，将其恢复为默认值(单击旁边的齿轮状图标，然后单击 "恢复默认值(Restore defaults)" 。 然后从浏览器发出更多请求，这时候这些请求应该显示在 "代理拦截(Proxy -> Intercept)" 选项卡中。  
	
	如果您的浏览器可以正确加载网页，但代理历史记录中没有显示任何项目，则需要检查浏览器的代理设置。 您的浏览器应配置为将 Burp 的代理用于 HTTP 和 HTTPS, 禁用任何 "自动" 代理选项，并删除代理设置中的任何 "例外" 条目。 如果您不确定是否设置，请仔细按照[配置浏览器](Getting_Started/Configuring_Your_Browser.md)中的步骤，确保您的浏览器设置正确。
6. Burp 不拦截 HTTPS 请求。  
	如果您的浏览器已经可以通过 Burp 发送 HTTP 请求，但不能发生 HTTPS 请求，则您的浏览器可能配置为仅代理 HTTP。请检查您的浏览器的代理设置，浏览器的代理配置为使用 Burp 的代理，应用到这两种协议。如果您不确定，请仔细按照[配置浏览器](Getting_Started/Configuring_Your_Browser.md)中的步骤，确保您的浏览器设置正确。  
7. 使用 HTTPS 的网站无法正常工作。  
	如果您的浏览器能够通过 Burp 来访问 HTTPS 的网站，但这些网站不能正常工作（例如用户界面不完整或功能齐全，或是浏览器发出警告），那么应用程序可能尝试通过 HTTPS 从另一个域加载脚本或其他资源，并且您的浏览器通过 Burp 加载这些资源时触发安全警报。您需要在浏览器中[安装 Burp 的CA证书](../Proxy/Options/Proxy_Listeners/Certificate/Install_CA_Certificate.md)，以确保使用 HTTPS 的应用程序正常工作。
8. 使用 Burp 时获取网站身份验证失败。  
	如果您测试的应用程序使用平台身份验证（通常会在浏览器中显示为弹出式登录对话框），并且当浏览器代理配置为使用 Burp 时，则会收到身份验证失败的消息，那么您需要配置 Burp 以处理网站的身份验证。转到 用户选项(User Options) 选项卡的 连接(Connections) 子选项卡中的 平台验证(Platform Authentication) 部分。在这里为应用程序使用的每个主机名添加一个新条目，配置相应的身份验证类型和凭据。如果你不确定认证类型，那么首先应当尝试 NTLMv2 ，然后尝试 NTLMv1 ，然后再尝试其他类型。您可能需要重启启动浏览器，必要的情况下可以清理浏览器缓存，以防止任何浏览器缓存干扰身份验证过程。
9. Burp 内存不足。  
	Burp 受到您的计算机对 Java 进程可用的内存量的限制。 您可以通过使用```-Xmx```参数从命令行启动 Burp, 为其分配相应的内存。有关该问题的详细信息，请参阅[启动 Burp](Getting_Started/Launching_Burp.md)。
10. 如何运行扫描？  
	Burp被设计为基于用户驱动的方式，以支持使用手动测试应用。尝试完全自动化扫描过程的常规 Web 扫描器具有一定的局限性，这些扫描器不能完全的扫描出相应的缺陷。 如果要使用 Burp 作为传统的扫描器，并希望完全自动化扫描的过程，请参阅[使用Burp作为点击扫描器](../Scanner/Point-and-Click.md)。