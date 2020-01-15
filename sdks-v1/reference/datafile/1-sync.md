---
template: multi-example
title: Synchronization
anchor: sync
code_examples:
  android:
    lang: java
    request: |
      public class MyApplication extends Application {

        private OptimizelyManager optimizelyManager;

        public OptimizelyManager getOptimizelyManager() {
          return optimizelyManager;
        }

        @Override public void onCreate() {
          super.onCreate();

          optimizelyManager = OptimizelyManager.builder("project_id")
          	.build(getApplicationContext());
        }
      }

  objectivec:
    lang: objectivec
    request: |
      OPTLYDatafileManagerDefault *datafileManager = [OPTLYDatafileManagerDefault initWithBuilderBlock:^(OPTLYDatafileManagerBuilder * _Nullable builder) {
        builder.projectId = @"1234";
        builder.datafileFetchInterval = 120; // seconds
      }];

      OPTLYManager *optlyManager = [OPTLYManager init:^(OPTLYManagerBuilder * _Nullable builder) {
        builder.projectId = @"1234";
        builder.datafileManager = datafileManager;
      }];

  swift:
    lang: swift
    request: |
      let datafileManager: OPTLYDatafileManagerDefault? = OPTLYDatafileManagerDefault.initWithBuilderBlock({ (builder) in
        builder!.projectId = "1234"
        builder!.datafileFetchInterval = 120 // seconds
      })

      let optimizelyManager: OPTLYManager? = OPTLYManager.init({ (builder) in
        builder!.projectId = "1234"
        builder!.datafileManager = datafileManager
      })

---

To stay up to date with your experiment configuration in Optimizely, the SDK needs to periodically synchronize its local copy of the datafile.

<div class="hidden" data-language-content="language" data-language="python">
To keep the datafile in sync, we recommend setting up a [webhook](#webhooks) to notify your servers when the datafile changes and then retrieving the latest version. Alternatively, you can pull an updated datafile from the CDN or REST API at a regular interval.
</div>

<div class="hidden" data-language-content="language" data-language="java">
To keep the datafile in sync, we recommend setting up a [webhook](#webhooks) to notify your servers when the datafile changes and then retrieving the latest version. Alternatively, you can pull an updated datafile from the CDN or REST API at a regular interval.
</div>

<div class="hidden" data-language-content="language" data-language="csharp">
To keep the datafile in sync, we recommend setting up a [webhook](#webhooks) to notify your servers when the datafile changes and then retrieving the latest version. Alternatively, you can pull an updated datafile from the CDN or REST API at a regular interval.
</div>

<div class="hidden" data-language-content="language" data-language="ruby">
To keep the datafile in sync, we recommend setting up a [webhook](#webhooks) to notify your servers when the datafile changes and then retrieving the latest version. Alternatively, you can pull an updated datafile from the CDN or REST API at a regular interval.
</div>

<div class="hidden" data-language-content="language" data-language="node">
To keep the datafile in sync, we recommend setting up a [webhook](#webhooks) to notify your servers when the datafile changes and then retrieving the latest version. Alternatively, you can pull an updated datafile from the CDN or REST API at a regular interval.
</div>

<div class="hidden" data-language-content="language" data-language="javascript">
To keep the datafile in sync, we recommend setting up a [webhook](#webhooks) to notify your servers when the datafile changes and then retrieving the latest version. Alternatively, you can pull an updated datafile from the CDN or REST API at a regular interval.
</div>

<div class="hidden" data-language-content="language" data-language="php">
To keep the datafile in sync, we recommend setting up a [webhook](#webhooks) to notify your servers when the datafile changes and then retrieving the latest version. Alternatively, you can pull an updated datafile from the CDN or REST API at a regular interval.
</div>

<div class="hidden" data-language-content="language" data-language="android">

<div></div>

Our Android SDK includes an `OptimizelyManager` class that can be used to handle this synchronization for you. It periodically downloads the latest datafile from Optimizely asynchronously.

You should create an `OptimizelyManager` inside of [`Application#onCreate()`](https://developer.android.com/reference/android/app/Application.html#onCreate().  The example shows how to store the manager as a field in your `Application` subclass and provide a getter for it.  This getter will be used to get the manager in `Activities` and `Services`.  `OptimizelyManager` can also be used with dependency injection frameworks such as Dagger and Guice.

`OptimizelyManager.builder()` is used to make an `OptimizelyManager`.  The builder allows you to configure the Android SDK.

<dfn>`.withEventDispatchInterval(long interval)`</dfn> Controls how often the Android SDK will attempt to dispatch events to Optimizely results if there are events stored that failed to dispatch initially. Dispatch happens in an Android Service and will occur even if the app is not opened back up by the user.  The service will only be scheduled when events that failed to dispatch are stored.  It will be unscheduled when all stored events are flushed. *Default:* `1 day`, `in seconds`

<dfn>`.withDataFileDownloadInterval(long interval)`</dfn> Controls how often the Android SDK will attempt to sync the [datafile](#datafile). This sync happens via an Android Service and helps ensure that the Android SDK's cached datafile is up to date. This service runs indefinitely on interval specified.  

Datafile polling is disabled by default. You can enable it by setting the download interval. This sets up datafile downloads at the specified interval in both foreground and background. In pre-Oreo (7.x and earlier) versions of Android, the service uses a timer and `context.startService` (the interval in seconds is always honored). In Oreo (8.x) and later versions of Android, the JobScheduler is used to queue work items (the OS determines when and if your service will run).

You can configure datafile polling by adding the `DatafileRescheduler` to your app's manifest. For more information, see **Breaking Changes** in the 1.4.0-1.5.1 sections of the <a href="https://github.com/optimizely/android-sdk/blob/master/CHANGELOG.md">Optimizely Android X Changelog</a>.

In order to have these handlers restarted if there is a reboot, reinstall, or for events wifi becomes available, you need to add intent filters to your application manifest.  Please see the android ['test_app'](https://github.com/optimizely/android-sdk/blob/master/test-app/src/main/AndroidManifest.xml)

#### Working with multiple projects

You can have multiple Optimizely projects running in the same app.  This can be accomplished by having one `OptimizelyManager` instance per project ID. Datafile caches, scheduling settings, and Optimizely objects are managed per project ID.

*Note:* You do not need to use `OptimizelyManager`.  You are free to fetch the [datafile](#datafile) on your own and create an `Optimizely` object via `Optimizely.builder(String dataFile, EventHandler)`. You must also use the included `EventHandler` or implement your own. This is explained in detail [below](#configuration).

</div>

<div class="hidden" data-language-content="language" data-language="objectivec">

<div></div>


The `OPTLYDatafileManager` can be used to synchronize the datafile for you. The following datafile implementations are available:

* `OPTLYDatafileManagerDefault`: Periodically downloads the datafile from Optimizely in the background (the default interval is set to 2 minutes). The datafile is saved if it has been updated. However, the SDK does not see this updated datafile until a new client is initialized with the new datafile. The ```OptimizelySDKiOS``` and ```OptimizelySDKTVOS``` frameworks use this implementation out of the box.
* `OPTLYDatafileManagerBasic`: Basic implementation that downloads the datafile but does not include polling and saving. The ```OptimizelySDKShared``` framework uses this implementation out of the box.
* `OPTLYDatafileMangerNoOp`: No-op implementation that does not attempt to download the datafile.

</div>

<div class="hidden" data-language-content="language" data-language="swift">

<div></div>

The `OPTLYDatafileManager` can be used to synchronize the datafile for you. The following datafile implementations are available:

* `OPTLYDatafileManagerDefault`: Periodically downloads the datafile from Optimizely in the background (the default interval is set to 2 minutes). The datafile is saved if it has been updated. However, the SDK does not see this updated datafile until a new client is initialized with the new datafile. The ```OptimizelySDKiOS``` and ```OptimizelySDKTVOS``` frameworks use this implementation out of the box.
* `OPTLYDatafileManagerBasic`: Basic implementation that downloads the datafile but does not include polling and saving. The ```OptimizelySDKShared``` framework uses this implementation out of the box.
* `OPTLYDatafileMangerNoOp`: No-op implementation that does not attempt to download the datafile.

</div>

<br>
