### 群组操控

#### 实例化

群组实例初始化

```java
ITuyaGroup mITuyaGroup= TuyaHomeSdk.newGroupInstance(groupId);
```
**参数说明**

| 参数         | 说明 |
| ------------ | -------------------------- |
| groupId             | 群组 id |

#### 修改群组名称

修改某个群组名称

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
**参数说明**

| 参数         | 说明 |
| ------------ | -------------------------- |
| groupId             | 群组 id |
| titleName           | 群组名称 |

#### 解散群组

解散一个群组

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
**参数说明**

| 参数         | 说明 |
| ------------ | -------------------------- |
| groupId             | 待解散的群组 id |

#### 群组控制回调

```java
//注册群组回调事件
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

//注销群组回调事件
mITuyaGroup.unRegisterGroupListener();
```

#### 发送群组控制命令

```java
mTuyaGroup.publishDps(String command, IResultCallback listener);
```
**参数说明**

| 参数         | 说明 |
| ------------ | -------------------------- |
| command             | 控制命令 |

**代码范例**

```java
//群组开灯代码片段
LampBean bean = new LampBean();
bean.setOpen(true);
HashMap<String, Object> hashMap = new HashMap<>();
hashMap.put(STHEME_LAMP_DPID_1, bean.isOpen());
mTuyaGroup.publishDps(JSONObject.toJSONString(hashMap),callback)；
```
**注意事项**

群组的发送命令返回结果，是指发送给云端成功，并不是指实际控制设备成功。 

#### 群组数据获取

获取群组数据，需要初始化 Home（调用 getHomeDetail() 或者 getHomeLocalCache() ）之后,才能取到数据

```java
//获取制定群组数据
TuyaHomeSdk.getDataInstance().getGroupBean(long groupId);

//获取群组下设备列表
TuyaHomeSdk.getDataInstance().getGroupDeviceList(long groupId);
```

#### 群组数据销毁

```java
//群组数据销毁，建议退出群组控制页面的时候调用。
mITuyaGroup.onDestroy();
```