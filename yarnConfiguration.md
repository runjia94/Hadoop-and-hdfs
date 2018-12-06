#yarn configuration
**1. 配置/mnt/home/5365100/hadoop-2.7.6/etc/hadoop/yarn-site.xml**
```
<configuration>
    <property>
        <name>yarn.resourcemanager.webapp.address</name>
        <value>bigdata0.novalocal:8088</value>
    </property>
    <property>
        <name>yarn.resourcemanager.hostname</name>
        <value>bigdata0.novalocal</value>
    </property>

    <property>
        <name>yarn.nodemanager.log-dirs</name>
        <value>/mnt/home/5365100/yarn/0/logs,/mnt/home/5365100/yarn/1/logs,/mnt/home/5365100/yarn/2/logs</value>
    </property>

    <property>
        <name>yarn.nodemanager.local-dirs</name>
        <value>/mnt/home/5365100/yarn/0/local,/mnt/home/5365100/yarn/1/local,/mnt/home/5365100/yarn/2/local</value>
    </property>
    <property>
        <name>yarn.nodemanager.aux-services</name>
        <value>mapreduce_shuffle</value>
    </property>
</configuration>
```

**2. 配置/mnt/home/5365100/hadoop-2.7.6/etc/hadoop/mapred-site.xml(这个文件一开始不存在，自己手动创建就行)**
```
<?xml version="1.0"?>
<?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
<configuration>
    <property>
        <name>mapreduce.framework.name</name>
        <value>yarn</value>
    </property>
    <property>
        <name>mapreduce.jobhistory.address</name>
        <value>bigdata0.novalocal:10020</value>
    </property>
    <property>
        <name>mapreduce.jobhistory.webapp.address</name>
        <value>bigdata0.novalocal:19888</value>
    </property>
</configuration>
```

**3. 启动resourcemanager**
```bash
yarn resourcemanager
```
-后台启动resourcemanager的方法：
```bash
hadoop-current/sbin/yarn-daemon.sh start resourcemanager
```
**4. 同样的方法，配置bigdata1, bigdata2, bigdata3几台机器，注意这里没有配置bigdata4，可能bigdata4用于其他特殊用途把，之前的HDFS也没有配置bigdata4。**
**5.启动nodemanager**
```bash
yarn nodemanager
```
-后台启动nodemanager的方法：
```bash
hadoop-current/sbin/yarn-daemon.sh start nodemanager
```
**6.运行yarn示例（注意要把HDFSdatanode打开）**
```bash
hadoop jar hadoop-current/share/hadoop/mapreduce/hadoop-mapreduce-examples-2.7.6.jar pi 5 10
```
