# Mesh
## Tuya Bluetooth
Tuya Bluetooth has 3 technology lines.

- **SingleBLE**: Bluetooth single point device, one-to-one connection between Bluetooth device and phone;
- **TuyaMesh**: Mesh released by Tuya.
- **SigMesh**: Mesh released by SIG (Bluetooth Special Interest Group).
In addition to the above three, there are some multi-protocol devices, such as **Dual-mode Device** with Wi-Fi and BLE capabilities. You can use both BLE and Wi-Fi capabilities.

|Category | Product Examples |
| ----------- | -----------------  |
| SingleBLE     | Body fat scale, bracelet, electric toothbrush, door lock, etc. |
| SigMesh     | Light bulb, socket, sensor,etc.|
| TuyaMesh    | Light bulb, socket, sensor,etc.|
| Dual-mode Device | Sigmesh gateways, IPC devices, and new multi-protocol Wi-Fi devices are all possible |
> Dual-mode's Bluetooth distribution network part, Use SingleBLE technology to network the device, Will be explained in the SingleBLE chapter.

## Tips
Please familiar with TuyaHomeSdk first and develop Bluetooth Mesh. All operations of Mesh are based on the initialization of family data.
A family can has multiple Meshs (recommend one family create one).

