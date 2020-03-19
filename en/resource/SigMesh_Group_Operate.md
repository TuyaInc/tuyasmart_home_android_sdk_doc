# SigMesh Group Operation
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

## Create Mesh Group

16128 groups can be created in a mesh network. The id range when returning is 0xC000-0xFEFF . It is maintained locally.

Declaration

```java
void addGroup(String name, String pcc, String localId,IAddGroupCallback callback);
```
Parameters

|param|describe|
|--|--|
|name|group name|
|pcc|device type|
|localId|LocalId (0xC000 - 0xFFFF)|
|callback|Callback|

Example

```java
ITuyaBlueMeshDevice mTuyaSigMeshDevice= TuyaHomeSdk.newSigMeshDeviceInstance("meshId");

mTuyaSigMeshDevice.addGroup("group name","pcc", "8001", new IAddGroupCallback() {
			@Override
     public void onError(String errorCode, String errorMsg) {
     }

     @Override
     public void onSuccess(long groupId) {
     }
     });
```



## Add Sub-devices to Group

**Declaration**

```java
void addDevice(String devId,IResultCallback callback);
```
**Parameters**

|param|describe|
|--|--|
|devId|device Id|
|callback|callback|

**Example**

```java
ITuyaGroup mGroup = TuyaHomeSdk.newSigMeshGroupInstance(groupId);
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

|param|describe|
|--|--|
|devId|Device Id|
|callback|Callback|

**Example**
```java
ITuyaGroup mGroup = TuyaHomeSdk.newSigMeshGroupInstance(groupId);
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

|param|describe|
|--|--|
|callback|Callback|

**Example**
```java
ITuyaGroup mGroup = TuyaHomeSdk.newSigMeshGroupInstance(groupId);
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

|param|describe|
|--|--|
|groupName|new name|
|callback|Callback|

**Example**

```java
ITuyaGroup mGroup = TuyaHomeSdk.newSigMeshGroupInstance(groupId);
mGroup.renameGroup("group name",new IResultCallback() {
            @Override
            public void onError(String code, String errorMsg) {
            }

            @Override
            public void onSuccess() {
            }
        });

```