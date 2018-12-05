HDFS CONFIGURATION
_____________________

1. 拷贝/home/hadoop/hadoop-2.7.6.tar.gz到自己的目录(以下操作都是在当前用户的家目录下进行操作的!)：
```bash
cp /home/hadoop/hadoop-2.7.6.tar.gz ~/
```
2. 解压
```bash
tar xzvf hadoop-2.7.6.tar.gz
```
3. 创建一个指向当前使用的hadoop的软连接，之所以要创建是为了以后在多版本hadoop共存时，方便知道自己使用的是哪个版本的hadoop，不至于混淆

```bash
ln -s hadoop-2.7.6 hadoop-current
```

4. 更改变量环境

在/mnt/home/5365100目录下输入 
```
vi ~/.bashrc
```
然后再在文件中添加下面一行指令
```bash
export PATH=/mnt/home/5365100/hadoop-current/bin:$PATH
```
保存后在命令行中输入，使 bashrc 生效
```bash
source ~/.bashrc
```

5. 更改hadoop中java的路径， 进入mnt/home/5365100/hadoop-2.7.6/etc/hadoop,命令行输入
```
vi hadoop-env.sh
```
然后更改java home的环境变量,在 the java implement to use下添加
```bash
export JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk
```
然后执行 hadoop， 可以运行则证明成功

6. 修改core-site.xml 文件
```
<configuration>
        <property>
                <name>fs.defaultFS</name>
                <value>hdfs://bigdata0:33586</value>
        </property>
</configuration>
```

7. 修改hdfs-site.xml文件。 首先在/mnt/home/5365100目录下输入 
```bash
mkdir name
mkdir -p data/{0..2}
```
这样此目录下会有一个 name文件夹和一个data文件夹，data文件夹中会有名字分别为 0， 1， 2的子文件夹

然后打开 hdfs-site.xml文件
```
<property>
                <name>dfs.namenode.rpc-address</name>
                <value>bigdata0:33586</value>
        </property>     
       <property>
                <name>dfs.namenode.http-address</name>
                <value>bigdata0:33587</value>
        </property>    

        <property>
                <name>dfs.datanode.address</name>
                <value>bigdata0:33588</value>
        </property>    
        <property>
                <name>dfs.datanode.http.address</name>
                <value>bigdata0:33589</value>
        </property>    
        <property>
                <name>dfs.datanode.ipc.address</name>
                <value>bigdata0:33590</value>
        </property>    
        <property>
                <name>dfs.namenode.name.dir</name>
                <value>/mnt/home/5365100/name</value>
        </property>    
      
        <property>
                <name>dfs.datanode.data.dir</name>
                <value>/mnt/home/5365100/data/0,/mnt/home/5365100/data/1,/mnt/home/5365100/data/2</value>
        </property>    
```
8. 初次启动hdfs，需要先格式化一下
```bash
hdfs namenode -format
```
9. 启动namenode
```bash
hdfs namenode
```
10. 在浏览器中输入 http.address的端口号
10.173.32.5:33587

11. 启动datanode
```bash
hdfs datanode
```
12. 配置其他远程主机的Hadoop环境，与bigdata0配置流程一样，注意把hdfs-site.xml中的datanode相关字段的bigdata0换成相应的bigdata1、bigdata2、bigdata3、bigdata4即可，namenode相关的value不用改变，因为namenode用的都是bigdata0上的namenode。




