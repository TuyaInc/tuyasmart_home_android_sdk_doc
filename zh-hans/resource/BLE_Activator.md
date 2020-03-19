# 蓝牙第二节——单点设备扫描与入网
本节将会介绍涂鸦单点设备、双模设备的扫描与入网。推荐先阅读 [第一节](./BLE.md) 
## 先要条件
开发 BLE 之前 需要先了解 TuyaHomeSDK 基本逻辑，需要已经使用 TuyaHomeSdk 完成初始化、登录、创建家庭等基本操作，在此之后可以进行 BLE 模块开发使用。 

## 扫描设备
待配网的蓝牙设备会向周围发送蓝牙广播包，SDK 会根据协议对广播包进行解析发现周围的涂鸦蓝牙单点设备和双模设备等。

> 再次提醒：蓝牙设备扫描前需要进行权限检测，只有**具备权限才能正常扫描**
> 1、蓝牙是否打开
> 2、应用是否具有定位权限

**接口说明**

```java
void startLeScan(int timeout, ScanType type, TyBleScanResponse response);
```
**参数说明**

|参数|类型|说明|
|--|--|--|
|timeout|int|配网超时时间，单位 ms ，推荐 60s|
|type|ScanType|`ScanType.SINGLE` 表示扫描单点设备|
|response|TyBleScanResponse|扫描结果的回调，不能为空|

**示例代码**

```java
TuyaHomeSdk.getBleOperator().startLeScan(60000, ScanType.SINGLE, new TyBleScanResponse() {
   @Override
   public void onResult(ScanDeviceBean bean) {
       
   }
});
```

**回调说明** 

`ScanDeviceBean` 说明

|属性|类型|说明|
|--|--|--|
|id|String|扫描 id 通常由 uuid 组成，可以唯一区别设备|
|name|String|扫描到的蓝牙名称 一般为空|
|providerName|String|SingleBleProvider 只开发单点设备不需要关注该字段|
|data|byte[]|原始数据|
|configType|String|`config_type_single`：单点设备;`config_type_wifi`：双模设备|
|productId|String|产品 id|
|uuid|String|产品 uuid，设备唯一码|
|mac|String|设备 mac，不可作为唯一码|
|isbind|boolean|是否被绑定，能回调的均为未配网的设备|
|flag|int|`bit0` ：是否支持 5G，表明双模设备是否支持 5G Wi-Fi；`bit1`：是否后绑定|

## 停止扫描
停止扫描设备，比如退出配网页面 或者 在执行设备入网时，建议停止扫描，以防止扫描影响到配网过程。

**接口说明**

```java
void stopLeScan();
```

**代码示例**

```java
TuyaHomeSdk.getBleOperator().stopLeScan();
```

## 单点设备入网激活
扫描到的设备 `configType=config_type_single` 表示单点蓝牙设备。`config_type_wifi`为双模设备。

**接口说明**
```java
void startBleConfig(long homeId, String devUuid, Map<String, Object> params, ITuyaBleConfigListener configListener);
```
**参数说明**

|参数|类型|说明|
|--|--|--|
|homeId|long|当前家庭 homeId|
|devUuid|String|扫描到的设备中 uuid。即 `ScanDeviceBean.uuid`|
|params|Map|传 null，单点配网不需要该参数|
|configListener|ITuyaBleConfigListener|配网回调，不可为空|

**代码示例**

```java
TuyaHomeSdk.getBleManager().startBleConfig(123456, "abc12345678", null, new ITuyaBleConfigListener() {
   @Override
   public void onSuccess(DeviceBean bean) {
      // 回调的 DeviceBean 数据说明 与WIFI的设备配网一致参见WiFI设备的配网回调说明。
   }

   @Override
   public void onFail(String code, String msg, Object handle) {
      // code msg 说明 见本章节配网错误码
   }
});
```
## 取消单点设备入网
配网过程中终止配网。

**接口说明**

```java
void stopBleConfig(String devUuid);
```
**参数说明**

|参数|类型|说明|
|--|--|--|
|devUuid|String|扫描到的设备中 uuid，即`ScanDeviceBean.uuid`|

**示例代码**

```java
TuyaHomeSdk.getBleManager().stopBleConfig("abc12345678");
```
## 双模设备入网激活
双模设备扫描到后 可以进行入网激活
扫描到的设备 `configType=config_type_single`表示单点蓝牙设备。`config_type_wifi`为双模设备。

**接口说明**
```java
void startBleConfig(long homeId, String devUuid, Map<String, Object> params, ITuyaBleConfigListener configListener);
```
**参数说明**

|参数|类型|说明|
|--|--|--|
|homeId|long|当前家庭 homeId|
|devUuid|String|扫描到的设备中 uuid，即 `ScanDeviceBean.uuid`|
|params|Map|双模设备需要传网络信息 ssid、pwd、token信息|
|configListener|ITuyaBleConfigListener|配网回调，不可为空|
> 若未说明，一般设备只支持 2.4G 频段WIFI配网，部分设备支持 5G。可以根据 `ScanDeviceBean.flag` 进行判定。
> token: 获取 token 的方式与 Wi-Fi 设备配网一致，见 Wi-Fi 部分配网获取 Token[获取 Token](./Activator_wifi.md#获取配网Token)

**代码示例**

```java
Map<String, Object> param = new HashMap<>();
param.put("ssid", "Tuya-Wifi-2.4G"); //wifi ssid
param.put("password", "12345678"); //wifi pwd
param.put("token", "xxxxxxxxxxxxx"); // user token
TuyaHomeSdk.getBleManager().startBleConfig(123456, "xyz12345678", param, new ITuyaBleConfigListener() {
	@Override
	public void onSuccess(DeviceBean bean) {
		// 回调的 DeviceBean 数据说明 参见WiFI设备的配网回调。
	}

	@Override
	public void onFail(String code, String msg, Object handle) {
		// code msg 说明 见本章节配网错误码
	}
});
```

**回调说明**

`DeviceBean`说明
见[DeviceBean 数据模型](./Device.md#DeviceBean 数据模型)

## 取消双模设备配网
配网中终止配网。

**接口说明**

```java
void stopBleConfig(String devUuid);
```

**参数说明**

|参数|类型|说明|
|--|--|--|
|devUuid|String|扫描到的设备中 uuid|
**示例代码**

```java
TuyaHomeSdk.getBleManager().stopBleConfig("xyz12345678");
```
## 错误码

|错误码|说明|
|--|--|
|1	|设备接收的数据包格式错误|
|2	|设备找不到路由器|
|3	|Wi-Fi 密码错误|
|4	|设备连不上路由器|
|5	|设备 DHCP 失败|
|6	|设备连云失败	|
|100	|用户取消配网|
|101	|蓝牙连接错误|
|102	|发现蓝牙服务错误|
|103	|打开蓝牙通讯通道失败|
|104	|蓝牙获取设备信息失败|
|105	|蓝牙配对失败|
|106	|配网超时|
|107	|Wi-Fi 信息发送失败|
|108	|Token 失效|
|109	|获取蓝牙加密密钥失败|
|110	|设备不存在|
|111	|设备云端注册失败|
|112	|设备云端激活失败|
|113	|云端设备已被绑定|
|114	|主动断开|
|115	|云端获取设备信息失败|
|116	|设备此时正被其他方式配网|
|117	|OTA 升级失败|
|118	|OTA 升级超时|
|119	|Wi-Fi 配网传参校验失败|

