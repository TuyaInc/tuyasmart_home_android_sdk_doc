### Family Member Management

**MemberBean Field Information**

| Field | Type | Description |
| --- | --- | --- |
| homeId | long  | Unique id of Home |
| nickName | String |The member nickName  |
| admin | boolean | Administrator or not |
| memberId | long | Member id |
| headPic | String | Directory of account picture|
| account | String  | AccountName of member |
| uid | String | Unique id of member |
| memberStatus | int| The member status （1:to be accepted 2:accepted 3:reject）|

#### Update Member Comment Names and Permissions

**Declaration**

```java
void updateMember(long memberId, String name, boolean admin, IResultCallback callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| memberId | Member ID |
| name | Name |
| admin | Administrator or not |

**Example**

```java
TuyaHomeSdk.getMemberInstance().updateMember(memberId, name, admin, new IResultCallback() {
        @Override
        public void onError(String code, String error) {
            // do something
        }
        @Override
        public void onSuccess() {
            // do something
        }
    });
```

#### Update Member Information

**Declaration**

```java
void updateMember(MemberWrapperBean memberWrapperBean, IResultCallback callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| memberWrapperBean | Member information |

**Example**

```java
TuyaHomeSdk.getMemberInstance().updateMember(memberWrapperBean, new IResultCallback() {
        @Override
        public void onError(String code, String error) {
            // do something
        }
        @Override
        public void onSuccess() {
            // do something
        }
    });
```

#### Update Member Permissions

**Declaration**

```java
void updateMemberRole(long memberId, boolean admin, IResultCallback callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| memberId | Member ID |
| admin | Administrator or not |

**Example**

```java
TuyaHomeSdk.getMemberInstance().updateMemberRole(memberId, admin, new IResultCallback() {
        @Override
        public void onError(String code, String error) {
            // do something
        }
        @Override
        public void onSuccess() {
            // do something
        }
    });
```

#### New Member

**Declaration**

```java
void addMember(MemberWrapperBean memberWrapperBean, ITuyaDataCallback<MemberBean> callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| memberWrapperBean | Member information |

**Example**

```java
TuyaHomeSdk.getMemberInstance().addMember(memberWrapperBean, new ITuyaDataCallback<MemberBean>() {
        @Override
        public void onError(String errorCode, String errorMessage) {
            // do something
        }
        @Override
        public void onSuccess(MemberBean result) {
            // do something
        }
    });
```

#### Add Members Under Home

**Declaration**

```java
void addMember(long mHomeId, String countryCode, String userAccount, String name, boolean admin, ITuyaMemberResultCallback callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| mHomeId | Family ID |
| countryCode | Country code |
| userAccount | User name |
| name | Nickname? |
| admin | Administrator or not |

**Example**

```java
TuyaHomeSdk.getMemberInstance().addMember(mHomeId, countryCode, userAccount, name, admin, new ITuyaMemberResultCallback() {
        @Override
        public void onError(String errorCode, String errorMsg) {
            // do something
        }
        @Override
        public void onSuccess(MemberBean bean) {
            // do something
        }
    });
```

#### Remove Members Under Home

**Declaration**

```java
void removeMember(long memberId, IResultCallback callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| memberId | Member ID |

**Example**

```java
TuyaHomeSdk.getMemberInstance().removeMember(memberId, new IResultCallback() {
        @Override
        public void onError(String code, String error) {
            // do something
        }
        @Override
        public void onSuccess() {
            // do something
        }
    });
```

#### Query the Member List Under Home

**Declaration**

```java
void queryMemberList(long mHomeId, ITuyaGetMemberListCallback callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| mHomeId | Family ID |

**Example**

```java
TuyaHomeSdk.getMemberInstance().queryMemberList(mHomeId, new ITuyaGetMemberListCallback() {
        @Override
        public void onError(String errorCode, String error) {
            // do something
        }
        @Override
        public void onSuccess(List<MemberBean> memberBeans) {
            // do something
        }
    });
```

#### Get Devices That Family Members Can Associate With

**Declaration**

```java
void getMemberDeviceList(long relationId, ITuyaDataCallback<Map<String, Object>> callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| relationId | Family member ID |

**Example**

```java
TuyaHomeSdk.getMemberInstance().getMemberDeviceList(relationId, new ITuyaDataCallback<<Map<String, Object>>>() {
        @Override
        public void onError(String errorCode, String errorMessage) {
            // do something
        }
        @Override
        public void onSuccess(<Map<String, Object>> result) {
            // do something
        }
    });
```

#### Get Authorization for Designated Family Member Rooms

**Declaration**

```java
void getAuthRoomList(long homeId, long memberId, ITuyaDataCallback<List<RoomAuthBean>> callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| homeId | Family ID |
| memberId | Member ID |
| callback | Result callback |

**Example**

```java
TuyaHomeSdk.getMemberInstance().getAuthRoomList(homeId, memberId, new ITuyaDataCallback<List<RoomAuthBean>>() {
        @Override
        public void onError(String errorCode, String errorMessage) {
            // do something
        }
        @Override
        public void onSuccess(<List<RoomAuthBean>> result) {
            // do something
        }
    });
```

#### Set Room Permissions for Specified Members of the Specified Family

**Declaration**

```java
void saveAuthRoomList(long homeId, long memberId, List<Long> rooms, IResultCallback callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| homeId | Family ID |
| memberId | Member ID |
| rooms | Room ID list |
| callback | Result callback |

**Example**

```java
TuyaHomeSdk.getMemberInstance().saveAuthRoomList(homeId, memberId, rooms, new IResultCallback() {
        @Override
        public void onError(String code, String error) {
            // do something
        }
        @Override
        public void onSuccess() {
            // do something
        }
    });
```

#### Get the Authorization List of Scenarios for Members Under the Specified Family

**Declaration**

```java
void getAuthSceneList(long homeId, long memberId, ITuyaDataCallback<List<SceneAuthBean>> callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| homeId | Family ID |
| memberId | Member ID |
| callback | Result callback |

**Example**

```java
TuyaHomeSdk.getMemberInstance().getAuthSceneList(homeId, memberId, new ITuyaDataCallback<List<SceneAuthBean>>() {
        @Override
        public void onError(String errorCode, String errorMessage) {
            // do something
        }
        @Override
        public void onSuccess(<List<SceneAuthBean>> result) {
            // do something
        }
    });
```

#### Set Scene Permissions for the Specified Members of the Specified Family

**Declaration**

```java
void saveAuthSceneList(long homeId, long memberId, List<String> ruleIds, IResultCallback callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| homeId | Family ID |
| memberId | Member ID |
| ruleIds | Scene rule ID list |
| callback | Result callback |

**Example**

```java
TuyaHomeSdk.getMemberInstance().saveAuthSceneList(homeId, memberId, ruleIds, new IResultCallback() {
        @Override
        public void onError(String code, String error) {
            // do something
        }
        @Override
        public void onSuccess() {
            // do something
        }
    });
```

#### Family Member Binding Associated Account

**Declaration**

```java
void addMemberAccount(long id, String countryCode, String userAccount, int role, IResultCallback callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| id | Member ID |
| countryCode | Country code |
| userAccount | Associated account |
| role | Member role |
| callback | Result callback |

**Example**

```java
TuyaHomeSdk.getMemberInstance().addMemberAccount(id, countryCode, userAccount, role, new IResultCallback() {
        @Override
        public void onError(String code, String error) {
            // do something
        }
        @Override
        public void onSuccess() {
            // do something
        }
    });
```

#### Family Member Binding Associated Account

**Declaration**

```java
void addMemberAccount(long id, String countryCode, String userAccount, boolean admin, IResultCallback callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| id | Member ID |
| countryCode | Country code |
| userAccount | User name |
| admin | Administrator or not |

**Example**

```java
TuyaHomeSdk.getMemberInstance().addMemberAccount(id, countryCode, userAccount, admin, new IResultCallback() {
        @Override
        public void onError(String code, String error) {
            // do something
        }
        @Override
        public void onSuccess() {
            // do something
        }
    });
```

#### Upload Member's Avatar

**Declaration**

```java
void uploadMemberAvatar(String filename, File file, IBooleanCallback callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| filename | file name |
| file | file |

**Example**

```java
TuyaHomeSdk.getMemberInstance().uploadMemberAvatar(filename, file, new IBooleanCallback() {
        @Override
        public void onError(String code, String error) {
            // do something
        }
        @Override
        public void onSuccess() {
            // do something
        }
    });
```

#### Accept or Refuse To Join the Family

**Declaration**

```java
void processInvitation(long homeId, boolean action, IResultCallback callBack)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| homeId | Family ID |
| action | Accept \/ reject |

**Example**

```java
TuyaHomeSdk.getMemberInstance().processInvitation(homeId, action, new IResultCallback() {
        @Override
        public void onError(String code, String error) {
            // do something
        }
        @Override
        public void onSuccess() {
            // do something
        }
    });
```


