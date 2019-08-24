| 名称 | 描述 | 类型 | 默认值 | 可用值  | 重要性 |
| --- | --- | --- | --- | --- | --- |
| bootstrap.servers | 用于建立初始化到kafka服务器连接的主机／端口的列表。客记端将使用所有服务器，不论哪些服务器在这里是用来引导的。这个列表只影响用来发现所有服务器集合的初始化主机。这个列表应当是以下形式 host1:port1,host2:port2,....因为这些服务器只用来初始化连接到发现所有的集群成员（有可能动态改变），这个列表没有必要包括所有的服务器集合（你想要多于一个，尽管，以防一台服务器已经挂了）。 | 列表 |  |  | 高 |
| key.deserializer | 用于键的实现Deserializer接口的反系列化类 | 类 |  |  | 高 |
| value.deserializer | 用于值的实现Deserializer接口的反系列化类 | 类 |  |  | 高 |
| fetch.min.bytes | 服务器为每个读取请求返回的最小数据量。如果没有足够的数据可用，在响应请求之前请求会等待大量的数据积累。默认的设置为1字节意味着只要一个字节的数据可用或是读取请求在数据到达之前超时，读取请求就可以被响应。设置这个值比1大将导致服务器等待更大的数据积累，它可以很大的提高服务器的吞吐量，但是需要以额外的延时作为代价。 | 整型 | 1 | [0,...] | 高 |
| group.id | 一个惟一的字符，用来识别消费者所属的一个组。如果消费者通过订阅主题的方式使用组管理功能或是基于kafka偏移管理策略，那么这个属性是必须要设的。 | 字符 | "" |  | 高 |
| heartbeat.interval.ms | 使用组管理设施时，到消费者协调器的心跳之间的预期时间。心跳用于确保消费者的会话保持激活并且当一个新的消费者加入或离开组时促进重新平衡。这个值必须小于session.timeout.ms 的值，但通常应设置不高于该值的1/3 。为了正常的重新平衡它可以调整更低来控制预期时间。 | 整型 | 3000 |  | 高 |
| max.partition.fetch.bytes | 服务器返回的每个分区数据的最大数量。记录被消费者批量读取。如果获取的第一个非空分区中的第一个记录批大于此限制，则仍将返回批处理，以确保消费者能够取得进展。broker接受的最大记录批次通过message.max.bytes（broker配置）或是max.message.bytes (主题配置)。查看fetch.max.bytes来限制消费者请求大小。 | 整型 | 1048576 | [0,...] | 高 |
| session.timeout.ms | 在使用kafka组管理功能时用于检查消费者失败的超时时间。消费者发送周期性的心跳来指示其对broker的活跃度。如果在此会话超时之前没有心跳被broker接收，那么broker会将这个消费者从这个组中删除并初始化一个重平衡。注意这个值必须在允许的范围内，与在broker配置中用group.min.session.timeout.ms和group.max.session.timeout.ms设置的一样。 | 整型 | 10000 |  | 高 |
| ssl.key.password | 在密钥存储文件的私钥的密码。这是客户端可选的。 | 密文 | null |  | 高 |
| ssl.keystore.location | 密钥存储文件的位置。这是客户端的可选项，可用于客户端的双向身份认证。 | 字符 | null |  | 高 |
| ssl.keystore.password | 密钥库文件的密码。这个对客户端是可选的并且只在ssl.keystore.location被配置时需要。 | 密文 | null |  | 高 |
| ssl.truststore.location | 受信任证书库文件的位置。 | 字符 | null |  | 高 |
| ssl.truststore.password | 受信任证书库文件的密码。如果没有设置密码，那么信任存储区的访问仍然可用，但完整性检查被禁用。 | 密文 | null |  | 高 |
| auto.offset.reset | 当在kafka中没有初始化的偏移或当前的偏移不再存在（被删除）时该做什么： earliest:自动重置偏移到最早的偏移。latest:自动重置偏移到最新的偏移。none:抛出一个异常给消费者，如果消费者组找不到先前的偏移。anything else:抛出一个异常给消费者。  | 字符 | latest | [latest, earliest, none] | 中 |
| connections.max.idle.ms | 在这个配置的毫秒的数字之后会关闭空闲连接 | 长整型 | 540000 |  | 中 |
| enable.auto.commit | 如果设置为true，消费者的偏移会在后台周期性的被提交。 | 布尔 | TRUE |  | 中 |
| exclude.internal.topics | 来自内部主题的记录(例如offsets)是否应该暴露给消费者。如果设置为true，从一个内部的主题接收记录的惟一方式订阅它。 | 布尔 | TRUE |  | 中 |
| fetch.max.bytes | 服务器为每个读取请求返回的最大的数据量。记录被消费者按批次获取，如果获取的第一个非空分区中的第一个记录批大于这个值，任然将返回记录批次，以确保消费者能够取得进展。因此，这不是绝对最大值。被broker接受的最大记录批次大小通过message.max.bytes (broker 配置) 或 max.message.bytes (topic 配置)定义。注意消费者并行进行多个读取。 | 整型 | 52428800 | [0,...] | 中 |
| isolation.level | 控制着在事务下写入的消息是如何读取的。如果设置为read_committed, consumer.poll() 将会只返回被提交的事务性消息。如果被设置为read_uncommitted(默认), consumer.poll()将返回所有消息，甚至是已经退出事务的消息。无事务消息将会在任一模式无条件被返回。消息通常按偏移顺序被返回。在read_committed模式，consumer.poll()只将消息返回到最后一个稳定偏移量，它比第一个开启的事务中的偏移要少。特别的是，在属于正在进行的事务的消息之后出现的消息都会被拒绝直到相关的事务已经完成。 | 字符 | read_uncommitted | [read_committed, read_uncommitted] | 中 |
|  |  |  |  |  |  |
|  |  |  |  |  |  |
|  | 的消费  |  |  |  |  |
|  | 作为一个结果，当有正在进行的事务，设为 read_committed的消费者无法读到高水位。还有就是在read_committed模式时 seekToEnd方法会返回最后一个稳定偏移量。 |  |  |  |  |
| max.poll.interval.ms | 使用消费者分组管理时poll()调用之间的最大延时。这就让消费者在读取更多记录之前的空闲在时间上有了一个上限。如果这poll()没有在这个过期时间内调用，消费者被认为是失败的并且分组会重平衡来重新分配分区给另外一个成员。 | 整型 | 300000 | [1,...] | 中 |
| max.poll.records | 在一次poll()调用时返回的最大记录数量。 | 整型 | 500 | [1,...] | 中 |
| partition.assignment.strategy | 当分组管理被使用时，在消费者中客户端用于分配分区所有者的分区分配策略的类名。 | 列表 | class org.apache.kafka.clients.consumer.RangeAssignor |  | 中 |
| receive.buffer.bytes | 接收数据时TCP接收的缓存 (SO_RCVBUF) 的大小。如果这个值被设置为-1,操作系统的默认值会被使用。 | 整型 | 65536 | [-1,...] | 中 |
| request.timeout.ms | 这个配置控制客户端等待请求响应的最大时间。在超时时间消逝之前如果没有收到响应，客户端在有必要的情况下将重发请求或是在重试耗尽后把请求置为失败。 | 整型 | 305000 | [0,...] | 中 |
| sasl.jaas.config | JAAS（Java验证和授权API）配置文件使用的SASL（简单身份验证和安全层）连接的 JAAS登录上下文参数格式。JAAS配置文件格式在此被描述。这个格式的值为 ' (=)*;' | 密文 | null |  | 中 |
| sasl.kerberos.service.name |  | 字符 | null |  | 中 |
|  | kafka运行Kerberos的主名称。这个可以在Kafka的 JAAS中配置或是在Kafka的配置文件中运行。 |  |  |  |  |
| sasl.mechanism | 用于客户端连接的简单身份验证和安全层机置。这可能是任何机构的安全提供商提供的。默认为通用安全服务应用程序接口 | 字符 | GSSAPI |  | 中 |
| security.protocol | broker之间通信的协议，可用的值有：PLAINTEXT, SSL, SASL_PLAINTEXT, SASL_SSL. | 字符 | PLAINTEXT |  | 中 |
| send.buffer.bytes | 发送数据时TCP发送的缓存 (SO_SNDBUF) 的大小。如果这个值被设置为-1,操作系统的默认值会被使用。 | 整型 | 131072 | [-1,...] | 中 |
| ssl.enabled.protocols | SSL连接的可用协议列表。 | 列表 | TLSv1.2,TLSv1.1,TLSv1 |  | 中 |
| ssl.keystore.type | 密钥库文件的格式，这是客户端的可选项。 | 字符 | JKS |  | 中 |
| ssl.protocol | 用来创建SSLContext的SSL协议。默认的设置为TLS，可以适用于大多数场合。在目前的JVM中允许的值有TLS, TLSv1.1 和  TLSv1.2. SSL，SSLv2 和SSLv3在老的JVM中支持，但它们由于已知的安全漏洞而不鼓励被使用。 | 字符 | TLS |  | 中 |
| ssl.provider | 用于SSL连接的安全提供商的名称。默认值为JVM的默认安全提供商。 | 字符 | null |  | 中 |
| ssl.truststore.type | 受信任库文件的文件格式。 | 字符 | JKS |  | 中 |
| auto.commit.interval.ms | enable.auto.commit设置为true时，消费者偏移自动提交到kafka的以毫秒为单位的频率。 | 整型 | 5000 | [0,...] | 低 |
| check.crcs | 自动的消费记录的32位循环冗余校验。这个确保没有正在写的或是在磁盘上的数据没有损坏。这样的检查会增加一些开销，因此它可以在追求极限性能的情况下禁用。 | 布尔 | TRUE |  | 低 |
| client.id | 发送请求时传递给服务器的一个标识字符串。这样做的目的是能过追踪请求的来源除了除了IP/端口。它是通过允许一个逻辑应用名称被包括在一个服务器端的请求日志来实现的。 | 字符 | "" |  | 低 |
| fetch.max.wait.ms | 如果没有足够的数据马上满足fetch.min.bytes所要求的，在响应读取请求之前服务器将要阻塞的时间。 | 整型 | 500 | [0,...] | 低 |
| interceptor.classes | 用作拦截器的类的列表。实现ConsumerInterceptor 接口，在它们被发布到kafka集群之前，允许你拦截（可能修改）被消费者收到的记录。默认情况下是没有拦截器的。 | 列表 | null |  | 低 |
| metadata.max.age.ms | 我们强制刷新一个元数据后的毫秒时间段，即使我们没有看到任何分区领导者变为主动发现任何新的broker或分区。 | 长整型 | 300000 | [0,...] | 低 |
| metric.reporters | 用作度量报告者的类列表。实现了MetricReporter接口，允许加入会被通知到新的度量创建的类。JMX统计登记通常包括 JmxReporter | 列表 | "" |  | 低 |
| metrics.num.samples | 样品保持计算指标的数量。 | 整型 | 2 | [1,...] | 低 |
| metrics.recording.level | 度量的最高记录级别。 | 字符 | INFO | [INFO, DEBUG] | 低 |
| metrics.sample.window.ms | 一个度量样本计算的时间窗口。 | 长整型 | 30000 | [0,...] | 低 |
| reconnect.backoff.max.ms | 当一个重复的失败连接重复连接到brokert等待的以毫秒计的最大时间量。如果已提供，每个主机的回退会因为连续的连接失败而指数级的增长，直到达到这个最大值。在计算回退增长后，20%的随机抖动被添加来避免连接风暴。 | 长整型 | 1000 | [0,...] | 低 |
| reconnect.backoff.ms | 尝试重新连接到一个给定的主机之前等待的最少时间。这避免了在一个密环里重复连接到一个主机。这个后退适用于客户端连接到broker所有尝试连接。 | 长整型 | 50 | [0,...] | 低 |
| retry.backoff.ms | 尝试重试请求到一个给定的主题分区之前等待的时间。这个避免在某些失败场景下的紧密循环中重复发送请求。 | 长整型 | 100 | [0,...] | 低 |
| sasl.kerberos.kinit.cmd | Kerberos kinit 命令路径. | 字符 | /usr/bin/kinit |  | 低 |
| sasl.kerberos.min.time.before.relogin | 刷新尝试之间的线程休眠时间。 | 长整型 | 60000 |  | 低 |
| sasl.kerberos.ticket.renew.jitter | 添加到更新时间的随机抖动的百分比。 | 双精度 | 0.05 |  | 低 |
| sasl.kerberos.ticket.renew.window.factor | 登录线程将休眠，直到从最后刷新到票证到期的指定的时间窗口因子到达，此时它将尝试续订该票证。 | 双精度 | 0.8 |  | 低 |
| ssl.cipher.suites | 加密套件列表。这是一个由认证，加密，MAC和用于协商使用TLS或SSL网络协议的网络连接的安全设置的密钥交换算法组合成的名称。 | list | null |  | 低 |
| ssl.endpoint.identification.algorithm | 使用服务器证书验证服务器主机名的端识别算法。 | string | null |  | 低 |
| ssl.keymanager.algorithm | 用于SSL连接的密钥管理工厂算法。默认情况下这个值是JVM中配置的用于SSL连接的密钥管理工厂算法 | string | SunX509 |  | 低 |
| ssl.secure.random.implementation | 用于SSL加密操作的SecureRandom的伪随机数产生算法。 | string | null |  | 低 |
| ssl.trustmanager.algorithm | 用于SSL连接的受信任管理器工厂算法。默认值是JVM中配置的用于SSL连接的受信任管理器工厂算法。 | string | PKIX |  | 低 |
