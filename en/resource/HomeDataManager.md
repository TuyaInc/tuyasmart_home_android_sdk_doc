### Operation Class of Cached Data

Every time `TuyaHomeSdk.newHomeInstance(homeId).getHomeDetail()` is used to get the details of the specified family, the family information will be cached in the SDK. At this time, you can use `ITuyaHomeDataManager` to operate the data cached in SDK.

#### Get Home Data

**Declaration**

```java
HomeBean getHomeBean(long homeId)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| homeId | Family ID |

**Example**

```java
TuyaHomeSdk.getDataInstance().getHomeBean(homeId);
```

#### Get a List of Devices, Groups and Rooms Under the Family

**Declaration**

```java
List<RoomBean> getHomeRoomList(long homeId)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| homeId | Family ID |

**Example**

```java
TuyaHomeSdk.getDataInstance().getHomeRoomList(homeId);
```

#### Get the Device List Below Home

**Declaration**

```java
List<DeviceBean> getHomeDeviceList(long homeId)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| homeId | Family ID |

**Example**

```java
TuyaHomeSdk.getDataInstance().getHomeDeviceList(homeId);
```

#### Get the List of Groups Under the Family

**Declaration**

```java
List<GroupBean> getHomeGroupList(long homeId)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| homeId | Family ID |

**Example**

```java
TuyaHomeSdk.getDataInstance().getHomeGroupList(homeId);
```

#### Get Groups

**Declaration**

```java
GroupBean getGroupBean(long groupId)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| groupId | Group ID |

**Example**

```java
TuyaHomeSdk.getDataInstance().getGroupBean(groupId);
```

#### Acquiring Equipment

**Declaration**

```java
DeviceBean getDeviceBean(String devId)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| devId | Device ID |

**Example**

```java
TuyaHomeSdk.getDataInstance().getDeviceBean(devId);
```

#### Get Rooms Based on Group ID

**Declaration**

```java
RoomBean getGroupRoomBean(long groupId)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| groupId | Group ID |

**Example**

```java
TuyaHomeSdk.getDataInstance().getGroupRoomBean(groupId);
```

#### Get Room

**Declaration**

```java
RoomBean getRoomBean(long roomId)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| homeId | Room ID |

**Example**

```java
TuyaHomeSdk.getDataInstance().getRoomBean(roomId);
```

#### Get Room Information According To Equipment

**Declaration**

```java
RoomBean getDeviceRoomBean(String devId)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| devId | Device ID |

**Example**

```java
TuyaHomeSdk.getDataInstance().getDeviceRoomBean(devId);
```

#### Get the Device List Under the Group

**Declaration**

```java
List<DeviceBean> getGroupDeviceList(long groupId)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| groupId | Group ID |

**Example**

```java
TuyaHomeSdk.getDataInstance().getGroupDeviceList(groupId);
```

#### Get the Group List Under Mesh

**Declaration**

```java
List<GroupBean> getMeshGroupList(String meshId)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| meshId | Mesh ID |

**Example**

```java
TuyaHomeSdk.getDataInstance().getMeshGroupList(meshId);
```

#### Get Mesh Device List

**Declaration**

```java
List<DeviceBean> getMeshDeviceList(String meshId)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| meshId | Mesh ID |

**Example**

```java
TuyaHomeSdk.getDataInstance().getMeshDeviceList(meshId);
```

#### Get the Equipment List Under the Room According To the Room ID

**Declaration**

```java
List<DeviceBean> getRoomDeviceList(long roomId)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| roomId | Room ID |

**Example**

```java
TuyaHomeSdk.getDataInstance().getRoomDeviceList(roomId);
```

#### Get the Group List Under the Room According To the Room ID

**Declaration**

```java
List<GroupBean> getRoomGroupList(long roomId)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| roomId | Room ID |

**Example**

```java
TuyaHomeSdk.getDataInstance().getRoomGroupList(roomId);
```

#### Get List of Sub Devices

**Declaration**

```java
List<DeviceBean> getSubDeviceBean(String devId)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| devId | Device ID |

**Example**

```java
TuyaHomeSdk.getDataInstance().getSubDeviceBean(devId);
```

#### Get Sub Devices According To Node ID

**Declaration**

```java
DeviceBean getSubDeviceBeanByNodeId(String devId, String nodeId)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| devId | Device ID |
| nodeId | Node ID |

**Example**

```java
TuyaHomeSdk.getDataInstance().getSubDeviceBeanByNodeId(devId, nodeId);
```

#### Get Product Information

**Declaration**

```java
ProductBean getProductBean(String productId)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| productId | Product ID |

**Example**

```java
TuyaHomeSdk.getDataInstance().getProductBean(productId);
```

#### Get DP Data

**Declaration**

```java
Object getDp(String devId, String dpId)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| devId | Device ID |
| dpId | DP ID |

**Example**

```java
TuyaHomeSdk.getDataInstance().getDp(devId, dpId);
```

#### Get DPS Data

**Declaration**

```java
Map<String, Object> getDps(String devId)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| devId | Device ID |

**Example**

```java
TuyaHomeSdk.getDataInstance().getDps(devId);
```

#### Get Device Schema

**Declaration**

```java
Map<String, SchemaBean> getSchema(String devId)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| devId | Device ID |

**Example**

```java
TuyaHomeSdk.getDataInstance().getSchema(devId);
```

#### Query Device

**Declaration**

```java
void queryDev(String devId, ITuyaDataCallback callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| devId | Device ID |
| callback | Result callback |

**Example**

```java
TuyaHomeSdk.getDataInstance().queryDev(devId, new ITuyaDataCallback() {
        @Override
        public void onError(String errorCode, String errorMessage) {
            // do something
        }
        @Override
        public void onSuccess(Object result) {
            // do something
        }
    });
```

#### Query Device

**Declaration**

```java
void discoveredLanDevice(ITuyaSearchDeviceListener listener)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| listener | Monitor |

**Example**

```java
TuyaHomeSdk.getDataInstance().discoveredLanDevice(new ITuyaSearchDeviceListener() {
        @Override
        public void onDeviceFind(String devId, DeviceActiveEnum activeEnum) {
            // do something
        }
    });
```

#### Unregister Device Query Listening

**Declaration**

```java
void unRegisterDiscoveredLanDeviceListener(ITuyaSearchDeviceListener listener)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| listener | Monitor |

**Example**

```java
TuyaHomeSdk.getDataInstance().unRegisterDiscoveredLanDeviceListener(new ITuyaSearchDeviceListener() {
        @Override
        public void onDeviceFind(String devId, DeviceActiveEnum activeEnum) {
            // do something
        }
    });
```

#### Query Sub Devices

**Declaration**

```java
void querySubDev(String meshId, String devId, ITuyaDataCallback callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| meshId | Mesh ID |
| devId | Device ID |
| callback | Result callback |

**Example**

```java
TuyaHomeSdk.getDataInstance().querySubDev(meshId, devId, new ITuyaDataCallback<DeviceBean>() {
        @Override
        public void onError(String errorCode, String errorMessage) {
            // do something
        }
        @Override
        public void onSuccess(DeviceBean result) {
            // do something
        }
    });
```

#### Get Device Information

**Declaration**

```java
DeviceRespBean getDevRespBean(String devId)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| devId | Device ID |

**Example**

```java
TuyaHomeSdk.getDataInstance().getDevRespBean(devId);
```

#### Get Sub Device Information

**Declaration**

```java
DeviceRespBean getSubDevRespBean(String meshId, String nodeId)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| meshId | Mesh ID |
| nodeId | Node ID |

**Example**

```java
TuyaHomeSdk.getDataInstance().getSubDevRespBean(meshId, nodeId);
```

#### Get Device Information List

**Declaration**

```java
List<DeviceRespBean> getDevRespBeanList();
```

**Example**

```java
TuyaHomeSdk.getDataInstance().getDevRespBeanList();
```

#### Add Device List

**Declaration**

```java
void addDevRespList(List<DeviceRespBean> deviceRespBeans)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| deviceRespBeans | Device list |

**Example**

```java
TuyaHomeSdk.getDataInstance().addDevRespList(deviceRespBeans);
```

#### Add Product List

**Declaration**

```java
void addProductList(List<ProductBean> productBeans)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| productBeans | Product list |

**Example**

```java
TuyaHomeSdk.getDataInstance().addProductList(productBeans);
```

#### Get List of Sub Devices

**Declaration**

```java
void getSubDevList(String devId, ITuyaDataCallback callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| devId | Device ID |
| callback | Result callback |

**Example**

```java
TuyaHomeSdk.getDataInstance().getSubDevList(devId, new ITuyaDataCallback() {
        @Override
        public void onError(String errorCode, String errorMessage) {
            // do something
        }
        @Override
        public void onSuccess(Object result) {
            // do something
        }
    });
```


