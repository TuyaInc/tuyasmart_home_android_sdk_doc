# Activation

### Scaning Mesh Devices
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
// SigMesh's UUID
UUID[] MESH_PROVISIONING_UUID = {UUID.fromString("00001827-0000-1000-8000-00805f9b34fb")};
SearchBuilder searchBuilder = new SearchBuilder()
								.setServiceUUIDs(MESH_PROVISIONING_UUID)
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
**Example**

```java
TuyaSigMeshActivatorBuilder tuyaSigMeshActivatorBuilder = new TuyaSigMeshActivatorBuilder()
            .setSearchDeviceBeans(mSearchDeviceBeanList)
            .setSigMeshBean(sigMeshBean) 
            .setTimeOut(timeout) 
            .setTuyaBlueMeshActivatorListener(new ITuyaBlueMeshActivatorListener() {
     @Override
     public void onSuccess(String mac, DeviceBean deviceBean) {
     }
     @Override
     public void onError(String mac, String errorCode, String errorMsg) {
     }
     @Override
     public void onFinish() {
     });

ITuyaBlueMeshActivator iTuyaBlueMeshActivator = TuyaHomeSdk.getTuyaBlueMeshConfig().newActivator(tuyaBlueMeshActivatorBuilder);

//start
iTuyaBlueMeshActivator.startActivator();
//stop
iTuyaBlueMeshActivator.stopActivator();
```

**Parameters**

|field|describe|
|--|--|
|mSearchDeviceBeanList|List of devices to be activated|
|timeout|Activation timeout，default 100s.|
|sigMeshBean|SigMeshBean|

**Data Model**

`DeviceBean` See [DeviceBean Data Model](./Device.md#Device Information Acquisition)

`errorCode` See Error Code

## Error Code

|Code|MSG|
|--|--|
|21002       |invite failed|
|21004       |provision failed|
|21006       |send public key failed|
|21008       |conform failed|
|210010      |random conform failed|
|210014      |send data failed|
|210016      |composition data failed|
|210018      |add appkey failed|
|210020      |bind model failed|
|210022      |publication model failed|
|210024      |network transmit failed|
|210026      |Cloud registration failed|
|210027      |Device address allocation is full|
|210034      |notify failed|
|20021       |timeout|


## Sub-devices Activation——Gateway Activation

See  [ZigBee Sub-devices Activation](./Activator_zigbee_subdevice.md)

## Gateway Activation

SigMesh gateway essentially dual-mode device
1. Activation as a Wi-Fi device. See [Wifi EZ Activation](./Activator_wifi_ez.md)
2. Activation as a BLE device. See [Dual-mode Activation](./BLE_Activator.md#Dual-mode-Device-Activation)
