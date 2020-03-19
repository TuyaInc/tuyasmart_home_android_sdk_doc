## APP Requirements

**Mobile System Requirements**

TuyaHomesdk has been supported since Android 4.4.   API>=19

**Manifest Permissions**

```java
<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
<uses-permission android:name="android.permission.BLUETOOTH" />
<uses-permission android:name="android.permission.BLUETOOTH_ADMIN" />
```

**Permissions  Check**

  *  Before the APP uses the Bluetooth connection or scanning operation, it needs to check whether the APP positioning permission is allowed.
  *  Check if the Bluetooth status is on.