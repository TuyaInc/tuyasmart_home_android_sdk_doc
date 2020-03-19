## Wi-Fi Network Configuration

### Description
Support Wi-Fi smart devices to connect to the cloud service.
The Wi-Fi network configuration mainly includes two network configuration modes, namely, EZ mode and AP mode.


| Attributes | Description |
| -------- | -------------------------------------------------------  |
| Wi-Fi Device | The device that use Wi-Fi module to connect the router, and interact with APP and cloud. |
| EZ mode   | Also known as the fast connection mode, the APP packs the distribution network data packets into the designated area of the 802.11 data packets and sends them to the surrounding environment; the Wi-Fi module of the smart device is in the promiscuous model and monitors the capture network All the packets in the parsing, according to the agreed protocol data format, parse out the distribution network information packet sent by the APP.|
| AP mode   | Also known as hotspot mode, the mobile phone connects the smart device's hotspot. The two parties establish a Socket connection to exchange data through the agreed port. |


### Conditions
Before developing Wi-Fi device network config, you need to understand the basic logic of TuyaHomeSDK, and have used TuyaHomeSdk to complete the basic operations such as logging in and creating a home.