---
template: multi-example
title: Initialization methods
anchor: sync-methods
code_examples:
  objectivec:
    lang: objectivec
    request: |
    
       // Create the manager and set the datafile manager
        OPTLYManager *manager = [OPTLYManager init:^(OPTLYManagerBuilder * _Nullable builder) {
            builder.projectId = @"projectId";
        }];
        
        // Synchronously initialize the client, then activate the client
        OPLTYClient *client = [manager initialize];
        OPTLYVariation *variation = [client activate:@"experimentKey"
                                              userId:@"userId"
                                          attributes:nil];
        
        // Or, asynchronously initialize the client, then activate the client
        [manager initializeWithCallback:^(NSError * _Nullable error,
                                          OPTLYClient * _Nullable client) {
            OPTLYVariation *variation = [client activate:@"experimentKey"
                                                  userId:@"userId"
                                              attributes:nil];
        }]
  swift:
    lang: swift
    request: |
    
        // Create the manager
        let optimizelyManager = OPTLYManager.init {(builder) in
            builder!.projectId = "projectId"
        }
        // Synchronously initialize the client, then activate the client
        let optimizelyClient = optimizelyManager?.initialize
        let variation = optimizelyClient?.activate("experimentKey",
                                                   userId:"userId",
                                                   attributes:nil)
        // Or asynchronously initialize the client, then activate the client
        optimizelyManager?.initialize(callback: { [weak self] (error, optimizelyClient) in
            let variation = optimizelyClient?.activate("experimentKey",
                                                        userId:"userId",
                                                        attributes:nil)
        })
  android:
    lang: java
    request: |
      
      // Initialize Optimizely asynchronously
            optimizelyManager.initialize(this,R.raw.datafile, new OptimizelyStartListener() {

                @Override
                public void onStart(OptimizelyClient optimizely) {
                    startVariation();
                }
            });
      

      // Initialize Optimizely synchronously

      optimizelyManager.initialize(myApplication, R.raw.datafile);
      
      optimizelyManager.getOptimizely().getNotificationCenter().addActivateNotificationListener(
        (Experiment experiment, 
          String s,  
          Map<String, String> map,  
          Variation variation,  
          LogEvent logEvent) -> {
        System.out.println("got activation");
      });
      
      optimizelyManager.getOptimizely().getNotificationCenter().addTrackNotificationListener(
        (String s, 
          String s1, 
          Map<String, String> map, 
          Map<String, ?> map1, 
          LogEvent logEvent) -> {
        System.out.println("got track");
      });
      
      startVariation();
    
---

<div class="hidden" data-language-content="language" data-language="android">
<div></div>

<div class="attention attention--good-news push--bottom push--top">
Before you begin to write the code for your Optimizely client initialization, consider the needs of your application.
</div>

The <span class="sdk-platform"></span> SDK offers two methods for initializing the Optimizely client: synchronous and asynchronous. The *behavioral* difference between the two methods is whether your application pings the Optimizely servers for a new datafile during initialization of the Optimizely client. The *functional* difference between the two methods is whether your app prioritizes accuracy or speed.

#### Asynchronous Initialization

The [asynchronous initialization method](#asynchronous-walkthrough) prioritizes accuracy over speed. During initialization of the Optimizely client, your app will request the newest datafile from the CDN servers. Requesting the newest datafile ensures that your app will always use the most current project settings, but it also means your app cannot initialize a client until it downloads a new datafile, discovers the datafile has not changed, or until the request times out. This process takes time.

If you app does not receive a new datafile (for any reason), it will attempt to initialize the client using a [synchronous initialization method](#synchronous-walkthrough).

#### Synchronous Initialization

The [synchronous initialization](#synchronous-walkthrough) method prioritizes speed over accuracy. Instead attempting to download a new datafile every time you initialize an Optimizely client, your app will use a local version of the datafile. This local datafile can be cached from a previous network request (see [datafile polling](#datafile-polling)) or embedded within your app (see [datafile bundling](#bundled-datafile)).

#### Further reading

Read the KB article [Best practices: Datafile management in Full Stack](https://help.optimizely.com/Set_Up_Optimizely/Best_practices%3A_Datafile_management_in_Full_Stack) for more information on the advantages and disadvantages of each initialization method.
</div>


<div class="hidden visible" data-language-content="language" data-language="csharp">
<div class="unsupported">This section is not applicable for the <span class="sdk-platform"></span> SDK.</div>
</div>


<div class="hidden visible" data-language-content="language" data-language="java">
<div class="unsupported">This section is not applicable for the <span class="sdk-platform"></span> SDK.</div>
</div>


<div class="hidden visible" data-language-content="language" data-language="javascript">
<div class="unsupported">This section is not applicable for the <span class="sdk-platform"></span> SDK.</div>
</div>


<div class="hidden visible" data-language-content="language" data-language="node">
<div class="unsupported">This section is not applicable for the <span class="sdk-platform"></span> SDK.</div>
</div>


<div class="hidden" data-language-content="language" data-language="objectivec">

The `OPTLYManager` class provides several options for initializing your client depending where you are running experiments in the app. See [OPTLYManager.h](https://github.com/optimizely/objective-c-sdk/blob/master/OptimizelySDKShared/OptimizelySDKShared/OPTLYManagerBase.h) for full details.

<h4>Synchronous Initialization</h4>

The synchronous initialize method creates a client using a datafile from the local cache. This is the most common way that customers choose to initialize the Optimizely SDK.  Synchronous initialization optimizes for speed, by initializing the SDK using the latest cached datafile. If no datafile is saved or there is an error retrieving the saved datafile, then the bundled datafile is used. If no bundled datafile is provided by the developer, then the SDK will return a dummy client.

<img src="/assets/img/x/solutions/sdks/reference/initialization/initialize-synchronous.png" class="diagram" alt="Synchronous initialization flowchart" title="Synchronous initialization flowchart">

<h4>Asynchronous Initialization</h4>

The asynchronous initialization allows the user to maximize having the most up-to-date experiment data by attempting to download the latest datafile. In the case that there is an error in the datafile download, the latest cached datafile (if one exists) is used. If there are no updates in the datafile, then the datafile is not downloaded and the latest cached datafile is used. If the cached datafile fails to load, then the bundled datafile is used.

<img src="/assets/img/x/solutions/sdks/reference/initialization/initialize-asynchronous.png" class="diagram" alt="Asynchronous initialization flowchart" title="Asynchronous initialization flowchart">

</div>


<div class="hidden visible" data-language-content="language" data-language="php">
<div class="unsupported">This section is not applicable for the <span class="sdk-platform"></span> SDK.</div>
</div>


<div class="hidden visible" data-language-content="language" data-language="python">
<div class="unsupported">This section is not applicable for the <span class="sdk-platform"></span> SDK.</div>
</div>


<div class="hidden visible" data-language-content="language" data-language="ruby">
<div class="unsupported">This section is not applicable for the <span class="sdk-platform"></span> SDK.</div>
</div>


<div class="hidden" data-language-content="language" data-language="swift">
<div></div>

The `OPTLYManager` class provides several options for initializing your client depending where you are running experiments in the app. See [OPTLYManager.h](https://github.com/optimizely/objective-c-sdk/blob/master/OptimizelySDKShared/OptimizelySDKShared/OPTLYManagerBase.h) for full details.

<h4>Synchronous Initialization</h4>

The synchronous initialize method creates a client using a datafile from the local cache. Synchronous initialization maximizes for speed by allowing the user to initialize the client immediately with the latest cached datafile. If no datafile is saved or there is an error retrieving the saved datafile, then the bundled datafile is used. If no bundled datafile is provided by the developer, then the SDK will return a dummy client.

<img src="/assets/img/x/solutions/sdks/reference/initialization/initialize-synchronous.png" class="diagram" alt="Synchronous initialization flowchart" title="Synchronous initialization flowchart">

<h4>Asynchronous Initialization</h4>

The asynchronous initialization allows the user to maximize having the most up-to-date experiment data by attempting to download the latest datafile. In the case that there is an error in the datafile download, the latest cached datafile (if one exists) is used. If there are no updates in the datafile, then the datafile is not downloaded and the latest cached datafile is used. If the cached datafile fails to load, then the bundled datafile is used.

<img src="/assets/img/x/solutions/sdks/reference/initialization/initialize-asynchronous.png" class="diagram" alt="Asynchronous initialization flowchart" title="Asynchronous initialization flowchart">

</div>

<br>