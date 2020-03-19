# 修改备注名

## 分享者修改被分享者的备注名

分享者修改被分享者的备注名，你分享给其他人设备，你可以修改这个人的备注名。

**接口说明**

```java
void addShareWithHomeId(long homeId, String countryCode, String userAccount, List<String> devIds, ITuyaResultCallback<SharedUserInfoBean> callback);
```

**参数说明**

| 参数        | 说明                                  |
| ----------- | ------------------------------------- |
| homeId      | 分享者家庭 id                          |
| countryCode | 手机区号码, 例如中国是 “86”             |
| phoneNumber | 手机号码                              |
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

## 被分享者修改分享者的备注名

被分享者修改分享人的备注名。你收到了其他人的分享，你可修改这个人的备注名。

**接口说明**

```java
void renameReceivedShareNickname(long memberId, String name, IResultCallback callback);
```

**参数说明**

| 参数     | 说明                                   |
| -------- | -------------------------------------- |
| memberId | 分享者家庭 id 从 SharedUserInfoBean 中获取 |
| callback | 回调，包括修改成功和失败，不能为 null  |

**示例代码**

```java
void addShareWithHomeId(homeId, countryCode, userAccount, devIds, new ITuyaResultCallback<SharedUserInfoBean>() {
    @Override
    public void onSuccess(SharedUserInfoBean bean) {}
    @Override
    public void onError(String errorMsg, String errorCode) {}
});
```