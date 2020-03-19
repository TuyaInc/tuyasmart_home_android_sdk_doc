# 配网与入网

## 扫描待配网子设备

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
ITuyaBlueMeshSearchListener iTuyaBlueMeshSearchListener = new ITuyaBlueMeshSearchListener() {
	@Override
	public void onSearched(SearchDeviceBean deviceBean) {
	}

	@Override
	public void onSearchFinish() {
	}
};

SearchBuilder searchBuilder = new SearchBuilder()
                //要扫描设备的名称（默认会是out_of_mesh，设备处于配网状态下的名称）
                .setMeshName("out_of_mesh") 
                .setTimeOut(100) //扫描时长 单位秒
                .setTuyaBlueMeshSearchListener(iTuyaBlueMeshSearchListener).build();

ITuyaBlueMeshSearch mMeshSearch = TuyaHomeSdk.getTuyaBlueMeshConfig().newTuyaBlueMeshSearch(searchBuilder);

//开启扫描
mMeshSearch.startSearch();

//停止扫描
mMeshSearch.stopSearch();
```

## 子设备入网 —— APP 入网
子设备入网分为 2 种，一种是普通设备入网，一种是 Mesh 网关入网

**接口说明**

```java
//开启配网
void startActivator();

//停止配网
void stopActivator();
```

**参数说明**

|参数|String|说明|
|--|--|--|
|mSearchDeviceBeans     |List|待配网的设备集合|
|timeout                |Int|配网的超时时间设置，默认是 100s.|
|ssid                   |String|配网之后，设备工作 Wi-Fi 的名称。（家庭网络）|
|password               |String|配网之后，设备工作 Wi-Fi 的密码。（家庭网络）|
|mMeshBean              |MeshBean|MeshBean |
|homeId                 |Long|设备要加入的 Mesh 网 所属家庭的 HomeId|
|version                |String|普通设备配网是 1.0    网关配网是 2.2|




**代码示例**
```java
//普通设备入网
TuyaBlueMeshActivatorBuilder tuyaBlueMeshActivatorBuilder = new TuyaBlueMeshActivatorBuilder()
                .setSearchDeviceBeans(foundDevices)
                .setVersion("1.0")
                .setBlueMeshBean(mMeshBean)
                .setTimeOut(timeOut)
                .setTuyaBlueMeshActivatorListener(new ITuyaBlueMeshActivatorListener() {
     @Override
     public void onSuccess(DeviceBean deviceBean) {
     }

     @Override
     public void onError(String errorCode, String errorMsg) {
     }

     @Override
     public void onFinish() {
     }});
      
ITuyaBlueMeshActivator iTuyaBlueMeshActivator = TuyaHomeSdk.getTuyaBlueMeshConfig().newActivator(tuyaBlueMeshActivatorBuilder);
//开始入网
iTuyaBlueMeshActivator.startActivator();

//停止入网
iTuyaBlueMeshActivator.stopActivator();

```

## 子设备入网——网关入网
子设备入网分为 2 种，一种是普通设备入网，一种是 Mesh 网关入网
**接口说明**
```java
//开启配网
void startActivator();
//停止配网
void stopActivator();
```
**参数说明**

|参数|String|说明|
|--|--|--|
|mSearchDeviceBeans     |List|待配网的设备集合|
|timeout                |Int|配网的超时时间设置，默认是 100s.|
|ssid                   |String|配网之后，设备工作 Wi-Fi 的名称。（家庭网络）|
|password               |String|配网之后，设备工作 Wi-Fi 的密码。（家庭网络）|
|mMeshBean              |MeshBean|MeshBean |
|homeId                 |Long|设备要加入的 Mesh 网 所属家庭的 HomeId|
|version                |String|普通设备配网是 1.0    网关配网是 2.2|

**代码示例**

```java
//网关入网
TuyaBlueMeshActivatorBuilder tuyaBlueMeshActivatorBuilder = new TuyaBlueMeshActivatorBuilder()
                .setWifiSsid(mSsid)
                .setWifiPassword(mPassword)
                .setSearchDeviceBeans(foundDevices)
                .setVersion("2.2  ")
                .setBlueMeshBean(mMeshBean)
                .setHomeId("homeId")
                .setTuyaBlueMeshActivatorListener(new ITuyaBlueMeshActivatorListener() {
                  @Override
                  public void onSuccess(DeviceBean devBean) {
                    //单个设备配网成功回调
                    L.d(TAG, "startConfig  success");
                  }

                  @Override
                  public void onError(String errorCode, String errorMsg) {
                    //单个设备配网失败回调
                    //errorCode 见错误码
                  L.d(TAG, "errorCode: " + errorCode + " errorMsg: " + errorMsg);
                  }

                  @Override
                  public void onFinish() {
                    //所有设备配网结束回调          
                  }
                });
ITuyaBlueMeshActivator iTuyaBlueMeshActivator = TuyaHomeSdk.getTuyaBlueMeshConfig().newWifiActivator(tuyaBlueMeshActivatorBuilder);

//开始入网
iTuyaBlueMeshActivator.startActivator();

//停止入网
//iTuyaBlueMeshActivator.stopActivator();
```


### 错误码

|Code|说明|
|--|--|
|13007|登录设备失败|
|13004|重置设备地址失败|
|13005|设备地址已满|
|13007|ssid为空|
|13011|配网超时|