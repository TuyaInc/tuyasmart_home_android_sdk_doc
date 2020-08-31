# 添加共享

## 添加多个设备共享（覆盖）

分享多个设备给指定用户，会将指定用户的以前所有分享覆盖掉

**接口说明**

```java
void addShare(long homeId, String countryCode, final String userAccount, ShareIdBean bean, boolean autoSharing, final ITuyaResultCallback<SharedUserInfoBean> callback);
```

**参数说明**

| 参数        | 说明                                  |
| ----------- | ------------------------------------- |
| homeId      | 设备所属的家庭 id                     |
| countryCode | 手机区号码,例如中国是 “86”            |
| userAccount | 分享对象的账号                        |
| bean        | 分享的设备 id 列表                    |
| autoSharing | 自动分享                              |
| callback    | 回调，包括分享成功或失败，不能为 null |

**示例代码**

```java
TuyaHomeSdk.getDeviceShareInstance().addShare(homeId, countryCode, userAccount,
                shareIdBean, autoSharing, new ITuyaResultCallback<SharedUserInfoBean>() {
                    @Override
                    public void onSuccess(SharedUserInfoBean sharedUserInfoBean) {}
                    @Override
                    public void onError(String errorCode, String errorMsg) {}
                });
```



## 添加共享（新增，不覆盖旧的分享）

### 添加共享（已知目标用户id）

分享多个设备给指定用户，会将要分享的设备追加到指定用户的所有分享中。

**接口说明**

```java
void addShareWithMemberId(long memberId,List<String> devIds,IResultCallback callback);
```

**参数说明**

| 参数     | 说明                                  |
| -------- | ------------------------------------- |
| memberId | 分享目标用户 id                       |
| devIds   | 分享的设备 id 列表                    |
| callback | 回调，包括分享成功或失败，不能为 null |

**示例代码**

```java
void addShareWithMemberId (memberId, devIds, new IResultCallback() {
    @Override
    public void onError(String code, String error) {}
    @Override
    public void onSuccess() {}
});
```



### 添加共享（已知目标用户账号）

分享多个设备给指定用户，会将要分享的设备追加到指定用户的所有分享中

**接口说明**

```java
void addShareWithHomeId(long homeId, String countryCode, String userAccount, List<String> devIds, ITuyaResultCallback<SharedUserInfoBean> callback);
```

**参数说明**

| 参数        | 说明                                  |
| ----------- | ------------------------------------- |
| homeId      | 设备的家庭 id                         |
| countryCode | 手机区号码,例如中国是 “86”             |
| userAccount | 被分享者账号                    |
| devIds      | 分享的设备 id 列表                      |
| callback    | 回调，包括分享成功或失败，不能为 null |

**示例代码**

```java
void addShareWithHomeId(homeId, countryCode, userAccount, devIds, new ITuyaResultCallback<SharedUserInfoBean>() {
    @Override
    public void onSuccess(SharedUserInfoBean bean) {}
    @Override
    public void onError(String errorMsg, String errorCode) {}
});
```