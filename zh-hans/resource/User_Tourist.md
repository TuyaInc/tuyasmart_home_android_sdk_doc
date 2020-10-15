# 匿名注册
## 匿名注册登录

 **接口说明**

 SDK提供匿名注册的方式登录，传参：nickName，匿名登录昵称；countryCode，国家码。

 ```java
void touristRegisterAndLogin(String countryCode, String nickName, final IRegisterCallback callback)
 ```

 **参数说明**

| 参数        | 类型             | 说明                                 |
| :---------- | :--------------- | :----------------------------------- |
| countryCode | String        | 国家码，86：中国，1：美              |
| nickName    | String        | 匿名登录昵称（例如：设备名称）       |
| callback     | IRegisterCallback | 回调             |


 **实例代码**

 ```java
TuyaHomeSdk.getUserInstance().touristRegisterAndLogin(countryCode, nickName, new IRegisterCallback() {
    @Override
    public void onSuccess(User user) {
        
    }
    @Override
    public void onError(String code, String error) {

    }
});
 ```

 ## 匿名注册退出登录

 **接口说明**

 匿名登录的用户可以通过这个接口退出登录，匿名账号会立即注销，其他账号有7天的窗口期

 ```java
void touristLogOut(final ILogoutCallback callback)
 ```

 **参数说明**

| 参数    | 类型            | 说明 |
| :------ | :-------------- | :--- |
| success | ILogoutCallback | 回调 |

 **实例代码**

```java
TuyaHomeSdk.getUserInstance().touristLogOut(new ILogoutCallback() {
    @Override
    public void onSuccess() {
        
    }
    @Override
    public void onError(String code, String error) {

    }
});
```



 ## 匿名登录绑定账号

 **接口说明**

 匿名登录的用户可以进一步完善手机或者邮箱信息，转化成正常用户。   
 完善信息通常有两步：

* 验证邮箱或者手机

* 设置账号密码

  

 ```java
void touristBindWithUserName(String countryCode, String userName, String verifyCode, String password, final IBooleanCallback callback)
 ```

 **参数说明**

| 参数        | 类型             | 说明                              |
| :---------- | :--------------- | :-------------------------------- |
| countryCode | String           | 国家码（例如：1，美国；86，中国） |
| userName    | String           | 用户绑定的手机号码或者邮箱        |
| vefifyCode  | String           | 验证码                            |
| password    | String           | 设置密码                          |
| callback    | IBooleanCallback | 回调                              |

 **实例代码**

```java
TuyaHomeSdk.getUserInstance().touristBindWithUserName(countryCode, userName, code, password, new IBooleanCallback() {
    @Override
    public void onSuccess() {
        
    }
    @Override
    public void onError(String code, String error) {

    }
});
```

