# Hadoop and HBase learning notes

## Hadoop 异常处理:  java.io.IOException: Inconsistent checkpoint fields

每次格式化namenode都会生成一个新的clusterID, 如果只格式化了namenode，没有格式化此datanode， 就会出现`java.io.IOException: Incompatible namespaceIDs`异常。  

这里有 2 种解决方案

* 删除 旧的clusterID(tmp/hadoop-hadoop/dfs/namesecondary), 然后重新格式化自动生成新的
* 修改secondarynamenode 的 clusterID , 使其一致

这里选择 第一种, 步骤如下

* 停止 yarn: sbin/stop-yarn.sh
* 停止 dfs: sbin/stop-dfs.sh
* 删除 dfs/namesecondary 目录下的 current 目录
* 格式化 namenode: bin/hdfs namenode -format
* 启动 dfs: sbin/start-dfs.sh
* 启动 yarn: sbin/start-yarn.sh

 [hadoop异常：Inconsistent checkpoint fields](https://blog.csdn.net/weixin_42316741/article/details/81809251)  
[secondnmaenode中错误：“Inconsistent checkpoint fields”的解决方案](https://blog.csdn.net/mr_zhang2014/article/details/78741971)
