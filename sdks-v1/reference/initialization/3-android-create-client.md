---
template: multi-example
title: Create a client
anchor: create-client
code_examples:
  android:
    lang: java
    request: |
       // Synchronous initialization
       public OptimizelyClient initialize(@NonNull Context context,
           @RawRes Integer datafileRes){
       }

       // Asynchronous initialization
       // Accomplished by overloading the initialize function
       public void initialize(@NonNull final Context context,
           @RawRes final Integer datafileRes,
           @NonNull OptimizelyStartListener optimizelyStartListener) {
       }
    
---

<div class="hidden" data-language-content="language" data-language="android">
<div></div>

The Optimizely client represents the state of your Optimizely project within your code. In more technical terms, the `OptimizelyClient` class wraps the `Optimizely` core and overrides the basic event dispatcher and datafile handler in the core.

<div class="attention attention--warning push--bottom">
<div></div>

Before initializing your client, you must decide on your datafile management strategy: [synchronous or asynchronous](#sync-methods). Each strategy has trade-offs, and you can read more about these in the detailed Optiverse article [Best practices: Datafile management in Full Stack](https://help.optimizely.com/Set_Up_Optimizely/Best_practices%3A_Datafile_management_in_Full_Stack).
</div>

<a name="synchronous-walkthrough">
#### Synchronous initialization

When you initialize a client synchronously, the Optimizely manager first looks for a [cached datafile](#datafile-polling). If one is available, the manager will use it to complete the client initialization. If the manager cannot find a cached datafile, the manager will look for a [bundled datafile](#bundled-datafile). If the manager finds a the bundled datafile, it will use the datafile to complete the client initialization. If the manager cannot find a bundled datafile, the manager will be unable to initialize the client.

<img src="/assets/img/x/solutions/sdks/reference/initialization/initialize-synchronous.png" class="diagram" alt="Synchronous initialization flowchart" title="Synchronous initialization flowchart">

To initialize an `OptimizelyClient` object synchronously, call `OptimizelyManager#initialize()` and provide two arguments:

* The Application instance (from `android.app.Application`)
* An `Integer` pointer to the datafile

For more details on the specific requirements, view [`OptimizelyManager.java` from the publicly available Android SDK](https://github.com/optimizely/android-sdk/blob/master/android-sdk/src/main/java/com/optimizely/ab/android/sdk/OptimizelyManager.java).

<a name="asynchronous-walkthrough">
#### Asynchronous initialization

Initializing a client asynchronously executes like the [synchronous initialization](#synchronous-walkthrough), except the Optimizely manager will first attempt to download the newest datafile. This network activity is what causes an asynchronous initialization to take longer to complete.

If the network request returns an error (such as when network connectivity is unreliable) or if the manager discovers that the cached datafile is identical to the newest datafile, the manager will follow the [synchronous initialization path](#synchronous-walkthrough). If manager discovers that the datafile has been updated and now differs from the cached datafile, the manager will download the new datafile and use it to initialize the client.

<img src="/assets/img/x/solutions/sdks/reference/initialization/initialize-asynchronous.png" class="diagram" alt="Asynchronous initialization flowchart" title="Asynchronous initialization flowchart">

To initialize an `OptimizelyClient` object asynchronously, call `OptimizelyManager#initialize()` and three arguments:

* The Application instance (from `android.app.Application`)
* An `Integer` pointer to the datafile
* A listener object

For more details on the specific requirements and to see how to build each object, view [`OptimizelyManager.java` from the publicly available Android SDK](https://github.com/optimizely/android-sdk/blob/master/android-sdk/src/main/java/com/optimizely/ab/android/sdk/OptimizelyManager.java).

<div class="attention attention--warning push--bottom">
<div></div>

The datafile you pass must have the same project ID that you provided when [initializing the Optimizely manager](#create-manager).
</div>
</div>


<div class="hidden visible" data-language-content="language" data-language="csharp">
<div class="unsupported">Client creation for the <span class="sdk-platform"></span> SDK is detailed elsewhere.</div>
</div>


<div class="hidden visible" data-language-content="language" data-language="java">
<div class="unsupported">Client creation for the <span class="sdk-platform"></span> SDK is detailed elsewhere.</div>
</div>


<div class="hidden visible" data-language-content="language" data-language="javascript">
<div class="unsupported">Client creation for the <span class="sdk-platform"></span> SDK is detailed elsewhere.</div>
</div>


<div class="hidden visible" data-language-content="language" data-language="node">
<div class="unsupported">Client creation for the <span class="sdk-platform"></span> SDK is detailed elsewhere.</div>
</div>


<div class="hidden visible" data-language-content="language" data-language="objectivec">
<div class="unsupported">Client creation for the <span class="sdk-platform"></span> SDK is detailed elsewhere.</div>
</div>


<div class="hidden visible" data-language-content="language" data-language="php">
<div class="unsupported">Client creation for the <span class="sdk-platform"></span> SDK is detailed elsewhere.</div>
</div>


<div class="hidden visible" data-language-content="language" data-language="python">
<div class="unsupported">Client creation for the <span class="sdk-platform"></span> SDK is detailed elsewhere.</div>
</div>


<div class="hidden visible" data-language-content="language" data-language="ruby">
<div class="unsupported">Client creation for the <span class="sdk-platform"></span> SDK is detailed elsewhere.</div>
</div>


<div class="hidden visible" data-language-content="language" data-language="swift">
<div class="unsupported">Client creation for the <span class="sdk-platform"></span> SDK is detailed elsewhere.</div>
</div>

<br>