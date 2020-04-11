### Camera scan code Network Configuration

#### Description

Use the camera device to scan the QR code of the APP to transfer the Configuration information to active and bind the camera device.


```sequence

Title: Camera scan code Network Configuration

participant APP
participant Camera
participant Server

Note over APP: Connect to the router 
Note over Camera: resetting the device status
APP-->Server: Get Token
Server-->APP: Response Token

Note over APP: Generate QR code through ssid / password / token

Camera-->APP: Get the ssid / password / token by scanning the QR code on the APP
APP-->Server: Use the token to poll the list of network activation devices every 2 seconds (the total duration is 100s by default)
Camera-->Server: Activate the device
Server-->Camera: Network configuration succeeds

Server-->APP: Network configuration succeeds

```

#### Initialize Parameters

```java
TuyaCameraActivatorBuilder builder = new TuyaCameraActivatorBuilder()
         .setContext(context)
         .setSsid(ssid)
         .setPassword(password)
         .setToken(token)
         .setTimeOut(timeout)
         .setListener(new ITuyaSmartCameraActivatorListener() {
             @Override
             public void onQRCodeSuccess(String qrcodeUrl) {
                 //Return URL link to generate QR code
             }

             @Override
             public void onError(String errorCode, String errorMsg) {
                 //Network configuration failed
             }

             @Override
             public void onActiveSuccess(DeviceBean devResp) {
                //Network configuration succeed    
             }
         }));
```
**Parameters**

| Parameters         | Description |
| ------------ | -------------------------- |
| token           | Activation key required for Configuration |
| context         | context |
| ssid            | WiFi ssid|
| password        | WiFi password|
| timeout         | Configuration timeout, default setting is 100s, unit is second|

**Get Network Configuration Token**

Before the Wi-Fi network configuration, the SDK needs to obtain the network configuration Token from the Tuya Cloud.
The term of validity of Token is 5 minutes, and the Token become invalid once the network configuration succeeds.
A new Token has to be obtained if you have to reconfigure network.

```java
TuyaHomeSdk.getActivatorInstance().getActivatorToken(homeId, 
        new ITuyaActivatorGetToken() {
        
            @Override
            public void onSuccess(String token) {
            
            }
            
            @Override
            public void onFailure(String s, String s1) {
            
            }
        });
```
**Parameters**

| Parameters         | Description |
| ------------ | -------------------------- |
| homeId          | Family ID, please refer to the family management section for details |

#### Configuration Method Invocation

* Instance class

```java
ITuyaCameraDevActivator mTuyaActivator = TuyaHomeSdk.getActivatorInstance().newCameraDevActivator(builder);
```

* Get QR code URL link

```java
mTuyaActivator.createQRCode(); //Return via onQRCodeSuccess callback
```

* Generate QR code based on url

Examples：Need to implement zxing（ implementation 'com.google.zxing:core:3.2.1' ）

```java
public static Bitmap createQRCode(String url, int widthAndHeight)
            throws WriterException {
        Hashtable hints = new Hashtable();
        hints.put(EncodeHintType.CHARACTER_SET, "utf-8");
        hints.put(EncodeHintType.MARGIN,0);
        BitMatrix matrix = new MultiFormatWriter().encode(url,
                BarcodeFormat.QR_CODE, widthAndHeight, widthAndHeight, hints);

        int width = matrix.getWidth();
        int height = matrix.getHeight();
        int[] pixels = new int[width * height];
        
        for (int y = 0; y < height; y++) {
            for (int x = 0; x < width; x++) {
                if (matrix.get(x, y)) {
                    pixels[y * width + x] = BLACK;
                }
            }
        }
        Bitmap bitmap = Bitmap.createBitmap(width, height,
                Bitmap.Config.ARGB_8888);
        bitmap.setPixels(pixels, 0, width, 0, 0, width, height);
        return bitmap;
    }
```

* Start configuration

```java
mTuyaActivator.start();
```

* Stop configuration

```java
mTuyaActivator.stop();
```

* Exit the page to destroy some cache data and monitoring data

```java
mTuyaActivator.onDestory();
```

