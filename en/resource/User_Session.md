## Handling of Expired Session


If you have not logged in to your account for a long time, the session expiration error will be returned when you access the server interface. You have to monitor the notification of the`setOnNeedLoginListener` and log in to the account again after the login page is displayed.

**Declaration**

```java
TuyaHomeSdk.setOnNeedLoginListener(INeedLoginListener needLoginListener);
```
**Example**

```java
public class TuyaSmartApp extends Application {

        @Override
        public void onCreate() {
            super.onCreate();
            //Need to register in the application
  			  TuyaHomeSdk.setOnNeedLoginListener(new INeedLoginListener() {
     		  @Override
      		  public void onNeedLogin(Context context) {

      		  }
    });
```
>- Precautions
>
> 	Once such a callback occurs, please go to the login page and let the user log in again.

---