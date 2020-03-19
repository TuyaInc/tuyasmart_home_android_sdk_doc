## 修改昵称
**接口说明**

修改昵称

```java
void reRickName(String name, final IReNickNameCallback callback);
```
**参数说明**

| 参数     | 说明 |
| -------- | ---- |
| name     | 昵称 |
| callback | 回调 |

**示例代码**

```java
TuyaHomeSdk.getUserInstance().reRickName(nickName, 
    new IReNickNameCallback() {
        @Override
        public void onSuccess() {
        }
        @Override
        public void onError(String code, String error) {

        }
});
```
## 更新用户时区

**接口说明**

用于更新用户时区。

```java
void updateTimeZone(String timezoneId, IResultCallback callback);
```
**参数说明**

| 参数       | 说明    |
| ---------- | ------- |
| timezoneId | 时区 id |
| callback   | 回调    |

**示例代码**

```java
TuyaHomeSdk.getUserInstance().updateTimeZone(
    timezoneId, 
    new IResultCallback() {
        @Override
        public void onSuccess() {
        }

        @Override
        public void onError(String code, String error) {

        }
});
```
## 上传用户头像
**接口说明**

用于上传用户自定义的头像。

```java
void uploadUserAvatar(File file, IBooleanCallback callback)
```
**参数说明**

| 参数     | 说明             |
| -------- | ---------------- |
| file     | 用户头像图片文件 |
| callback | 回调             |

**代码范例**

```java
TuyaHomeSdk.getUserInstance().uploadUserAvatar(
    file, 
    new IBooleanCallback() {
        @Override
        public void onSuccess() {
        }

        @Override
        public void onError(String code, String error) {

        }
});
```
## 设置温度单位
**接口说明**

设置温度单位是摄氏度还是华氏度

TempUnitEnum.Celsius：摄氏度

,TempUnitEnum.Fahrenheit：华摄度

```java
void setTempUnit(TempUnitEnum unit, IResultCallback callback);
```

| 参数     | 说明 |
| -------- | ---- |
| unit     | 单位 |
| callback | 回调 |


## 退出登录接口

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
## 更新用户定位

如果有需要的话，定位信息可以通过以下接口上报：

```java
TuyaSdk.setLatAndLong(lat,lon);
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