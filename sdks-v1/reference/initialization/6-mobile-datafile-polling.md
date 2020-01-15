---
template: multi-example
title: Datafile polling
anchor: datafile-polling
code_examples:
  android:
    lang: java
    request: |
        optimizelyManager = OptimizelyManager.builder(PROJECT_ID)
            .withDatafileDownloadInterval(60L * 10L)

  objectivec:
    lang: objectivec
    request: |
    
        // Create the datafile manager and set the datafile fetch interval
        OPTLYDatafileManager *datafileManager =
            [OPTLYDatafileManagerDefault init:^(OPTLYDatafileManagerBuilder * _Nullable builder) {
        {
            builder.projectId = @"projectId";
            builder.datafileFetchInterval = 120.0;
        }];
        
        // Create the manager and set the datafile manager
        OPTLYManager *manager = [OPTLYManager init:^(OPTLYManagerBuilder * _Nullable builder) {
            builder.projectId = @"projectId";
            builder.datafileManager = datafileManager;
        }];
        
        // Asynchronously initialize the client, then activate the client
        [manager initializeWithCallback:^(NSError * _Nullable error,
                                          OPTLYClient * _Nullable client) {
            variation = [client activate:@"experimentKey"
                                  userId:@"userId"
                              attributes:nil];
        }
       
  swift:
    lang: swift
    request: |
    
        // Create the datafile manager and set the datafile fetch interval
        let datafileManager = OPTLYDatafileManagerDefault.init{(builder) in
            builder!.projectId = "projectId"
            builder!.datafileFetchInterval = 120.0
        }
        
        // Create the manager and set the datafile manager
        let optimizelyManager = OPTLYManager.init {(builder) in
            builder!.projectId = "projectId"
            builder!.datafileManager = datafileManager!
        }
        
        // Asynchronously initialize the client, then activate the client
        optimizelyManager?.initialize(callback: { [weak self] (error, optimizelyClient) in
            let variation = optimizelyClient?.activate("experimentKey",
                                                       userId:"userId",
                                                       attributes:nil)
        })

---

<div class="hidden" data-language-content="language" data-language="android">
<div></div>

This section applies only if your app uses the datafile handler module included in the Optimizely Android SDK.

During its initialization, the Optimizely manager attempts to pull the newest datafile from the CDN servers. After this, the Optimizely manager will periodically check for and pull a new datafile at the time interval you set during its initialization. The process of checking for and downloading a new datafile is called *datafile polling*.

<div class="attention attention--good-news push--bottom">
To ensure your app always has the latest datafile, you should enable periodic datafile polling.
</div>  

To enable periodic datafile polling, set a value for `withDatafileDownloadInterval` when you initialize the Optimizely manager. This value is the number of seconds the Optimizely manager will wait between datafile polling attempts. If you do not set a value for `.withDatafileDownloadInterval`, the Optimizely manager will check for a new datafile during initialization, but it will not check again.

#### Notes

* Updated datafiles do not take effect until your app is restarted or when you re-initialize the Optimizely manager. This implementation strategy allows the Optimizely SDK to change while the app is running without causing nondeterministic behavior.

* By default, the Optimizely manager will only check for new datafiles when the SDK is active and the app is running. You can configure datafile polling by adding the `DatafileRescheduler` to your app's manifest. For more information, see **Breaking Changes** in the 1.4.0-1.5.1 sections of the <a href="https://github.com/optimizely/android-sdk/blob/master/CHANGELOG.md">Optimizely Android X Changelog</a>. For Android Oreo (8.x) and later where polling is set up to also run in background and foreground: If you don't want background polling you need to unschedule your datafile downloads using the scheduler.
</div>


<div class="hidden visible" data-language-content="language" data-language="csharp">
<div class="unsupported">The <span class="sdk-platform"></span> does not use datafile polling.</div>
</div>


<div class="hidden visible" data-language-content="language" data-language="java">
<div class="unsupported">The <span class="sdk-platform"></span> does not use datafile polling.</div>
</div>


<div class="hidden visible" data-language-content="language" data-language="javascript">
<div class="unsupported">The <span class="sdk-platform"></span> does not use datafile polling.</div>
</div>


<div class="hidden visible" data-language-content="language" data-language="node">
<div class="unsupported">The <span class="sdk-platform"></span> does not use datafile polling.</div>
</div>


<div class="hidden" data-language-content="language" data-language="objectivec">
<div></div>

It is recommended that you enable periodic datafile manager polling so that you will always try to save the latest datafile. When the datafile manager is first created, it will try to pull a new datafile. The datafile manager will wait for the duration of the datafile manager download interval before attempting the next datafile download. The new datafile, however, is not reflected until the next launch or when you initialize the manager again—this is enforced to prevent nondeterministic behavior if the Optimizely SDK changes while the app is running.

In order to enable the datafile manager polling, set a value for `datafileManagerDownloadInterval` when creating the datafile manager. The time unit is in seconds. The datafile polling behavior depends on your SDK and Android versions:
* If you're using SDK 1.4.x and Android Nougat (7.x), datafile polling is never done in the background.
* If you're using SDK 1.5.x and Oreo (8.x) or later, you can configure the time of datafile polling to your preferences.
</div>


<div class="hidden visible" data-language-content="language" data-language="php">
<div class="unsupported">The <span class="sdk-platform"></span> does not use datafile polling.</div>
</div>


<div class="hidden visible" data-language-content="language" data-language="python">
<div class="unsupported">The <span class="sdk-platform"></span> does not use datafile polling.</div>
</div>


<div class="hidden visible" data-language-content="language" data-language="ruby">
<div class="unsupported">The <span class="sdk-platform"></span> does not use datafile polling.</div>
</div>


<div class="hidden" data-language-content="language" data-language="swift">
<div></div>

It is recommended that you enable periodic datafile manager polling so that you will always try to save the latest datafile. When the datafile manager is first created, it will try to pull a new datafile. The datafile manager will wait for the duration of the datafile manager download interval before attempting the next datafile download. The new datafile, however, is not reflected until the next launch or when you initialize the manager again—this is enforced to prevent nondeterministic behavior if the Optimizely SDK changes while the app is running.

In order to enable the datafile manager polling, set a value for `datafileManagerDownloadInterval` when creating the datafile manager. The time unit is in seconds. The datafile polling is never done in the background (only when the SDK is up and running).
</div>

<br>
