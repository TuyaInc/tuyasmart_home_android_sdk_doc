# Add Share

## Add multiple device shares

Sharing multiple devices to a specified user will add the device to be shared to all shares of the specified user.

**Declaration**

```java
void addShareWithHomeId(long homeId, String countryCode, String userAccount, List<String> devIds, ITuyaResultCallback<SharedUserInfoBean> callback);
```

**Parameters**

| Parameters        | Description                                  |
| ----------- | ------------------------------------- |
| homeId      | Sharer family id                         |
| countryCode | Mobile area number, for example China is "86"             |
| phoneNumber | mobile phone number                              |
| devIds      | List of shared device ids                      |
| callback    | Callback, including sharing success or failure, cannot be null |

**Example**

```java
void addShareWithHomeId(homeId, countryCode, userAccount, devIds, new ITuyaResultCallback<SharedUserInfoBean>() {
    @Override
    public void onSuccess(SharedUserInfoBean bean) {}
    @Override
    public void onError(String errorMsg, String errorCode) {}
});
```

## Add device shares in bulk

Add device shares in batches. Called when the target user's id is known.

**Declaration**

```java
void addShareWithMemberId(long memberId,List<String> devIds,IResultCallback callback);
```

**Parameters**

| Parameters     | Description                                  |
| -------- | ------------------------------------- |
| memberId | Share target user id                        |
| devIds   | List of shared device ids                     |
| callback | Callback, including sharing success or failure, cannot be null |

**Example**

```java
void addShareWithMemberId (memberId, devIds, new IResultCallback() {
    @Override
    public void onError(String code, String error) {}
    @Override
    public void onSuccess() {}
});
```

## Single device unshare

Cancel individual device sharing by user relationship id.

**Declaration**

```java
void disableDevShare(String devId, long memberId, IResultCallback callback);
```

**Parameters**

| Parameters     | Description                                      |
| -------- | ----------------------------------------- |
| devId    | Device ID to be canceled                             |
| memberId | Users to be unshared                            |
| callback | Callback, including share cancellation success or failure, cannot be null |

**Example**

```java
void disableDevShare (devId, memberId, new IResultCallback() {
    @Override
    public void onError(String code, String error) {}
    @Override
    public void onSuccess() {}
});
```

## Sharing on a single device

Enable individual device sharing through user relationship id.

**Declaration**

```java
void enableDevShare(String devId, long memberId, IResultCallback callback);
```

**Parameters**

| Parameters     | Description                                      |
| -------- | ----------------------------------------- |
| devId    | Device ID to be canceled                                 |
| memberId | Users to be unshared                           |
| callback | Callback, including sharing success or failure, cannot be null |

**Example**

```java
void enableDevShare (devId, memberId, new IResultCallback() {
    @Override
    public void onError(String code, String error) {}
    @Override
    public void onSuccess() {}
});
```