### ZigBee Group

#### Group List Acquisition

```java
TuyaHomeSdk.newHomeInstance(homeId).queryZigbeeDeviceListToAddGroup(groupId, productId, 
        new ITuyaResultCallback<List<GroupDeviceBean>>() {
        
            @Override
            public void onSuccess(List<GroupDeviceBean> arrayList) {
                
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
| productId    | Select the pid of the device that created the group |

#### Creating a Group

```java
TuyaHomeSdk.newHomeInstance(homeId).createZigbeeGroup(productId, meshId, name, 
        new ITuyaResultCallback<CloudZigbeeGroupCreateBean>() {
        
            @Override
            public void onSuccess(CloudZigbeeGroupCreateBean cloudZigbeeGroupCreateBean) {
                //输出结果
                long mGroupId = cloudZigbeeGroupCreateBean.getGroupId();
                String mGId = cloudZigbeeGroupCreateBean.getLocalId();
            }
        
            @Override
            public void onError(String errorCode, String errorMsg) {
                
            }
        });
});
```
**Parameters**

| Parameters    | Description |
| ------------ | -------------------------- |
| homeId              | Family ID, please refer to the family management section for details |
| productId           | the pid of the device what is using to create group|
| name                | a name of the group to be created |
| meshId              | deviceBean.getMeshId() |

#### Add Devices to Group

Add new devices to the group, mainly interact with the firmware, write group devices to the gateway

```java
mITuyaZigbeeGroup.addDeviceToGroup(meshId, selectedDeviceIds, gid, 
        new ITuyaResultCallback<ZigbeeGroupCreateResultBean>() {
       
            @Override
            public void onSuccess(ZigbeeGroupCreateResultBean zigbeeGroupCreateResultBean) {
                if (zigbeeGroupCreateResultBean != null) {
                    //新增设备成功的列表
                    if (zigbeeGroupCreateResultBean.getSuccess() != null && zigbeeGroupCreateResultBean.getSuccess().size() > 0) {
                        List<String> mAddSuccessDeviceIds = new ArrayList<>();
                        mAddSuccessDeviceIds.addAll(zigbeeGroupCreateResultBean.getSuccess());
                    }
                    //新增设备失败的列表
                    if (zigbeeGroupCreateResultBean.getFailure() != null && zigbeeGroupCreateResultBean.getFailure().size() > 0) {
                        List<String>mAddFailDeviceIds = new ArrayList<>();
                        mAddFailDeviceIds.addAll(zigbeeGroupCreateResultBean.getFailure());
                    }
                }
            }
            
            @Override
            public void onError(String errorCode, String errorMsg) {
                
            }
        });
```

**Parameters**

| Parameters    | Description |
| ------------ | -------------------------- |
| meshId                 | Select the gateway id of the device that created the group, (deviceBean.getMeshId())|
| selectedDeviceIds      | the idList of the selected devices |
| gid                    | the localId of group（groupBean.getLocalId() or cloudZigbeeGroupCreateBean.getLocalId()) |

#### Delete Devices of Group

Delete existing devices in the group stored in the gateway

```java
mITuyaZigbeeGroup.delDeviceToGroup(meshId, selectedDeviceIds, gid, 
        new ITuyaResultCallback<ZigbeeGroupCreateResultBean>() {
        
            @Override
            public void onSuccess(ZigbeeGroupCreateResultBean zigbeeGroupCreateResultBean) {
                if (zigbeeGroupCreateResultBean != null) {
                    //删除设备成功的列表
                    if (zigbeeGroupCreateResultBean.getSuccess() != null && zigbeeGroupCreateResultBean.getSuccess().size() > 0) {
                        List<String> mDelSuccessDeviceIds = new ArrayList<>();
                        mDelSuccessDeviceIds.addAll(zigbeeGroupCreateResultBean.getSuccess());
                    }
                    //删除设备失败的列表
                    if (zigbeeGroupCreateResultBean.getFailure() != null && zigbeeGroupCreateResultBean.getFailure().size() > 0) {
                        List<String> mDelFailDeviceIds = new ArrayList<>();
                        mDelFailDeviceIds.addAll(zigbeeGroupCreateResultBean.getFailure());
                    }
                }
            }
            
            @Override
            public void onError(String errorCode, String errorMsg) {
                
            }
        }); 
```
**Parameters**

| Parameters    | Description |
| ------------ | -------------------------- |
| meshId                 | Select the gateway id of the device that created the group, (deviceBean.getMeshId())|
| selectedDeviceIds      | the idList of the selected devices |
| gid                    | the localId of group（groupBean.getLocalId() or cloudZigbeeGroupCreateBean.getLocalId()) |

#### Update and Save Group

Save and update the results of the addition and deletion of the gateway firmware group device to the cloud

```java
TuyaHomeSdk.newZigbeeGroupInstance(groupId).updateGroupDeviceList(homeId, selectedDeviceIds, 
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
| groupId                | group id |
| homeId                 | Family ID, please refer to the family management section for details |
| selectedDeviceIds      | the ids of the choosed device that to add or del successfully |
