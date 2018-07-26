# Oneup connect for Android

### Table of Contents

- [Installation](#installation)
	- [1. Add Library with Gradle](#1-add-library-with-gradle)
	- [2. Manifest requirements](#2-manifest-requirements)
	- [3. Important: Manage User Permission Authorizations in your Application](#3-important-manage-user-permission-authorizations-in-your-application)
	- [4. Source code to start the monitoring](#4-source-code-to-start-the-monitoring)
- [Sample App](#sample-app)

## Installation

### 1. Add Library with Gradle

Add the below line to your build.gradle file,

```
implementation 'com.oneupconnect:sdk:1.0.0'
```

> If you are using Gradle version below `3.0.0` then you should use `compile` instead of `implementation`.

### 2. Manifest requirements

Add or check you have this permissions in the manifest file,

```
<manifest ...>

  <uses-permission android:name="android.permission.INTERNET" />
  <uses-permission android:name="android.permission.BLUETOOTH"/>
  <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED"/>
  <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
  <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
  ...
  
  <application ...>
    
    <receiver android:name="com.oneupconnect.receiver.BluetoothStateReceiver">
      <intent-filter>
        <action android:name="android.bluetooth.adapter.action.STATE_CHANGED"/>
      </intent-filter>
    </receiver>

    <receiver android:name="com.oneupconnect.receiver.BootReceiver">
      <intent-filter>
        <action android:name="android.intent.action.BOOT_COMPLETED" />
      </intent-filter>
    </receiver>
    
    <service
        android:name="com.oneupconnect.service.BeaconsMonitoringService"
        android:enabled="true">
    </service>
    
    ...
  </application>
  
</manifest>
```


### 3. Important: Manage User Permission Authorizations in your Application

To be able to work correctly, the user must have: 

 - the bluethooth turned ON
 - allowed the Location permision

You have to validate them and include screen/dialog to inform and suggest the users to enable them as often as possible.

### 4. Source Code to start the monitoring

Extends Application and add it to start the monitoring:


```

import com.oneupconnect.service.BeaconsMonitoringService;

...

public class MainApplication extends Application {

	@Override
	public void onCreate() {
		super.onCreate();
		
		BeaconsMonitoringService.setAppToken("YOUR_API_KEY");
		startService(new Intent(this, BeaconsMonitoringService.class));
		
	}

}
```

## Sample App

To run the example project, clone the repo, and run `pod install` from the Example directory.
