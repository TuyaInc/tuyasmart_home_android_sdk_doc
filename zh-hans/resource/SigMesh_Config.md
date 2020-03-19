## 配网与入网

### 扫描附近待配网子设备
扫描前需要检查蓝牙和位置权限

**接口说明**

```java
//开启扫描
void startSearch();
//停止扫描
void stopSearch();

```

**示例代码**

```java
ITuyaBlueMeshSearchListener iTuyaBlueMeshSearchListener=new ITuyaBlueMeshSearchListener() {
    @Override
    public void onSearched(SearchDeviceBean deviceBean) {

    }

    @Override
    public void onSearchFinish() {

    }
};
// 待配网的SigMesh设备UUID是固定的
UUID[] MESH_PROVISIONING_UUID = {UUID.fromString("00001827-0000-1000-8000-00805f9b34fb")};
SearchBuilder searchBuilder = new SearchBuilder()
								.setServiceUUIDs(MESH_PROVISIONING_UUID)	//SigMesh的UUID是固定值
                .setTimeOut(100)        //扫描时长 单位秒
                .setTuyaBlueMeshSearchListener(iTuyaBlueMeshSearchListener).build();

ITuyaBlueMeshSearch mMeshSearch = TuyaHomeSdk.getTuyaBlueMeshConfig().newTuyaBlueMeshSearch(searchBuilder);

//开启扫描
mMeshSearch.startSearch();

//停止扫描
mMeshSearch.stopSearch();
```


## 子设备入网——通过 APP 蓝牙入网

子设备入网有两种方式，一种是通过 App 蓝牙入网，另一种是通过网关直接配子设备入网。

**接口说明**

```java
//开启配网
void startActivator();
//停止配网
void stopActivator();
```
**示例代码**

```java
TuyaSigMeshActivatorBuilder tuyaSigMeshActivatorBuilder = new TuyaSigMeshActivatorBuilder()
            .setSearchDeviceBeans(mSearchDeviceBeanList)
            .setSigMeshBean(sigMeshBean) // Sigmesh基本信息
            .setTimeOut(timeout)  //超时时间
            .setTuyaBlueMeshActivatorListener(new ITuyaBlueMeshActivatorListener() {
     @Override
     public void onSuccess(String mac, DeviceBean deviceBean) {
         L.d(TAG, "subDevBean onSuccess: " + deviceBean.getName());
     }
     @Override
     public void onError(String mac, String errorCode, String errorMsg) {
         L.d(TAG, "config mesh error" + errorCode + " " + errorMsg);
     }
     @Override
     public void onFinish() {
      L.d(TAG, "config mesh onFinish： ");
     });

ITuyaBlueMeshActivator iTuyaBlueMeshActivator = TuyaHomeSdk.getTuyaBlueMeshConfig().newActivator(tuyaBlueMeshActivatorBuilder);

//开启配网
iTuyaBlueMeshActivator.startActivator();
//停止配网
iTuyaBlueMeshActivator.stopActivator();
```

**入参说明**

|参数|说明|
|--|--|
|mSearchDeviceBeanList|待配网的设备集合,通过 startSearch 扫描得到的|
|timeout|配网的超时时间设置，默认是 100s（配网设备过多时，需要增加时间)|
|sigMeshBean|SigMeshBean|

**出参说明**

`DeviceBean` 见 [DeviceBean数据模型](./Device.md#DeviceBean数据模型)

`errorCode` 见错误码

## 错误码

|Code|MSG|
|--|--|
|21002       |invite 失败|
|21004       |provision 失败|
|21006       |send public key 失败|
|21008       |conform 失败|
|210010      |random conform 失败|
|210014      |send data 失败|
|210016      |composition data 失败|
|210018      |add appkey 失败|
|210020      |bind model 失败|
|210022      |publication model 失败|
|210024      |network transmit 失败|
|210026      |云端注册失败|
|210027      |设备地址分配已满|
|210034      |notify 失败|
|20021       |配网超时|


## 子设备入网——通过网关通道入网

同 [ZigBee 子设备配网](./Activator_zigbee_subdevice.md)

## 网关入网

SigMesh 网关 本质上为双模设备；

可以使用 Wi-Fi设备的入网 同 [Wifi EZ 配网模式](./Activator_wifi_ez.md)；

也可以使用单点蓝牙双模入网 [双模设备配网](./BLE_Activator.md#双模设备入网激活)。