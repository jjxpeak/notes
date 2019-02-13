# Jmeter 并发测试
- - - -
* **前提：**
1.  所有设备在同一网段
2. jmeter版本统一
3. 关闭防火墙
4. 一台电脑做master 其他电脑做slave
- - - -
* **配置：**
1. master：
```
修改配置文件 jmeter.properties 
# Remote Hosts - comma delimited
remote_hosts=改为slave的ip:prot(多个已,分割)
-----------------------------------------------
# Set this if you don't want to use SSL for RMI
server.rmi.ssl.disable=true
```
修改这两个地方
2. slave配置
```
修改配置文件 jmeter.properties 
-----------------------------------------------
# Set this if you don't want to use SSL for RMI
server.rmi.ssl.disable=true

创建环境变量
------------------------------------------------
JMETER_HOME=/Users/peak/Downloads/apache-jmeter-5.0

修改jmeter-server(linux) 约30行
# One way to fix this is to define RMI_HOST_DEF below
#RMI_HOST_DEF='-Djava.rmi.server.hostname=xxx.xxx.xxx.xxx 改为slave ip'

修改jmeter-server.bat(win) 约57行
rem On NT/2K grab all arguments at once
set JMETER_CMD_LINE_ARGS="-Djava.rmi.server.hostname=xxx.xxx.xxx.xxx 改为slave ip"
```
- - - -
* 使用
```
命令行
./jmeter -n -t plan.jmx -R slaveIp_1:port,slaveIp_2:port -l newfile.jtl -e -o html_folder
UI
./jmeter 启动
创建计划脚本/打开计划脚本
点击Run->Remote Start-> slaveIp:prot(单个运行配置文件中配置的slave)
点击Run->Remote Start All (运行所有slave)
```


