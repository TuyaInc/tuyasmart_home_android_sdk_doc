# Modifying Remark Name

## Modifying the remark name of the person issuing the sharing information

The sharer modifies the remark name of the person being shared. If you share the device with other people, you can modify the remark name of the person.

**Declaration**

```java
void addShareWithHomeId(long homeId, String countryCode, String userAccount, List<String> devIds, ITuyaResultCallback<SharedUserInfoBean> callback);
```

**Parameters**

| Parameters        | Description                                  |
| ----------- | ------------------------------------- |
| homeId      | Sharer family id                          |
| countryCode | Mobile area number, for example China is "86"             |
| phoneNumber | mobile phone number                             |
| devIds      | List of shared device ids                     |
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

## Modifying the remark name of the person receiving the sharing information

The person who has shared changes the name of the person who shared it. You have received a share from someone else. You can modify this person's note name.

**Declaration**

```java
void renameReceivedShareNickname(long memberId, String name, IResultCallback callback);
```

**Parameters**

| Parameters     | Description |                               
| -------- | -------------------------------------- |
| memberId | Sharer family id is obtained from SharedUserInfoBean |
| callback | Callback, including modification success and failure, cannot be null  |

**Example**

```java
void addShareWithHomeId(homeId, countryCode, userAccount, devIds, new ITuyaResultCallback<SharedUserInfoBean>() {
    @Override
    public void onSuccess(SharedUserInfoBean bean) {}
    @Override
    public void onError(String errorMsg, String errorCode) {}
});
```