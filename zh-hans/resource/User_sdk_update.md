### 1 系列 SDK 账户迁移（非 1 系列用户可以忽略此步）
如果是 1 系列 SDK (版本号：1.x.x )，接入最新版本时需要对 用户进行升级

* 检测是否要升级用户数据

  **接口说明**

  ```java
  boolean checkVersionUpgrade();
  ```
  **代码示例**
  
  ```java
  TuyaHomeSdk.getUserInstance().checkVersionUpgrade();
  ```
  
* 升级账号

  **接口说明**

  ```java
  void upgradeVersion(IResultCallback callback);
  ```

  **代码示例**
  ```
  TuyaHomeSdk.getUserInstance().upgradeVersion()
  ```

