# Message Push Settings

## Get the current status of the message master switch

The message push switch is the master switch. In the off state, no messages such as device alarms, home messages, and notification messages can be received.

**Declaration**

```java
void getPushStatus(ITuyaResultCallback<PushStatusBean> callback);
```

**Parameters**

| Parameters     | Description                    |
| -------- | ----------------------- |
| callback | Callbacks, including success and failure to get total switch status |

**Example**

```java
 TuyaHomeSdk.getPushInstance().getPushStatus(new ITuyaResultCallback<PushStatusBean>() {
       @Override
       public void onSuccess(PushStatusBean result) {}
       @Override
       public void onError(String errorCode, String errorMessage) {}
 });
```

## Set the current state of the message master switch

The message push switch is the master switch, and no messages such as device alarms, home messages, notification messages, etc. can be received in the off state.

**Declaration**

```java
void setPushStatus(boolean isOpen, ITuyaDataCallback<Boolean> callback);
```

**Parameters**

| parameters    | description                       |
| -------- | --------------------------- |
| isOpen   | Whether to open                    |
| callback | Callbacks, including setting success and failure             |

**Example**

```java
TuyaHomeSdk.getPushInstance().setPushStatus(open, new ITuyaDataCallback<Boolean>() {
      @Override
      public void onSuccess(Boolean result) {}
      @Override
      public void onError(String errorCode, String errorMessage) {}
});
```

## Get the switch status of the message according to the message type

Get the switch status of the current type of message according to the message type

**Declaration**

```java
void getPushStatusByType(PushType type, ITuyaDataCallback<Boolean> callback);
```

**Parameters**

| parameters     | description                     |
| -------- | ------------------------ |
| type     | Message type                |
| callback | Callbacks, including success and failure |

**Example**

```java
TuyaHomeSdk.getPushInstance().getPushStatusByType(type, new ITuyaDataCallback<Boolean>() {
      @Override
      public void onSuccess(Boolean result) {}
      @Override
      public void onError(String errorCode, String errorMessage) {}
});
```

## Get the switch status of the message according to the message type

Gets the switch status of the current type of message according to the message type.

**Declaration**

```java
void setPushStatusByType(PushType type, isOpen, ITuyaDataCallback<Boolean> callback);
```

**Parameter**

| parameters     | description                     |
| -------- | ------------------------ |
| type     | Message type                 |
| isOpen     | Whether to open                 |
| callback | Callbacks, including success and failure |

**Example**

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
