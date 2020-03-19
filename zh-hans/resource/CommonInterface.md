# 通用接口

服务端 api 调用功能通用接口在类 `ITuyaSmartRequest` 中

有如下接口可供调用

**接口说明**

带 session 的接口请求

```java
<T> void requestWithApiName(String apiName, String version, Map<String, Object> postData, Class<T> object, final ITuyaDataCallback<T> callback);
```

**参数说明**

| 参数     | 说明                 |
| -------- | -------------------- |
| apiName  | api 名               |
| version  | api 版本号           |
| postData | postData             |
| object   | 服务端返回的数据对象 |
| callback | 回调                 |

**接口说明**

不带 session 的接口请求

```java
<T> void requestWithApiNameWithoutSession(String apiName, String version, Map<String, Object> postData, Class<T> object, final ITuyaDataCallback<T> callback);
```

**参数说明**

| 参数     | 说明                 |
| -------- | -------------------- |
| apiName  | api 名               |
| version  | api 版本号           |
| postData | post 发送的数据      |
| object   | 服务端返回的数据对象 |
| callback | 回调                 |

调用方式 `TuyaHomeSdk.getRequestInstance()`

**示例代码**

| 接口说明| apiName             | version | postData |
| ------| ------------------- | ------- | -------- |
|获取国家列表| tuya.m.country.list | 1.0 | 无 |

```java
Map<String, Object> postData = null;

TuyaHomeSdk.getRequestInstance().requestWithApiNameWithoutSession("tuya.m.country.list", "1.0", postData, String.class, new ITuyaDataCallback<String>() {
    @Override
    public void onSuccess(String result) {
        Log.i("TAG" , result);
    }

    @Override
    public void onError(String errorCode, String errorMessage) {
        Log.i("TAG" , errorCode);
    }
});
```

