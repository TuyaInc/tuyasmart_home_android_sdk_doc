# 用户邮箱账号体系
涂鸦智能提供邮箱密码登陆体系。
## 用户邮箱密码注册
邮箱注册分两个接口，先获取验证码，然后使用验证码、密码注册。

**接口说明**

邮箱注册获取验证码

```java
void getRegisterEmailValidateCode(String countryCode, String email, IResultCallback callback);
```

**参数说明**

| 参数        | 说明              |
| ----------- | ----------------- |
| countryCode | 国家区号,例如：86 |
| email       | email             |
| callback    | 回调              |

**接口说明**

邮箱注册获取验证码

```java
TuyaHomeSdk.getUserInstance().registerAccountWithEmail(final String countryCode, final String email, final String passwd, final String code, final IRegisterCallback callback);
```

**参数说明**

| 参数        | 说明              |
| ----------- | ----------------- |
| countryCode | 国家区号,例如：86 |
| email       | email             |
| passwd      | 密码              |
| code        | 验证码            |
| callback    | 回调              |

**代码范例**

```java
//注册获取邮箱验证码
TuyaHomeSdk.getUserInstance().getRegisterEmailValidateCode("86","123456@123.com",new IResultCallback() {
    @Override
    public void onError(String code, String error) {
    }

    @Override
    public void onSuccess() {
    }
} );

//邮箱密码注册
TuyaHomeSdk.getUserInstance().registerAccountWithEmail("86", "123456@123.com","123456","5723", new IRegisterCallback() {
    @Override
    public void onSuccess(User user) {
        Toast.makeText(mContext, "注册成功", Toast.LENGTH_SHORT).show();
    }

    @Override
    public void onError(String code, String error) {
        Toast.makeText(mContext, "code: " + code + "error:" + error, Toast.LENGTH_SHORT).show();
    }
});
```
> 注意事项:
>
>  账户一旦注册到一个国家，目前数据无法迁移其他国家。

## 用户邮箱密码登陆
**接口说明**

用户邮箱密码登陆

```java
TuyaHomeSdk.getUserInstance().loginWithEmail(String countryCode, String email, String passwd, final ILoginCallback callback);
```
| 参数        | 说明              |
| ----------- | ----------------- |
| countryCode | 国家区号,例如：86 |
| email       | 邮箱              |
| passwd      | 登陆密码          |
| callback    | 回调              |

**代码范例**

```java
//邮箱密码登陆
TuyaHomeSdk.getUserInstance().loginWithEmail("86", "123456@123.com", "123123", new ILoginCallback() {
    @Override
    public void onSuccess(User user) {
        Toast.makeText(mContext, "登录成功，用户名：").show();
    }

    @Override
    public void onError(String code, String error) {
        Toast.makeText(mContext, "code: " + code + "error:" + error, Toast.LENGTH_SHORT).show();
    }
});
```
## 用户邮箱重置密码
用户邮箱重置密码功能分为两个接口，发送验证码接口和重置密码接口。

**接口说明**

邮箱找回密码，获取验证码

```java
TuyaHomeSdk.getUserInstance().getEmailValidateCode(String countryCode, final String email, final IValidateCallback callback);
```
**参数说明**

| 参数        | 说明              |
| ----------- | ----------------- |
| countryCode | 国家区号,例如：86 |
| email       | 邮箱              |
| callback    | 回调              |

**接口说明**

邮箱重置密码

```java
TuyaHomeSdk.getUserInstance().resetEmailPassword(String countryCode, final String email, final String emailCode, final String passwd, final IResetPasswordCallback callback);
```

**参数说明**

| 参数        | 说明              |
| ----------- | ----------------- |
| countryCode | 国家区号,例如：86 |
| email       | 邮箱              |
| emailCode   | 验证码            |
| passwd      | 新密码            |
| callback    | 回调              |

**示例代码**

```java
//获取邮箱验证码
TuyaHomeSdk.getUserInstance().getEmailValidateCode("86", "123456@123.com", new IValidateCallback() {
    @Override
    public void onSuccess() {
        Toast.makeText(mContext, "获取验证码成功", Toast.LENGTH_SHORT).show();
    }
    @Override
    public void onError(String code, String error) {
        Toast.makeText(mContext, "code: " + code + "error:" + error, Toast.LENGTH_SHORT).show();
    }
});
//重置密码
TuyaHomeSdk.getUserInstance().resetEmailPassword("86", "123456@123.com", "123123"，"a12345", new IResetPasswordCallback() {
    @Override
    public void onSuccess() {
        Toast.makeText(mContext, "找回密码成功", Toast.LENGTH_SHORT).show();
    }
    @Override
    public void onError(String code, String error) {
        Toast.makeText(mContext, "code: " + code + "error:" + error, Toast.LENGTH_SHORT).show();
    }
});
```