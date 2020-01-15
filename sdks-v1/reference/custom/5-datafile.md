---
template: multi-example
title: Datafile Handler
anchor: datafile-handler
code_examples:
  android:
    lang: java
    request: |
      DatafileHandler datafileHandler = YourDatafileHandler.getInstance();

      // Create an Optimizely client with your own event handler
      Optimizely optimizelyClient = Optimizely.builder(datafile).
         withDatafileHandler(datafileHandler).
         build(getApplicationContext());
---

The default datafile handler is only available in mobile sdks.
<div class="hidden" data-language-content="language" data-language="android">

<div></div>

On some SDKs, you can use a default datafile handler or provide an override. The datafile handler handles how often the datafile is polled for changes. If a modified datafile is found, it is cached for the next startup of the application.  The datafile cache is also available to you.  All of these reside in the datafile-handler module on Android.
<br>
The included event handler implementation includes queueing and flushing so will work even if an app is offline.  It uses an `IntentService` to queue up events to dispatch.  If they fail to send they are stored in a `sqlite` database and scheduled to be dispatched later.  If you would like to have events flushed when wifi is available or after reboot or reinstall using the default event handler, you need to augment your AndroidManifest.xml to include the intent filter declarations.  

```java
        <!--
           Add these lines to your manifest if you want the datafile download background services to schedule themselves again after a boot
           or package replace.
        -->
         <receiver
             android:name="com.optimizely.ab.android.datafile_handler.DatafileRescheduler"
             android:enabled="true"
             android:exported="false">
             <intent-filter>
                 <action android:name="android.intent.action.MY_PACKAGE_REPLACED" />
                 <action android:name="android.intent.action.BOOT_COMPLETED" />
             </intent-filter>
         </receiver>
```

If you would like to override the default datafile handler, you would need to implement [DatafileHandler](https://github.com/optimizely/android-sdk/blob/master/datafile-handler/src/main/java/com/optimizely/ab/android/datafile_handler/DatafileHandler.java) to use your own.

</div>


<div class="hidden" data-language-content="language" data-language="objectivec">

<div></div>
</div>


<div class="hidden" data-language-content="language" data-language="swift">

<div></div>

</div>
