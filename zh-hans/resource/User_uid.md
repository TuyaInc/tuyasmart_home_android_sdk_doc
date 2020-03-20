# 用户 uid 登陆体系
涂鸦智能提供 uid 登陆体系。如果客户自有用户体系，那么可以通过 uid 登陆体系，接入我们的 SDK。
## 用户 uid 注册

**接口说明**

用户 uid 注册

```java
TuyaHomeSdk.getUserInstance().registerAccountWithUid(String countryCode, String uid, String password, IRegisterCallback callback);
```
**参数说明**

| 参数        | 说明              |
| ----------- | ----------------- |
| countryCode | 国家区号,例如：86 |
| uid         | 用户 uid          |
| password    | 用户密码          |
| callback    | 回调              |

**示例代码**

```java
//uid 注册
TuyaHomeSdk.getUserInstance().registerAccountWithUid("86", "1234","123456", new IRegisterCallback() {
    @Override
    public void onSuccess(User user) {
        Toast.makeText(mContext, "UID注册成功", Toast.LENGTH_SHORT).show();
    }
    @Override
    public void onError(String code, String error) {
        Toast.makeText(mContext, "code: " + code + "error:" + error, Toast.LENGTH_SHORT).show();
    }
});
```
## 用户 uid 登陆
**接口说明**

用户uid登陆

```java
TuyaHomeSdk.getUserInstance().loginWithUid(String countryCode, String uid, String passwd, ILoginCallback callback);
```
**参数说明**

| 参数        | 说明              |
| ----------- | ----------------- |
| countryCode | 国家区号,例如：86 |
| uid         | 用户 uid          |
| passwd      | 用户密码          |
| callback    | 回调              |

**示例代码**

```java
//uid登陆
TuyaHomeSdk.getUserInstance().loginWithUid("86", "1234", "123456", new ILoginCallback() {
    @Override
    public void onSuccess(User user) {
        Toast.makeText(mContext, "登录成功，用户名：" , Toast.LENGTH_SHORT).show();
    }

    @Override
    public void onError(String code, String error) {
        Toast.makeText(mContext, "code: " + code + "error:" + error, Toast.LENGTH_SHORT).show();
    }
});
```
## 用户 uid 重置密码
用户 uid 重置密码，需要通过云云对接的方式进行重置密码。详看[云端 API 文档](https://docs.tuya.com/cn/openapi/api/post_apps.schema.user_1.0.html)

## 用户 uid 登陆注册接口
**接口描述**

用户 uid 登陆注册合成一个接口。

```java
TuyaHomeSdk.getUserInstance().loginOrRegisterWithUid(String countryCode, String uid, String passwd, ILoginCallback callback);
```
| 参数        | 说明              |
| ----------- | ----------------- |
| countryCode | 国家区号,例如：86 |
| uid         | uid               |
| passwd      | 用户密码          |
| callback    | 回调              |

**示例代码**

```java
//uid登陆
TuyaHomeSdk.getUserInstance().loginOrRegisterWithUid("86", "1234", "123456", new ILoginCallback() {
    @Override
    public void onSuccess(User user) {
        Toast.makeText(mContext, "登录成功，用户名：" , Toast.LENGTH_SHORT).show();
    }

    @Override
    public void onError(String code, String error) {
        Toast.makeText(mContext, "code: " + code + "error:" + error, Toast.LENGTH_SHORT).show();
    }
});
```
