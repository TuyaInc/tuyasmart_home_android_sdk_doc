## Get Message List

Used to get a list of all messages.

|     classname     |      description      |
| ---------- | ------------ |
| ITuyaMessage | User feedback management class |

**Declaration**

```java
void getMessageList(ITuyaDataCallback<List<MessageBean>> callback);
```

**Parameters**

| parameter     | description                             |
| -------- | -------------------------------- |
| callback | Callbacks, including success and failure of getting message list |

**MessageBean data model**

|      field      |  type   |               description               |
| ------------ | ----- | ------------------------------ |
|    dateTime    | String  |            Date and time           |
|      Icon      | String  |           Message icon URL            |
| msgTypeContent | String  |           Message type name           |
|   msgContent   | String  |             Message content             |
|    msgType     | Integer |             Message type             |
|    msgSrcId    | String  | Device Id (this field is only available in alarm messages) |
|       id       | String  |              Message id             |

**Example**

```java
TuyaHomeSdk.getMessageInstance().getMessageList(new ITuyaDataCallback<List<MessageBean>>() {
    @Override
    public void onSuccess(List<MessageBean> result) {}
    @Override
    public void onError(String errorCode, String errorMessage) {}
});
```

## Delete message

Used to delete messages in batches.

**Declaration**

```java
void deleteMessage(List<String> mIds, IBooleanCallback callback);
```

**Parameters**

| parameter    | description                             |
| ------- | -------------------------------- |
| mIds    | Device ids |
| contact | Callbacks, including delete success and failure        |

**Example**

```java
TuyaMessage.getInstance().deleteMessages(
    deleteList, 
    new IBooleanCallback() {
        @Override
        public void onSuccess() {}
        @Override
        public void onError(String errorCode, String errorMessage) {}
});
```

## Get the latest news

Gets the timestamp of the latest message.

**Declaration**

```java
void getMessageMaxTime(ITuyaDataCallback<Integer> callback);
```

**Parameters**

| parameter     | description                             |
| -------- | -------------------------------- |
| callback | Callbacks, including getting latest news success and failure |

**Example**

```java
TuyaHomeSdk.getMessageInstance().getMessageMaxTime(new ITuyaDataCallback<Integer>() {
      @Override
      public void onSuccess(Integer integer) {}
      @Override
      public void onError(String s, String s1) {}
});
```

## Get latest messages based on message type

Get the latest news according to the message type, there are currently 3 types of messages (MSG\_REPORT alert) (MSG\_FAMILY family) (MSG\_NOTIFY notification).

**Declaration**

```java
void getMessageListByMsgType(int offset, int limit, MessageType msgType, ITuyaDataCallback<MessageListBean> callback);
```

**Parameters**

| parameter     | description                                                         |
| -------- | ------------------------------------------------------------ |
| offset   | Offset is obtained from the nth data                                      |
| limit    | Number of messages per page                                               |
| msgType  | Message type (MSG\_REPORT alert) (MSG\_FAMILY family) (MSG\_NOTIFY notification) |
| callback | Callbacks, including success and failure                                    |

**Example**

```java
TuyaHomeSdk.getMessageInstance().getMessageListByMsgType(offset, limit, type, new ITuyaDataCallback<MessageListBean>() {
      @Override
      public void onSuccess(MessageListBean result) {}
      @Override
      public void onError(String errorCode, String errorMessage) {}
});
```

## Get message list based on message SrcId

The message list is obtained according to the message SrcId. Currently, only messages of the type (MSG_REPORT alarm) are supported.

**Declaration**

```java
void getMessageListByMsgSrcId(int offset, int limit, MessageType msgType, String msgSrcId, ITuyaDataCallback<MessageListBean> callback);
```

**Parameters**

| parameter     | description                       |
| -------- | --------------------------- |
| offset   | Offset is obtained from the nth data   |
| limit    | Number of messages per page              |
| msgType  | Message type (MSG_REPORT alert) |
| msgSrcId | Interest group id                   |
| callback | Callbacks, including success and failure    |

**Example**

```java
TuyaHomeSdk.getMessageInstance().getMessageListByMsgType(offset, limit, type, new ITuyaDataCallback<MessageListBean>() {
      @Override
      public void onSuccess(MessageListBean result) {}
      @Override
      public void onError(String errorCode, String errorMessage) {}
});
```