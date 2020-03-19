### Wi-Fi 群组

#### 群组列表获取

查询可以创组建群组的设备列表

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
**参数说明**

| 参数         | 说明 |
| ------------ | -------------------------- |
| homeId          | 家庭 id |
| groupId         | 群组未创建，入参 groupId 传-1；已有群组，请传实际群组 ID |
| productId       | 选择创建群组的设备的 pid |

#### 创建群组

创建一个群组

```java
TuyaHomeSdk.newHomeInstance(homeId).createNewGroup(productId, name, selectedDeviceIds, 
        new ICreateGroupCallback() {
        
            @Override
            public void onSuccess(long groupId) {
                    //返回groupId
            }
            
            @Override
            public void onError(String errorCode, String errorMsg) {
            
            }
        });
```
**参数说明**

| 参数         | 说明 |
| ------------ | -------------------------- |
| homeId              | 家庭 id |
| productId           | 选择创建群组的设备的 pid |
| name                | 选择创建群组的名称 |
| selectedDeviceIds   | 选择的设备的 deviceId 列表 |


#### 更新保存群组

更新保存群组到云端

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
**参数说明**

| 参数         | 说明 |
| ------------ | -------------------------- |
| groupId             | 群组 id |
| deviceIds           | 新增或者删除选择后的设备 id 列表 |