# 使用Zabbix监控Android设备
[toc]

## 0. 测试环境信息

测试机 android box

测试zbx server 10.xxx.xxx.221


## 1. 概述
    1. 使用非官方android agent，经安全部门逆向分析可内网使用。
    2. android设备数量比较大，可以考虑部署proxy或使用主动模式减少对zabbix server的压力。
    3. 我们可以监控如下内容：  
        - CPU负载，架构，核数   
        - 内存剩余量，总量  
        - 存储剩余量，总量  
        - GPS位置（需要设备有GPS芯片且android权限开放）   
        - 电源状态，电池容量     
        - 网络出入流量  
        - Android版本   
        - ....
    4. 每次修改配置需要重启代理服务。
    5. 有错发生软件下部会报错，有助排错。
    6. 个别设备需要设置此应用后台永久运行。


## 2. 非官方android agent
![image](https://res.cloudinary.com/liz/image/upload/v1543398044/Android-devices-monitoring-with-Zabbix/01.jpg)

可以从Google Play商店免费下载和安装该应用（需要梯子）：   
https://play.google.com/store/apps/details?id=fr.damongeot.zabbixagent&hl=es  

或通过第三方APK下载工具下载如：  
https://apkpure.com/cn/store/apps/details?id=fr.damongeot.zabbixagent


## 3. agent端配置
![image](https://res.cloudinary.com/liz/image/upload/v1543397973/Android-devices-monitoring-with-Zabbix/002.jpg)
![image](https://res.cloudinary.com/liz/image/upload/v1543397974/Android-devices-monitoring-with-Zabbix/003.jpg)

#### Service online 
启动和关闭代理，中开启（ON）/关闭（OFF）  

#### Settings
被动模式选项
|选项          |值                 |说明  
|---           |---                |---  
|Start at boot |勾选               |开机启动  
|Port          | 10050             |被动模式监听端口  
|Comma .....   | zabbix server IP  |zabbix服务器IP   

自定义key选项  
|选项  |值     |说明  
|---   |---    |---  
|View  |自定义 |根据自己需求可以定制key  

主动模式选项  
|选项                 |值                |说明  
|---                  |---               |---  
|Enable actice checks |勾选              |开启主动模式  
|Server host/ip       |zabbix server IP  |zabbix服务器IP  
|Server port          |10051             | zabbix server主动模式端口  
|Agent hostname       |自定义            |需要与前端配置一致，区分大小写  

#### IP(s) of this device
这台设备的本地IP，IPv4和IPv6，无网络时无信息

## 4. zabbix 前端操作
#### 1). 导入zabbix agent模板
具体操作参见zabbix官方文档

#### 2). 导入android模板  
具体操作参见zabbix官方文档


## 5. “最新数据”展示
![image](https://res.cloudinary.com/liz/image/upload/v1543397976/Android-devices-monitoring-with-Zabbix/04.jpg)


## 6. 参考资料
模板下载  
https://github.com/muutech/zabbix-templates/tree/master/ANDROID

模板导入/导出  
https://www.zabbix.com/documentation/3.4/zh/manual/xml_export_import/templates
