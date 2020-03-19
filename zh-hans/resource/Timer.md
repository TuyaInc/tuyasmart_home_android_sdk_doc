## 定时任务

涂鸦智能提供了基本的定时能力，支持设备定时（包括 WiFi 设备，蓝牙 Mesh 子设备，Zigbee 子设备）和群组定时。并封装了针对设备 dp 点的定时器信息的增删改查接口。APP 通过定时接口设置好定时器信息后，硬件模块会自动根据定时要求进行预订的操作。每个定时任务下可以包含多个定时器。如下图所示：
![timer](./images/ios-sdk-timer.jpg)

定时相关的所有方法都在`TuyaHomeSdk.getTimerManagerInstance()` 中

以下多个接口用到了 taskName 这个参数，具体可描述为一个分组，一个分组可以有多个定时器。每个定时属于或不属于一个分组，分组目前仅用于展示。例如一个开关可能有多个 dp 点，可以根据每个 dp 点设置一个定时分组，每个分组可以添加多个定时器，用于控制这个 dp 点各个时段的开启或关闭。

#### 增加定时器

我们提供了两个方法实现定时器的添加，第一个接口是老接口，只支持单 dp 点的定时任务，并且默认开启状态；第二个接口支持 HashMap 类型入参，开发者自由配置。

**接口说明**

增加一个定时器

```java
void addTimerWithTask(String taskName, String loops, String devId, String dpId, String time, final IResultStatusCallback callback);
```

**参数说明**

| 参数        | 说明                                            |
| ----------- | ----------------------------------------------- |
| taskName | 定时分组名称                              |
| loops | 一周7天定时执行次数，"0000000", 每一位 0:关闭,1:开启, 从左至右依次表示: 周日 周一 周二 周三 周四 周五 周六 。"0000000" 表示只执行一次，"1111111" 表示每天执行。                                    |
| devId    | 设备id或群组id |
| dpId		 | dp点名称 |
| time		 | 下发执行的时间，例如"14:00",目前只支持24小时制|
| callback | 回调，返回成功或失败的结果，不能为 null|


**接口说明**

增加一个定时器

```java
void addTimerWithTask(String taskName, String devId, String loops, Map<String, Object> dps, String time, final IResultStatusCallback callback);
```


**参数说明**

| 参数        | 说明                                            |
| ----------- | ----------------------------------------------- |
| taskName | 定时分组名称                              |
| devId    | 设备 id 或群组 id |
| loops | 一周7天定时执行次数，"0000000", 每一位 0:关闭,1:开启, 从左至右依次表示: 周日 周一 周二 周三 周四 周五 周六 。"0000000" 表示只执行一次，"1111111" 表示每天执行。                                    |
| dps		 | 由 dpId 和 dpValue 构成的键值对，例如{"1":true} |
| time		 | 下发执行的时间，例如"14:00",目前只支持24小时制|
| callback | 回调，返回成功或失败的结果，不能为 null|


**示例代码**

```java
TuyaHomeSdk.getTimerManagerInstance().addTimerWithTask("task01", "1111111",mDevId,  "1", "14:29", new IResultStatusCallback() {
    @Override
    public void onSuccess() {
        Toast.makeText(mContext, "添加定时任务成功", Toast.LENGTH_LONG).show();
    }

    @Override
    public void onError(String errorCode, String errorMsg) {
        Toast.makeText(mContext, "添加定时任务失败 " + errorMsg, Toast.LENGTH_LONG).show();
    }
});
```

#### 获取某设备下的所有定时任务状态

**接口说明**

获取某设备下的所有定时任务状态

```java
void getTimerTaskStatusWithDeviceId(String devId, final IGetDeviceTimerStatusCallback callback);

```

**参数说明**

| 参数        | 说明                                            |
| ----------- | ----------------------------------------------- |
| devId | 设备 id 或群组 id                             |
| callback    | 回调，主要包括发送成功或失败的回调，不能为 null |


**示例代码**

```java
TuyaHomeSdk.getTimerManagerInstance().getTimerTaskStatusWithDeviceId(mDevId, new IGetDeviceTimerStatusCallback() {
    @Override
    public void onSuccess(ArrayList<TimerTaskStatus> list) {
        Toast.makeText(mContext,"获取设备的定时状态成功",Toast.LENGTH_LONG).show();
    }
    @Override
    public void onError(String errorCode, String errorMsg) {
        Toast.makeText(mContext, "获取设备的定时状态失败 " + errorMsg, Toast.LENGTH_LONG).show();
    }
});
```


#### 控制某个定时器的开关状态

当关闭某个定时器时，定时不再执行

**接口说明**

控制某个定时器的开关状态

```java
void updateTimerStatusWithTask(String taskName, String devId, String timerId, boolean isOpen, IResultStatusCallback callback);
```

**参数说明**

| 参数        | 说明                                            |
| ----------- | ----------------------------------------------- |
| taskname | 定时分组 |
| devId | 设备 id 或群组 id                             |
| timerId | 定时器 id |
| isOpen | 是否开启 |
| callback    | 回调，主要包括发送成功或失败的回调，不能为 null |

**示例代码**

```java
TuyaHomeSdk.getTimerManagerInstance().updateTimerStatusWithTask(taskName, mDevId, timeId, false, new IResultStatusCallback() {
        @Override
        public void onSuccess() {
            Toast.makeText(mContext, "控制定时器的开关状态成功", Toast.LENGTH_LONG).show();
        }

        @Override
        public void onError(String errorCode, String errorMsg) {
            Toast.makeText(mContext, "控制定时器的开关状态失败 " + errorMsg, Toast.LENGTH_LONG).show();
        }
    });
```

#### 删除定时器

**接口说明**

删除定时器

```java
void removeTimerWithTask(String taskName, String devId, String timerId, IResultStatusCallback callback);
```
**参数说明**

| 参数        | 说明                                            |
| ----------- | ----------------------------------------------- |
| taskname | 定时分组 |
| devId | 设备 id 或群组 id                             |
| timerId | 定时器 id |
| callback    | 回调，主要包括发送成功或失败的回调，不能为 null |


**示例代码**

```java
TuyaHomeSdk.getTimerManagerInstance().removeTimerWithTask(taskName, mDevId, timeId, new IResultStatusCallback() {
    @Override
    public void onSuccess() {
        Toast.makeText(mContext, "删除定时成功", Toast.LENGTH_LONG).show();
    }

    @Override
    public void onError(String errorCode, String errorMsg) {
        Toast.makeText(mContext, "删除定时失败" + errorMsg, Toast.LENGTH_LONG).show();
    }
});
```

### 更新定时器的状态

更新定时器的执行时间等参数，我们提供两个方法实现定时器的更新。第一个是老接口，只支持单 dp 点，第二个是新接口，支持多 dp 点。

**接口说明**

更新定时器的状态 该接口可以修改一个定时器的所有属性。

```java
void updateTimerWithTask(String taskName, String loops, String devId, String timerId, String dpId, String time, boolean isOpen, final IResultStatusCallback callback);

```
**参数说明**

| 参数        | 说明                                            |
| ----------- | ----------------------------------------------- |
| taskname | 定时分组 |
| loops | 一周7天定时执行次数，"0000000", 每一位 0:关闭,1:开启, 从左至右依次表示: 周日 周一 周二 周三 周四 周五 周六 。"0000000" 表示只执行一次，"1111111" 表示每天执行。                                    |
| devId | 设备 id 或群组 id                             |
| timerId | 定时器 id |
| dpId | 设备 dpId |
| time | 定时器执行时间，例如"14:00" ，只支持24小时制 |
| isOpen | 是否开启定时器 |
| callback    | 回调，主要包括发送成功或失败的回调，不能为 null |

**示例代码**

```java
TuyaHomeSdk.getTimerManagerInstance().updateTimerWithTask(taskName,"0011001", mDevId, timeId,  "1", "14:00",true,  new IResultStatusCallback() {
    @Override
    public void onSuccess() {
        Toast.makeText(mContext, "更新定时器属性成功", Toast.LENGTH_LONG).show();
    }
    @Override
    public void onError(String errorCode, String errorMsg) {
        Toast.makeText(mContext, "更新定时器属性失败" + errorMsg, Toast.LENGTH_LONG).show();
    }
});
```

**接口说明**

更新定时器的状态 该接口可以修改一个定时器的所有属性。

```java
void updateTimerWithTask(String taskName, String loops, String devId, String timerId, String instruct, final IResultStatusCallback callback);


```
**参数说明**

| 参数        | 说明                                            |
| ----------- | ----------------------------------------------- |
| taskname | 定时分组 |
| loops | 一周7天定时执行次数，"0000000", 每一位 0:关闭,1:开启, 从左至右依次表示: 周日 周一 周二 周三 周四 周五 周六 。"0000000" 表示只执行一次，"1111111" 表示每天执行。                                    |
| devId | 设备 id 或群组 id                             |
| timerId | 定时器 id |
| instruct | 定时 dp 点数据,json 格式，必须包含 time、dps 字段，例如[{"time": "20:00","dps": {"1": true }] |
| time | 定时器执行时间，例如"14:00" ，只支持24小时制 |
| isOpen | 是否开启定时器 |
| callback    | 回调，主要包括发送成功或失败的回调，不能为 null |

**示例代码**


```java
TuyaHomeSdk.getTimerManagerInstance().updateTimerWithTask(taskName,"0011001", mDevId, timeId,  "[{"time": "20:00", "dps": { "1": true},{"time": "22:00","dps": {"2": true}]",  new IResultStatusCallback() {
    @Override
    public void onSuccess() {
        Toast.makeText(mContext, "更新定时器属性成功", Toast.LENGTH_LONG).show();
    }
    @Override
    public void onError(String errorCode, String errorMsg) {
        Toast.makeText(mContext, "更新定时器属性失败" + errorMsg, Toast.LENGTH_LONG).show();
    }
});
```

### 获取定时任务下所有定时器

**接口说明**

获取一个定时分组下所有定时器

```java
void getTimerWithTask(String taskName, String devId, final IGetTimerWithTaskCallback callback);
```

**参数说明**

| 参数        | 说明                                            |
| ----------- | ----------------------------------------------- |
| taskname | 定时分组 |
| devId | 设备 id 或群组 id                             |
| callback    | 回调，主要包括发送成功或失败的回调，不能为 null |

**示例代码**

```java
TuyaHomeSdk.getTimerManagerInstance().getTimerWithTask(taskName, mDevId, new IGetTimerWithTaskCallback() {
    @Override
    public void onSuccess(TimerTask timerTask) {
        Toast.makeText(mContext, "获取定时任务下的定时 成功", Toast.LENGTH_LONG).show();
    }
    @Override
    public void onError(String errorCode, String errorMsg) {
        Toast.makeText(mContext, "获取定时任务下的定时 失败" + errorMsg, Toast.LENGTH_LONG).show();
    }
});
```



### 获取设备所有定时器

**接口说明**

获取设备所有定时器

```java
void getAllTimerWithDeviceId(String devId, final IGetAllTimerWithDevIdCallback callback);
```
**参数说明**

| 参数        | 说明                                            |
| ----------- | ----------------------------------------------- |
| devId | 设备 id 或群组 id                             |
| callback    | 回调，主要包括发送成功或失败的回调，不能为 null |

**示例代码**

```java
TuyaHomeSdk.getTimerManagerInstance().getAllTimerWithDeviceId(mDevId, new IGetAllTimerWithDevIdCallback() {
    @Override
    public void onSuccess(ArrayList<TimerTask> taskArrayList) {
        Toast.makeText(mContext, "获取设备下的定时 成功", Toast.LENGTH_LONG).show();
    }

    @Override
    public void onError(String errorCode, String errorMsg) {
        Toast.makeText(mContext, "获取设备下的定时 失败" + errorMsg, Toast.LENGTH_LONG).show();
    }
});
```

 