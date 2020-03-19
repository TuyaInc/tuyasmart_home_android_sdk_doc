# 智能场景

智能场景分为「一键执行场景」和「自动化场景」，下文分别简称为「场景」和「自动化」。

场景是用户添加动作，手动触发；自动化是由用户设定条件，当条件触发后自动执行设定的动作。

涂鸦云支持用户根据实际生活场景，通过设置气象或设备条件，当条件满足时，让一个或多个设备执行相应的任务。

| 场景管理 | 说明 | 
| -------------- | ---------- |
|  TuyaHomeSdk.newSceneInstance(String sceneId)   |   提供了单个场景的编辑、删除、执行操作，需要使用场景 id  进行初始化，场景 id 指的是 `SceneBean` 的 `id` 字段，可以从[获取场景列表接口](#GetSceneList)的返回结果中获取。 |
|TuyaHomeSdk.getSceneManagerInstance()| 主要提供了场景里条件、任务、设备、城市相关的所有数据，和场景列表数据获取。|



在使用智能场景相关的接口之前，需要首先了解场景条件和场景任务这两个概念。
## 场景条件

场景条件对应 `SceneCondition` 类，涂鸦云支持以下条件类型：

- 气象条件：包括温度、湿度、天气、PM2.5、空气质量、日落日出，用户选择气象条件时，可以选择当前城市。
- 设备条件：指用户可预先选择一个设备的功能状态，当该设备达到该状态时，会触发当前场景里的任务，但同一设备不能同时作为条件和任务，避免操作冲突。
- 定时条件：指可以按照指定的时间去执行预定的任务。

## 场景任务

场景任务是指当该场景满足已经设定的气象或设备条件时，让一个或多个设备执行某种操作，对应 `SceneTask` 类。或者关闭、开启一个自动化。

## 场景数据操作
### <span id="GetSceneList">场景列表功能</span>


**接口说明**


获取场景列表数据。场景和自动化一起返回，通过条件 conditions 字段是否为空来区分场景和自动化。

```java
void getSceneList(long homeId,ITuyaDataCallback<List<SceneBean>> callback)
```
**参数说明**

| 参数 | 说明 |
| ----------- | ----------------------------------------------- |
| homeId | 家庭 id                           |                                   |
| callback    | 回调 |


其中，`SceneBean`的主要属性定义如下

|字段|类型| 描述 |
| ------ | ------ | ----------- |
| id |Sting| 场景 id 
| name |String| 场景名称 
| conditions | List&lt;SceneCondition&gt; | 场景条件列表
| actions | List&lt;SceneTask&gt; | 场景任务列表
| matchType | int | 满足条件的类型，满足任意条件为1，满足所有条件为2
| enable | boolean | 自动化是否启用



**示例代码**

```java
TuyaHomeSdk.getSceneManagerInstance().getSceneList(long homeId, new ITuyaResultCallback<List<SceneBean>>() {
    @Override
    public void onSuccess(List<SceneBean> result) {
    }

    @Override
    public void onError(String errorCode, String errorMessage) {
    }
});
```


### 获取条件列表

**接口说明**

获取条件列表，如温度、湿度、天气、PM2.5、日落日出等，注意：设备也可作为条件。
条件中的温度分为摄氏度和华氏度，根据需求传入需要的数据。


```java
void getConditionList(boolean showFahrenheit,ITuyaResultCallback<List<ConditionListBean>> callback);
```
**参数说明**

|参数|说明|
| ------ | ----- |
| showFahrenheit |true：使用华氏单位，false：使用摄氏单位|
| callback |回调|

**示例代码**

```java
TuyaHomeSdk.getSceneManagerInstance().getConditionList(new ITuyaDataCallback<List<ConditionListBean>>() {
    @Override
    public void onSuccess(List<ConditionListBean> conditionActionBeans) {
    }

    @Override
    public void onError(String errorCode, String errorMessage) {
    }
});

```

其中， `ConditionListBean` 主要属性定义如下

|字段|类型| 描述 |
| ------ | ------ | ----------- |
| name |Sting| 条件名称 
| type |String| 条件类别 
| Property | IProperty | 条件属性


目前支持的天气条件类别及其名称和 Property 类型 
	
| 名称     | Type       | Property Type |
| -------- | ---------- | ------------- |
| 温度     | Temp       | ValueProperty |
| 湿度     | humidity   | EnumProperty  |
| 天气     | condition  | EnumProperty  |
| PM2.5    | pm25       | EnumProperty  |
| 空气质量 | aqi        | EnumProperty   |
| 日出日落 | sunsetrise | EnumProperty  |
| 定时     | timer      | TimerProperty |
	
	
 Property 是涂鸦智能中一种常用的数据结构，可以用来控制设备和其他功能。目前提供四种 Property: 数值型，枚举型，布尔型和用于定时的类型(与条件中的数值型，枚举型，布尔型相对应), 每种 Property 提供不同的访问接口。详见[规则介绍处](#rules)。



### 创建天气型条件

**接口说明**

天气条件包括温度、湿度、天气、PM2.5、空气质量、日出日落， 可自由选定城市。根据用户账号中设备的不同，可选择的天气条件也不同。

```java
SceneCondition createWeatherCondition(PlaceFacadeBean place, String type, Rule rule)
```
**参数说明**

| 参数        | 说明                                            |
| ----------- | ----------------------------------------------- |
| place | 对应城市天气 。 PlaceFacadeBean 对象请从[获取城市列表](#GetCityList),[根据经纬度获取城市](#GetCityInfoByLATLNG), [根据城市id获取城市](#GetCityByCityId)接口获取。目前获取城市接口只支持国内。                             |
| type | 条件类型。                                      |
| rule    | 条件规则，详见[规则介绍处](#rules) |


**示例代码**

```java
 ValueRule tempRule = ValueRule.newInstance(
      "temp",  //类别：温度
      ">",     //运算规则(">", "==", "<")
      20       //临界值，例子中代表20摄氏度
  );
SceneCondition tempCondition = SceneCondition.createWeatherCondition(
      placeFacadeBean,   //城市类
      "temp",            //类别为温度
      tempRule           //数值类型规则
  );
```


### 创建设备型条件

**接口说明**

设备条件是指当一个设备处于某种状态时，会触发另一台或多台设备的预定任务。<strong>为了避免循环控制，同一台设备无法同时作为条件和任务。</strong>

```java
SceneCondition createDevCondition(DeviceBean devBean, String dpId, Rule rule) 
```
**参数说明**

| 参数        | 说明                                            |
| ----------- | ----------------------------------------------- |
| devBean | 条件设备 。 DeviceBean 从 [获取条件设备列表](#GetConditionDeviceList)接口获取                             
| dpId | 条件dpId。                                      |
| rule    | 条件规则 |

**实例代码**

```java
BoolRule boolRule = BoolRule.newInstance(
    "dp1",    //"dp" + dpId
    true    //触发条件的bool
);
SceneCondition devCondition = SceneCondition.createDevCondition(
    devBean,    //设备
    "1",        //dpId
    boolRule    //规则
);
SceneCondition createDevCondition(DeviceBean devBean, String dpId, Rule rule) 

```

### 创建定时类型条件

**接口说明**

定时条件是指到达指定时间执行预定任务  

```java
SceneCondition createTimerCondition(String display,String name,String type,Rule rule)
```

**参数说明**

| 参数        | 说明                                            |
| ----------- | ----------------------------------------------- |
| display | 用于展示的用户选定的时间条件                          
| name | 定时条件的名称                                     |
| type    | 条件类型|
| rule    | 条件规则|

**示例代码**


```java
TimerRule timerRule = TimerRule.newInstance("Asia/Shanghai","0111110","16:00","20180310")
SceneCondition.createTimerCondition(
      "周一周二周三周四周五",
      "工作日定时",
      "timer",
      timerRule
      )
```

### <span id="rules">rule-条件规则有四种规则:</span>


- 数值型

	以温度为例，数值型条件的最终表达式为" temp > 20"的格式。您可以从获取条件列表接口获得目前支持的温度最大值、最小值、粒度（步进)，您可以从获取条件列表获取支持的温度等。在用户界面上完成配置后， 调用 `ValueRule.newInstance` 方法构建规则，并用规则构成条件。

	**示例代码**

	```java
	
	  ValueProperty tempProperty = (ValueProperty) conditionListBean.getProperty();       //数值型Property
	
	  int max = tempProperty.getMax();       //最大值
	  int min = tempProperty.getMin();       //最小值
	  int step = tempProperty.getStep();     //粒度
	  String unit = tempProperty.getUnit();  //单位
	
	//温度大于20度
	  ValueRule tempRule = ValueRule.newInstance(
	      "temp",  //类别
	      ">",     //运算规则(">", "==", "<")
	      20       //临界值
	  ); 
	SceneCondition tempCondition = SceneCondition.createWeatherCondition(
	      placeFacadeBean,   //城市
	      "temp",            //类别
	      tempRule           //规则
	  );
	```

	  

- 枚举型

	以天气状况为例, 枚举型条件的最终表达式为 "condition == rainy" 的格式，您可以从获取条件列表接口获得目前支持的天气状况，包括每种天气状况的 code 和名称。在用户界面上完成配置后， 调用 `EnumRule.newInstance` 方法构建规则，并用规则构成条件。

	**示例代码**

	```java
	EnumProperty weatherProperty = (EnumProperty) conditionListBean.getProperty();  //枚举型Property
		
	/** 
	*{
	*	{"sunny", "晴天"},
	*	{"rainy", "雨天"}
	*} 
	*/
	HashMap<Object, String> enums = weatherProperty.getEnums();
		
	//天气为下雨
	EnumRule enumRule = EnumRule.newInstance(
	      "condition",  //类别 
	      "rainy"        //选定的枚举值
	);
	SceneCondition weatherCondition = SceneCondition.createWeatherCondition(
	      placeFacadeBean,    //城市
	      "condition",        //类别
	      enumRule            //规则
);
	```

- 布尔型

	布尔型常见于设备型条件, 最终表达式为 "dp1 == true" 的格式, 您需要调用[获取条件设备列表](#GetConditionDeviceList)接口获取支持配置智能场景的设备， 然后根据设备id查询该设备可支持的操作，详见获取设备支持的操作。在用户界面上完成配置后， 调用 `BoolRule.newInstance` 方法构建规则，并用规则构成条件。

	**示例代码**

	```java
	BoolProperty devProperty = (BoolProperty) conditionListBean.getProperty();  //布尔型Property
	
	/**
	{
	  {true, "已开启"},
	  {false, "已关闭"}
	}
	*/
	HashMap<Boolean, String> boolMap = devProperty.getBoolMap(); 
	
	//当设备开启时
	BoolRule boolRule = BoolRule.newInstance(
	    "dp1",    //"dp" + dpId
	    true    //触发条件的bool
	);
	SceneCondition devCondition = SceneCondition.createDevCondition(
	    devBean,    //设备
	    "1",        //dpId
	    boolRule    //规则
	);
	```

- 定时型

	定时的表达式是 Map 类型，即 Key：Value。当用户完成定时配置后，调用 `TimerRule.newInstance` 由SDK完成Map数据组装，构成规则条件。

	**示例代码**

	```java
		
	TimerProperty timerProperty = (TimerProperty)conditionListBean.
	getProperty();	//定时型property
		
	//TimerRule.newInstance 提供两个构造方法，区别是是否传入时区。
	//如果不传入时区将读取默认时区
	/**
	* 
	* @param timeZoneId 时区，格式例如"Asia/Shanghai"
	* @param loops 7位字符串，每一位表示星期几，第一位表示星期日，第二位表示星期一，
	* 依次类推，表示在哪些天启用定时。0表示未选中，1表示选中.格式例如只选中星期一
	* 星期二："0110000"。如果都未选中，则表示定时只执行一次，格式："0000000"
	* @param time 时间，24小时制。格式例如"08:00",如果用户使用12小时制，需要
	* 开发者将之转换为24小时制上传
	* @param date 日期，格式例如"20180310"
	* @return
	*/
	public static TimerRule newInstance(String timeZoneId,String loops,String time,String date);
	  
	//构建定时规则
	TimerRule timerRule = TimerRule.newInstance("Asia/Shanghai","0111110","16:00","20180310") 
	
	/**
	* 所需要的参数与上述方法的参数意义相同，读取默认时区
	* @param loops
	* @param time
	* @param date
	* @return
	*/
	public static TimerRule newInstance(String loops,String time,String date);
	  
	/**
	* 创建定时条件
	* @param display 用于展示给用户的选定的时间
	* @param name  定时条件的名称
	* @param type  条件类型
	* @param rule  条件规则
	* @return
	*/
	public static SceneCondition createTimerCondition(String display,String name,String type,Rule rule);
	  
	//创建定时条件,以上面构建的定时规则为例
	SceneCondition.createTimerCondition(
	"周一周二周三周四周五",
	"工作日定时",
	"timer",
	timerRule
	)
		
	```
	
### <span id="GetConditionDeviceList">获取条件设备列表</span>

**接口说明**

选择场景条件时，选择了设备，需要根据选择设备的 deviceId 获取设备 dp 列表，进而选择某一个dp功能点，即指定该设备执行该dp功能作为该场景的执行条件。


```java
void getConditionDevList(long homeId, ITuyaResultCallback<List<DeviceBean>> callback);
```

**参数说明**

| 参数        | 说明                                            |
| ----------- | ----------------------------------------------- |
| homeId | 家庭 id                          
| callback | 回调                                     |


**示例代码**

```java
TuyaHomeSdk.getSceneManagerInstance().getConditionDevList(homeId ,new ITuyaResultCallback<List<DeviceBean>>() {
    @Override
    public void onSuccess(List<DeviceBean> deviceBeans) {
    }

    @Override
    public void onError(String errorCode, String errorMessage) {
    }
});
```

### 根据设备 id 获取设备任务

**接口说明**

用于获取在选择设备具体的触发条件时， 可选择的任务。

```java
/**
 * 获取设备支持的任务条件列表
 *
 * @param devId    设备 id
 * @param callback 回调
 */
void getDeviceConditionOperationList(String devId,ITuyaResultCallback<List<TaskListBean>> callback);
```
**参数说明**

| 参数        | 说明                                            |
| ----------- | ----------------------------------------------- |
| devId | 设备 id                       
| callback | 回调                                     |

**示例代码**


```java
TuyaHomeSdk.getSceneManagerInstance().getDeviceConditionOperationList(
    devId, //设备 id
    new ITuyaDataCallback<List<TaskListBean>>() {
        @Override
        public void onSuccess(List<TaskListBean> conditionActionBeans) {
        }

        @Override
        public void onError(String errorCode, String errorMessage) {
        }
});
}
```

其中, `TaskListBean` 主要属性定义:

|字段|类型| 描述 |
| ------ | ------ | ----------- |
| name |Sting| dp 点名称， 用于界面展示 
| dpId |long| 设备 dpId
| tasks | HashMap&lt;Object, String&gt;  | dp 点可配置的操作,格式:{true, "已开启"},{false, "已关闭"}
| type | String  | 条件的类型 bool、value、enum 等



### <span id="GetCityList">获取城市列表</span>

**接口说明**

用于在创建天气条件时，选择城市。
注： 目前城市列表暂时仅支持中国。

```java
void getCityListByCountryCode(String countryCode, ITuyaResultCallback<List<PlaceFacadeBean>> callback);
```

**参数说明**

| 参数        | 说明                                            |
| ----------- | ----------------------------------------------- |
| countryCode | 国家码 例如中国="cn"                   
| callback | 回调                                     |

**示例代码**

```java

TuyaHomeSdk.getSceneManagerInstance().getCityListByCountryCode(
	"cn",  //中国
	new ITuyaResultCallback<List<PlaceFacadeBean>>() {
    	@Override
    	public void onSuccess(List<PlaceFacadeBean> placeFacadeBeans) {
    	}

    	@Override
    	public void onError(String errorCode, String errorMessage) {
    	}
});

```

其中, `PlaceFacadeBean` 类主要属性定义如下:

|字段|类型| 描述 |
| ------ | ------ | ----------- |
| area |Sting| 区域名称
| province | String | 省份名称
| city | String | 城市名称
| cityId | long  | cityId


##### 【代码范例】

```java
TuyaHomeSdk.getSceneManagerInstance().getCityListByCountryCode(
	"cn",  //中国
	new ITuyaResultCallback<List<PlaceFacadeBean>>() {
    	@Override
    	public void onSuccess(List<PlaceFacadeBean> placeFacadeBeans) {
    	}

    	@Override
    	public void onError(String errorCode, String errorMessage) {
    	}
});
```

### <span id="GetCityInfoByLATLNG">根据经纬度获取城市信息</span>

**接口说明**

根据经纬度获取城市信息， 用于展示已有的天气条件。

```java
void getCityByLatLng(String lon, String lat, ITuyaResultCallback<PlaceFacadeBean> callback);
```
**参数说明**

|参数|说明|
| ------ | ----- |
| lon | 经度 |
| lat |纬度|
| callback |回调|

**示例代码**

```java
TuyaHomeSdk.getSceneManagerInstance().getCityByLatLng(
    String.valueOf(longitude), //经度
    String.valueOf(latitude),   //纬度
    new ITuyaResultCallback<PlaceFacadeBean>() {
        @Override
        public void onSuccess(PlaceFacadeBean placeFacadeBean) {
        }

        @Override
        public void onError(String errorCode, String errorMessage) {
        }
});
```

### <span id="GetCityByCityId">根据城市 id 获取城市信息</span>

**接口说明**

根据城市 id 获取城市信息， 用于展示已有的天气条件。城市 id 可以在获取城市列表接口中获取。

```java
void getCityByCityIndex(long cityId, ITuyaResultCallback<PlaceFacadeBean> callback);
```

**参数说明**

|参数|说明|
| ------ | ----- |
| cityId |城市 Id|
| callback |回调|

**示例代码**

```java
TuyaHomeSdk.getSceneManagerInstance().getCityByCityIndex(
	cityId, //城市id
	new ITuyaResultCallback<PlaceFacadeBean>() {
		@Override
		public void onSuccess(PlaceFacadeBean placeFacadeBean) {
		}

		@Override
		public void onError(String errorCode, String errorMessage) {
		}
});
```


### 场景动作

场景动作指当条件触发时执行的控制动作。手动场景可执行的动作包含[智能设备类型](#Device_Type)、[群组设备类型](#Group_Type)、[自动化场景类型](#Scene_Type)、[延时类型](#Delay_Type)。自动化场景可执行的动作包含[智能设备类型](#Device_Type)、[群组设备类型](#Group_Type)、[手动场景类型](#Scene_Type)、[自动化场景类型](#Scene_Type)、[延时类型](#Delay_Type)和[消息类型](#Message_Type)。用户可设定的任务视用户的设备而定，请注意，并不是每一款产品都支持场景。

### <span id="Device_Type">1.创建设备类型动作</span>

**接口说明**

用于创建设备类型场景动作。

```java
/**
 * 创建设备类型场景动作
 *
 * @param devId 设备id
 * @param tasks 要执行的任务 格式: { dpId: dp 点值 }
 *                          例：
 *                          {
 *                              "1": true,
 *                          }
 * @return 场景动作
 */
SceneTask createDpTask(@NonNull String devId, HashMap<String, Object> tasks)

```

**参数说明**

|参数|说明|
| ------ | ----- |
| devId |设备  id|
| tasks |要执行的任务 格式: { dpId: dp 点值 } 例:{"1":true}|


**示例代码**

```java
HashMap<String, Object> taskMap = new HashMap<>();
taskMap.put("1", true); //开启设备
SceneTask task = TuyaHomeSceneManager.getInstance().createDpTask(
    devId,      //设备 id
    taskMap     //设备动作
);
```

### <span id="GetActionDevList">获取执行动作支持的设备列表</span>

**接口说明**

获取支持场景动作的设备列表， 用于选择添加到要执行的动作中。

```java
void getTaskDevList(long homeId, ITuyaResultCallback<List<DeviceBean>> callback);
```

**参数说明**

|参数|说明|
| ------ | ----- |
| homeId |家庭 id|
| callback |回调|


其中， `DeviceBean` 主要属性定义如下:

|字段|类型| 描述 |
| ------ | ------ | ----------- |
| name | String | 设备名称
| productId | String | 产品 id
| devId | String | 设备 id
| iconUrl | String  | 图标地址
| isOnline | Boolean  | 设备在线状态，注意：设备在线状态的获取请用此方法 getIsOnline()



**示例代码**

```java
TuyaHomeSdk.getSceneManagerInstance().getTaskDevList(new ITuyaResultCallback<List<DeviceBean>>() {
    @Override
    public void onSuccess(List<DeviceBean> deviceBeans) {
    }

    @Override
    public void onError(String errorCode, String errorMessage) {
    }
});
```

### 根据设备 id 获取可执行的动作

**接口说明**

用于在创建动作时， 获取设备可执行的任务。设备id可以从[获取执行动作支持的设备列表](#GetActionDevList)获取

```java
void getDeviceTaskOperationList(String devId, ITuyaResultCallback<List<TaskListBean>> callback);
```

**参数说明**

|参数|说明|
| ------ | ----- |
| devId | 设备 id|
| callback |回调|

其中, `TaskListBean` 主要属性定义如下:

|字段|类型| 描述 |
| ------ | ------ | ----------- |
| name |Sting| dp 点名称， 用于界面展示 
| dpId |long| 设备 dpId
| tasks | HashMap&lt;Object, String&gt;  | dp 点可配置的操作,格式:{true, "已开启"},{false, "已关闭"}
| type | String  | 条件的类型 bool、value、enum 等


**示例代码**

```java
TuyaHomeSdk.getSceneManagerInstance().getDeviceTaskOperationList(
    devId, //设备id
    new ITuyaResultCallback<List<TaskListBean>>() {
        @Override
        public void onSuccess(List<TaskListBean> conditionActionBeans) {
        }

        @Override
        public void onError(String errorCode, String errorMessage) {
        }
});
```
### <span id="Group_Type">2.创建群组设备类型动作</span>

**接口说明**

用于创建群组设备类型动作

```java
SceneTask createDpGroupTask(@NonNull long groupId, HashMap<String, Object> tasks);

```
**参数说明**

|参数|说明|
| ------ | ----- |
| groupId | 群组 id|
| tasks |要执行的任务，格式: { dpId: dp 点值 }，例{"1":true}|


**示例代码**

```java
HashMap<String, Object> taskMap = new HashMap<>();
taskMap.put("1", true); //开启设备
TuyaHomeSceneManager.getInstance().createDpGroupTask(
	groupId, 	//群组 id
	taskMap 	//设备动作
);
```
### <span id="GetGroupActionDevList">获取执行动作中包含群组设备的设备列表</span>

**接口说明**

获取支持场景动作的设备列表，包含普通设备和群组设备， 用于选择添加到要执行的动作中。


```java
getTaskDevAndGoupList(long homeId, ITuyaResultCallback<SceneTaskGroupDevice> callback)
```
**参数说明**

|参数|说明|
| ------ | ----- |
| homeId | 家庭 id|
| callback |回调|


其中, `SceneTaskGroupDevice` 主要属性定义如下:

|字段|类型| 描述 |
| ------ | ------ | ----------- |
| devices |List&lt;DeviceBean&gt; |普通设备列表
| goups |List&lt; GroupBean&gt;| 群组设备列表

**示例代码**

```java
TuyaHomeSdk.getSceneManagerInstance().getTaskDevAndGoupList(homeId, new ITuyaResultCallback<SceneTaskGroupDevice>() {
                @Override
                public void onSuccess(SceneTaskGroupDevice sceneTaskGroupDevice) {
                    List<DeviceBean> deviceBeans = sceneTaskGroupDevice.getDevices();
                    List<GroupBean> groupBeans = sceneTaskGroupDevice.getGoups();
                    ...
                }

                @Override
                public void onError(String errorCode, String errorMessage) {
                    ...
                }
            });
```


### 根据群组 id 获取可执行的动作

**接口说明**

用于在创建动作时， 获取群组可执行的任务。群组 id 可以从[获取执行动作中包含群组设备的设备列表](#GetGroupActionDevList)获取

```java
void getDeviceTaskOperationListByGroup(String goupId, ITuyaResultCallback<List<TaskListBean>> callback)
```
**参数说明**

|参数|说明|
| ------ | ----- |
| groupId | 群组 id|
| callback |回调|

**示例代码**

```java
TuyaHomeSdk.getSceneManagerInstance().getDeviceTaskOperationListByGroup(groupId, new ITuyaResultCallback<List<TaskListBean>>() {
                @Override
                public void onSuccess(List<TaskListBean> result) {
                    
                }

                @Override
                public void onError(String errorCode, String errorMessage) {

                }
            });
```

### <span id="Scene_Type">3.创建场景类型动作</span>

**接口说明**

用于创建场景类型动作，包含手动场景和自动化场景。
参数可以通过 [场景列表接口](#GetSceneList) 获取

```java
SceneTask createSceneTask(SceneBean sceneBean);

```
**参数说明**

|参数|说明|
| ------ | ----- |
| sceneBean | 场景或自动化对象|

**示例代码**

```java
TuyaHomeSceneManager.getInstance().createSceneTask(scnenBean);
```
### <span id="Delay_Type">4.创建延时类型动作</span>

**接口说明**

用于创建延时类型动作。sdk版本3.13.3之后最大支持300分钟的延时时间，3.13.3之前只支持59分钟59s

```java
SceneTask createDelayTask(int minute, int second);

```
**参数说明**

|参数|说明|
| ------ | ----- |
| minute | 分钟数|
| second | 秒数|


**示例代码**

```java
TuyaHomeSceneManager.getInstance().createDelayTask(
	2,  //分钟
	2	//秒
);
```

### <span id="Message_Type">5、创建消息类型动作</span>

**接口说明**

用于创建消息类型动作。

```java
SceneTask createPushMessage();
```


**示例代码**

```java
TuyaHomeSceneManager.getInstance().createPushMessage();
```

### 场景排序

**接口说明**

对已经存在的场景或自动化进行排序。注意：只能单独对场景或自动化排序，不能混排。

```java
void sortSceneList(long homeId, List<String> sceneIds, IResultCallback callback)
```


**参数说明**

|参数|说明|
| ------ | ----- |
| homeId |家庭 Id|
| sceneIds |手动场景或自动化场景已排序好的的id列表|
| callback |回调|


**示例代码**

```java
TuyaHomeSdk.getSceneManagerInstance().sortSceneList(
    homeId, //家庭列表
    sceneIds,//场景 id 列表
    new IResultCallback() {
        @Override
        public void onSuccess() {
        }

        @Override
        public void onError(String errorCode, String errorMessage) {
        }
});
```
###  <span id="GET_BGS">获取场景背景图片列表</span>

**接口说明**

获取场景支持的背景图片 url 列表。

```java
 void getSceneBgs(ITuyaResultCallback<ArrayList<String>> callback);
```

**参数说明**

|参数|说明|
| ------ | ----- |
| callback |回调|

**示例代码**

```java
TuyaHomeSdk.getSceneManagerInstance().getSceneBgs(new ITuyaResultCallback<ArrayList<String>>() {
        @Override
        public void onSuccess(ArrayList<String> strings) {
            
        }

        @Override
        public void onError(String s, String s1) {

        }
    });
```


## 单个场景操作

TuyaHomeSdk 提供了单个场景的创建、修改、执行、删除4种操作，除了创建其他操作需要使用场景id进行初始化，场景id可以从[获取场景列表接口](#GetSceneList)的接口中拿到

### 添加场景

**接口说明**

添加场景需要传入家庭的 Id，场景名称，是否显示在首页，背景图片的 url，条件列表，任务列表（至少一个任务），前置条件列表（生效时间段,可不传，默认全天生效)，满足任一条件还是满足所有条件时执行。也可以只设置名称和任务，背景图片，不设置条件，但是需要手动执行。


##### 【方法原型】

```java
public void createScene(long homeId, String name, boolean stickyOnTop, String background, List<SceneCondition> conditions, List<SceneTask> tasks, List<PreCondition> preConditions, int matchType, final ITuyaResultCallback<SceneBean> callback);

```
**参数说明**

|参数|说明|
| ------ | ----- |
| homeId | 家庭 Id |
| name | 场景名称 |
| stickyOnTop |  是否显示在首页标识 |
| background | 背景图url，只能使用[获取场景背景图片列表](#GET_BGS)接口中提供的背景图 |
| preConditions | 生效时间段，以前置条件对象集合的形式传入，可不传，默认全天生效 |
| conditions | 场景触发条件  |
| tasks | 场景执行任务 |
| matchType |条件的匹配类型，「与」或者「或」，默认值: SceneBean.MATCH\_TYPE\_OR 表示满足任意条件执行，SceneBean.MATCH\_TYPE\_AND 表示满足所有条件|
| callback |回调|

其中 `PreCondition` 属性定义如下

|字段|类型| 描述 |
| ------ | ------ | ----------- |
| id |Sting| 生效时间段 id，场景创建完成后，云端自动生成，无需手动设置
| condType |String| 当前请设置 PreCondition.TYPE\_TIM\E_CHECK，代表预置条件为生效时间段类型
| expr | PreConditionExpr | 前置条件规则对象

`PreConditionExpr` 属性定义如下 

|字段|类型| 描述 |
| ------ | ------ | ----------- |
| loops | String | 7位字符串，每一位表示星期几，第一位表示星期日，第二位表示星期一， 依次类推，表示在哪些天自动化生效。0表示未选中，1表示选中.格式例如只选中星期一星期二："0110000"。如果都未选中，则表示只生效一次，格式："0000000"|
| start |String| 开始时间（只有 `TIMEINTERVAL_CUSTOM` 自定义类型设置才会生效）
| end | String | 结束时间（只有 `TIMEINTERVAL_CUSTOM` 自定义类型设置才会生效）
| timeInterval | String | 生效时间段类型，`PreCondition.TIMEINTERVAL_ALLDAY`全天，`TIMEINTERVAL_NIGHT` 晚上,`TIMEINTERVAL_DAYTIME` 白天，`TIMEINTERVAL_CUSTOM` 自定义 |
| cityId | String | 城市 Id，可以通过[获取城市列表](#GetCityList)获取
| timeZoneId | String | 生效时区
| cityName | String | 城市名称

**示例代码**

```java
//生效时间段数据创建，可以为空
PreCondition preCondition = new PreCondition();
PreConditionExpr expr = new PreConditionExpr();
expr.setCityName("杭州");
expr.setCityId("xxxxx");//cityId 可通过城市列表接口获取
expr.setStart("00:00");
expr.setEnd("23:59");
expr.setLoops("1111111");
expr.setTimeInterval(PreCondition.TIMEINTERVAL_ALLDAY);
preCondition.setCondType(PreCondition.TYPE_TIME_CHECK);
expr.setTimeZoneId(TimeZone.getDefault().getID());
preCondition.setExpr(expr);
List<PreCondition> preConditions = new ArrayList<>();
preConditions.add(preCondition);

TuyaHomeSdk.getSceneManagerInstance().createScene(
	 100001,
    "Morning", //场景名称
    "https://images.png"
    true,  //是否显示在首页
    preConditions, //生效时间段，可不传
    conditions, //条件
    tasks,     //任务
    SceneBean.MATCH_TYPE_AND, //执行条件类型
    new ITuyaResultCallback<SceneBean>() {
        @Override
        public void onSuccess(SceneBean sceneBean) {
            Log.d(TAG, "createScene Success");
        }

        @Override
        public void onError(String errorCode, String errorMessage) {
        }
});
```

###  编辑场景

**接口说明**

用于修改场景， 成功后会返回新的场景数据。
注：该接口只能用于修改场景，请勿传入新建的 SceneBean 对象。

```java
void modifyScene(SceneBean sceneReqBean, ITuyaResultCallback<SceneBean> callback);
```

**参数说明**

|参数|说明|
| ------ | ----- |
| sceneReqBean | 修改后的场景对象 |


**示例代码**

```java
sceneBean.setName("New name");  //更改场景名称
sceneBean.setConditions(Collections.singletonList(condition)); //更改场景条件
sceneBean.setActions(tasks); //更改场景动作

String sceneId = sceneBean.getId();  //获取场景 id 以初始化
TuyaHomeSdk.newSceneInstance(sceneId).modifyScene(
    sceneBean,  //修改后的场景数据类
    new ITuyaResultCallback<SceneBean>() {
        @Override
        public void onSuccess(SceneBean sceneBean) {
            Log.d(TAG, "Modify Scene Success");
        }

        @Override
        public void onError(String errorCode, String errorMessage) {
        }
});
```


### 删除场景


**接口说明**

用于删除场景。

```java
void deleteScene(IResultCallback callback);
```

**参数说明**

|参数|说明|
| ------ | ----- |
| callback | 回调 |

**示例代码**

```java
String sceneId = sceneBean.getId();  

TuyaHomeSdk.newSceneInstance(sceneId).deleteScene(new 
IResultCallback() {
    @Override
    public void onSuccess() {
        Log.d(TAG, "Delete Scene Success");
    }

    @Override
    public void onError(String errorCode, String errorMessage) {
    }
});
```

### 执行场景

**接口说明**

用于执行手动场景。
	
注：这个方法只管发送指令到云端执行场景，具体设备执行成功与否，需要通过TuyaHomeSdk.newDeviceInstance(devId).registerDevListener() 监听设备的 dp 点变化。

```java
void executeScene(IResultCallback callback);
```

**参数说明**

|参数|说明|
| ------ | ----- |
| callback | 回调 |


**示例代码**

```java
String sceneId = sceneBean.getId();  
TuyaHomeSdk.newSceneInstance(sceneId).executeScene(new IResultCallback() {
    @Override
    public void onSuccess() {
        Log.d(TAG, "Excute Scene Success");
    }

    @Override
    public void onError(String errorCode, String errorMessage) {
    }
});
```

### 开启关闭自动化场景（只有自动化场景才可以开启和失效场景）

**接口说明**

用于开启或关闭自动化场景

```java
void enableScene(String sceneId, final IResultCallback callback);

void disableScene(String sceneId, final IResultCallback callback);
```


**参数说明**

|参数|说明|
| ------ | ----- |
| sceneId |场景 id |
| callback | 回调 |

**示例代码**

```java
String sceneId = sceneBean.getId();  

TuyaHomeSdk.newSceneInstance(sceneId).enableScene(sceneId,new 
IResultCallback() {
    @Override
    public void onSuccess() {
        Log.d(TAG, "enable Scene Success");
    }

    @Override
    public void onError(String errorCode, String errorMessage) {
    }
});

TuyaHomeSdk.newSceneInstance(sceneId).disableScene(sceneId,new 
IResultCallback() {
    @Override
    public void onSuccess() {
        Log.d(TAG, "disable Scene Success");
    }

    @Override
    public void onError(String errorCode, String errorMessage) {
    }
});
```


### 销毁

**接口说明**

如果退出场景的 activity，应该调用场景的销毁方法，以回收内存，提升体验

**示例代码**

```java
TuyaHomeSdk.getSceneManagerInstance().onDestroy();

TuyaHomeSdk.newSceneInstance(sceneId).onDestroy();
```

