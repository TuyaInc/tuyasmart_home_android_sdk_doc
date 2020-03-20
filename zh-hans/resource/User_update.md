# 修改用户信息

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

```java
void setTempUnit(TempUnitEnum unit, IResultCallback callback);
```

| 参数     | 说明                                                         |
| -------- | ------------------------------------------------------------ |
| unit     | 文档的单位。<br>TempUnitEnum.Celsius：摄氏度<br>TempUnitEnum.Fahrenheit：华摄度 |
| callback | 回调                                                         |

## 更新用户定位

如果有需要的话，定位信息可以通过以下接口上报：

```java
TuyaSdk.setLatAndLong(lat,lon);
```
