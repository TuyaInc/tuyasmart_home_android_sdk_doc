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
## Update user time zone

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
## Upload user avatar
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
## Set the temperature unit
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


## Logout interface

When the user account is switched, it is necessary to call the logout interface

**Example**

```java
TuyaHomeSdk.getUserInstance ().logout (new ILogoutCallback () {
  @Override
  public void onSuccess () {
    // Sign out successfully
  }

  @Override
  public void onError (String errorCode, String errorMsg) {
  }
});
```
## Update user targeting

If necessary, the positioning information can be reported through the following interfaces:

```java
TuyaSdk.setLatAndLong (lat, lon);
```

## Disable account

**Declaration**

After calling the logout account interface, the account will be permanently deactivated after one week and all information under your account will be deleted. Log back in before that, and your deactivation request will be cancelled.

```java
void cancelAccount (IResultCallback callback);
```
**Example**

```java
TuyaHomeSdk.getUserInstance().cancelAccount (new IResultCallback () {
    @Override
    public void onError (String code, String error) {

    }
    @Override
    public void onSuccess () {

    }
});

```