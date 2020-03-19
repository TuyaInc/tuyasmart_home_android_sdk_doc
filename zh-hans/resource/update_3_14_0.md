# 升级指南

如果你已经集成了之前的版本，要升级到 3.14.x 版本请参照如下步骤：

更新 tuyasmart 库的版本为 3.14.x 对应的版本

1. 移除 paho mqtt 库的依赖

	```groovy
	implementation 'org.eclipse.paho:org.eclipse.paho.client.mqttv3:1.2.0'
	```

![image-20200113142931719](images/image-20200113142931719.png)

2. 移除 paho 库的混淆规则

	```
	-keep class org.eclipse.paho.client.mqttv3.** { *; }
	-dontwarn org.eclipse.paho.client.mqttv3.**
	```

	![image-20200113143040062](images/image-20200113143040062.png)

3. 新增混淆规则

	```
	#mqtt
	-keep class com.tuya.smart.mqttclient.mqttv3.** { *; }
	-dontwarn com.tuya.smart.mqttclient.mqttv3.**
	```

	