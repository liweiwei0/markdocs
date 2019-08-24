# <p align='center'>jmap</p>
## 简介
jdk安装后会自带一些小工具，jmap命令(Java Memory Map)是其中之一。主要用于打印指定Java进程(或核心文件、远程调试服务器)的共享对象内存映射或堆内存细节。

jmap命令可以获得运行中的jvm的堆的快照，从而可以离线分析堆，以检查内存泄漏，检查一些严重影响性能的大对象的创建，检查系统中什么对象最多，各种对象所占内存的大小等等。可以使用jmap生成Heap Dump。 

java memory = direct memory（直接内存） + jvm memory(MaxPermSize +Xmx)

## 命令
### Usage:
    jmap [option] <pid>
        (to connect to running process)
    jmap [option] <executable <core>
        (to connect to a core file)
    jmap [option] [server_id@]<remote server IP or hostname>
        (to connect to remote debug server)

### where <option> is one of:
    <none>               to print same info as Solaris pmap
    -heap                to print java heap summary
    -histo[:live]        to print histogram of java object heap; if the "live"
                         suboption is specified, only count live objects
    -clstats             to print class loader statistics
    -finalizerinfo       to print information on objects awaiting finalization
    -dump:<dump-options> to dump java heap in hprof binary format
                         dump-options:
                           live         dump only live objects; if not specified, all objects in the heap are dumped.
                           format=b     binary format
                           file=<file>  dump heap to <file>
                         Example: jmap -dump:live,format=b,file=heap.bin <pid>
    -F                   force. Use with -dump:<dump-options> <pid> or -histo to force a heap dump or histogram when <pid> does not respond. The "live" suboption is not supported in this mode.
    -h | -help           to print this help message
    -J<flag>             to pass <flag> directly to the runtime system
    
### 参数如下：  
-heap：打印jvm heap的情况  
-histo：打印jvm heap的直方图。其输出信息包括类名，对象数量，对象占用大小。  
-histo：live ：同上，但是只答应存活对象的情况  
-permstat：打印permanent generation heap情况  