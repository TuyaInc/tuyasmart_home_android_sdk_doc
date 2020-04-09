### Group Operation

#### Instantiation

```java
ITuyaGroup mITuyaGroup= TuyaHomeSdk.newGroupInstance(groupId);
```

**Parameters**

| Parameters         | Description |
| ------------ | -------------------------- |
| groupId             | group id |

#### Modifying group name

```java
TuyaHomeSdk.newGroupInstance(groupId).renameGroup(titleName, 
            new IResultCallback() {
            
            @Override
            public void onError(String s, String s1) {
            
            }
            
            @Override
            public void onSuccess() {
                
            }
        });
```
**Parameters**

| Parameters    | Description |
| ------------ | ----------- |
| groupId      | group id    |
| titleName    | group name  |

#### Dismiss Group

```java
TuyaHomeSdk.newGroupInstance(groupId).dismissGroup(new IResultCallback() {
    
            @Override
            public void onError(String s, String s1) {
            
            }
            
            @Override
            public void onSuccess() {
            
            }
        });
```

**Parameters**

| Parameters    | Description |
| ------------ | ----------- |
| groupId      | the id of Group to be disbanded |

#### Group callback event

```java
//Registering group callback event
mITuyaGroup.registerGroupListener(new IGroupListener() {
        
            @Override
            public void onDpUpdate(long l, String s) {
            
            }
            
            @Override
            public void onGroupInfoUpdate(long l) {
            
            }
            
            @Override
            public void onGroupRemoved(long l) {
            
            }
        });

//Cancel group callback event
mITuyaGroup.unRegisterGroupListener();
```

#### Sending group control command

```java
mTuyaGroup.publishDps(String command, IResultCallback listener);
```

**Parameters**

| Parameters    | Description |
| ------------ | ----------- |
| command      | control commands |

**Example**

```java
//Code segment for switching on the light in a group
LampBean bean = new LampBean();
bean.setOpen(true);
HashMap<String, Object> hashMap = new HashMap<>();
hashMap.put(STHEME_LAMP_DPID_1, bean.isOpen());
mTuyaGroup.publishDps(JSONObject.toJSONString(hashMap),callback)；
```
**Notes**

The returned result of a command sent from a group means that the command is sent to the cloud successfully, and it does not mean that the device has been actually controlled.

#### Group data acquisition

For obtaining the group data, the data cannot be obtained before the initialization of Home (invoking getHomeDetail() or getHomeLocalCache).

```java
//Get customized group data
TuyaHomeDataManager.getInstance().getGroupBean(long groupId);

//Get device list under group
TuyaHomeDataManager.getInstance().getGroupDeviceList(long groupId);
```

#### Group data destruction

```java
//It is recommended to invoke the group data destruction function when exiting the group control page.
mITuyaGroup.onDestroy();
```