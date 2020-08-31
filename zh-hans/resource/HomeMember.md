# 家庭成员管理

**MemberBean 字段信息**

| 字段 | 类型 | 描述 |
| --- | --- | --- |
| homeId | long  | 家庭 ID |
| nickName | String | 备注名 |
| admin | boolean | 是否是管理员 |
| memberId | long | 成员 ID |
| headPic | String | 头像 Url 地址 |
| account | String  | 成员账户名称 |
| uid | String | 成员唯一标识 ID |
| memberStatus | int| 成员状态 （1:等待接受 2:接受 3:拒绝）|

## 更新成员备注名和权限

**接口说明**

```java
void updateMember(long memberId, String name, boolean admin, IResultCallback callback)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| memberId | 成员 ID |
| name | 名称 |
| admin | 是否是管理员 |

**示例代码**

```java
TuyaHomeSdk.getMemberInstance().updateMember(memberId, name, admin, new IResultCallback() {
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

## 更新成员信息

**接口说明**

```java
void updateMember(MemberWrapperBean memberWrapperBean, IResultCallback callback)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| memberWrapperBean | 成员信息 |

**示例代码**

```java
TuyaHomeSdk.getMemberInstance().updateMember(memberWrapperBean, new IResultCallback() {
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

## 更新成员权限

**接口说明**

```java
void updateMemberRole(long memberId, boolean admin, IResultCallback callback)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| memberId | 成员 ID |
| admin | 是否是管理员 |

**示例代码**

```java
TuyaHomeSdk.getMemberInstance().updateMemberRole(memberId, admin, new IResultCallback() {
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

## 新增成员

**接口说明**

`MemberWrapperBean` 对象中的 autoAccept 字段用于控制是否需要受邀者同意，若为 false 则需要受邀者调用 `processInvitation()` 方法接受或者同意邀请后才能加入家庭。

```java
void addMember(MemberWrapperBean memberWrapperBean, ITuyaDataCallback<MemberBean> callback)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| memberWrapperBean | 成员信息 |

**示例代码**

```java
TuyaHomeSdk.getMemberInstance().addMember(memberWrapperBean, new ITuyaDataCallback<MemberBean>() {
        @Override
        public void onSuccess(MemberBean result) {
            // do something
        }
        @Override
        public void onError(String errorCode, String errorMessage) {
            // do something
        }
    });
```

## Home下面添加成员

**接口说明**

```java
void addMember(long mHomeId, String countryCode, String userAccount, String name, boolean admin, ITuyaMemberResultCallback callback)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| mHomeId | 家庭 ID |
| countryCode | 国家码 |
| userAccount | 用户名 |
| name | 昵称 |
| admin | 是否是管理员 |

**示例代码**

```java
TuyaHomeSdk.getMemberInstance().addMember(mHomeId, countryCode, userAccount, name, admin, new ITuyaMemberResultCallback() {
        @Override
        public void onSuccess(MemberBean bean) {
            // do something
        }
        @Override
        public void onError(String errorCode, String errorMsg) {
            // do something
        }
    });
```

## 移除 Home下面的成员

**接口说明**

```java
void removeMember(long memberId, IResultCallback callback)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| memberId | 成员 ID |

**示例代码**

```java
TuyaHomeSdk.getMemberInstance().removeMember(memberId, new IResultCallback() {
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

## 查询 Home 下面的成员列表

**接口说明**

```java
void queryMemberList(long mHomeId, ITuyaGetMemberListCallback callback)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| mHomeId | 家庭 ID |

**示例代码**

```java
TuyaHomeSdk.getMemberInstance().queryMemberList(mHomeId, new ITuyaGetMemberListCallback() {
        @Override
        public void onSuccess(List<MemberBean> memberBeans) {
            // do something
        }
        @Override
        public void onError(String errorCode, String error) {
            // do something
        }
    });
```

## 获取家庭成员可关联设备

**接口说明**

```java
void getMemberDeviceList(long relationId, ITuyaDataCallback<Map<String, Object>> callback)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| relationId | 家庭成员 ID |

**示例代码**

```java
TuyaHomeSdk.getMemberInstance().getMemberDeviceList(relationId, new ITuyaDataCallback<Map<String, Object>>() {
        @Override
        public void onSuccess(Map<String, Object> result) {
            // do something
        }
        @Override
        public void onError(String errorCode, String errorMessage) {
            // do something
        }
    });
```

## 获取指定家庭成员房间的授权情况

**接口说明**

```java
void getAuthRoomList(long homeId, long memberId, ITuyaDataCallback<List<RoomAuthBean>> callback)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| homeId | 家庭 ID |
| memberId | 成员 ID |
| callback | 结果回调 |

**示例代码**

```java
TuyaHomeSdk.getMemberInstance().getAuthRoomList(homeId, memberId, new ITuyaDataCallback<List<RoomAuthBean>>() {
        @Override
        public void onError(String errorCode, String errorMessage) {
            // do something
        }
        @Override
        public void onSuccess(<List<RoomAuthBean>> result) {
            // do something
        }
    });
```

## 设置指定家庭的指定成员的房间权限

**接口说明**

```java
void saveAuthRoomList(long homeId, long memberId, List<Long> rooms, IResultCallback callback)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| homeId | 家庭 ID |
| memberId | 成员 ID |
| rooms | 房间 ID 列表 |
| callback | 结果回调 |

**示例代码**

```java
TuyaHomeSdk.getMemberInstance().saveAuthRoomList(homeId, memberId, rooms, new IResultCallback() {
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

## 获取指定家庭下面的成员的场景的授权列表

**接口说明**

```java
void getAuthSceneList(long homeId, long memberId, ITuyaDataCallback<List<SceneAuthBean>> callback)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| homeId | 家庭 ID |
| memberId | 成员 ID |
| callback | 结果回调 |

**示例代码**

```java
TuyaHomeSdk.getMemberInstance().getAuthSceneList(homeId, memberId, new ITuyaDataCallback<List<SceneAuthBean>>() {
        @Override
        public void onError(String errorCode, String errorMessage) {
            // do something
        }
        @Override
        public void onSuccess(<List<SceneAuthBean>> result) {
            // do something
        }
    });
```

## 设置指定家庭的指定成员的场景权限

**接口说明**

```java
void saveAuthSceneList(long homeId, long memberId, List<String> ruleIds, IResultCallback callback)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| homeId | 家庭 ID |
| memberId | 成员 ID |
| ruleIds | 场景规则 ID 列表 |
| callback | 结果回调 |

**示例代码**

```java
TuyaHomeSdk.getMemberInstance().saveAuthSceneList(homeId, memberId, ruleIds, new IResultCallback() {
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

## 家庭成员绑定关联账号

**接口说明**

```java
void addMemberAccount(long id, String countryCode, String userAccount, int role, IResultCallback callback)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| id | 成员 ID |
| countryCode | 国家码 |
| userAccount | 关联账号 |
| role | 成员角色 |
| callback | 结果回调 |

**示例代码**

```java
TuyaHomeSdk.getMemberInstance().addMemberAccount(id, countryCode, userAccount, role, new IResultCallback() {
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

## 家庭成员绑定关联账号

**接口说明**

```java
void addMemberAccount(long id, String countryCode, String userAccount, boolean admin, IResultCallback callback)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| id | 成员 ID |
| countryCode | 国家码 |
| userAccount | 用户名 |
| admin | 是否是管理员 |

**示例代码**

```java
TuyaHomeSdk.getMemberInstance().addMemberAccount(id, countryCode, userAccount, admin, new IResultCallback() {
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

## 上传成员头像

**接口说明**

```java
void uploadMemberAvatar(String filename, File file, IBooleanCallback callback)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| filename | 文件名 |
| file | 文件 |

**示例代码**

```java
TuyaHomeSdk.getMemberInstance().uploadMemberAvatar(filename, file, new IBooleanCallback() {
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

## 接受或拒绝加⼊入家庭

**接口说明**

```java
void processInvitation(long homeId, boolean action, IResultCallback callBack)
```

**参数说明**

| 参数 | 说明 |
| :--- | :--- |
| homeId | 家庭 ID |
| action | 接受/拒绝 |

**示例代码**

```java
TuyaHomeSdk.getMemberInstance().processInvitation(homeId, action, new IResultCallback() {
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


