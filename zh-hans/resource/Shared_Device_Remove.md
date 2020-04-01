# 移除分享

## 删除共享关系

分享者通过memberId 删除与这个关系用户的所有共享关系（用户维度删除）。

**接口说明**

```java
void removeUserShare(long memberId, IResultCallback callback);
```

**参数说明**

| 参数     | 说明                                  |
| :-------- | :------------------------------------- |
| memberId | 待删除分享的用户 id                    |
| callback | 回调，包括删除成功或失败，不能为 null |

**示例代码**

```java
void removeUserShare(memberId, new IResultCallback() {
    @Override
    public void onError(String code, String error) {}
    @Override
    public void onSuccess() {}
})
```

## 删除收到的共享关系

被分享者通过 memberId 获取收到这个关系用户的所有共享设备信息。

**接口说明**

```java
void removeReceivedUserShare(long memberId, IResultCallback callback);
```

**参数说明**

| 参数     | 说明                                  |
| -------- | ------------------------------------- |
| memberId | 待删除分享的用户id                    |
| callback | 回调，包括删除成功或失败，不能为 null |

**示例代码**

```java
void removeReceivedUserShare(memberId, new IResultCallback() {
    @Override
    public void onError(String code, String error) {}
    @Override
    public void onSuccess() {}
})
```

## 删除某个设备共享

分享者删除指定关系用户下的某个共享的设备。

**接口说明**

```java
void disableDevShare(String devId, long memberId, IResultCallback callback);
```

**参数说明**

| 参数     | 说明                                  |
| -------- | ------------------------------------- |
| devId    | 待删除的设备 id                        |
| memberId | 待删除分享的用户 id                    |
| callback | 回调，包括删除成功或失败，不能为 null |

**示例代码**

```java
void disableDevShare(devId, memberId, new IResultCallback() {
    @Override
    public void onError(String code, String error) {}
    @Override
    public void onSuccess() {}
})
```

## 移除收到的分享设备

分享者删除指定关系用户下的某个共享的设备。

**接口说明**

```java
void removeReceivedDevShare(String devId, IResultCallback callback);
```

**参数说明**

| 参数     | 说明                                  |
| -------- | ------------------------------------- |
| devId    | 待删除的设备 id                        |
| callback | 回调，包括删除成功或失败，不能为 null |

**示例代码**

```java
TuyaHomeSdk.getDeviceShareInstance().removeReceivedDevShare(devId,new IResultCallback() {
    @Override
    public void onError(String code, String error) {}
    @Override
    public void onSuccess() {}
})

```