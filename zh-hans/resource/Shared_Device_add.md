# 添加分享

## 添加多个设备共享

分享多个设备给指定用户，会将要分享的设备追加到指定用户的所有分享中。

**接口说明**

```java
void addShareWithHomeId(long homeId, String countryCode, String userAccount, List<String> devIds, ITuyaResultCallback<SharedUserInfoBean> callback);
```

**参数说明**

| 参数        | 说明                                  |
| ----------- | ------------------------------------- |
| homeId      | 分享者家庭 id                          |
| countryCode | 手机区号码,例如中国是 “86”             |
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

## 批量添加设备共享

批量添加设备共享，当知道目标用户的 id 时调用。

**接口说明**

```java
void addShareWithMemberId(long memberId,List<String> devIds,IResultCallback callback);
```

**参数说明**

| 参数     | 说明                                  |
| -------- | ------------------------------------- |
| memberId | 分享目标用户 id                        |
| devIds   | 分享的设备 id 列表                      |
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

## 单个设备取消共享

通过用户关系id取消单个设备分享。

**接口说明**

```java
void disableDevShare(String devId, long memberId, IResultCallback callback);
```

**参数说明**

| 参数     | 说明                                      |
| -------- | ----------------------------------------- |
| devId    | 待取消设备 id                              |
| memberId | 待取消分享用户                            |
| callback | 回调，包括分享取消成功或失败，不能为 null |

**示例代码**

```java
void disableDevShare (devId, memberId, new IResultCallback() {
    @Override
    public void onError(String code, String error) {}
    @Override
    public void onSuccess() {}
});
```

## 单个设备开启分享

通过用户关系id开启单个设备分享。

**接口说明**

```java
void enableDevShare(String devId, long memberId, IResultCallback callback);
```

**参数说明**

| 参数     | 说明                                      |
| -------- | ----------------------------------------- |
| devId    | 待取消设备 id                              |
| memberId | 待取消分享用户                            |
| callback | 回调，包括分享开启成功或失败，不能为 null |

**示例代码**

```java
void enableDevShare (devId, memberId, new IResultCallback() {
    @Override
    public void onError(String code, String error) {}
    @Override
    public void onSuccess() {}
});
```