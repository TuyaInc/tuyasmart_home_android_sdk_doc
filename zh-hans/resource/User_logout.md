
## 退出登录

用户账号切换的时候需要调用退出登录接口

**示例代码**

```java
TuyaHomeSdk.getUserInstance().logout(new ILogoutCallback() {
  @Override
  public void onSuccess() {
    //退出登录成功
  }

  @Override
  public void onError(String errorCode, String errorMsg) {
  }
});
```
## 停用账户

**接口说明**

调用注销账户接口后，账号在一周后才会永久停用并删除你账户下的所有信息。在此之前重新登录，则你的停用请求将被取消。

```java
void cancelAccount(IResultCallback callback);    
```
**示例代码**

```java
TuyaHomeSdk.getUserInstance().cancelAccount(new IResultCallback() {
    @Override
    public void onError(String code, String error) {

    }
    @Override
    public void onSuccess() {

    }
});

```