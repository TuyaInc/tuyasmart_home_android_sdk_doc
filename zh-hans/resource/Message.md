## 获取消息列表

用于获取全部消息列表。

|     类名     |      说明      |
| ---------- | ------------ |
| ITuyaMessage | 用户反馈管理类 |

**接口说明**

```java
void getMessageList(ITuyaDataCallback<List<MessageBean>> callback);
```

**参数说明**

| 参数     | 说明                             |
| -------- | -------------------------------- |
| callback | 回调，包括获取消息列表成功和失败 |

**MessageBean 数据模型**

|      字段      |  类型   |               描述               |
| ------------ | ----- | ------------------------------ |
|    dateTime    | String  |            日期和时间            |
|      Icon      | String  |           消息图标 URL            |
| msgTypeContent | String  |           消息类型名称           |
|   msgContent   | String  |             消息内容             |
|    msgType     | Integer |             消息类型             |
|    msgSrcId    | String  | 设备 id（只有告警消息才有该字段） |
|       id       | String  |              消息 id              |

**示例代码**

```java
TuyaHomeSdk.getMessageInstance().getMessageList(new ITuyaDataCallback<List<MessageBean>>() {
    @Override
    public void onSuccess(List<MessageBean> result) {}
    @Override
    public void onError(String errorCode, String errorMessage) {}
});
```

## 删除消息

用于批量删除消息。

**接口说明**

```java
void deleteMessage(List<String> mIds, IBooleanCallback callback);
```

**参数说明**

| 参数    | 说明                             |
| ------- | -------------------------------- |
| mIds    | 回调，包括获取消息列表成功和失败 |
| contact | 回调，包括删除成功和失败         |

**示例代码**

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

## 获取最新的消息

获取最新一条消息的时间戳。

**接口说明**

```java
void getMessageMaxTime(ITuyaDataCallback<Integer> callback);
```

**参数说明**

| 参数     | 说明                             |
| -------- | -------------------------------- |
| callback | 回调，包括获取最新消息成功和失败 |

**示例代码**

```java
TuyaHomeSdk.getMessageInstance().getMessageMaxTime(new ITuyaDataCallback<Integer>() {
      @Override
      public void onSuccess(Integer integer) {}
      @Override
      public void onError(String s, String s1) {}
});
```

## 根据消息类型获取最新的消息

根据消息类型获取最新消息, 目前有3种类型的消息 ( MSG_REPORT 告警) ( MSG_FAMILY 家庭) ( MSG_NOTIFY 通知)。

**接口说明**

```java
void getMessageListByMsgType(int offset, int limit, MessageType msgType, ITuyaDataCallback<MessageListBean> callback);
```

**参数说明**

| 参数     | 说明                                                         |
| -------- | ------------------------------------------------------------ |
| offset   | 偏移从第n条数据开始获取                                      |
| limit    | 每页的消息数量                                               |
| msgType  | 消息类型  (MSG_REPORT 告警) (MSG_FAMILY 家庭) (MSG_NOTIFY 通知) |
| callback | 回调，包括获取成功和失败                                     |

**示例代码**

```java
TuyaHomeSdk.getMessageInstance().getMessageListByMsgType(offset, limit, type, new ITuyaDataCallback<MessageListBean>() {
      @Override
      public void onSuccess(MessageListBean result) {}
      @Override
      public void onError(String errorCode, String errorMessage) {}
});
```

## 根据消息 SrcId 获取消息列表

根据消息 SrcId 获取消息列表， 目前只支持( MSG_REPORT 告警)类型的消息。

**接口说明**

```java
void getMessageListByMsgSrcId(int offset, int limit, MessageType msgType, String msgSrcId, ITuyaDataCallback<MessageListBean> callback);
```

**参数说明**

| 参数     | 说明                        |
| -------- | --------------------------- |
| offset   | 偏移从第n条数据开始获取     |
| limit    | 每页的消息数量              |
| msgType  | 消息类型  ( MSG_REPORT 告警) |
| msgSrcId | 消息组 id                    |
| callback | 回调，包括获取成功和失败    |

**示例代码**

```java
TuyaHomeSdk.getMessageInstance().getMessageListByMsgType(offset, limit, type, new ITuyaDataCallback<MessageListBean>() {
      @Override
      public void onSuccess(MessageListBean result) {}
      @Override
      public void onError(String errorCode, String errorMessage) {}
});
```