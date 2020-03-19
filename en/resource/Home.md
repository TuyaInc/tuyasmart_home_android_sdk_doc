### Family management

Get the family list, family management, room and equipment management under the family and information monitoring, etc.

**HomeBean description**

| Parameters | Type | Description |
| :--- | :--- | :--- |
| name | String  | The home name|
| lon | double   | The home lon |
| lat | double | The home lat |
| geoName | String | The home location name |
| homeId | long | The home Id |
| admin | boolean  | Administrator status |
| rooms | List&lt;RoomBean&gt; | All the rooms|
| deviceList | List&lt;DeviceBean&gt;  | All the devices |
| groupList | List&lt;GroupBean&gt; | All the groups |
| meshList | List&lt;BlueMeshBean&gt; |All of the mesh devices |
| sharedDeviceList | List&lt;DeviceBean&gt;|Shared devices received |
| sharedGroupList | List&lt;GroupBean&gt; |Shared groups received |
| homeStatus | int| The home status （1:to be accepted 2:accepted 3:reject）|

#### Get data information in local cache

**Declaration**

```java
void getHomeLocalCache(ITuyaHomeResultCallback callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| callback | Callback to get results |

**Example**

```java
TuyaHomeSdk.newHomeInstance(10000).getHomeLocalCache(new ITuyaHomeResultCallback() {
        @Override
        public void onError(String errorCode, String errorMsg) {
            // do something
        }
        @Override
        public void onSuccess(HomeBean bean) {
            // do something
        }
    });
```

#### Update family information

**Declaration**

```java
void updateHome(String name, double lon, double lat, String geoName, IResultCallback callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| name | Family name |
| lon | Longitude of current family |
| lat | Latitude of the current family |
| geoName | Address of geographical location |
| callback | Result callback |

**Example**

```java
TuyaHomeSdk.newHomeInstance(10000).updateHome(name, lon, lat, geoName, new IResultCallback() {
        @Override
        public void onError(String code, String error) {
            // do something
        }
        @Override
        public void onSuccess() {
            // do something
        }
    });
```

#### Family sort

**Declaration**

```java
void sortHome(List idList, IResultCallback callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| idList | Family ID list |
| callback | Result callback |

**Example**

```java
TuyaHomeSdk.newHomeInstance(10000).sortHome(idList, new IResultCallback() {
        @Override
        public void onError(String code, String error) {
            // do something
        }
        @Override
        public void onSuccess() {
            // do something
        }
    });
```

#### Get family list

Obtain all data under the family, including equipment, groups, rooms, etc

**Declaration**

```java
void getHomeDetail(ITuyaHomeResultCallback callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| callback | Callback to get results |

**Example**

```java
TuyaHomeSdk.newHomeInstance(10000).getHomeDetail(new ITuyaHomeResultCallback() {
        @Override
        public void onError(String errorCode, String errorMsg) {
            // do something
        }
        @Override
        public void onSuccess(HomeBean bean) {
            // do something
        }
    });
```

#### Disband family

**Declaration**

```java
void dismissHome(IResultCallback callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| callback | Result callback |

**Example**

```java
TuyaHomeSdk.newHomeInstance(10000).dismissHome(new IResultCallback() {
        @Override
        public void onError(String code, String error) {
            // do something
        }
        @Override
        public void onSuccess() {
            // do something
        }
    });
```

#### Add room

**Declaration**

```java
void addRoom(String name, ITuyaRoomResultCallback callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| name | Room name |
| callback | Result callback |

**Example**

```java
TuyaHomeSdk.newHomeInstance(10000).addRoom(name, new ITuyaRoomResultCallback() {
        @Override
        public void onError(String errorCode, String errorMsg) {
            // do something
        }
        @Override
        public void onSuccess(RoomBean bean) {
            // do something
        }
    });
```

#### Remove room

**Declaration**

```java
void removeRoom(long roomId, IResultCallback callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| roomId | Room ID |
| callback | Result callback |

**Example**

```java
TuyaHomeSdk.newHomeInstance(10000).removeRoom(roomId, new IResultCallback() {
        @Override
        public void onError(String code, String error) {
            // do something
        }
        @Override
        public void onSuccess() {
            // do something
        }
    });
```

#### Sorting rooms

**Declaration**

```java
void sortRoom(List<Long> idList, IResultCallback callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| idList | Room ID list |
| callback | Result callback |

**Example**

```java
TuyaHomeSdk.newHomeInstance(10000).sortRoom(idList, new IResultCallback() {
        @Override
        public void onError(String code, String error) {
            // do something
        }
        @Override
        public void onSuccess() {
            // do something
        }
    });
```

#### Query room list

**Declaration**

```java
void queryRoomList(ITuyaGetRoomListCallback callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| callback | Result callback |

**Example**

```java
TuyaHomeSdk.newHomeInstance(10000).queryRoomList(new ITuyaGetRoomListCallback() {
        @Override
        public void onError(String errorCode, String error) {
            // do something
        }
        @Override
        public void onSuccess(List<RoomBean> romeBeans) {
            // do something
        }
    });
```

#### Get home instance information

**Declaration**

```java
HomeBean getHomeBean()
```

**Example**

```java
TuyaHomeSdk.newHomeInstance(10000).getHomeBean();
```

#### Create Group

**Declaration**

```java
void createGroup(String productId, String name, List<Long> devIdList, ITuyaResultCallback<Long> callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| productId | Product ID |
| name | group name |
| devIdList | Device ID list |
| callback | Result callback |

**Example**

```java
TuyaHomeSdk.newHomeInstance(10000).createGroup(productId, name, devIdList, new ITuyaResultCallback() {
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

#### Query room information according to equipment

**Declaration**

```java
List<RoomBean> queryRoomInfoByDevice(List<DeviceBean> deviceList)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| deviceList | Device list |

**Example**

```java
TuyaHomeSdk.newHomeInstance(10000).queryRoomInfoByDevice(deviceList);
```

#### Monitor the change of information in the home

**Declaration**

```java
void registerHomeStatusListener(ITuyaHomeStatusListener listener)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| listener | Monitor |

**Example**

```java
TuyaHomeSdk.newHomeInstance(10000).registerHomeStatusListener(new ITuyaHomeStatusListener() {
        @Override
        public void onDeviceAdded(String devId) {
            // do something
        }
        @Override
        public void onDeviceRemoved(String devId) {
            // do something
        }
        @Override
        public void onGroupAdded(long groupId) {
            // do something
        }
        @Override
        public void onGroupRemoved(long groupId) {
            // do something
        }
        @Override
        public void onMeshAdded(String meshId) {
            // do something
        }
    });
```

#### Log off monitoring of information changes below home

**Declaration**

```java
void unRegisterHomeStatusListener(ITuyaHomeStatusListener listener)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| listener | Monitor |

**Example**

```java
TuyaHomeSdk.newHomeInstance(10000).unRegisterHomeStatusListener(new ITuyaHomeStatusListener() {
        @Override
        public void onDeviceAdded(String devId) {
            // do something
        }
        @Override
        public void onDeviceRemoved(String devId) {
            // do something
        }
        @Override
        public void onGroupAdded(long groupId) {
            // do something
        }
        @Override
        public void onGroupRemoved(long groupId) {
            // do something
        }
        @Override
        public void onMeshAdded(String meshId) {
            // do something
        }
    });
```

#### Monitor the change of device information under the home

**Declaration**

```java
void registerHomeDeviceStatusListener(ITuyaHomeDeviceStatusListener listener)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| listener | Monitor |

**Example**

```java
TuyaHomeSdk.newHomeInstance(10000).registerHomeDeviceStatusListener(new ITuyaHomeDeviceStatusListener() {
        @Override
        public void onDeviceStatusChanged(String devId, boolean online) {
            // do something
        }
        @Override
        public void onDeviceInfoUpdate(String devId) {
            // do something
        }
        @Override
        public void onDeviceDpUpdate(String devId, String dpStr) {
            // do something
        }
    });
```

#### Log off monitoring of device information changes under home

**Declaration**

```java
void unRegisterHomeDeviceStatusListener(ITuyaHomeDeviceStatusListener listener)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| listener | Monitor |

**Example**

```java
TuyaHomeSdk.newHomeInstance(10000).unRegisterHomeDeviceStatusListener(new ITuyaHomeDeviceStatusListener() {
        @Override
        public void onDeviceStatusChanged(String devId, boolean online) {
            // do something
        }
        @Override
        public void onDeviceInfoUpdate(String devId) {
            // do something
        }
        @Override
        public void onDeviceDpUpdate(String devId, String dpStr) {
            // do something
        }
    });
```

#### Create Bluetooth mesh

**Declaration**

```java
void createBlueMesh(String meshName, ITuyaResultCallback<BlueMeshBean> callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| meshName | Mesh name |
| callback | Result callback |

**Example**

```java
TuyaHomeSdk.newHomeInstance(10000).createBlueMesh(meshName, new ITuyaResultCallback() {
        @Override
        public void onError(String errorCode, String errorMessage) {
            // do something
        }
        @Override
        public void onSuccess(BlueMeshBean result) {
            // do something
        }
    });
```

#### Create Bluetooth SIG mesh

**Declaration**

```java
void createSigMesh(ITuyaResultCallback<SigMeshBean> callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| callback | Result callback |

**Example**

```java
TuyaHomeSdk.newHomeInstance(10000).createSigMesh(new ITuyaResultCallback() {
        @Override
        public void onError(String errorCode, String errorMessage) {
            // do something
        }
        @Override
        public void onSuccess(SigMeshBean result) {
            // do something
        }
    });
```

#### Query the list of devices added to the group

**Declaration**

```java
void queryDeviceListToAddGroup(long groupId, String productId, ITuyaResultCallback<List<GroupDeviceBean>> callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| groupId | Group ID |
| productId | Product ID |
| callback | Result callback |

**Example**

```java
TuyaHomeSdk.newHomeInstance(10000).queryDeviceListToAddGroup(groupId, productId, new ITuyaResultCallback<List<GroupDeviceBean>>() {
        @Override
        public void onError(String errorCode, String errorMessage) {
            // do something
        }
        @Override
        public void onSuccess(List<GroupDeviceBean> result) {
            // do something
        }
    });
```

#### Query ZigBee device list added to group

**Declaration**

```java
void queryZigbeeDeviceListToAddGroup(long groupId, String productId, String parentId, ITuyaResultCallback<List<GroupDeviceBean>> callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| groupId | Group ID |
| productId | Product ID |
| parentId | mesh id |
| callback | Result callback |

**Example**

```java
TuyaHomeSdk.newHomeInstance(10000).queryZigbeeDeviceListToAddGroup(groupId, productId, parentId, new ITuyaResultCallback<List<GroupDeviceBean>>() {
        @Override
        public void onError(String errorCode, String errorMessage) {
            // do something
        }
        @Override
        public void onSuccess(<List<GroupDeviceBean>> result) {
            // do something
        }
    });
```

#### Destruction

**Declaration**

```java
void onDestroy()
```

**Example**

```java
TuyaHomeSdk.newHomeInstance(10000).onDestroy();
```

#### Create ZigBee group

**Declaration**

```java
void createZigbeeGroup(String productId, String parentId, int parentType, String name, ITuyaResultCallback<CloudZigbeeGroupCreateBean> callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| productId | Product Id |
| parentId | Parent node ID |
| parentType | Parent node type |
| name | group name |
| callback | Result callback |

**Example**

```java
TuyaHomeSdk.newHomeInstance(10000).createZigbeeGroup(productId, parentId, parentType, name, new ITuyaResultCallback<CloudZigbeeGroupCreateBean>() {
        @Override
        public void onError(String errorCode, String errorMessage) {
            // do something
        }
        @Override
        public void onSuccess(CloudZigbeeGroupCreateBean result) {
            // do something
        }
    });
```

#### Use groups to query room information

**Declaration**

```java
List<RoomBean> queryRoomInfoByGroup(List<GroupBean> groupList)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| groupList | Group list |

**Example**

```java
TuyaHomeSdk.newHomeInstance(10000).queryRoomInfoByGroup(groupList);
```

#### Bind new device

**Declaration**

```java
void bindNewConfigDevs(List<String> devIds, IResultCallback callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| devIds | Device ID list |
| callback | Result callback |

**Example**

```java
TuyaHomeSdk.newHomeInstance(10000).bindNewConfigDevs(devIds, new IResultCallback() {
        @Override
        public void onError(String code, String error) {
            // do something
        }
        @Override
        public void onSuccess() {
            // do something
        }
    });
```

#### Registered product alarm monitoring

**Declaration**

```java
void registerProductWarnListener(IWarningMsgListener listener)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| listener | Monitor |

**Example**

```java
TuyaHomeSdk.newHomeInstance(10000).registerProductWarnListener(new IWarningMsgListener() {
        @Override
        public void onWarnMessageArrived(WarnMessageBean warnMessageBean) {
            // do something
        }
    });
```

#### Unregister product alarm monitoring

**Declaration**

```java
void unRegisterProductWarnListener(IWarningMsgListener listener)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| listener | Monitor |

**Example**

```java
TuyaHomeSdk.newHomeInstance(10000).unRegisterProductWarnListener(new IWarningMsgListener() {
        @Override
        public void onWarnMessageArrived(WarnMessageBean warnMessageBean) {
            // do something
        }
    });
```

#### Sort groups or devices in your home

**Declaration**

```java
void sortDevInHome(String homeId, List<DeviceAndGroupInHomeBean> list, IResultCallback callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| homeId | Room ID |
| list | Room or group list |
| callback | Result callback |

**Example**

```java
List<DeviceAndGroupInHomeBean> list = new ArrayList<>();
TuyaHomeSdk.newHomeInstance(10000).sortDevInHome(homeId, list, new IResultCallback() {
        @Override
        public void onError(String code, String error) {
            // do something
        }
        @Override
        public void onSuccess() {
            // do something
        }
    });
```

#### Update family information

**Declaration**

```java
void updateHome(String name, double lon, double lat, String geoName, List rooms, boolean overWriteRoom, IResultCallback callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| name | Family name |
| lon | Longitude of current family |
| lat | Latitude of the current family |
| geoName | Address of geographical location |
| rooms | Room information |
| overWriteRoom | Whether to overwrite the existing room |
| callback | Result callback |

**Example**

```java
TuyaHomeSdk.newHomeInstance(10000).updateHome(name, lon, lat, geoName, rooms, overWriteRoom, new IResultCallback() {
        @Override
        public void onError(String code, String error) {
            // do something
        }
        @Override
        public void onSuccess() {
            // do something
        }
    });
```

#### Create ZigBee group

**Declaration**

```java
void createZigbeeGroup(String productId, String parentId, String name, ITuyaResultCallback<CloudZigbeeGroupCreateBean> callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| productId | Product Id |
| parentId | Parent node ID |
| name | group name |
| callback | Result callback |

**Example**

```java
TuyaHomeSdk.newHomeInstance(10000).createZigbeeGroup(productId, parentId, name, new ITuyaResultCallback<CloudZigbeeGroupCreateBean>() {
        @Override
        public void onError(String errorCode, String errorMessage) {
            // do something
        }
        @Override
        public void onSuccess(CloudZigbeeGroupCreateBean result) {
            // do something
        }
    });
```

#### Register upgrade status listener

**Declaration**

```java
void registerUpgradeStatusListener(ITuyaDeviceUpgradeStatusCallback callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| callback | Result callback |

**Example**

```java
TuyaHomeSdk.newHomeInstance(10000).registerUpgradeStatusListener(new ITuyaDeviceUpgradeStatusCallback() {
        @Override
        public void onStatusUpgrade(String devId, UpgradeStatusEnum upgradeStatusEnum) {
            // do something
        }
    });
```




