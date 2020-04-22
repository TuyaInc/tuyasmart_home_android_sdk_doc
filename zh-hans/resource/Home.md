# 家庭管理

获取家庭列表，家庭管理，家庭下面的房间和设备管理以及信息监听等

**HomeBean 字段信息**

| 字段 | 类型 | 描述 |
| :--- | :--- | :--- |
| name | String  | 家庭名称|
| lon | double   | 经度 |
| lat | double | 纬度|
| geoName | String |家庭地理位置名称 |
| homeId | long | 家庭 ID |
| admin | boolean  | 管理员身份 |
| rooms | List&lt;RoomBean&gt;  | 所有房间列表 |
| deviceList | List&lt;DeviceBean&gt;  | 所有设备列表 |
| groupList | List&lt;GroupBean&gt;  |所有群组 |
| meshList | List&lt;BlueMeshBean&gt; |网关设备 |
| sharedDeviceList | List&lt;DeviceBean&gt; |收到的共享设备 |
| sharedGroupList | List&lt;GroupBean&gt; |收到的共享群组|
| homeStatus | int | 家庭状态（1:等待接受 2:接受 3:拒绝）|

## 获取本地缓存中的数据信息

**接口说明**

```java
void getHomeLocalCache(ITuyaHomeResultCallback callback)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| callback | 获取结果的回调 |

**示例代码**

```java
TuyaHomeSdk.newHomeInstance(10000).getHomeLocalCache(new ITuyaHomeResultCallback() {
        @Override
        public void onSuccess(HomeBean bean) {
            // do something
        }
        @Override
        public void onError(String errorCode, String errorMsg) {
            // do something
        }
    });
```

## 更新家庭信息

**接口说明**

```java
void updateHome(String name, double lon, double lat, String geoName, IResultCallback callback)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| name | 家庭名称 |
| lon | 当前家庭的经度 |
| lat | 当前家庭的纬度 |
| geoName | 地理位置的地址 |
| callback | 结果回调 |

**示例代码**

```java
TuyaHomeSdk.newHomeInstance(10000).updateHome(name, lon, lat, geoName, new IResultCallback() {
        @Override
        public void onSuccess() {
            // do something
        }
        @Override
        public void onError(String code, String error) {
            // do something
        }
    });
```

## 更新家庭信息

**接口说明**

```java
void updateHome(String name, double lon, double lat, String geoName, List rooms, boolean overWriteRoom, IResultCallback callback)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| name | 家庭名称 |
| lon | 当前家庭的经度 |
| lat | 当前家庭的纬度 |
| geoName | 地理位置的地址 |
| rooms | 房间信息 |
| overWriteRoom | 是否覆盖已有房间 |
| callback | 结果回调 |

**示例代码**

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

## 解散家庭

**接口说明**

```java
void dismissHome(IResultCallback callback)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| callback | 结果回调 |

**示例代码**

```java
TuyaHomeSdk.newHomeInstance(10000).dismissHome(new IResultCallback() {
        @Override
        public void onSuccess() {
            // do something
        }
        @Override
        public void onError(String code, String error) {
            // do something
        }
    });
```

## 获取家庭详情

获取家庭下的所有数据，包括设备、群组、房间等

**接口说明**

```java
void getHomeDetail(ITuyaHomeResultCallback callback)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| callback | 获取结果的回调 |

**示例代码**

```java
TuyaHomeSdk.newHomeInstance(10000).getHomeDetail(new ITuyaHomeResultCallback() {
        @Override
        public void onSuccess(HomeBean bean) {
            // do something
        }
        @Override
        public void onError(String errorCode, String errorMsg) {
            // do something
        }
    });
```

## 家庭排序

**接口说明**

```java
void sortHome(List<Long> idList, IResultCallback callback)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| idList | 家庭 ID 列表 |
| callback | 结果回调 |

**示例代码**

```java
TuyaHomeSdk.newHomeInstance(10000).sortHome(idList, new IResultCallback() {
        @Override
        public void onSuccess() {
            // do something
        }
        @Override
        public void onError(String code, String error) {
            // do something
        }
    });
```

## 添加房间

**接口说明**

```java
void addRoom(String name, ITuyaRoomResultCallback callback)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| name | 房间名称 |
| callback | 结果回调 |

**示例代码**

```java
TuyaHomeSdk.newHomeInstance(10000).addRoom("房间名称", new ITuyaRoomResultCallback() {
        @Override
        public void onSuccess(RoomBean bean) {
            // do something
        }
        @Override
        public void onError(String errorCode, String errorMsg) {
            // do something
        }
    });
```

## 移除房间

**接口说明**

```java
void removeRoom(long roomId, IResultCallback callback)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| roomId | 房间 ID |
| callback | 结果回调 |

**示例代码**

```java
TuyaHomeSdk.newHomeInstance(10000).removeRoom(roomId, new IResultCallback() {
        @Override
        public void onSuccess() {
            // do something
        }
        @Override
        public void onError(String code, String error) {
            // do something
        }
    });
```

## 排序房间

**接口说明**

```java
void sortRoom(List<Long> idList, IResultCallback callback)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| idList | 房间 ID 列表 |
| callback | 结果回调 |

**示例代码**

```java
TuyaHomeSdk.newHomeInstance(10000).sortRoom(idList, new IResultCallback() {
        @Override
        public void onSuccess() {
            // do something
        }
        @Override
        public void onError(String code, String error) {
            // do something
        }
    });
```

## 查询房间列表

**接口说明**

```java
void queryRoomList(ITuyaGetRoomListCallback callback)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| callback | 结果回调 |

**示例代码**

```java
TuyaHomeSdk.newHomeInstance(10000).queryRoomList(new ITuyaGetRoomListCallback() {
        @Override
        public void onSuccess(List<RoomBean> romeBeans) {
            // do something
        }
        @Override
        public void onError(String errorCode, String error) {
            // do something
        }
    });
```

## 获取家庭实例的信息

**接口说明**

```java
HomeBean getHomeBean()
```

**示例代码**

```java
TuyaHomeSdk.newHomeInstance(10000).getHomeBean();
```

## 创建群组

**接口说明**

```java
void createGroup(String productId, String name, List<Long> devIdList, ITuyaResultCallback<Long> callback)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| productId | 产品 ID |
| name | 群组名称 |
| devIdList | 设备 ID List |
| callback | 结果回调 |

**示例代码**

```java
TuyaHomeSdk.newHomeInstance(10000).createGroup(productId, name, devIdList, new ITuyaResultCallback<Long>() {
        @Override
        public void onSuccess(Long result) {
            // do something
        }
        @Override
        public void onError(String errorCode, String errorMessage) {
            // do something
        }
    });
```

## 根据设备查询房间信息

**接口说明**

```java
List<RoomBean> queryRoomInfoByDevice(List<DeviceBean> deviceList)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| deviceList | 设备列表 |

**示例代码**

```java
TuyaHomeSdk.newHomeInstance(10000).queryRoomInfoByDevice(deviceList);
```

## 监听家庭下面信息变更的监听

**接口说明**

```java
void registerHomeStatusListener(ITuyaHomeStatusListener listener)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| listener | 监听器 |

**示例代码**

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

## 注销家庭下面信息变更的监听

**接口说明**

```java
void unRegisterHomeStatusListener(ITuyaHomeStatusListener listener)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| listener | 监听器 |

**示例代码**

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

## 监听家庭下面设备信息变更的监听

**接口说明**

```java
void registerHomeDeviceStatusListener(ITuyaHomeDeviceStatusListener listener)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| listener | 监听器 |

**示例代码**

```java
TuyaHomeSdk.newHomeInstance(10000).registerHomeDeviceStatusListener(new ITuyaHomeDeviceStatusListener() {
        @Override
        public void onDeviceDpUpdate(String devId, String dpStr) {
            // do something
        }
        @Override
        public void onDeviceStatusChanged(String devId, boolean online) {
            // do something
        }
        @Override
        public void onDeviceInfoUpdate(String devId) {
            // do something
        }
    });
```

## 注销家庭下面设备信息变更的监听

**接口说明**

```java
void unRegisterHomeDeviceStatusListener(ITuyaHomeDeviceStatusListener listener)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| listener | 监听器 |

**示例代码**

```java
TuyaHomeSdk.newHomeInstance(10000).unRegisterHomeDeviceStatusListener(new ITuyaHomeDeviceStatusListener() {
        @Override
        public void onDeviceDpUpdate(String devId, String dpStr) {
            // do something
        }
        @Override
        public void onDeviceStatusChanged(String devId, boolean online) {
            // do something
        }
        @Override
        public void onDeviceInfoUpdate(String devId) {
            // do something
        }
    });
```

## 创建蓝牙 Mesh

**接口说明**

```java
void createBlueMesh(String meshName, ITuyaResultCallback<BlueMeshBean> callback)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| meshName | Mesh 名称 |
| callback | 结果回调 |

**示例代码**

```java
TuyaHomeSdk.newHomeInstance(10000).createBlueMesh(meshName, new ITuyaResultCallback<BlueMeshBean>() {
        @Override
        public void onSuccess(BlueMeshBean result) {
            // do something
        }
        @Override
        public void onError(String errorCode, String errorMessage) {
            // do something
        }
    });
```

## 创建蓝牙 SigMesh

**接口说明**

```java
void createSigMesh(ITuyaResultCallback<SigMeshBean> callback)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| callback | 结果回调 |

**示例代码**

```java
TuyaHomeSdk.newHomeInstance(10000).createSigMesh(new ITuyaResultCallback<SigMeshBean>() {
        @Override
        public void onSuccess(SigMeshBean result) {
            // do something
        }
        @Override
        public void onError(String errorCode, String errorMessage) {
            // do something
        }
    });
```

## 查询添加到群组的设备列表

**接口说明**

```java
void queryDeviceListToAddGroup(long groupId, String productId, ITuyaResultCallback<List<GroupDeviceBean>> callback)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| groupId | 群组 ID |
| productId | 产品 ID |
| callback | 结果回调 |

**示例代码**

```java
TuyaHomeSdk.newHomeInstance(10000).queryDeviceListToAddGroup(groupId, productId, new ITuyaResultCallback<List<GroupDeviceBean>>() {
        @Override
        public void onSuccess(List<GroupDeviceBean> result) {
            // do something
        }
        @Override
        public void onError(String errorCode, String errorMessage) {
            // do something
        }
    });
```

## 查询添加到群组的 ZigBee 设备列表

**接口说明**

```java
void queryZigbeeDeviceListToAddGroup(long groupId, String productId, String parentId, ITuyaResultCallback<List<GroupDeviceBean>> callback)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| groupId | 群组 ID |
| productId | 产品 ID |
| parentId | Mesh ID |
| callback | 结果回调 |

**示例代码**

```java
TuyaHomeSdk.newHomeInstance(10000).queryZigbeeDeviceListToAddGroup(groupId, productId, parentId, new ITuyaResultCallback<List<GroupDeviceBean>>() {
        @Override
        public void onSuccess(List<GroupDeviceBean> result) {
            // do something
        }
        @Override
        public void onError(String errorCode, String errorMessage) {
            // do something
        }
    });
```

## 销毁

**接口说明**

```java
void onDestroy()
```

**示例代码**

```java
TuyaHomeSdk.newHomeInstance(10000).onDestroy();
```

## 创建 Zigbee 群组

**接口说明**

```java
void createZigbeeGroup(String productId, String parentId, int parentType, String name, ITuyaResultCallback<CloudZigbeeGroupCreateBean> callback)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| productId | 产品 ID |
| parentId | 父节点 ID |
| parentType | 父节点类型 |
| name | 群组名称 |
| callback | 结果回调 |

**示例代码**

```java
TuyaHomeSdk.newHomeInstance(10000).createZigbeeGroup(productId, parentId, parentType, name, new ITuyaResultCallback<CloudZigbeeGroupCreateBean>() {
        @Override
        public void onSuccess(CloudZigbeeGroupCreateBean result) {
            // do something
        }
        @Override
        public void onError(String errorCode, String errorMessage) {
            // do something
        }
    });
```

## 创建 Zigbee 群组

**接口说明**

```java
void createZigbeeGroup(String productId, String parentId, String name, ITuyaResultCallback<CloudZigbeeGroupCreateBean> callback)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| productId | 产品 Id |
| parentId | 父节点 id |
| name | 群组名称 |
| callback | 结果回调 |

**示例代码**

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

## 使用群组查询房间信息

**接口说明**

```java
List<RoomBean> queryRoomInfoByGroup(List<GroupBean> groupList)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| groupList | 群组列表 |

**示例代码**

```java
TuyaHomeSdk.newHomeInstance(10000).queryRoomInfoByGroup(groupList);
```

## 绑定新设备

**接口说明**

```java
void bindNewConfigDevs(List<String> devIds, IResultCallback callback)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| devIds | 设备 ID 列表 |
| callback | 结果回调 |

**示例代码**

```java
TuyaHomeSdk.newHomeInstance(10000).bindNewConfigDevs(devIds, new IResultCallback() {
        @Override
        public void onSuccess() {
            // do something
        }
        @Override
        public void onError(String code, String error) {
            // do something
        }
    });
```

## 注册产品告警监听

**接口说明**

```java
void registerProductWarnListener(IWarningMsgListener listener)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| listener | 监听器 |

**示例代码**

```java
TuyaHomeSdk.newHomeInstance(10000).registerProductWarnListener(new IWarningMsgListener() {
        @Override
        public void onWarnMessageArrived(WarnMessageBean warnMessageBean) {
            // do something
        }
    });
```

## 取消注册产品告警监听

**接口说明**

```java
void unRegisterProductWarnListener(IWarningMsgListener listener)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| listener | 监听器 |

**示例代码**

```java
TuyaHomeSdk.newHomeInstance(10000).unRegisterProductWarnListener(new IWarningMsgListener() {
        @Override
        public void onWarnMessageArrived(WarnMessageBean warnMessageBean) {
            // do something
        }
    });
```

## 对家庭里的群组或者设备进行排序

**接口说明**

```java
void sortDevInHome(String homeId, List<DeviceAndGroupInHomeBean> list, IResultCallback callback)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| homeId | 房间 ID |
| list | 房间或者群组列表，这里元素 DeviceAndGroupInHomeBean 包含两个字段。一个是 `bizType` 表示被排序的对象的类型，比如是群组还是设备，是一个整数类型的枚举，参考 BizParentTypeEnum 对象；另一个是 `bizId` 表示被排序的对象的 id，比如群组 id 或者设备 id. |
| callback | 结果回调 |

BizParentTypeEnum 对象的枚举值：

- LOCATION
- MESH
- ROOM
- GROUP
- DEVICE

**示例代码**

```java
List<DeviceAndGroupInHomeBean> list = new ArrayList<>();
List<DeviceBean> deviceList = homeBean.getDeviceList();
List<GroupBean> groupList = homeBean.getGroupList();
for (GroupBean bean : groupList) {
    DeviceAndGroupInHomeBean deviceInRoomBean = new DeviceAndGroupInHomeBean();
    deviceInRoomBean.setBizId(bean.getDevId());
    deviceInRoomBean.setBizType(BizParentTypeEnum.GROUP.getType());
    list.add(deviceInRoomBean);
}
for (DeviceBean bean : deviceList) {
    DeviceAndGroupInHomeBean deviceInRoomBean = new DeviceAndGroupInHomeBean();
    deviceInRoomBean.setBizId(bean.getDevId());
    deviceInRoomBean.setBizType(BizParentTypeEnum.DEVICE.getType());
    list.add();
}
TuyaHomeSdk.newHomeInstance(10000).sortDevInHome(homeId, list, new IResultCallback() {
        @Override
        public void onSuccess() {
            // do something
        }
        @Override
        public void onError(String code, String error) {
            // do something
        }
    });
```

## 监听设备更新状态

**接口说明**

```java
void registerUpgradeStatusListener(ITuyaDeviceUpgradeStatusCallback callback)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| callback | 结果回调 |

**示例代码**

```java
TuyaHomeSdk.newHomeInstance(10000).registerUpgradeStatusListener(new ITuyaDeviceUpgradeStatusCallback() {
        @Override
        public void onStatusUpgrade(String devId, UpgradeStatusEnum upgradeStatusEnum) {
            // do something
        }
    });
```