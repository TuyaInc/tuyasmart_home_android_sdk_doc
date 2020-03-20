#  第三方登陆


## QQ 登陆

**接口说明**

QQ 登录接口

```java
TuyaHomeSdk.getUserInstance().loginByQQ(String countryCode, String userId, String accessToken, ILoginCallback callback);
```

**参数说明**

| 参数        | 说明                         |
| ----------- | ---------------------------- |
| countryCode | 国家区号,例如：86            |
| userId      | QQ授权登录获取的 userId      |
| accessToken | QQ授权登录获取的 accessToken |
| callback    | 回调                         |

## 微信登陆

**接口说明**

```java
TuyaHomeSdk.getUserInstance().loginByWechat(String countryCode, String code, ILoginCallback callback);
```

**参数说明**

| 参数      | 说明                    |
| --------- | ----------------------- |
| phoneCode | 手机区号,例如：86       |
| code      | 微信授权登录获取的 code |
| callback  | 回调                    |

## Facebook 登陆

**接口说明**


```java
TuyaHomeSdk.getUserInstance().loginByFacebook(String phoneCode, String token, ILoginCallback callback);
```

**参数说明**

| 参数        | 说明                          |
| ----------- | ----------------------------- |
| countryCode | 手机区号,例如：86             |
| token       | facebook 授权登录获取的 token |