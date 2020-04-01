# Remove Share

## Delete sharing relationship

The sharer deletes all shared relationships with the user of this relationship through the memberId (user dimension deletion).

**Declaration**

```java
void removeUserShare(long memberId, IResultCallback callback);
```

**Parameters**

| Parameters     | Description                                  |
| :-------- | :------------------------------------- |
| memberId | User ID to be deleted                   |
| callback | Callback, including delete success or failure, cannot be null |

**Example**

```java
void removeUserShare(memberId, new IResultCallback() {
    @Override
    public void onError(String code, String error) {}
    @Override
    public void onSuccess() {}
})
```

## Delete received sharing relationship

The shared person obtains all shared device information of the user who has received this relationship through memberId.

**Declaration**

```java
void removeReceivedUserShare(long memberId, IResultCallback callback);
```

**Parameters**

| Parameters     | Description                                  |
| -------- | ------------------------------------- |
| memberId | User ID to be deleted                   |
| callback | Callback, including delete success or failure, cannot be null |

**Example**

```java
void removeReceivedUserShare(memberId, new IResultCallback() {
    @Override
    public void onError(String code, String error) {}
    @Override
    public void onSuccess() {}
})
```

## Delete a device share

The sharer deletes a shared device under the specified relationship user.

**Declaration**

```java
void disableDevShare(String devId, long memberId, IResultCallback callback);
```

**Parameters**

| Parameters     | Description                                  |
| -------- | ------------------------------------- |
| devId    | Device ID to be deleted                       |
| memberId | User ID to be deleted                   |
| callback | Callback, including delete success or failure, cannot be null |

**Example**

```java
void disableDevShare(devId, memberId, new IResultCallback() {
    @Override
    public void onError(String code, String error) {}
    @Override
    public void onSuccess() {}
})
```

## Remove received shared device

The sharer deletes a shared device under the specified relationship user.

**Declaration**

```java
void removeReceivedDevShare(String devId, IResultCallback callback);
```

**Parameters**

| Parameters     | Description                                  |
| -------- | ------------------------------------- |
| devId    | Device ID to be deleted                        |
| callback | Callback, including delete success or failure, cannot be null |

**Example**

```java
TuyaHomeSdk.getDeviceShareInstance().removeReceivedDevShare(devId,new IResultCallback() {
    @Override
    public void onError(String code, String error) {}
    @Override
    public void onSuccess() {}
})

```