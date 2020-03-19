# Migration of One Series of SDK Accounts
If it is a 1 series SDK, users need to upgrade when accessing the latest version

### Check if you want to upgrade user data

   **Declaration**

```java
    boolean checkVersionUpgrade();
```
   
   **Example**

```java
    TuyaHomeSdk.getUserInstance().checkVersionUpgrade();
```

### Upgrade account

   **Declaration**

```java
   void upgradeVersion(IResultCallback callback);
```

   **Example**

```java
   TuyaHomeSdk.getUserInstance().upgradeVersion ()
```