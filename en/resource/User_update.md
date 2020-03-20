# Modify User Infomation

## Change Nickname

**Declaration**

Change nickname

```java
void reRickName (String name, final IReNickNameCallback callback);
```
**Parameters**

| Parameters | Description |
| -------- | ---- |
| name | Nickname |
| callback | callback |

**Example**

```java
TuyaHomeSdk.getUserInstance().reRickName (nickName,
    new IReNickNameCallback () {
        @Override
        public void onSuccess () {
        }
        @Override
        public void onError (String code, String error) {

        }
});
```
## Update User Time Zone

**Declaration**

Used to update the user time zone.

```java
void updateTimeZone(String timezoneId, IResultCallback callback);
```
**Parameters**

| Parameters | Description |
| ---------- | ------ |
| timezoneId | timezone id |
| callback | callback |

**Example**

```java
TuyaHomeSdk.getUserInstance().updateTimeZone (
    timezoneId,
    new IResultCallback () {
        @Override
        public void onSuccess () {
        }

        @Override
        public void onError (String code, String error) {

        }
});
```
## Upload User Avatar
**Declaration**

Used to upload user-defined avatars.

```java
void uploadUserAvatar(File file, IBooleanCallback callback)
```
**Parameters**

| Parameters | Description |
| -------- | ---------------- |
| file | User avatar image file |
| callback | callback |

** Code Example **

```java
TuyaHomeSdk.getUserInstance().uploadUserAvatar (
    file,
    new IBooleanCallback () {
        @Override
        public void onSuccess () {
        }

        @Override
        public void onError (String code, String error) {

        }
});
```
## Set the Temperature Unit
**Declaration**

Set whether the temperature unit is Celsius or Fahrenheit

* TempUnitEnum.Celsius: Celsius
* TempUnitEnum.Fahrenheit: Hua degree

```java
void setTempUnit (TempUnitEnum unit, IResultCallback callback);
```

| Parameters | Description |
| -------- | ---- |
| unit | unit |
| callback | callback |

## Update User Targeting

If necessary, the positioning information can be reported through the following interfaces:

```java
TuyaSdk.setLatAndLong (lat, lon);
```
