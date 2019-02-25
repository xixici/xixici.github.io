---
title: Spark集群搭建教程 in Ubuntu 14.04
date: 2016-07-18 11:29:32
tags: Hadoop Spark
categories: 学习笔记
---
## 基本环境总览-及下载链接
[VMware 12.1.1](http://www.zdfans.com/5928.html)
[Ubuntu 14.04](http://www.ubuntu.com/download/desktop)
[JAVA 1.8.0](http://www.oracle.com/technetwork/java/javase/downloads/index-jsp-138363.html)
[Hadoop 2.7.2](http://hadoop.apache.org/releases.html#Download)
[Spark 1.6.2](http://spark.apache.org/downloads.html)
[SCALA 2.10.6](http://www.scala-lang.org/download/)
[ideaIC-2016.2](http://www.jetbrains.com/idea/download/)
[scala-intellij-bin-2016.2.1](http://plugins.jetbrains.com/plugin/?idea&id=1347)
**文末有网盘提供本文环境下载**
## VMtools安装
- VMware菜单-虚拟机-安装VMtools
- 解压tar.gz
- teminal中执行./vmware-install.pl
- 重启虚拟机系统
---------------------------------------------------------------------
## Hadoop 2.7.2 in Ubuntu 14.04 LTS 配置开始##

## Ubuntu开启root账户登录
- vim 安装 可以用gedit代替
``` 
sudo apt-get install vim 
```
- Ubuntu14.04桌面环境目录
``` 
sudo gedit /usr/share/lightdm/lightdm.conf.d/50-unity-greeter.conf
```
- 桌面环境设置如下 开启root账户
```
[SeatDefaults]
greeter-session=unity-greeter
user-session=ubuntu
greeter-show-manual-login=true
allow-guest=false
- 启用root账号
sudo passwd root 
```

## SSH实现无密码登录
- ssh通讯安装
```
sudo apt-get install ssh
```
- ssh启动
```
/etc/init.d/ssh start
```
- ssh状态
```
ps -e |grep ssh
```
- 生成公钥 私钥
```
ssh-keygen -t rsa -P ""
```
- 公钥添加授权
```
cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys 
```
- 登入
```
ssh localhost
```
- 登出
```
exit 
```

<!--more-->

- 更改hosts 与hostname
- 查看IP
```
ifconfig
```
- 编辑hostname
```
vim /etc/hostname # 用gedit也可
i #更改为主机名SparkMaster SparkWorker1 SparkWorker2
shift+zz 保存退出 
```
- 更改hosts
```
vim /etc/hosts
i #更改IP及对应主机名字
shift+zz 保存退出 
```
- 公钥添加至授权
```
scp传输 方法失效，通过拷贝即可
cd /root/.ssh/将slave的密钥传到Master上
scp id_rsa.pub  root@SparkMaster:/root/.ssh/id_rsa.pub.SparkWorker1 
scp id_rsa.pub  root@SparkMaster:/root/.ssh/id_rsa.pub.SparkWorker2
cat ~/.ssh/id_rsa.pub.SparkWorker1 >> ~/.ssh/authorized_keys 
cat ~/.ssh/id_rsa.pub.SparkWorker2 >> ~/.ssh/authorized_keys 
```

这样我们的authorized_keys就有了三台主机的密钥,将authorized_keys分别复制到另外两台电脑对应目录下

## Java环境安装1.8.0
- 下载安装Java
```
mkdir /usr/lib/java
mv /root/.... /usr/lib/java
tar -xvf jdk-....
```
- 修改JAVA环境配置使生效1.8.0
```
gedit ~/.bashrc
export JAVA_HOME=/usr/lib/java/jdk1.8.0_91
export JRE_HOME=${JAVA_HOME}/jre
export CLASS_PATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib
export PATH=${JAVA_HOME}/bin:$PATH
- 使bashrc生效
source ~/.bashrc```
## Hadoop环境安装2.7.2
- 下载安装Hadoop
```
mkdir /usr/lib/hadoop
tar -xvf hadoop-....
```
- 修改Hadoop环境配置使生效2.7.2
```
gedit ~/.bashrc
export JAVA_HOME=/usr/lib/java/jdk1.8.0_91
export JRE_HOME=${JAVA_HOME}/jre
export CLASS_PATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib
export PATH=${JAVA_HOME}/bin:/usr/lib/hadoop/hadoop-2.7.2/bin:$PATH 
- 使bashrc生效
source ~/.bashrc```

- hadoop 版本
`hadoop version`
- 更改hadoop三个文件的java环境
```
cd /usr/lib/hadoop/hadoop-2.7.2/etc/hadoop
gedit hadoop-env.sh # 修改如下
export JAVA_HOME=/usr/lib/java/jdk1.8.0_91 
gedit yarn-env.sh # 修改如下
export JAVA_HOME=/usr/lib/java/jdk1.8.0_91
gedit mapred-env.sh # 修改如下
export JAVA_HOME=/usr/lib/java/jdk1.8.0_91 ```
- 更改slaves 为2个子节
```
gedit slaves #SparkWorker1 Sparkworker2
```
- 更改三个xml文件
```
cd /usr/lib/hadoop/hadoop-2.7.2/etc/hadoop
```
- 更改site.xml文件
```
<configuration>
    <property>
    <name>fs.defaultFS</name>
    <value>hdfs://SparkMaster:9000/</value>
    <description>The name of default file system</description>
    </property>  
    <property>  
    <name>hadoop.tmp.dir</name>
    <value>/usr/lib/hadoop/hadoop-2.7.2/tmp</value>
    <description>A base for other temporary directories</description>
    </property>  
</configuration>
```
- 更改dfs.xml文件
```
<configuration>
    <property>
    <name>dfs.replication</name>
    <value>2</value>
    </property>  
    <property>  
    <name>dfs.namenode.name.dir</name>
    <value>/usr/lib/hadoop/hadoop-2.7.2/dfs/name</value>
    </property>  
    <property>  
    <name>dfs.datanode.name.dir</name>
    <value>/usr/lib/hadoop/hadoop-2.7.2/dfs/data</value>
    </property>  
</configuration>
```
- 更改mapred.xml文件
```
<configuration>
    <property>
    <name>mapreduce.framework.name</name>
    <value>yarn</value>
    </property>  
</configuration>
```
- 更改yarn.xml文件
```
<configuration>
    <property>
    <name>yarn.resourcemanager.hostname</name>
    <value>SparkMaster</value>
    </property>  
    <property>
    <name>yarn.nodemanager.aux-services</name>
    <value>mapreduce_shuffle</value>
    </property>  
</configuration>
```
- scp 传输环境到节点机器
```
scp -r hadoop/ root@SparkWorker1:/usr/lib/
scp -r java/ root@SparkWorker1:/usr/lib/
scp -r hadoop/ root@SparkWorker2:/usr/lib/
scp -r java/ root@SparkWorker2:/usr/lib/
```
- 编辑bashrc
```
gedit ~/.bashrc
export JAVA_HOME=/usr/lib/java/jdk1.8.0_91
export JRE_HOME=${JAVA_HOME}/jre
export CLASS_PATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib
export PATH=${JAVA_HOME}/bin:/usr/lib/hadoop/hadoop-2.7.2/bin:$PATH 
- 使bashrc生效
source ~/.bashrc```
- 格式化hdfs系统
```
cd /usr/lib/hadoop/hadoop-2.7.2/sbin
hadoop namenode -format ```
- 启动hdfs系统
```
./start-dfs.sh 
htttp://SparkMaster:50070 # HDFS集群 ```
- 启动yarn集群
```
./start-yarn.sh
http://SparkMaster:8088 #ResourceManager状态
http://SparkWorker1:8042 #NodeManager状态
http://SparkWorker1:8042 #NodeManager状态
```
- 历史服务
```
./mr-jobhistory-daemon.sh start historyserver #历史服务
http://SparkMaster:19888 #ResourceManager状态
./mr-jobhistory-daemon.sh stop historyserver #停止
```

- slave无法启动nodemanager可以删除data文件夹 
```
usr/lib/hadoop/tmp/dfs/  -ls
rm -r /data/
```
## Hadoop实例测试
- 建立输入输出文件夹
```
hadoop fs -mkdir -p /data/wordcount
hadoop fs -mkdir -p /output/
```
- 复制所需文件到输入文件夹
```
hadoop fs -put ../etc/haddop/#.xml /data/wordcount/
```
- 执行wordcount 的mapreduce命令
```
hadoop jar ../share/hadoop//mapreduce/hadoop-mapreduce-examples-2.7.2.jar wordcount /data/wordcount/hadoop /output/wordcount2
```
- 可以查看个文件夹及文件
```
http://sparkmaster:50070/explorer.html#/
```

** hadoop 配置完毕 运行实例成功 **

---------------------------------------------------------------------------------------------

** Spark 1.6.2 SCALA 2.10.6 配置开始 **

## SPARK SCALA环境配置
- Spark环境安装1.6.2
```
mkdir /usr/lib/spark
tar -xvf spark-....
```
- Scala环境安装2.10.6
```
mkdir /usr/lib/scala
tar -xvf scala-....
```
- Spark Scala配置
```
gedit ~/.bashrc
# SCALA 配置
export JAVA_HOME=/usr/lib/java/jdk1.8.0_91
export JRE_HOME=${JAVA_HOME}/jre
export SCALA_HOME=/usr/lib/scala/scala-2.10.6
export CLASS_PATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib
export PATH=${SCALA_HOME}/bin:${JAVA_HOME}/bin:/usr/lib/hadoop/hadoop-2.7.2/bin:$PATH
# SPARK 配置
export JAVA_HOME=/usr/lib/java/jdk1.8.0_91
export JRE_HOME=${JAVA_HOME}/jre
export SCALA_HOME=/usr/lib/scala/scala-2.10.6
export SPARK_HOME=/usr/lib/spark/spark-1.6.2-bin-hadoop2.6
export CLASS_PATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib
export PATH=${SPARK_HOME}/lib:${SCALA_HOME}/bin:${JAVA_HOME}/bin:/usr/lib/hadoop/hadoop-2.7.2/bin:$PATH
- 使bashrc生效
source ~/.bashrc
```
- Spark-env.sh slave 配置
```
cp spark-env.sh.template spark-env.sh
cp slave.template slave
gedit spark-env.sh
gedit slave
```
- 追加spark-env.sh信息
```
export JAVA_HOME=/usr/lib/java/jdk1.8.0_91
export SCALA_HOME=/usr/lib/scala/scala-2.10.6
export SPARK_MASTER_IP=192.168.204.130
export SPARK_WORKER_MEMORY=2g
export HADOOP_CONF_DIR=/usr/lib/hadoop/hadoop-2.7.2/conf
```
- 修改slave
```
SparkMaster
SparkWorker1
SparkWorker2
```
- 传输 SCALA 和 SPARK
```
scp -r /usr/lib/spark/ root@SparkWorker1:/usr/lib/
scp -r /usr/lib/spark/ root@SparkWorker2:/usr/lib/
scp -r /usr/lib/scala/ root@SparkWorker1:/usr/lib/
scp -r /usr/lib/scala/ root@SparkWorker2:/usr/lib/
```
- 启动spark
```
cd /usr/lib/spark/spark-1.6.2-bin-hadoop2.6/sbin# 
./start-all.sh 
```
- 观察Spark
```
http://sparkmaster:8080/
```
- 启动spark-shell
```
cd /usr/lib/spark/spark-1.6.2-bin-hadoop2.6/bin# 
./spark-shell
```
- 观察Spark-shell
```
http://sparkmaster:4040/
```
## SPARK测试
- 切换目录
```
cd /usr/lib/spark/spark-1.6.2-bin-hadoop2.6
```
- 将README.md 上传至data
```
hadoop fs -put README.md /data/
```
- 启动Spark shell 时间要用12 Min
```
MASTER=spark://SparkMaster:7077 ./spark-shell
```
- 读取README.md 做如下处理
```
val file = sc.textFile("hdfs://SparkMaster:9000/data/README.md")
val count = file.flatMap(line => line.split(" ")).map(word => (word, 1)).reduceByKey(_+_)
count collect
```
** SPARK SCALA 配置完毕 运行实例成功 **

## IDEA 安装测试

- 创建文件夹
```
mkdir /usr/local/idea
```
- 拷贝至文件夹
```
cp /root/ideaIC-2016.2.tar.gz /usr/local/idea/
```
- 切换至目录并解压
```
cd /usr/local/idea/
tzr -xvf ideaIC-2016.2.tar.gz
```
- 为方便是用bin下命令,将其配置在`~/.bashrc`的`PATH`里.下面就是截止目前为止的所有环境配置.
```
export JAVA_HOME=/usr/lib/java/jdk1.8.0_91
export JRE_HOME=${JAVA_HOME}/jre
export SCALA_HOME=/usr/lib/scala/scala-2.10.6
export SPARK_HOME=/usr/lib/spark/spark-1.6.2-bin-hadoop2.6
export CLASS_PATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib
export PATH=/usr/local/idea/idea-IC-162.1121.32/bin:${SPARK_HOME}/lib:${SCALA_HOME}/bin:${JAVA_HOME}/bin:/usr/lib/hadoop/hadoop-2.7.2/bin:$PATH
- 使bashrc生效
source ~/.bashrc
```
- 打开IDEA
```
cd /usr/local/idea/idea-IC-162.1121.32/bin
idea.sh
```

- 安装SCALA插件plugins
- 在线安装
`欢迎界面`-`右下角configuration`-`左下角Install JetBrains`-`搜索scala`-`install即可`
- 离线安装
`欢迎界面`-`右下角configuration`-`下方Install plugins from disk`-`选择安装`

- 创建项目
`Create New Project`-`Scala-SBT`-`name-location-SDK(选择JAVA路径)-SBT-SCALA`-`Finash`
由于要自动完成SBT工具的安装,用时较长,本人用时30min以上.



## 资料提供
链接: [http://pan.baidu.com/s/1slQpli1](http://pan.baidu.com/s/1slQpli1)
密码: ####请打赏索要.

## 环境提供
链接: [http://pan.baidu.com/s/1bpcDkxL](http://pan.baidu.com/s/1bpcDkxL) 
密码: ####请打赏索要.

---------------------------------------------------------

{% cq %}
## 友情提示,如有帮助,文章底下有打赏按键.
{% endcq %}