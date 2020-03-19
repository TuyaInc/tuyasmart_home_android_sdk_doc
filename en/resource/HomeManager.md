### Family management

Create and query family information change monitor

#### Destruction

**Declaration**

```java
void onDestroy()
```

**Example**

```java
TuyaHomeSdk.getHomeManagerInstance().onDestroy();
```

#### Get family list

**Declaration**

```java
void createHome(String name, double lon, double lat, String geoName, List rooms, ITuyaHomeResultCallback callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| name | Family name |
| lon | longitude |
| lat | latitude |
| geoName | Home location name |
| rooms | Room list |
| callback | Result callback |

**Example**

```java
TuyaHomeSdk.getHomeManagerInstance().createHome(name, lon, lat, geoName, rooms, new ITuyaHomeResultCallback() {
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

#### Get family list

**Declaration**

```java
void queryHomeList(ITuyaGetHomeListCallback callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| callback | Result callback |

**Example**

```java
TuyaHomeSdk.getHomeManagerInstance().queryHomeList(new ITuyaGetHomeListCallback() {
        @Override
        public void onError(String errorCode, String error) {
            // do something
        }
        @Override
        public void onSuccess(List<HomeBean> homeBeans) {
            // do something
        }
    });
```

#### Change of registered family information

There are: addition and deletion of family, information change, change of sharing list and successful monitoring of server connection

**Declaration**

```java
void registerTuyaHomeChangeListener(ITuyaHomeChangeListener listener)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| listener | Monitor |

**Example**

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
        public void onHomeAdded(long homeId) {
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
    });
```

#### Change of cancellation family information

**Declaration**

```java
void unRegisterTuyaHomeChangeListener(ITuyaHomeChangeListener listener)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| listener | Monitor |

**Example**

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
        public void onHomeAdded(long homeId) {
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
    });
```


