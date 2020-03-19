# 家庭管理

创建和查询家庭已经家庭信息变化监听

## 销毁

**接口说明**

```java
void onDestroy()
```

**示例代码**

```java
TuyaHomeSdk.getHomeManagerInstance().onDestroy();
```

## 获取家庭列表

**接口说明**

```java
void queryHomeList(ITuyaGetHomeListCallback callback)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| callback | 结果回调 |

**示例代码**

```java
TuyaHomeSdk.getHomeManagerInstance().queryHomeList(new ITuyaGetHomeListCallback() {
        @Override
        public void onSuccess(List<HomeBean> homeBeans) {
            // do something
        }
        @Override
        public void onError(String errorCode, String error) {
            // do something
        }
    });
```

## 获取家庭列表

**接口说明**

```java
void createHome(String name, double lon, double lat, String geoName, List<String> rooms, ITuyaHomeResultCallback callback)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| name | 家庭名称 |
| lon | 经度 |
| lat | 纬度 |
| geoName | 家庭地理位置名称 |
| rooms | 房间列表 |
| callback | 结果回调 |

**示例代码**

```java
TuyaHomeSdk.getHomeManagerInstance().createHome(name, lon, lat, geoName, rooms, new ITuyaHomeResultCallback() {
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

## 注册家庭信息的变更

有：家庭的增加、删除、信息变更、分享列表的变更和服务器连接成功的监听

**接口说明**

```java
void registerTuyaHomeChangeListener(ITuyaHomeChangeListener listener)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| listener | 监听器 |

**示例代码**

```java
TuyaHomeSdk.getHomeManagerInstance().registerTuyaHomeChangeListener(new ITuyaHomeChangeListener() {
        @Override
        public void onHomeInvite(long homeId, String homeName) {
            // do something
        }
        @Override
        public void onHomeRemoved(long homeId) {
            // do something
        }
        @Override
        public void onHomeInfoChanged(long homeId) {
            // do something
        }
        @Override
        public void onSharedDeviceList(List<DeviceBean> sharedDeviceList) {
            // do something
        }
        @Override
        public void onSharedGroupList(List<GroupBean> sharedGroupList) {
            // do something
        }
        @Override
        public void onServerConnectSuccess() {
            // do something
        }
        @Override
        public void onHomeAdded(long homeId) {
            // do something
        }
    });
```

## 注销家庭信息的变更

**接口说明**

```java
void unRegisterTuyaHomeChangeListener(ITuyaHomeChangeListener listener)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| listener | 监听器 |

**示例代码**

```java
TuyaHomeSdk.getHomeManagerInstance().unRegisterTuyaHomeChangeListener(new ITuyaHomeChangeListener() {
        @Override
        public void onHomeInvite(long homeId, String homeName) {
            // do something
        }
        @Override
        public void onHomeRemoved(long homeId) {
            // do something
        }
        @Override
        public void onHomeInfoChanged(long homeId) {
            // do something
        }
        @Override
        public void onSharedDeviceList(List<DeviceBean> sharedDeviceList) {
            // do something
        }
        @Override
        public void onSharedGroupList(List<GroupBean> sharedGroupList) {
            // do something
        }
        @Override
        public void onServerConnectSuccess() {
            // do something
        }
        @Override
        public void onHomeAdded(long homeId) {
            // do something
        }
    });
```


