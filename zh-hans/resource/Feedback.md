# 意见反馈

用于在用户和企业或开发者之间提供一种沟通通道。

|         类名         |           说明           |
| ------------------ | ---------------------- |
| ITuyaFeedbackManager |      用户反馈管理类      |
|   ITuyaFeedbackMsg   | 针对某一会话的反馈管理类 |

## 获取反馈列表

获取该用户所有的反馈。

**接口说明**

```java
void getFeedbackManager().getFeedbackList(final ITuyaDataCallback<List<FeedbackBean>> callback);
```

**参数说明**

| 参数     | 说明                                         |
| -------- | -------------------------------------------- |
| callback | 回调，包括获取反馈列表成功和失败，不能为 null |

**FeedbackBean 数据模型**

|   字段   |  类型  |                  描述                  |
| ------ | ---- | ------------------------------------ |
| dateTime | String |               日期和时间               |
| content  | String |                反馈内容                |
|   hdId   | String |               反馈类目 id               |
|  hdType  | String |                反馈类型                |
|  title   | String | 类目标题(如果为设备故障反馈即设备名称) |

**示例代码**

```java
TuyaHomeSdk.getTuyaFeekback().getFeedbackManager().getFeedbackList(new ITuyaDataCallback<List<FeedbackBean>>() {
    @Override
    public void onSuccess(List<FeedbackBean> feedbackTalkBeans) {}
    @Override
    public void onError(String errorCode, String errorMessage) {}
});
```

## 获取反馈类型列表

获取可选择的反馈类型列表，用于创建反馈之前选择。

**接口说明**

```java
void getFeedbackType(final ITuyaDataCallback<List<FeedbackTypeRespBean>> callback);
```

**参数说明**

| 参数     | 说明                                             |
| -------- | ------------------------------------------------ |
| callback | 回调，包括获取反馈类型列表成功和失败，不能为 null |

**FeedbackTypeRespBean 数据模型**

| 字段 |          类型          |             描述             |
| -- | -------------------- | -------------------------- |
| list | List<FeedbackTypeBean> |         反馈类型列表         |
| type |         String         | 列表类别(目前仅有设备和其它) |

**FeedbackTypeBean 数据模型**

|  字段  |  类型  |                  描述                  |
| ---- | ---- | ------------------------------------ |
|  hdId  | String |               反馈类目 id               |
| hdType | String |                反馈类型                |
| title  | String | 类目标题(如果为设备故障反馈即设备名称) |

**示例代码**

```java
TuyaHomeSdk.getTuyaFeekback().getFeedbackManager().getFeedbackType(new ITuyaDataCallback<List<FeedbackTypeRespBean>>() {
    @Override
    public void onSuccess(List<FeedbackTypeRespBean> feedbackTypeRespBeans) {}
    @Override
    public void onError(String errorCode, String errorMsg) {}
});
```

## 新增反馈

新增一条反馈信息。

**接口说明**

```java
void addFeedback(final String message,String contact, String hdId, int hdType, final ITuyaDataCallback<FeedbackMsgBean> callback);
```

**参数说明**

| 参数     | 说明                     |
| -------- | ------------------------ |
| message  | 反馈内容                 |
| contact  | 联系方式（电话或邮箱）   |
| hdId     | 反馈类目 id               |
| hdType   | 反馈类型                 |
| callback | 回调，包含新增成功和失败 |

**示例代码**

```java
TuyaHomeSdk.getTuyaFeekback().getFeedbackManager().addFeedback(
    "设备存在故障",
    "abc@qq.com",
    feebackTypeBean.getHdId(), 
    feebackTypeBean.getHdType(), 
    new ITuyaDataCallback<FeedbackMsgBean>() {
        @Override
        public void onSuccess(FeedbackMsgBean feedbackMsgBean) {}
        @Override
        public void onError(String errorCode, String errorMsg) {}
});
```

## 获取反馈消息列表

用于获取当前反馈话题（会话场景）的消息列表。

**接口说明**

```java
void getMsgList(ITuyaDataCallback<List<FeedbackMsgBean>> callback);
```

**参数说明**

| 参数     | 说明                             |
| -------- | -------------------------------- |
| callback | 回调，包括获取消息列表成功和失败 |

**示例代码**

```java
mFeedbackMsg.getMsgList(new ITuyaDataCallback<List<FeedbackMsgBean>>() {
    @Override
    public void onSuccess(List<FeedbackMsgBean> result) {}
    @Override
    public void onError(String errorCode, String errorMessage) {}
});
```

## 添加新反馈

用于在当前对话中添加新的反馈消息。

**接口说明**

```java
void addMsg(String msg, String contact, ITuyaDataCallback<FeedbackMsgBean> callback);
```

**参数说明**

| 参数     | 说明                             |
| -------- | -------------------------------- |
| msg      | 回调，包括获取消息列表成功和失败 |
| contact  | 联系方式                         |
| callback | 回调，包括反馈成功和失败         |

**示例代码**

```java
mFeedbackMsg.addMsg(
    "再次反馈问题","abc@qq.com", 
    new ITuyaDataCallback<FeedbackMsgBean>() {
        @Override
        public void onSuccess(FeedbackMsgBean result) {}
        @Override
        public void onError(String errorCode, String errorMessage) {}
});
```