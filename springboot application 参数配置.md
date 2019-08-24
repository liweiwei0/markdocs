# <p align='center'>springboot application 配置 </p>

| 参数 | 介绍 |
| :-- | :-- |
| server.address | 服务器应绑定到的网络地址 |
| server.compression.enabled = false | 如果启用响应压缩 |
| server.compression.excluded-user-agents | 从压缩中排除的用户代理列表 |
| server.compression.mime-types | 应该压缩的MIME类型的逗号分隔列表。例如text / html，text / css，application / json |
| server.compression.min-response-size | 执行压缩所需的最小响应大小。例如2048服务器 |
| connection-timeout | 连接器在关闭连接之前等待另一个HTTP请求的时间（以毫秒为单位）。未设置时，将使用连接器的容器特定默认值。使用-1表示no（即无限）超时 |
| server.context-parameters.* | Servlet上下文初始化参数。例如server.context-parameters.a = alpha |
| server.context-path | 应用程序的上下文路径 |
| server.display-name = application | 显示应用程序的名称 |
| server.max-http-header-size = 0 | HTTP消息头的最大大小（以字节为单位） |
| server.error.include-stacktrace = never | 何时添加“stacktrace” 属性 |
| server.error.path = / error | 错误控制器的路径 |
| server.error.whitelabel.enabled = true | 在服务器发生错误的情况下，启用浏览器中显示的默认错误页面 |
| server.jetty.acceptors | 要使用的接受者线程数 |
| server.jetty.max-http-post-size = 0 | HTTP发布或放置内容的最大大小（以字节为单位） |
| server.jetty.selectors | 要使用的选择器线程数 |
| server.jsp-servlet.class-name = org.apache.jasper.servlet.JspServlet | JSP servlet的类名 |
| server.jsp-servlet.init-parameters.* | 用于配置JSP Servlet 服务器的Init参数 |
| jsp-servlet.registered = true | 是否注册了JSP servlet |
| server.port = 8080 | Server HTTP端口 |
| server.server-header | 用于服务器响应头的值（没有头发送为空） |
| server.servlet-path = / | 主调度程序servlet的路径 |
| server.use-forward-headers | 如果X-Forwarded- *头应该应用于HttpRequest |
| server.session.cookie.comment | 会话cookie的注释。 |
| server.session.cookie.domain | 会话cookie的域 |
| server.session.cookie.http-only | “HttpOnly”会话cookie的标志 |
| server.session.cookie.max-age | 会话cookie的最大年龄（以秒为单位） |
| server.session.cookie.name | 会话cookie名称 |
| server.session.cookie.path | 会话cookie的路径 |
| server.session.cookie.secure | “安全”标志为会话cookie |
| server.session.persistent = false | 重新启动之间持续会话数据 |
| server.session.store-dir | 用于存储会话数据的目录 |
| server.session.timeout | 会话超时（秒） |
| server.session.tracking-modes | 会话跟踪模式（以下一个或多个：“cookie”，”url”, “ssl”) |
| server.ssl.ciphers | 支持SSL加密 |
| server.ssl.client-auth | 是否是想客户认证（“想要”）或需要（“需要”）需要信任存储 |
| server.ssl.enabled | 启用SSL的支持 |
| server.ssl.enabled-protocols | 启用SSL协议 |
| server.ssl.key-alias | 标识密钥存储区中的密钥的别名 |
| server.ssl.key-password | 用于访问密钥存储区中的密钥的密码 |
| server.ssl.key-store | 认为SSL证书的密钥存储路径（通常是 jks 文件） |
| server.ssl.key-store-password | 用于访问密钥库的密码 |
| server.ssl.key-store-provider | 密钥存储的提供者 |
| server.ssl.key-store-type | 密钥存储的类型 |
| server.ssl.protocol = TLS | SSL协议使用 |
| server.ssl.trust-store | 保存SSL证书的Trust存储 |
| server.ssl.trust-store-password | 用于访问信任存储的密码 |
| server.ssl.trust-store-provider | 信任存储的提供者 |
| server.ssl.trust-store-type | 信任存储的类型 |
| server.tomcat.accept-count | 所有可能的请求处理线程正在使用时，传入连接请求的最大队列长度 |
| server.tomcat.accesslog.buffered = true | 缓冲区输出，使其只被定期刷新 |
| server.tomcat.accesslog.directory = logs | 创建日志文件的目录可以相对于tomcat base dir或absolute |
| server.tomcat.accesslog.enabled = false | 启用访问日志 |
| server.tomcat.accesslog.file-date-format = .yyyy-MM-dd | 要在日志文件名中放置的日期格式 |
| server.tomcat.accesslog.pattern = common | 访问日志的格式模式 |
| server.tomcat.accesslog.prefix = access_log | 日志文件名前缀 |
| server.tomcat.accesslog.rename-on-rotate = false | 将文件名中的日期戳延迟到旋转时间 |
| server.tomcat.accesslog.request-attributes-enabled = false | 设置请求的IP地址，主机名，协议和端口的请求属性 |
| server.tomcat.accesslog.rotate = true | 启用访问日志轮换 |
| server.tomcat.accesslog.suffix = .log | 日志文件名后缀 |
| server.tomcat.additional-tld-skip-patterns | 匹配要忽略TLD扫描的jar的附加模式的逗号分隔列表 |
| server.tomcat.background-processor-delay = 30 | 在调用backgroundProcess方法之间以秒为单位的延迟 |
| server.tomcat.basedir | Tomcat基本目录。如果未指定，将使用临时目录 |
| server.tomcat.max-connections | 服务器在任何给定时间接受和处理的最大连接数 |
| server.tomcat.max-http-post-size = 0 | HTTP帖子内容的最大大小（以字节为单位） |
| server.tomcat.max-threads = 0 | 最大工作线程数 |
| server.tomcat.min-spare-threads = 0 | 最小工作线程数 |
| server.tomcat.port-header = X-Forwarded-Port | 用于覆盖原始端口值的HTTP头的名称 |
| server.tomcat.protocol-header | 保存传入协议的头,通常命名为“X-Forwarded-Proto” |
| server.tomcat.protocol-header-https-value = https | 指示传入请求使用SSL的协议头的值 |
| server.tomcat.redirect-context-root | 是否通过在路径上附加/重定向到上下文根的请求 |
| server.tomcat.remote-ip-header | 从中提取远程ip的HTTP头的名称。例如X-FORWARDED-FOR |
| server.tomcat.uri-encoding = UTF-8 | 用于解码URI的字符编码 |
| server.undertow.accesslog.dir | 访问日志目录 |
| server.undertow.accesslog.enabled = false | 启用访问日志 |
| server.undertow.accesslog.pattern = common | 访问日志的格式模式 |
| server.undertow.accesslog.prefix = access_log. | 日志文件名前缀 |
| server.undertow.accesslog.rotate = true | 启用访问日志轮换 |
| server.undertow.accesslog.suffix = log | 日志文件名后缀 |
| server.undertow.buffer-size | 每个缓冲区的大小（以字节为单位） |
| server.undertow.direct-buffers | 在Java堆之外分配缓冲区 |
| server.undertow.io-threads | 为工作者创建的I / O线程数 |
| server.undertow.max-http-post-size = 0 | HTTP帖子内容的最大大小（以字节为单位） |
| server.undertow.worker-threads | 工作线程数 |
