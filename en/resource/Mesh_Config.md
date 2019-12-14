## Configuration

### Scan nearby sub-devices to be configured
##### 【Description】
Need to check Bluetooth and location permissions before scanning

##### 【Method Invocation】

```java
//start search
mMeshSearch.startSearch();
//stop search
mMeshSearch.stopSearch();

```
##### 【Example Codes】
```java
ITuyaBlueMeshSearchListener iTuyaBlueMeshSearchListener=new ITuyaBlueMeshSearchListener() {
    @Override
    public void onSearched(SearchDeviceBean deviceBean) {

    }

    @Override
    public void onSearchFinish() {

    }
};

SearchBuilder searchBuilder = new SearchBuilder()
				.setMeshName("out_of_mesh")        //To scan the name of the device (the default will be out_of_mesh, the name of the device in the unconfigured state)
                .setTimeOut(100)        //Scan duration in seconds
                .setTuyaBlueMeshSearchListener(iTuyaBlueMeshSearchListener).build();

ITuyaBlueMeshSearch mMeshSearch = TuyaHomeSdk.getTuyaBlueMeshConfig().newTuyaBlueMeshSearch(searchBuilder);

//start search
mMeshSearch.startSearch();

//stop search
mMeshSearch.stopSearch();
```

### Sub-device Configuration
##### 【Description】
There are two types of sub-device configuration, one is common device access, and the other is mesh gateway access.

##### 【Initial parameter configuration】
```java
//common sub-device configuration parameter
TuyaBlueMeshActivatorBuilder tuyaBlueMeshActivatorBuilder = new TuyaBlueMeshActivatorBuilder()
            .setSearchDeviceBeans(mSearchDeviceBeanList)
            //default version number
            .setVersion("1.0")
            .setBlueMeshBean(mMeshBean)
            .setTimeOut(CONFIG_TIME_OUT)  //scan duration in seconds
            .setTuyaBlueMeshActivatorListener();
            
//Mesh gateway configuration parameter    
TuyaBlueMeshActivatorBuilder tuyaBlueMeshActivatorBuilder = new TuyaBlueMeshActivatorBuilder()
            .setWifiSsid(mSsid)
            .setWifiPassword(mPassword)     
            .setSearchDeviceBeans(mSearchDeviceBeanList)
            .setVersion("2.2")
            .setBlueMeshBean(mMeshBean)
            .setHomeId("homeId")
        	  .setTimeOut(CONFIG_TIME_OUT)
            .setTuyaBlueMeshActivatorListener();
```

##### 【参数说明】
###### 【入参】
```java
* @param mSearchDeviceBeans     list of device to be configured
* @param timeout   Timeout setting for network configuration, default is 100s
* @param ssid        Name of the Wifi used by devices in working after the network isconfigured.  (Home network)
* @param password   Password of the Wifi used by devices in working after the network is configured.  (Home network)
* @param mMeshBean  MeshBean 
* @param homeId     join homeId
* @param version    Common device is 1.0 , gateway is 2.2
```

###### 【出参】
ITuyaBlueMeshActivatorListener listener configuration callback

```java
//single device configuration failed callback
void onError(String errorCode, String errorMsg);

@param errorCode:
13007       login failed
13004       reset device address failed
13005       device address allocation is full
13007       ssid is empty 
13011       configuration time out

//single device configuration success callback
void onSuccess(DeviceBean deviceBean);

//configuration finish callback
void onFinish();

```

##### 【Method Invocation】

```java
//start activator
iTuyaBlueMeshActivator.startActivator();

//stop activator
iTuyaBlueMeshActivator.stopActivator();
```

##### 【Example Codes】
```java
//common sub-device configuration
TuyaBlueMeshActivatorBuilder tuyaBlueMeshActivatorBuilder = new TuyaBlueMeshActivatorBuilder()
                .setSearchDeviceBeans(foundDevices)
                .setVersion("1.0")
                .setBlueMeshBean(mMeshBean)
                .setTimeOut(timeOut)
                .setTuyaBlueMeshActivatorListener(new ITuyaBlueMeshActivatorListener() {
                    @Override
                    public void onSuccess(DeviceBean deviceBean) {
                        L.d(TAG, "subDevBean onSuccess: " + deviceBean.getName());
                    }

                    @Override
                    public void onError(String errorCode, String errorMsg) {
                        L.d(TAG, "config mesh error" + errorCode + " " + errorMsg);
                    }

                    @Override
                    public void onFinish() {
                        L.d(TAG, "config mesh onFinish： ");
                    }
                });
ITuyaBlueMeshActivator iTuyaBlueMeshActivator = TuyaHomeSdk.getTuyaBlueMeshConfig().newActivator(tuyaBlueMeshActivatorBuilder);

iTuyaBlueMeshActivator.startActivator();


//gateway sub-device configuration
TuyaBlueMeshActivatorBuilder tuyaBlueMeshActivatorBuilder = new TuyaBlueMeshActivatorBuilder()
                .setWifiSsid(mSsid)
                .setWifiPassword(mPassword)
                .setSearchDeviceBeans(foundDevices)
                .setVersion("2.2")
                .setBlueMeshBean(mMeshBean)
                .setHomeId("homeId")
                .setTuyaBlueMeshActivatorListener(new ITuyaBlueMeshActivatorListener() {

                    @Override
                    public void onSuccess(DeviceBean devBean) {
                        L.d(TAG, "startConfig  success");
                    }

                    @Override
                    public void onError(String errorCode, String errorMsg) {
                        L.d(TAG, "errorCode: " + errorCode + " errorMsg: " + errorMsg);
                    }

                    @Override
                    public void onFinish() {
                        L.d(TAG, "subDevBean onFinish: ");             
                    }
                });
ITuyaBlueMeshActivator iTuyaBlueMeshActivator = TuyaHomeSdk.getTuyaBlueMeshConfig().newWifiActivator(tuyaBlueMeshActivatorBuilder);
iTuyaBlueMeshActivator.startActivator();

```