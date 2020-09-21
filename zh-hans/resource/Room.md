# 房间管理

**RoomBean 字段信息**

| 字段 | 类型 | 描述 |
| --- | --- | --- |
| roomId | long  | 房间 id |
| name | String   | 房间名字|
| deviceList | List &lt;DeviceBean&gt;   | 房间下面的设备|
| groupList | List &lt;GroupBean&gt;  | 房间下面的群组|
| displayOrder | int | 房间顺序|

## 更新房间名称

**接口说明**

```java
void updateRoom(String name, IResultCallback callback)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| name | 新房间名称 |

**示例代码**

```java
TuyaHomeSdk.newRoomInstance(10000).updateRoom(name, new IResultCallback() {
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

## 自定义房间图片

房间可支持自定义 image，成功后可通过 `RoomBean.iconUrl` 进行获取房间图片地址

**接口说明**

```java
void updateIcon(File file, IResultCallback callback);
```

**参数说明**

| 参数     | 说明     |
| -------- | -------- |
| file     | 房间图片 |
| callback | 回调     |

**示例代码**

```java
TuyaHomeSdk.newRoomInstance(10000).updateIcon(file, new IResultCallback() {
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

## 添加设备

**接口说明**

```java
void addDevice(String devId, IResultCallback callback)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| devId | 设备 ID |

**示例代码**

```java
TuyaHomeSdk.newRoomInstance(10000).addDevice(devId, new IResultCallback() {
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

## 删除设备

**接口说明**

```java
void removeDevice(String devId, IResultCallback callback)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| devId | 设备 ID |

**示例代码**

```java
TuyaHomeSdk.newRoomInstance(10000).removeDevice(devId, new IResultCallback() {
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

## 添加群组

**接口说明**

```java
void addGroup(long groupId, IResultCallback callback)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| groupId | 群组 ID |

**示例代码**

```java
TuyaHomeSdk.newRoomInstance(10000).addGroup(groupId, new IResultCallback() {
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

## 删除群组

**接口说明**

```java
void removeGroup(Long groupId, IResultCallback resultCallback)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| groupId | 群组 ID |

**示例代码**

```java
TuyaHomeSdk.newRoomInstance(10000).removeGroup(groupId, new IResultCallback() {
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

## 把群组或者设备移除房间

**接口说明**

```java
void moveDevGroupListFromRoom(List<DeviceAndGroupInRoomBean> list, IResultCallback callback)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| list | 群组或者设备 |

**示例代码**

```java
TuyaHomeSdk.newRoomInstance(10000).moveDevGroupListFromRoom(list, new IResultCallback() {
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

## 对房间里的群组或者设备进行排序

**接口说明**

```java
void sortDevInRoom(List<DeviceAndGroupInRoomBean> list, IResultCallback callback)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| list | 群组或者设备 |

**示例代码**

```java
TuyaHomeSdk.newRoomInstance(10000).sortDevInRoom(list, new IResultCallback() {
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


