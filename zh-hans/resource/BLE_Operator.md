# 蓝牙第三节——单点设备操作
本节将会介绍已配网的单点设备，如何进行状态检测、连接、解绑等。推荐先阅读蓝牙[第一节](./BLE.md)、[第二节](./BLE_Activator.md)。

**本节概要**

1. 操作设备包含设备状态查询
2. 设备连接
3. 设备发送指令
4. 修改设备
5. 解绑设备


## 先要条件
1. 开发 BLE 之前 需要先了解 TuyaHomeSDK 基本逻辑，需要已经使用 TuyaHomeSdk 完成初始化、登录、创建家庭等基本操作，在此之后可以进行 BLE 模块开发使用。 
2. 设备参照第二节已正常配网。配网成功后，将会得到 deviceBean，可以取到 devId，后续操作主要根据 devId 进行操作。

## 判断设备在线状态
* 通过通用方式查询 与 Wi-Fi 设备一致（此状态是综合状态，若蓝牙设备添加到网关下面 则蓝牙设备可云端在线）

  ```java
  TuyaHomeSdk.getDataInstance().getDeviceBean(devId).getIsOnline();
  ```
* 查询设备蓝牙是否本地连接

  ```java
  TuyaHomeSdk.getBleManager().isBleLocalOnline(devId);
  ```

  > 通常情况下蓝牙只需要考虑本地状态即可。只有加入蓝牙网关下的蓝牙设备才需要考虑是否云端在线。

## 连接设备
若设备处于离线状态 可以调用连接方法 进行设备连接。

**接口说明**

```java
void addScanLinkTaskIds(String idJsonString);
```

**参数说明**

|参数|类型|说明|
|--|--|--|
|idJsonString|String|devId 集合|

**示例代码**

```java
 List<String> devIdList = new ArrayList<>();
 devIdList.add(devId1); //设备1 devId
 devIdList.add(devId2); //设备2 devId
 
 String ids = JSONObject.toJSONString(devIdList);
 TuyaHomeSdk.getBleManager().addScanLinkTaskIds(ids);
```

## 设备操作
可以通过设备的操作类进行监听设备状态。该部分与 Wi-Fi 逻辑类似，可先参考获取更多逻辑信息[WIFI设备操作](./Device.md)

### 设备信息获取

与 Wi-Fi 设备的指令下发一致 [设备信息获取](./Device.md#设备信息获取)

### 初始化设备控制

与 Wi-Fi 设备的指令下发一致 [初始化设备控制](./Device.md#初始化设备控制)

### 注册设备监听

与 Wi-Fi 设备的指令下发一致 [注册设备监听](./Device.md#注册设备监听)

### 取消设备监听

与 Wi-Fi 设备的指令下发一致 [取消设备监听](./Device.md#取消设备监听)

### 设备功能点说明
与 Wi-Fi 设备的指令下发一致 [设备功能点说明](./Device.md#设备功能点说明)

### 设备控制方法

与 Wi-Fi 设备不同 不具备局域网下发功能。仅支持部分下发功能。设备控制接口功能为向设备发送功能点，来改变设备状态或功能。

**接口说明**

```java
void publishDps(String dps, IResultCallback callback);
```

**参数说明**

| 参数|类型|说明|
| ---- |--|--- |
| dps |String|data points， 设备功能点，格式为 json 字符串|
| callback|IResultCallback|发送控制指令是否成功的回调|

**示例代码**

假设开灯的设备功能点是 101，那么开灯的控制代码如下所示：
```java
HashMap<String, Object> hashMap = new HashMap<>();
hashMap.put("101", true);
mDevice.publishDps(JSONObject.toJSONString(hashMap), new IResultCallback() {
	@Override
	public void onError(String code, String error) {
		Toast.makeText(mContext, "开灯失败", Toast.LENGTH_SHORT).show();
	}

	@Override
	public void onSuccess() {
		Toast.makeText(mContext, "开灯成功", Toast.LENGTH_SHORT).show();
	}
});
```

### 设备重命名

与 Wi-Fi 设备的指令下发一致 [设备重命名](./Device.md#设备重命名)

### 移除设备

与 Wi-Fi 设备的指令下发一致 [移除设备](./Device.md#移除设备)

> 蓝牙设备的解绑与 Wi-Fi 使用方式一致 都是调用
> `TuyaHomeSdk.newDeviceInstance("devId").removeDevice()` 或者`resetFactory()` 
> 只是蓝牙设备除了进行云端移除之外。若设备此时本地连接状态 则会自动移除设备，若此时设备离线，则只会云端移除。设备会扔处于绑定状态。 下次想要继续重新绑定设备，需要将设备手动置为配网状态。sdk在扫描时，若发现设备处于绑定状态但是云端已解绑也会进行自动重置。

### 回收设备资源

与 Wi-Fi 设备的指令下发一致 [回收设备资源](./Device.md#回收设备资源)
