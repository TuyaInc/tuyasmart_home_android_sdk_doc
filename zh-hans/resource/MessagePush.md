# 消息推送设置

## 获取消息总开关的当前状态

消息推送开关为总开关，关闭状态下无法接收到 设备告警、家庭消息、通知消息 等任何消息。

**接口说明**

```java
void getPushStatus(ITuyaResultCallback<PushStatusBean> callback);
```

**参数说明**

| 参数     | 说明                               |
| -------- | ---------------------------------- |
| callback | 回调，包括获取总开关状态成功和失败 |

**示例代码**

```java
 TuyaHomeSdk.getPushInstance().getPushStatus(new ITuyaResultCallback<PushStatusBean>() {
       @Override
       public void onSuccess(PushStatusBean result) {}
       @Override
       public void onError(String errorCode, String errorMessage) {}
 });
```

## 设置消息总开关的当前状态

消息推送开关为总开关，关闭状态下无法接收到 设备告警、家庭消息、通知消息 等任何消息

**接口说明**

```java
void setPushStatus(boolean isOpen, ITuyaDataCallback<Boolean> callback);
```

**参数说明**

| 参数     | 说明                     |
| -------- | ------------------------ |
| isOpen   | 是否开启                 |
| callback | 回调，包括设置成功和失败 |

**示例代码**

```java
TuyaHomeSdk.getPushInstance().setPushStatus(open, new ITuyaDataCallback<Boolean>() {
      @Override
      public void onSuccess(Boolean result) {}
      @Override
      public void onError(String errorCode, String errorMessage) {}
});
```

## 根据消息类型获取消息的开关状态

根据消息类型获取当前类型消息的开关状态

**接口说明**

```java
void getPushStatusByType(PushType type, ITuyaDataCallback<Boolean> callback);
```

**参数说明**

| 参数     | 说明                     |
| -------- | ------------------------ |
| type     | 消息类型                 |
| callback | 回调，包括获取成功和失败 |

**示例代码**

```java
TuyaHomeSdk.getPushInstance().getPushStatusByType(type, new ITuyaDataCallback<Boolean>() {
      @Override
      public void onSuccess(Boolean result) {}
      @Override
      public void onError(String errorCode, String errorMessage) {}
});
```

## 根据消息类型获取消息的开关状态

根据消息类型获取当前类型消息的开关状态。

**接口说明**

```java
void setPushStatusByType(PushType type, isOpen, ITuyaDataCallback<Boolean> callback);
```

**参数说明**

| 参数     | 说明                     |
| -------- | ------------------------ |
| type     | 消息类型                 |
| isOpen   | 是否开启                 |
| callback | 回调，包括获取成功和失败 |

**示例代码**

```java
TuyaHomeSdk.getPushInstance().setPushStatusByType(pushType, checked, new ITuyaDataCallback<Boolean>() {
      @Override
      public void onSuccess(Boolean result) {
      }

      @Override
      public void onError(String errorCode, String errorMessage) {
      }
});
```