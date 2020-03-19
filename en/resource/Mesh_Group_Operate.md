# Mesh Group Operation
`ITuyaGroup` provides operations for Mesh group.

## Find Mesh Group

A Mesh group or a WiFi group can be distinguished by whether it has a MeshId.

**Example**

```java
GroupBean groupBean=TuyaHomeSdk.getDataInstance().getGroupBean("groupId");
if(!TextUtils.isEmpty(groupBean.getMeshId())){    
	L.d(TAG, "This group is mesh group");
}
```

## Add Sub-devices to Group

**Declaration**

```java
void addDevice(String devId,IResultCallback callback);
```
**Parameters**

|field|type|describe|
|--|--|--|
|devId|String|Device Id|
|callback|IResultCallback|Callback|

**Example**

```java
ITuyaGroup mGroup = TuyaHomeSdk.newBlueMeshGroupInstance(groupId);
mGroup.addDevice("devId", new IResultCallback() {
            @Override
            public void onError(String code, String errorMsg) {
            }

            @Override
            public void onSuccess() {
            }
        });
```


## Remove Sub-devices From Group
**Declaration**

```java
void removeDevice(String devId,IResultCallback callback);
```

**Parameters**

|field|type|describe|
|--|--|--|
|devId|String|Device Id|
|callback|IResultCallback|Callback|



**Example**

```java
ITuyaGroup mGroup = TuyaHomeSdk.newBlueMeshGroupInstance(groupId);
mGroup.removeDevice("devId", new IResultCallback() {
            @Override
            public void onError(String code, String errorMsg) {
            }

            @Override
            public void onSuccess() {
            }
        });

```

## Disband Group

**Declaration**

```java
void dismissGroup(IResultCallback callback);
```
**Parameters**

|field|type|describe|
|--|--|--|
|callback|IResultCallback|Callback|

**Example**

```java
ITuyaGroup mGroup = TuyaHomeSdk.newBlueMeshGroupInstance(groupId);
mGroup.dismissGroup(new IResultCallback() {
            @Override
            public void onError(String code, String errorMsg) {
            }

            @Override
            public void onSuccess() {
            }
        });

```


## Group Rename

**Declaration**

```java
void renameGroup(String groupName,IResultCallback callback);
```

**Parameters**

|field|type|describe|
|--|--|--|
|groupName|String|Rename|
|callback|IResultCallback|Callback|

**Example**

```java
ITuyaGroup mGroup = TuyaHomeSdk.newBlueMeshGroupInstance(groupId);
mGroup.renameGroup("group name",new IResultCallback() {
            @Override
            public void onError(String code, String errorMsg) {
            }

            @Override
            public void onSuccess() {
            }
        });

```