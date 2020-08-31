# Getting Shared Relationships

## Get List of All Active Shared Users in the Home

**Declaration**

```java
void queryUserShareList(long homeId, final ITuyaResultCallback<List<SharedUserInfoBean>> callback);
```

**Parameters**

| Parameter | Description                                            |
| --------- | ------------------------------------------------------ |
| homeId    | home id                                                |
| callback  | callback, including success or failure, cannot be null |

**Example**

```java
TuyaHomeSdk.getDeviceShareInstance().queryUserShareList(homeId, new ITuyaResultCallback<List<SharedUserInfoBean>>() {
            @Override
            public void onSuccess(List<SharedUserInfoBean> sharedUserInfoBeans) {}
            @Override
            public void onError(String errorCode, String errorMsg) {}
        });
```



## Get List of All Shared Uers Received

**Declaration**

```java
void queryShareReceivedUserList(final ITuyaResultCallback<List<SharedUserInfoBean>> callback);
```

**Parameters**

| Parameter | Description                                            |
| --------- | ------------------------------------------------------ |
| callback  | callback, including success or failure, cannot be null |

**Example**

```java
TuyaHomeSdk.getDeviceShareInstance().queryShareReceivedUserList(new ITuyaResultCallback<List<SharedUserInfoBean>>() {
            @Override
            public void onSuccess(List<SharedUserInfoBean> sharedUserInfoBeans) {}
            @Override
            public void onError(String errorCode, String errorMsg) {}
        });
```



## Obtaining User-shared Data that is Actively Shared by a Single User

**Declaration**

```java
void getUserShareInfo(long memberId, final ITuyaResultCallback<ShareSentUserDetailBean> callback);
```

**Parameters**

| Parameter | Description                                            |
| --------- | ------------------------------------------------------ |
| memberId  | share member id                                        |
| callback  | callback, including success or failure, cannot be null |

**Example**

```java
TuyaHomeSdk.getDeviceShareInstance().getUserShareInfo(mRelationId, new ITuyaResultCallback<ShareSentUserDetailBean>() {
                @Override
                public void onSuccess(ShareSentUserDetailBean shareSentUserDetailBean) {}
                @Override
                public void onError(String errorCode, String errorMsg) {}
            });
```



## Getting Shared Data from a Single Recipient

**Declaration**

```java
void getReceivedShareInfo(long memberId, final ITuyaResultCallback<ShareReceivedUserDetailBean> callback);
```

**Parameters**

| Parameter | Description                                            |
| --------- | ------------------------------------------------------ |
| memberId  | member id                                              |
| callback  | callback, including success or failure, cannot be null |

**Example**

```java
TuyaHomeSdk.getDeviceShareInstance().getReceivedShareInfo(mRelationId, new ITuyaResultCallback<ShareReceivedUserDetailBean>() {
                @Override
                public void onSuccess(ShareReceivedUserDetailBean shareReceivedUserDetailBean) {}
                @Override
                public void onError(String errorCode, String errorMsg) {}
            });
```



## Get a Single Device Shared User List

**Declaration**

```java
void queryDevShareUserList(String devId, final ITuyaResultCallback<List<SharedUserInfoBean>> callback);
```

**Parameters**

| Parameter | Description                                            |
| --------- | ------------------------------------------------------ |
| devId     | device id                                              |
| callback  | callback, including success or failure, cannot be null |

**Example**

```java
TuyaHomeSdk.getDeviceShareInstance().queryDevShareUserList(mDevId, new ITuyaResultCallback<List<SharedUserInfoBean>>() {
        @Override
        public void onError(String errorCode, String errorMsg) {}
        @Override
        public void onSuccess(List<SharedUserInfoBean> shareUserBeen) {}
    });
```



## Who Shares Access Devices

**Declaration**

```java
void queryShareDevFromInfo(String devId, final ITuyaResultCallback<SharedUserInfoBean> callback);
```

**Parameters**

| Parameter | Description                                            |
| --------- | ------------------------------------------------------ |
| devId     | receive share device id                                |
| callback  | callback, including success or failure, cannot be null |

**Example**

```java
TuyaHomeSdk.getDeviceShareInstance().queryDevShareUserList(devId, new ITuyaResultCallback<List<SharedUserInfoBean>>() {
            @Override
            public void onError(String s, String s1) {}
            @Override
            public void onSuccess(List<SharedUserInfoBean> list) {
            }
        });
```