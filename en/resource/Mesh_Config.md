# Activation

## Scaning Mesh Devices

 Keep bluetooth ON and check location permissions before scanning.

**Declaration**

```java
//start scanning
void startSearch();
//stop scanning
void stopSearch();

```
**Example**

```java
ITuyaBlueMeshSearchListener iTuyaBlueMeshSearchListener=new ITuyaBlueMeshSearchListener() {
    @Override
    public void onSearched(SearchDeviceBean deviceBean) {
    }

    @Override
    public void onSearchFinish() {
    }
};

SearchBuilder searchBuilder = new SearchBuilder()
		 .setMeshName("out_of_mesh")        
     .setTimeOut(100)        
     .setTuyaBlueMeshSearchListener(iTuyaBlueMeshSearchListener).build();

ITuyaBlueMeshSearch mMeshSearch = TuyaHomeSdk.getTuyaBlueMeshConfig().newTuyaBlueMeshSearch(searchBuilder);

//start
mMeshSearch.startSearch();
//stop
mMeshSearch.stopSearch();
```

## Sub-devices Activation —— APP Activation
Two types of sub-devices Activation, App activation and Mesh gateway activation.

**Declaration**

```java
void startActivator();

void stopActivator();
```

**Parameters**

|field|type|describe|
|--|--|--|
|mSearchDeviceBeans     |List|List of devices to be activated|
|timeout                |Int|Activation timeout，default 100s.|
|ssid                   |String|After activation, Wi-Fi's ssid.|
|password               |String|After activation, Wi-Fi's password.|
|mMeshBean              |MeshBean|MeshBean |
|homeId                 |Long|HomeId|
|version                |String|Devices activation is 1.0, gateway activation is 2.2.|



**Example**

```java
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

iTuyaBlueMeshActivator.startActivator();

iTuyaBlueMeshActivator.stopActivator();

```

## Sub-devices Activation——Gateway Activation
Two types of sub-devices Activation, device activation and Mesh gateway activation.
**Declaration**

```java
void startActivator();

void stopActivator();
```
**Parameters**

|field|type|describe|
|--|--|--|
|mSearchDeviceBeans     |List|List of devices to be configured|
|timeout                |Int|Activation timeout，default 100s.|
|ssid                   |String|After activation, Wi-Fi's ssid.|
|password               |String|After activation, Wi-Fi's password.|
|mMeshBean              |MeshBean|MeshBean |
|homeId                 |Long|HomeId|
|version                |String|Devices activation is 1.0, gateway activation is 2.2.|

**Example**

```java
TuyaBlueMeshActivatorBuilder tuyaBlueMeshActivatorBuilder = new TuyaBlueMeshActivatorBuilder()
                .setWifiSsid(mSsid)
                .setWifiPassword(mPassword)
                .setSearchDeviceBeans(foundDevices)
                .setVersion("2.2")
                .setBlueMeshBean(mMeshBean)
                .setHomeId("homeId")
                .setTuyaBlueMeshActivatorListener(new ITuyaBlueMeshActivatorListener() {

   @Override
   public void onSuccess(DeviceBean devBean) {
    }

   @Override
   public void onError(String errorCode, String errorMsg) {
  }

   @Override
   public void onFinish() {  
 
   }});
ITuyaBlueMeshActivator iTuyaBlueMeshActivator = TuyaHomeSdk.getTuyaBlueMeshConfig().newWifiActivator(tuyaBlueMeshActivatorBuilder);

iTuyaBlueMeshActivator.startActivator();

iTuyaBlueMeshActivator.stopActivator();

```


### Error Code

|Code|describe|
|--|--|
|13007|Device login failed|
|13004|Failed to reset device address|
|13005|Device address is full|
|13007|Ssid is empty|
|13011|Activation timeout|