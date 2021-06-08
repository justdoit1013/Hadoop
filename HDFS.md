## HDFS

![图片](https://user-images.githubusercontent.com/39020574/121199254-5f5cac00-c8a5-11eb-9435-147adf238c52.png)
### NameNode

- 中央服务器，**元数据**的仲裁和管理（文件路径信息）
- 负责管理**文件系统**的命名空间以及**客户端对文件的访问**
- 管理数据块到DataNode的映射
- 处理客户端读写请求
- 副本配置策略

### DataNode

- 存储实际的数据块

- 执行数据端的读写操作

### Seondary Namenode

- 辅助NameNode，分担部分工作
- 紧急情况下,辅助恢复NameNode
- 并非NameNode的热备份

### Client客户端

- 文件切分——Blocks
- 与NameNode交互，获取文件位置信息
- 与DataNode交互，读入或写入数据
- 提供一些开关HDFS命令


![图片](https://user-images.githubusercontent.com/39020574/121199317-697eaa80-c8a5-11eb-84a7-76eb27f11d00.png)

### NameNode作用

- 在内存中保存整个文件系统的**名称空间**和文件数据块的地址映射
- 整个HDFS可存储的文件数受限于**NameNode的内存大小**

1.元数据信息：文件名、文件目录结构、文件属性、每个文件块列表以及列表中块与块所在的DataNode之间的映射关系，数据会定期持久化到本地磁盘的fsImage文件和edits文件中

2.文件操作：DataNode负责文件内容的读写请求，数据流不经过NameNode。

3.副本机制：文件存在哪些DataNode上是由NameNode上决定的。

4.心跳机制：DataNode周期性向NameNode发送心跳信号和块状态报告

### DataNode作用

提供真实文件数据的存储服务

1.DataNode以数据块形式存储HDFS文件

2.DataNode响应HDFS客户端**读写请求**

3.DataNode周期性向NameNode汇报**心跳信息、数据块信息、缓存数据块信息**



### HDFS副本机制和机架感知

- **配置文件：hdfs-site.xml**

- 文件切片大小设置：默认128M

- 文件切片副本数：一个Block默认副本值为3

- **机架感知Rack—数据备份**

![图片](https://user-images.githubusercontent.com/39020574/121199381-769b9980-c8a5-11eb-8960-9e26b38f895c.png)

