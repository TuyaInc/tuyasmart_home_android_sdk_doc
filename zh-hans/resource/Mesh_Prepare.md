## APP 使用蓝牙所需要权限

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

