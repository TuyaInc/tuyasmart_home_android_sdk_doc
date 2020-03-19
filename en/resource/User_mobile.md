# Mobile account system

Tutu Smart provides a mobile phone verification code login system.
## Mobile Verification Code Login

The verification code login function of the mobile phone needs to call the verification code sending interface first to send the verification code. Then call the mobile phone verification code verification interface. Fill the received verification code into the corresponding parameters.

**Declaration**

Get phone verification code

```java
TuyaHomeSdk.getUserInstance().getValidateCode(String phoneCode, String phoneNumber, final IValidateCallback callback);
```

**Parameters**

| Parameters | Description |
| ----------- | ----------------- |
| phoneCode | Mobile Area Code: Such as "86" |
| phoneNumber | mobile number |
| callback | callback |

**Declaration** 

Phone verification code login


```java
TuyaHomeSdk.getUserInstance().loginWithPhone(String phoneCode, String phone, String code, final ILoginCallback callback)
```

**Parameters**

| Parameters | Description |
| ----------- | ----------------- |
|phoneCode | Mobile Area Code: Such as "86" |
| phone | phone number |
| code | Verification Code |
|callback | Login callback interface |

**Example**

```java
// Get phone verification code
TuyaHomeSdk.getUserInstance().getValidateCode("86", "13666666666", new IValidateCallback () {
    @Override
    public void onSuccess () {
        Toast.makeText (mContext, "Success in obtaining verification code", Toast.LENGTH_SHORT) .show ();
    }

    @Override
    public void onError (String code, String error) {
        Toast.makeText (mContext, "code:" + code + "error:" + error, Toast.LENGTH_SHORT) .show ();
    }
});
// Mobile verification code login
TuyaHomeSdk.getUserInstance().loginWithPhone("86", "13355555555", "123456", new ILoginCallback () {
    @Override
    public void onSuccess (User user) {
        Toast.makeText (mContext, "Successfully logged in, username:" + TuyaHomeSdk.getUserInstance (). GetUser (). GetUsername (), Toast.LENGTH_SHORT) .show ();
    }
    @Override
    public void onError (String code, String error) {
        Toast.makeText (mContext, error, Toast.LENGTH_SHORT) .show ();
    }
});
```
## User mobile password login

Tuyao provides mobile phone password login system.
### Phone password registration
Mobile phone password registration, including obtaining a verification code interface and a registration interface

**Declaration**

Get phone verification code

```java
TuyaHomeSdk.getUserInstance().getValidateCode(String phoneCode, String phoneNumber, final IValidateCallback callback);
```

**Parameters**

| Parameters | Description |
| ----------- | ----------------- |
| phoneCode | Mobile Area Code: Such as "86" |
| phoneNumber | phone number |
| callback | callback |

**Declaration**

Phone password registration

```java
TuyaHomeSdk.getUserInstance().registerAccountWithPhone(final String phoneCode, final String phoneNumber, final String passwd, final String code, final IRegisterCallback callback);
```

**Parameters**

| Parameters | Description |
| ----------- | ----------------- |
| phoneCode | Mobile Area Code: Such as "86" |
| phoneNumber | phone number |
| passwd | password |
| code | Verification Code |
| callback | callback |

**Example**

```java
// Get phone verification code
TuyaHomeSdk.getUserInstance().getValidateCode("86", "13666666666", new IValidateCallback () {
    @Override
    public void onSuccess () {
        Toast.makeText (mContext, "Success in obtaining verification code", Toast.LENGTH_SHORT) .show ();
    }

    @Override
    public void onError (String code, String error) {
        Toast.makeText (mContext, "code:" + code + "error:" + error, Toast.LENGTH_SHORT) .show ();
    }
 });
// Register mobile password account
TuyaHomeSdk.getUserInstance().registerAccountWithPhone("86", "13666666666", "123456", "124332", new IRegisterCallback () {
    @Override
    public void onSuccess (User user) {
        Toast.makeText (mContext, "Registration succeeded", Toast.LENGTH_SHORT) .show ();
    }
    @Override
    public void onError (String code, String error) {
        Toast.makeText (mContext, "code:" + code + "error:" + error, Toast.LENGTH_SHORT) .show ();
    }
});
```
### Phone password login
**Declaration**

Sign in with your mobile number and password.

```java
TuyaHomeSdk.getUserInstance().loginWithPhonePassword(String phoneCode, String phone, String passwd, final ILoginCallback callback);
```

**Parameters**

| Parameter | Description |
| ----------- | ----------------- |
| phoneCode | Mobile Area Code: Such as "86" |
| phone | mobile number |
| passwd | Login password |
callback | Login callback interface |

**Example**

```java
// Mobile password login
TuyaHomeSdk.getUserInstance().loginWithPhonePassword ("86", "13666666666", "123456", new ILoginCallback () {
    @Override
    public void onSuccess (User user) {
        Toast.makeText (mContext, "Successfully logged in, username:" + TuyaHomeSdk.getUserInstance (). GetUser (). GetUsername (), Toast.LENGTH_SHORT) .show ();
    }

    @Override
    public void onError (String code, String error) {
        Toast.makeText (mContext, "code:" + code + "error:" + error, Toast.LENGTH_SHORT) .show ();
    }
});
```
### Phone reset password

Phone reset password function, including two interfaces: send verification code interface and reset password interface

**Declaration**

Get phone verification code

```java
TuyaHomeSdk.getUserInstance().getValidateCode (String phoneCode, String phoneNumber, final IValidateCallback callback);
```

**Parameters**

| Parameter | Description |
| ----------- | ----------------- |
|phoneCode | Mobile Area Code: Such as "86" |
| phoneNumber | mobile number |

**Declaration**

reset Password

```java
TuyaHomeSdk.getUserInstance().resetPhonePassword (final String phoneCode, final String phone, final String code, final String newPasswd, final IResetPasswordCallback callback);
```

**Parameters**

| Parameter | Description |
| ----------- | ----------------- |
| phoneCode | Mobile Area Code: Such as "86" |
| phone | mobile number |
| code | Verification Code |
| newPasswd | new password |
| callback |