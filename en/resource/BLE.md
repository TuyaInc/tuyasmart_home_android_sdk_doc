# Section I: Tuya Bluetooth Introduction
## Tuya Bluetooth
Tuya Bluetooth has 3 technology lines.
- **SingleBLE**: Bluetooth single point device, one-to-one connection between Bluetooth device and phone;
- **TuyaMesh**:  Mesh released by Tuya.
- **SigMesh**: Mesh released by SIG (Bluetooth Special Interest Group). 
In addition to the above three, there are some multi-protocol devices, such as **Dual-mode Device** with Wi-Fi and BLE capabilities. You can use both BLE and Wi-Fi capabilities.

|Category | Product Examples |
| ----------- | -----------------  |
| SingleBLE     | Body fat scale, bracelet, electric toothbrush, door lock, etc. |
| SigMesh     | Light bulb, socket, sensor,etc.|
| TuyaMesh    | Light bulb, socket, sensor,etc.|
| Dual-mode Device | Sigmesh gateways, IPC devices, and new multi-protocol Wi-Fi devices are all possible |
> The activation of dual-mode devices uses SingleBLE technology, which will be described in the SingleBLE chapter.


The Bluetooth part has the following functions:

**1.Activate Device**

- Scan BLE devices
- Device activation

**2.Device Function**
- Check device connection status
- Connect To BLE Device
- Device Function
- Unbind Device

**3.Upgrade Firmware**
- Check device new  version
- OTA(Upgrade device firmware)

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

