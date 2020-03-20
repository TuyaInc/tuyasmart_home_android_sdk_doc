# User Uid Login System
Tuya Smart provides a uid login system. If customers have their own user system, they can access our SDK through uid login system.
## User Uid Registration

**Declaration**

User uid registration

```java
TuyaHomeSdk.getUserInstance().registerAccountWithUid (String countryCode, String uid, String password, IRegisterCallback callback);
```
**Parameters**

|Parameters | Description |
| ----------- | ----------------- |
|countryCode | country code, for example: 86 |
| uid | User uid |
|password | User Password |
| callback | callback |

**Example**

```java
// uid registration
TuyaHomeSdk.getUserInstance().registerAccountWithUid ("86", "1234", "123456", new IRegisterCallback () {
    @Override
    public void onSuccess (User user) {
        Toast.makeText (mContext, "UID registered successfully", Toast.LENGTH_SHORT) .show ();
    }
    @Override
    public void onError (String code, String error) {
        Toast.makeText (mContext, "code:" + code + "error:" + error, Toast.LENGTH_SHORT) .show ();
    }
});
```
## User Uid Login
**Declaration**

User uid login

```java
TuyaHomeSdk.getUserInstance().loginWithUid (String countryCode, String uid, String passwd, ILoginCallback callback);
```
**Parameters**

|Parameters | Description |
| ----------- | ----------------- |
|countryCode | country code, for example: 86 |
| uid | User uid |
| passwd | User Password |
| callback | callback |

**Example**

```java
// uid login
TuyaHomeSdk.getUserInstance().loginWithUid ("86", "1234", "123456", new ILoginCallback () {
    @Override
    public void onSuccess (User user) {
        Toast.makeText (mContext, "Successfully logged in, username:", Toast.LENGTH_SHORT) .show ();
    }

    @Override
    public void onError (String code, String error) {
        Toast.makeText (mContext, "code:" + code + "error:" + error, Toast.LENGTH_SHORT) .show ();
    }
});
```
## User Uid Reset Password
The user uid resets the password. You need to reset the password through the cloud connection. See [Cloud API Documentation](https://docs.tuya.com/cn/openapi/api/post_apps.schema.user_1.0.html)

## User Uid Login Registration Interface
**Declaration**

The user UID login and registers to form an interface.

```java
TuyaHomeSdk.getUserInstance().loginOrRegisterWithUid(String countryCode, String uid, String passwd, ILoginCallback callback);
```
**Parameters**

|Parameters | Description |
| ----------- | ----------------- |
|countryCode | country code, for example: 86 |
| uid | uid |
| passwd | User Password |
| callback | callback |

**Example**

```java
// uid login
TuyaHomeSdk.getUserInstance().loginOrRegisterWithUid("86", "1234", "123456", new ILoginCallback () {
    @Override
    public void onSuccess (User user) {
        Toast.makeText (mContext, "Successfully logged in, username:", Toast.LENGTH_SHORT) .show ();
    }

    @Override
    public void onError (String code, String error) {
        Toast.makeText (mContext, "code:" + code + "error:" + error, Toast.LENGTH_SHORT) .show ();
    }
});
```