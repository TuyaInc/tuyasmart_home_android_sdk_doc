# 蓝牙第一节——涂鸦蓝牙简介
## 涂鸦蓝牙体系简介
涂鸦蓝牙有三条技术线路。蓝牙设备与手机一对一相连的蓝牙单点设备 **SingleBLE**，涂鸦自研的蓝牙拓扑通信 **TuyaMesh** 和蓝牙技术联盟发布的蓝牙拓扑通信 **SigMesh**。除了以上三种之外，还有一些多协议设备也会使用到蓝牙技术，比如同时具备 Wi-Fi 能力和 BLE 能力的 **双模设备**，也可以使用蓝牙进行配网，当然 Wi-Fi 设备原本的配网仍然可用。

| 蓝牙技术分类  | 产品举例              |
| ----------- | -----------------  |
| SingleBLE     | 体脂秤、手环、温控器、电动牙刷、门锁等 |
| SigMesh     | 一路、二路、五路等灯泡、插座、传感器等 Sigmesh 子设备|
| TuyaMesh    | 与 Sigmesh 产品类似，协议为 Tuya 自研|
| 双模设备     | Sigmesh 网关、IPC 设备以及新版多协议 Wi-Fi 设备等均有可能|
> 双模配网的蓝牙配网部分，使用的是 SingleBLE 技术为设备配网，将放到 SingleBLE 章节进行说明。

蓝牙部分所具备的功能如下：

**1.配网**

- 扫描发现设备
- 设备配网

**2.配网后的设备操作**
- 检查设备当前连接状态
- 连接设备
- 设备操作
- 解绑设备

**3.设备升级固件**
- 检测设备版本
- 升级设备固件 OTA

## APP使用蓝牙所需要权限

**手机系统要求**

BLE 使用需要 Android 4.3 以及以上版本，TuyaHomesdk 从 Android 4.4 开始支持。

**Manifest 的权限**

```java
<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
<uses-permission android:name="android.permission.BLUETOOTH" />
<uses-permission android:name="android.permission.BLUETOOTH_ADMIN" />
```

**使用蓝牙前需要检测权限已被授予**

  *  APP 在使用蓝牙连接或者扫描操作前 需要检查 APP 定位权限是否被允许。
  *  检查蓝牙状态是否为开启。
> 该部分检查逻辑，TuyaHomeSdk 未提供 API，开发者可自行检测。每次扫描和连接前都要进行检测，否则 APP 无法正常使用蓝牙。
