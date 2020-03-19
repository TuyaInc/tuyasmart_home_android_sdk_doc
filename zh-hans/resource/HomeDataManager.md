# 缓存数据的操作类

每当使用 `TuyaHomeSdk.newHomeInstance(homeId).getHomeDetail()` 获取了指定家庭的详细信息之后家庭的信息会缓存到 SDK 当中，此时你可以使用 `ITuyaHomeDataManager` 来操作缓存到 SDK 到数据

## 获取 Home 数据

**接口说明**

```java
HomeBean getHomeBean(long homeId)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| homeId | 家庭 ID |

**示例代码**

```java
TuyaHomeSdk.getDataInstance().getHomeBean(homeId);
```

## 获取家庭下面的设备、群组、房间列表

**接口说明**

```java
List<RoomBean> getHomeRoomList(long homeId)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| homeId | 家庭 ID |

**示例代码**

```java
TuyaHomeSdk.getDataInstance().getHomeRoomList(homeId);
```

## 获取家庭下面的设备列表

**接口说明**

```java
List<DeviceBean> getHomeDeviceList(long homeId)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| homeId | 家庭 ID |

**示例代码**

```java
TuyaHomeSdk.getDataInstance().getHomeDeviceList(homeId);
```

## 获取家庭下面的群组列表

**接口说明**

```java
List<GroupBean> getHomeGroupList(long homeId)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| homeId | 家庭 ID |

**示例代码**

```java
TuyaHomeSdk.getDataInstance().getHomeGroupList(homeId);
```

## 获取群组

**接口说明**

```java
GroupBean getGroupBean(long groupId)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| groupId | 群组 ID |

**示例代码**

```java
TuyaHomeSdk.getDataInstance().getGroupBean(groupId);
```

## 获取设备

**接口说明**

```java
DeviceBean getDeviceBean(String devId)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| devId | 设备 ID |

**示例代码**

```java
TuyaHomeSdk.getDataInstance().getDeviceBean(devId);
```

## 根据群组 ID 获取房间

**接口说明**

```java
RoomBean getGroupRoomBean(long groupId)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| groupId | 群组 ID |

**示例代码**

```java
TuyaHomeSdk.getDataInstance().getGroupRoomBean(groupId);
```

## 获取房间

**接口说明**

```java
RoomBean getRoomBean(long roomId)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| homeId | 房间 ID |

**示例代码**

```java
TuyaHomeSdk.getDataInstance().getRoomBean(roomId);
```

## 根据设备获取房间信息

**接口说明**

```java
RoomBean getDeviceRoomBean(String devId)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| devId | 设备 ID |

**示例代码**

```java
TuyaHomeSdk.getDataInstance().getDeviceRoomBean(devId);
```

## 获取群组下面的设备列表

**接口说明**

```java
List<DeviceBean> getGroupDeviceList(long groupId)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| groupId | 群组 ID |

**示例代码**

```java
TuyaHomeSdk.getDataInstance().getGroupDeviceList(groupId);
```

## 获取 Mesh 下面的群组列表

**接口说明**

```java
List<GroupBean> getMeshGroupList(String meshId)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| meshId | Mesh ID |

**示例代码**

```java
TuyaHomeSdk.getDataInstance().getMeshGroupList(meshId);
```

## 获取 Mesh 设备列表

**接口说明**

```java
List<DeviceBean> getMeshDeviceList(String meshId)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| meshId | Mesh ID |

**示例代码**

```java
TuyaHomeSdk.getDataInstance().getMeshDeviceList(meshId);
```

## 根据房间ID获取房间下面的设备列表

**接口说明**

```java
List<DeviceBean> getRoomDeviceList(long roomId)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| roomId | 房间 ID |

**示例代码**

```java
TuyaHomeSdk.getDataInstance().getRoomDeviceList(roomId);
```

## 根据房间 ID 获取房间下面的群组列表

**接口说明**

```java
List<GroupBean> getRoomGroupList(long roomId)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| roomId | 房间 ID |

**示例代码**

```java
TuyaHomeSdk.getDataInstance().getRoomGroupList(roomId);
```

## 获取子设备列表

**接口说明**

```java
List<DeviceBean> getSubDeviceBean(String devId)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| devId | 设备 ID |

**示例代码**

```java
TuyaHomeSdk.getDataInstance().getSubDeviceBean(devId);
```

## 根据 Node ID 获取子设备

**接口说明**

```java
DeviceBean getSubDeviceBeanByNodeId(String devId, String nodeId)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| devId | 设备 ID |
| nodeId | Node ID |

**示例代码**

```java
TuyaHomeSdk.getDataInstance().getSubDeviceBeanByNodeId(devId, nodeId);
```

## 获取产品信息

**接口说明**

```java
ProductBean getProductBean(String productId)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| productId | 产品 ID |

**示例代码**

```java
TuyaHomeSdk.getDataInstance().getProductBean(productId);
```

## 获取 dp 数据

**接口说明**

```java
Object getDp(String devId, String dpId)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| devId | 设备 ID |
| dpId | DP ID |

**示例代码**

```java
TuyaHomeSdk.getDataInstance().getDp(devId, dpId);
```

## 获取 dps 数据

**接口说明**

```java
Map<String, Object> getDps(String devId)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| devId | 设备 ID |

**示例代码**

```java
TuyaHomeSdk.getDataInstance().getDps(devId);
```

## 获取设备 schema

**接口说明**

```java
Map<String, SchemaBean> getSchema(String devId)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| devId | 设备 ID |

**示例代码**

```java
TuyaHomeSdk.getDataInstance().getSchema(devId);
```

## 查询设备

**接口说明**

```java
void queryDev(String devId, ITuyaDataCallback callback)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| devId | 设备 ID |
| callback | 结果回调 |

**示例代码**

```java
TuyaHomeSdk.getDataInstance().queryDev(devId, new ITuyaDataCallback<DeviceBean>() {
        @Override
        public void onSuccess(DeviceBean result) {
            // do something
        }
        @Override
        public void onError(String errorCode, String errorMessage) {
            // do something
        }
    });
```

## 查询设备

**接口说明**

```java
void discoveredLanDevice(ITuyaSearchDeviceListener listener)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| listener | 监听器 |

**示例代码**

```java
TuyaHomeSdk.getDataInstance().discoveredLanDevice(new ITuyaSearchDeviceListener() {
        @Override
        public void onDeviceFind(String devId, DeviceActiveEnum activeEnum) {
            // do something
        }
    });
```

## 取消注册设备查询监听

**接口说明**

```java
void unRegisterDiscoveredLanDeviceListener(ITuyaSearchDeviceListener listener)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| listener | 监听器 |

**示例代码**

```java
TuyaHomeSdk.getDataInstance().unRegisterDiscoveredLanDeviceListener(new ITuyaSearchDeviceListener() {
        @Override
        public void onDeviceFind(String devId, DeviceActiveEnum activeEnum) {
            // do something
        }
    });
```

## 查询子设备

**接口说明**

```java
void querySubDev(String meshId, String devId, ITuyaDataCallback callback)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| meshId | Mesh ID |
| devId | 设备 ID |
| callback | 结果回调 |

**示例代码**

```java
TuyaHomeSdk.getDataInstance().querySubDev(meshId, devId, new ITuyaDataCallback<DeviceBean>() {
        @Override
        public void onSuccess(DeviceBean result) {
            // do something
        }
        @Override
        public void onError(String errorCode, String errorMessage) {
            // do something
        }
    });
```

## 获取设备信息

**接口说明**

```java
DeviceRespBean getDevRespBean(String devId)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| devId | 设备 ID |

**示例代码**

```java
TuyaHomeSdk.getDataInstance().getDevRespBean(devId);
```

## 获取子设备信息

**接口说明**

```java
DeviceRespBean getSubDevRespBean(String meshId, String nodeId)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| meshId | Mesh ID |
| nodeId | Node ID |

**示例代码**

```java
TuyaHomeSdk.getDataInstance().getSubDevRespBean(meshId, nodeId);
```

## 获取设备信息列表

**接口说明**

```java
List<DeviceRespBean> getDevRespBeanList();
```

**示例代码**

```java
TuyaHomeSdk.getDataInstance().getDevRespBeanList();
```

## 添加设备列表

**接口说明**

```java
void addDevRespList(List<DeviceRespBean> deviceRespBeans)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| deviceRespBeans | 设备列表 |

**示例代码**

```java
TuyaHomeSdk.getDataInstance().addDevRespList(deviceRespBeans);
```

## 添加产品列表

**接口说明**

```java
void addProductList(List<ProductBean> productBeans)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| productBeans | 产品列表 |

**示例代码**

```java
TuyaHomeSdk.getDataInstance().addProductList(productBeans);
```

## 获取子设备列表

**接口说明**

```java
void getSubDevList(String devId, ITuyaDataCallback<List<DeviceBean>> callback)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| devId | 设备 ID |
| callback | 结果回调 |

**示例代码**

```java
TuyaHomeSdk.getDataInstance().getSubDevList(devId, new ITuyaDataCallback<List<DeviceBean>>() {
        @Override
        public void onSuccess(List<DeviceBean> result) {
            // do something
        }
        @Override
        public void onError(String errorCode, String errorMessage) {
            // do something
        }
    });
```


