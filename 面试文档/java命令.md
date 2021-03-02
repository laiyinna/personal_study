#### java命令

​	**1、jps命令：**显示当前所有java进程pid的命令(pid：进程ID)，命令格式：jps [ options ] [ hostid ]

​		无参数时只显示进程id和类名称。jps 支持查看远程服务上的 jvm 进程信息。如果需要查看其他机器上的 jvm 进程，需要在待查看机器上启动 jstatd 服务。

​		参数说明：-p：只显示pid，不显示class名称，jar文件名和传递给main方法的参数；

​				  -m：输出传递给main方法的参数，在嵌入式jvm上可能是null；

​				  -l：输出完全的包名，应用主类名，jar的完全路径名；

​				  -v：输出传递给JVM的参数；

​				  -V：输出通过flag文件传递到JVM中的参数。

​	**2、jcmd命令：**在JDK 1.7之后，新增了一个命令行工具jcmd。它是一个多功能工具，能够用来导出堆，查看java进程，导出线程信息。运行GC等。jcmd拥有jmap的大部分功能，而且Oracle官方也建议使用jcmd取代jmap

​		参数说明：-l：表示列出全部java虚拟机，针对每个虚拟机，可以使用help命令列出该虚拟机支持的全部命令，例：jcmd -l ：列出全部java虚拟机；

​		使用说明：jcmd pid help：查看支持的命令；

​				  jcdm pid VM.uptime：查看虚拟机启动时间；

​				  jcmd pid Thread.print：打印线程栈信息；

​				  jcmd pid GC.class_histogram：查看系统中类统计信息；

​				  jcmd pid GC.heap_dump：导出堆信息；

​				  jcmd pid VM.system_properties：获取系统Properties内容；

​				  jcmd pid VM.flags：获取启动參数；

​				  jcmd pid PerfCounter.print：获取全部性能相关数据；

​	**3、jstack命令：**jstack用于打印出给定的java进程ID或core file或远程调试服务的Java堆栈信息，详解见：https://blog.csdn.net/zhaozheng7758/article/details/8623549

​	**4、jvisualvm命令：**打开**jvisualvm.exe**文件，用来监控内存泄露，跟踪垃圾回收，执行时内存、cpu分析，线程分析。与jconsole类似。jconsole中有死锁检测。