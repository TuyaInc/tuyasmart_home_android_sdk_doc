### 摄像头扫码配网

#### 描述

通过摄像头设备扫描 APP 二维码来传递配网信息的方式来实现配网设备


```sequence

Title: 摄像头二维码配网

participant APP
participant Camera
participant Server

Note over APP: 连上路由器
Note over Camera: 置于待配网状态
APP-->Server: 获取 token
Server-->APP: 返回 token

Note over APP: ssid/password/token 生成二维码

Camera-->APP: 通过扫描 APP 上的二维码获取 ssid/password/token
APP-->Server: 根据 token 2秒钟轮询一次入网激活设备列表(总时长默认120s)
Camera-->Server: 去激活设备
Server-->Camera: 激活成功

Server-->APP: 激活成功，返回成功设备列表

```

#### 初始化配网参数

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
                 //返回生成二维码的 url 链接
             }

             @Override
             public void onError(String errorCode, String errorMsg) {
                 //配网失败
             }

             @Override
             public void onActiveSuccess(DeviceBean devResp) {
                //配网成功      
             }
         }));
```
**参数说明**

| 参数         | 说明 |
| ------------ | -------------------------- |
| token           | 配网所需要的激活 key |
| context         | 需要传入 activity 的 context |
| ssid            | 配网之后，设备工作 Wi-Fi 的名称（家庭网络） |
| password        | 配网之后，设备工作 Wi-Fi 的密码（家庭网络） |
| timeout         | 配网的超时时间设置，默认是 100s ，单位是秒 |

**获取配网 token**

开始配网之前，SDK 需要在联网状态下从涂鸦云获取配网 Token，Token 的有效期为5分钟，且配置成功后就会失效（再次配网需要重新获取）。

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
**参数说明**

| 参数         | 说明 |
| ------------ | -------------------------- |
| homeId          | 家庭 id，详情参考家庭管理章节 |

#### 配网方法调用

* 配网实现类

```java
ITuyaCameraDevActivator mTuyaActivator = TuyaHomeSdk.getActivatorInstance().newCameraDevActivator(builder);
```

* 获取二维码url链接

```java
mTuyaActivator.createQRCode(); //通过 onQRCodeSuccess 回调返回
```

* 根据url生成二维码

示例：需要依赖 zxing（ implementation 'com.google.zxing:core:3.2.1' ）

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

* 开始配网

```java
mTuyaActivator.start();
```

* 停止配网

```java
mTuyaActivator.stop();
```

* 销毁数据

```java
mTuyaActivator.onDestory();
```

