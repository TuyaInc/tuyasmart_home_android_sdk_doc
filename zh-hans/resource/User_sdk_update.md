# 1.x 版本SDK 账户迁移

不是 1.x 版本 SDK 用户请忽略此步

如果是 1 系列 SDK (版本号：1.x.x )，接入最新版本时需要对用户进行升级

## 检查是否需要升级
检测是否要升级用户数据

**接口说明**

```java
boolean checkVersionUpgrade();
```
**代码示例**

```java
TuyaHomeSdk.getUserInstance().checkVersionUpgrade();
```

## 升级账号

**接口说明**

```java
void upgradeVersion(IResultCallback callback);
```

**代码示例**
```java
TuyaHomeSdk.getUserInstance().upgradeVersion()
```

