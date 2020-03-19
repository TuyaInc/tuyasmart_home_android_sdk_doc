### Room management

**RoomBean**

| Parameters | Type | Description |
| :--- | :--- | :--- |
| roomId | long  | Room id|
| name | String   | Room name|
| deviceList | List &lt;DeviceBean&gt;   | Devices of room |
| groupList | List &lt;GroupBean&gt;  | Groups of room |
| displayOrder | int | Room display order |

#### add group

**Declaration**

```java
void addGroup(long groupId, IResultCallback callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| groupId | Group ID |

**Example**

```java
TuyaHomeSdk.newRoomInstance(10000).addGroup(groupId, new IResultCallback() {
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

#### Update room name

**Declaration**

```java
void updateRoom(String name, IResultCallback callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| name | New room name |

**Example**

```java
TuyaHomeSdk.newRoomInstance(10000).updateRoom(name, new IResultCallback() {
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

#### Add device

**Declaration**

```java
void addDevice(String devId, IResultCallback callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| devId | Device ID |

**Example**

```java
TuyaHomeSdk.newRoomInstance(10000).addDevice(devId, new IResultCallback() {
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

#### Delete device

**Declaration**

```java
void removeDevice(String devId, IResultCallback callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| devId | Device ID |

**Example**

```java
TuyaHomeSdk.newRoomInstance(10000).removeDevice(devId, new IResultCallback() {
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

#### Delete Group

**Declaration**

```java
void removeGroup(Long groupId, IResultCallback resultCallback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| groupId | Group ID |

**Example**

```java
TuyaHomeSdk.newRoomInstance(10000).removeGroup(groupId, new IResultCallback() {
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

#### Remove group or device from room

**Declaration**

```java
void moveDevGroupListFromRoom(List list, IResultCallback callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| list | Group or device |

**Example**

```java
TuyaHomeSdk.newRoomInstance(10000).moveDevGroupListFromRoom(list, new IResultCallback() {
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

#### Sort groups or devices in a room

**Declaration**

```java
void sortDevInRoom(List<DeviceAndGroupInRoomBean> list, IResultCallback callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| list | Group or device |

**Example**

```java
TuyaHomeSdk.newRoomInstance(10000).sortDevInRoom(list, new IResultCallback() {
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


