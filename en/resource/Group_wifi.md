### Wi-Fi Group

#### Group List Acquisition

Obtain the device list of product

```java
TuyaHomeSdk.newHomeInstance(homeId).queryDeviceListToAddGroup(groupId, productId, 
        new IGetDevsFromGroupByPidCallback() {
        
            @Override
            public void onSuccess(List<GroupDeviceBean> bizResult) {
        
            }
        
            @Override
            public void onError(String errorCode, String errorMsg) {
        
            }
        });
```

**Parameters**


| Parameters    | Description |
| ------------ | -------------------------- |
| homeId       | Family ID, please refer to the family management section for details |
| groupId      | the group is not created, parameter groupId must be an integer -1 |
| productId      | Select the pid of the device that created the group |

#### Creating a Group

```java
TuyaHomeSdk.newHomeInstance(homeId).createNewGroup(productId, name, selectedDeviceIds, 
        new ICreateGroupCallback() {
        
            @Override
            public void onSuccess(long groupId) {
                    //return groupId
            }
            
            @Override
            public void onError(String errorCode, String errorMsg) {
            
            }
        });
```
**Parameters**

| Parameters    | Description |
| ------------ | -------------------------- |
| homeId       | Family ID, please refer to the family management section for details |
| productId           | the pid of the device what is using to create group|
| name                | a name of the group to be created |
| selectedDeviceIds   | the deviceList choosed |

#### Update and Save Group

```java
TuyaHomeSdk.newGroupInstance(groupId).updateDeviceList(deviceIds, 
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
| ------------ | -------------------------- |
| groupId             | group id |
| deviceIds           | Add or delete the selected device id list |