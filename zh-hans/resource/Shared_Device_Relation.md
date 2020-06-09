# 分享关系获取

## 获取家庭下所有主动共享的用户列表

**接口说明**

```java
void queryUserShareList(long homeId, final ITuyaResultCallback<List<SharedUserInfoBean>> callback);
```

**参数说明**

| 参数     | 说明                                  |
| -------- | ------------------------------------- |
| homeId   | 家庭id                                |
| callback | 回调，包括获取成功或失败，不能为 null |

**示例代码**

```java
TuyaHomeSdk.getDeviceShareInstance().queryUserShareList(homeId, new ITuyaResultCallback<List<SharedUserInfoBean>>() {
            @Override
            public void onSuccess(List<SharedUserInfoBean> sharedUserInfoBeans) {}
            @Override
            public void onError(String errorCode, String errorMsg) {}
        });
```



## 获取所有收到共享的用户列表

**接口说明**

```java
void queryShareReceivedUserList(final ITuyaResultCallback<List<SharedUserInfoBean>> callback);
```

**参数说明**

| 参数     | 说明                                 |
| -------- | ------------------------------------ |
| callback | 回调，包括获取成功或失败，不能为null |

**示例代码**

```java
TuyaHomeSdk.getDeviceShareInstance().queryShareReceivedUserList(new ITuyaResultCallback<List<SharedUserInfoBean>>() {
            @Override
            public void onSuccess(List<SharedUserInfoBean> sharedUserInfoBeans) {}
            @Override
            public void onError(String errorCode, String errorMsg) {}
        });
```



## 获取单个主动共享的用户共享数据

**接口说明**

```java
void getUserShareInfo(long memberId, final ITuyaResultCallback<ShareSentUserDetailBean> callback);
```

**参数说明**

| 参数     | 说明                                 |
| -------- | ------------------------------------ |
| memberId | 分享用户的id                         |
| callback | 回调，包括获取成功或失败，不能为null |

**示例代码**

```java
TuyaHomeSdk.getDeviceShareInstance().getUserShareInfo(mRelationId, new ITuyaResultCallback<ShareSentUserDetailBean>() {
                @Override
                public void onSuccess(ShareSentUserDetailBean shareSentUserDetailBean) {}

                @Override
                public void onError(String errorCode, String errorMsg) {}
            });
```



## 获取单个收到共享的用户共享数据

**接口说明**

```java
void getReceivedShareInfo(long memberId, final ITuyaResultCallback<ShareReceivedUserDetailBean> callback);
```

**参数说明**

| 参数     | 说明                                 |
| -------- | ------------------------------------ |
| memberId | 用户id                               |
| callback | 回调，包括获取成功或失败，不能为null |

**示例代码**

```java
 TuyaHomeSdk.getDeviceShareInstance().getReceivedShareInfo(mRelationId, new ITuyaResultCallback<ShareReceivedUserDetailBean>() {
                @Override
                public void onSuccess(ShareReceivedUserDetailBean shareReceivedUserDetailBean) {}
                @Override
                public void onError(String errorCode, String errorMsg) {}
            });
```



## 获取单设备共享用户列表

**接口说明**

```java
void queryDevShareUserList(String devId, final ITuyaResultCallback<List<SharedUserInfoBean>> callback);
```

**参数说明**

| 参数     | 说明                                 |
| -------- | ------------------------------------ |
| devId    | 分享的设备id                         |
| callback | 回调，包括获取成功或失败，不能为null |

**示例代码**

```java
TuyaHomeSdk.getDeviceShareInstance().queryDevShareUserList(mDevId, new ITuyaResultCallback<List<SharedUserInfoBean>>() {
        @Override
        public void onError(String errorCode, String errorMsg) {}
        @Override
        public void onSuccess(List<SharedUserInfoBean> shareUserBeen) {}
    });
```



## 获取设备分享来自哪里

**接口说明**

```java
void queryShareDevFromInfo(String devId, final ITuyaResultCallback<SharedUserInfoBean> callback);
```

**参数说明**

| 参数     | 说明                                 |
| -------- | ------------------------------------ |
| devId    | 设备id                               |
| callback | 回调，包括获取成功或失败，不能为null |

**示例代码**

```java
TuyaHomeSdk.getDeviceShareInstance().queryDevShareUserList(devId, new ITuyaResultCallback<List<SharedUserInfoBean>>() {
            @Override
            public void onError(String s, String s1) {}
            @Override
            public void onSuccess(List<SharedUserInfoBean> list) {}
        });
```
