# 标准设备控制

涂鸦智能提供了丰富的接口供开发者实现设备信息的获取和管理能力(移除等)。设备相关的返回数据都采用异步消息的方式通知接收者。


|   类名    |       说明       |
| :-------: | :-------------- |
| ITuyaDevice | ITuyaDevice类提供了设备状态通知能力，通过注册回调函数，开发者可以方便的获取设备数据接受、设备移除、设备上下线、手机网络变化的通知。同时也提供了控制指令下发，设备固件升级的接口 |

## 设备信息获取

设备控制必须先初始化数据，调用下面的方法获取家庭下的设备信息：

    TuyaHomeSdk.newHomeInstance(homeId).getHomeDetail(new ITuyaHomeResultCallback() {
        @Override
        public void onSuccess(HomeBean homeBean) {
        	
        }
    
        @Override
        public void onError(String errorCode, String errorMsg) {
    
        }
    });

该接口的onSuccess方法中将返回`HomeBean`，然后调用`HomeBean`的`getDeviceList`即可获得设备列表：

	List<DeviceBean> deviceList = homeBean.getDeviceList();

其中，`DeviceBean`中字段说明如下：

**DeviceBean 数据模型**


| 字段|类型|描述|
| :--| :--| :--|
| devId |String|设备唯一标示id|
| name |String|设备名称|
| iconUrl |String|图标地址|
| isOnline |Boolean|设备是否在线（局域网或者云端在线）|
| schema |String|设备控制数据点的类型信息|
| productId |String|产品ID，同一个产品ID，Schema信息一致|
| supportGroup |Boolean|设备是否支持群组，如果不支持请到开放平台开启此项功能|
| time | Long |设备激活时间|
| pv | String |网关协议版本|
| bv | String |网关通用固件版本|
| schemaMap | Map |Schema缓存数据|
| dps | Map |设备当前数据信息。key 是 dpId ，value 是值|
| isShare | boolean |是否是分享设备|
| virtual|boolean |是否是虚拟设备|
| lon、lat |String| 用来标示经纬度信息，需要用户使用sdk前，调用TuyaSdk.setLatAndLong 设置经纬度信息 |
| isLocalOnline|boolean|设备局域网在线状态|
| nodeId |String|用于网关和子设备类型的设备，属于子设备的一个属性，标识其短地址ID，一个网关下面的nodeId都唯一的|
| timezoneId |String|设备时区|
| category | String |设备类型|
| meshId |String|用于网关和子设备类型的设备，属于子设备的一个属性，标识其网关ID|
| isZigBeeWifi |boolean|是否是ZigBee网关设备|
| hasZigBee |boolean|hasZigBee|


**注意事项**

设备控制如果需要使用经纬度，需要在配网前调用方法设置经纬度:

	TuyaSdk.setLatAndLong(String latitude, String longitude)

## 初始化设备控制

**方法说明**

根据设备id初始化设备控制类

	TuyaHomeSdk.newDeviceInstance(String devId);

**参数说明**

| 参数| 说明|
| ---- | --- |
| devId |设备id|

**示例代码**

	ITuyaDevice mDevice = TuyaHomeSdk.newDeviceInstance(deviceBean.getDevId());

## 注册设备监听

**描述**

TuyaHomeDevice 提供设备相关信息（dp数据、设备名称、设备在线状态和设备移除）的监听，会实时同步到这里。

**方法说明**
	
	ITuyaDevice.registerDeviceListener(IDeviceListener listener)


**参数说明**

| 参数| 说明|
| ---- | --- |
| listener| 设备状态监听|

`IDevListener`接口如下：

	public interface IDeviceListener {
	
	    /**
	     * dp数据更新
	     *
	     * @param devId 设备id
	     * @param dpCommands 设备发生变动的功能点，为Map类型	     */
	    void onDpUpdate(String devId, Map<String, Object> dpCommands);
	
	    /**
	     * 设备移除回调
	     *
	     * @param devId 设备id
	     */
	    void onRemoved(String devId);
	
	    /**
	     * 设备上下线回调
	     *
	     * @param devId  设备id
	     * @param online 是否在线，在线为true
	     */
	    void onStatusChanged(String devId, boolean online);
	
	    /**
	     * 网络状态发生变动时的回调
	     *
	     * @param devId  设备id
	     *  @param status 网络状态是否可用，可用为true
	     */
	    void onNetworkStatusChanged(String devId, boolean status);
	
	    /**
	     * 设备信息更新回调
	     *
	     * @param devId  设备id
	     */
	    void onDevInfoUpdate(String devId);
	
	}

其中，设备功能点说明见下一节文档中的"设备功能点说明"

**示例代码**


	mDevice.registerDeviceListener(new IDeviceListener() {
	    @Override
	    public void onDpUpdate(String devId, Map<String, Object> dpCommands) {
	
	    }
	    @Override
	    public void onRemoved(String devId) {
	
	    }
	    @Override
	    public void onStatusChanged(String devId, boolean online) {
	
	    }
	    @Override
	    public void onNetworkStatusChanged(String devId, boolean status) {
	
	    }
	    @Override
	    public void onDevInfoUpdate(String devId) {
	
	    }
	});

## 设备控制

设备控制接口功能为向设备发送功能点，来改变设备状态或功能。

**接口说明**

发送命令，通过标准dp code发送指令

    void publishCommands(Map<String, Object> commands, IResultCallback callback);

**参数说明**

| 参数| 说明|
| ---- | --- |
| commands | data points, 设备功能点，格式为Map|
| publishModeEnum | 设备控制方式|
| callback |发送控制指令是否成功的回调|

**示例代码**

开灯的设备功能点code是"switch_led"，那么开灯的控制代码如下所示：
	
	HashMap<String, Object> hashMap = new HashMap<>();
	hashMap.put("switch_led", true);
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
}

> 注意事项
>
> * 指令下发成功并不是指设备真正操作成功，只是意味着指令成功发送出去。操作成功会有dp数据信息上报上来 ，且通过`IDeviceListener onDpUpdate`接口返回。
> * command 命令字符串 是以`Map<String dpId,Object dpValue>` 数据格式转成JsonString。
> * command 命令可以一次发送多个dp数据。


可一次控制多个功能点，示例代码如下:

```java
//作用:开关打开 
dps.put("switch_led",true);

//字符串型功能点示例 作用:设置彩光颜色
dps.put("colour_data": "009003e803e8"};

//枚举型功能点示例 作用:设置模式为"white"白光模式
dps.put("work_mode","white");

//设置数值型功能点示例 用:设置亮度为100
dps.put("bright_value",100);


//多个功能合并发送
dps.put("work_mode","colour");
dps.put("colour_data","009003e803e8");

mDevice.publishCommands(dps, new IResultCallback() {
        @Override
        public void onError(String code, String error) {
        //错误码11001
        //有下面几种情况：
        //1、类型不对导致，例如，string类型格式，发成boolean类型数据。
        //2、只读类型dp数据不能下发，参考SchemaBean getMode "ro"是只读类型。
        //3、raw格式发送数据格式不是16进制字符串。
        }
        @Override
        public void onSuccess() {
        }
    });
```

> 注意事项
>
> - 控制命令的发送需要特别注意数据类型.
	比如功能点的数据类型是数值型（value），那控制命令发送的应该是 `{"bright_value": 25}`  而不是  `{"bright_value": "25"}`
>
> - 透传类型传输的byte数组是16进制字符串格式并且必须是偶数位。
	比如正确的格式是: `{"*code": "0110"}` 而不是 `{"*code": "110"}`

## 取消设备监听

**方法说明**

	ITuyaDevice.unRegisterDevListener()

**调用示例**


	mDevice.unRegisterDevListener();

## 设备信息查询

**描述**

查询单个dp数据 从设备上查询dp最新数据 会经过 IDevicePanelCallback onDpUpdate 接口回调。

**方法调用**

```java
mDevice.getDp(String dpId, IResultCallback callback);
```

**示例代码**

```java
1、通过调用mTuyaDevice.getDp方法。
  
2、数据会通过dp数据更新监听上报上来。
IDevListener.onDpUpdate(String devId,String dpStr)
```

> 注意事项
>
> 该接口主要是针对那些数据不主动去上报的dp点。 常规查询dp数据值可以通过 DeviceBean里面 getDps()去获取。

## 设备重命名

**描述**

设备重命名，支持多设备同步。

**方法调用**

```java
//重命名
mDevice.renameDevice(String name,IResultCallback callback);
```

**示例代码**

```java
mDevice.renameDevice("设备名称", new IResultCallback() {
    @Override
    public void onError(String code, String error) {
        //重命名失败
    }
    @Override
    public void onSuccess() {
        //重命名成功
    }
});
```

成功之后 ，`IDevListener.onDevInfoUpdate()` 会收到通知。

调用以下方法获取最新数据，然后刷新设备信息即可。

```java
TuyaHomeSdk.getDataInstance().getDeviceBean(String devId);
```

## 移除设备

**描述**

用于从用户设备列表中移除设备

**接口说明**

移除设备

```java
void removeDevice(IResultCallback callback);
```

**示例代码**

```java
mDevice.removeDevice(new IResultCallback() {
    @Override
    public void onError(String errorCode, String errorMsg) {
    }

    @Override
    public void onSuccess() {
    }
});
```

## 查询WiFi信号强度

**描述**

查询当前设备WiFi的信号强度

**接口说明**

```java
void requestWifiSignal(WifiSignalListener listener);
```

**示例代码**

```java
mDevice.requestWifiSignal(new WifiSignalListener() {
     
     @Override
     public void onSignalValueFind(String signal) {
      
     }
     
     @Override
     public void onError(String errorCode, String errorMsg) {

     }
 });;
```

## 回收设备资源
应用或者Activity关闭时，可以调用此接口，回收设备占用的资源。

**接口说明**

	void onDestroy()

**调用示例**

	mDevice.onDestroy();
