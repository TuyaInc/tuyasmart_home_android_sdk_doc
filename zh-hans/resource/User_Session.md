# Session 失效监听
**描述**

Session 由于可能存在一些异常或者在一段时间不操作（45 天）会失效掉，这时候需要退出应用，重新登陆获取 Session。

**接口说明**

```java
TuyaHomeSdk.setOnNeedLoginListener(INeedLoginListener needLoginListener);
```
**实现回调**

```java
needLoginListener.onNeedLogin(Context context);
```
**代码示例**

```java
TuyaHomeSdk.setOnNeedLoginListener(new INeedLoginListener() {
  @Override
  public void onNeedLogin(Context context) {

  }
});
```
注意事项

* 建议在 Application 中注册该监听
* 一旦出现此类回调，请跳转到登陆页面，让用户重新登陆。

