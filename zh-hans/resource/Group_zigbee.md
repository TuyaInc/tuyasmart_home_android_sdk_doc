### Zigbee 群组

#### 群组列表获取

获取可创建群组设备列表

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
**参数说明**

| 参数         | 说明 |
| ------------ | -------------------------- |
| homeId             | 家庭 id |
| groupId            | 群组未创建，入参 groupId 传-1；已有群组，请传实际群组 ID |
| productId          | 选择创建群组的设备的 pid |

#### 创建群组

创建一个空群组

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
```
**参数说明**

| 参数         | 说明 |
| ------------ | -------------------------- |
| homeId    | 家庭 id |
| productId | 选择创建群组的设备的 pid |
| meshId    | 选择创建群组的设备的网关 id（可使用 deviceBean.getMeshId() 获取）|
| name      | 选择创建群组的名称 |

#### 新增设备到群组

添加新设备到群组，主要跟固件交互，写入群组设备到网关

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
**参数说明**

| 参数         | 说明 |
| ------------ | -------------------------- |
| meshId                 | 选择创建群组的设备的网关 id（可使用 deviceBean.getMeshId() 获取）|
| selectedDeviceIds      | 选择新增设备的 deviceId 列表 |
| gid                    | 群组的 localId 可以通过创建空群组时获得，若已有群组可通过 groupBean.getLocalId() 获取 |

#### 删除群组已有设备

删除网关中存储的群组中已有设备

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
**参数说明**

| 参数         | 说明 |
| ------------ | -------------------------- |
| meshId                 | 选择创建群组的设备的网关 id（可使用 deviceBean.getMeshId() 获取）|
| selectedDeviceIds      | 选择删除设备的 deviceId 列表 |
| gid                    | 群组的 localId 可以通过创建空群组时获得，若已有群组可通过 groupBean.getLocalId() 获取 |

#### 更新保存群组

将跟网关固件群组设备增删的结果同步更新保存到云端

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
**参数说明**

| 参数         | 说明 |
| ------------ | -------------------------- |
| groupId                | 群组 id |
| homeId                 | 家庭 id |
| selectedDeviceIds      | 新增或者删除成功的设备 id 列表 |
