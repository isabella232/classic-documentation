---
template: multi-example
title: Create a manager
anchor: create-manager
code_examples:
  android:
    lang: java
    request: |
      // This example demonstrates instantiating an 
      // Optimizely manager during application creation.

      import android.app.Application;
      import com.optimizely.ab.android.sdk.OptimizelyManager;

      public class MyApplication extends Application {

          // You would substitute your Optimizely project ID
          public static final String PROJECT_ID = "86427227240";

          private OptimizelyManager optimizelyManager;


          @Override
          public void onCreate() {
              super.onCreate();

              optimizelyManager = OptimizelyManager.builder(PROJECT_ID)
                      .withEventDispatchInterval(60L * 10L)
                      .withDatafileDownloadInterval(60L * 10L)
                      .build(getApplicationContext());
          }
      }
    
---

<div class="hidden" data-language-content="language" data-language="android">
<div></div>

For the <span class="sdk-platform"></span> SDK, instead of directly initializing the Optimizely client, you first create an Optimizely manager, which you will later use to initialize Optimizely clients.

The Optimizely manager is where you can describe *how* the Optimizely client will function. For example, you will use the Optimizely client to [record when a user performs an action on your site (an event)](#tracking), but you can first specify how often those events will be sent to Optimizely's servers with the Optimizely manager.

<div class="attention attention--good-news push--bottom push--top">
You should create the Optimizely manager inside `Application#onCreate()`.
</div>

#### 1. Get your project ID

To build a manager, you'll need to provide your project ID, which you can find by navigating to the Settings page in the Optimizely web app. The Project ID will be displayed on the Datafile tab under the Details section.

<img src="/assets/img/x/solutions/sdks/reference/initialization/settings-page-project-id.png" class="screenshot" alt="Settings page, project ID" title="Settings page, project ID">

#### 2. Build the manager

To build the manager, use the builder function and pass the project ID: `OptimizelyManager.builder(PROJECT_ID)`.

#### 3. Set parameters (optional)

While building the manager, you can optionally set a couple parameters.

* [*Datafile polling*](#datafile-polling) (highly recommended): Set how often the manager fetches and caches a new datafile: `.withDatafileDownloadInterval(long interval)`.
* [*Event dispatcher*](#event-dispatcher): Set how often your app sends collected events to Optimizely: `withEventDispatchInterval(long interval)`.

Note: `interval` is in seconds.

#### Additional configurations

You can further customize the behavior of the Optimizely manager by overriding default modules with your own. To read more about your configuration options, see [SDK configuration](#configuration).

* `.withDatafileHandler(DatafileHandler overrideHandler)`
* `.withErrorHandler(ErrorHandler errorHandler)`
* `.withEventHandler(EventHandler eventHandler)`
* `.withLogger(Logger overrideHandler)`
* `.withUserProfileService(UserProfileService userProfileService)`
</div>


<div class="hidden visible" data-language-content="language" data-language="csharp">
<div class="unsupported">The <span class="sdk-platform"></span> SDK does not use Optimizely managers.</div>
</div>


<div class="hidden visible" data-language-content="language" data-language="java">
<div class="unsupported">The <span class="sdk-platform"></span> SDK does not use Optimizely managers.</div>
</div>


<div class="hidden visible" data-language-content="language" data-language="javascript">
<div class="unsupported">The <span class="sdk-platform"></span> SDK does not use Optimizely managers.</div>
</div>


<div class="hidden visible" data-language-content="language" data-language="node">
<div class="unsupported">The <span class="sdk-platform"></span> SDK does not use Optimizely managers.</div>
</div>


<div class="hidden visible" data-language-content="language" data-language="objectivec">
<div class="unsupported">The <span class="sdk-platform"></span> SDK does not use Optimizely managers.</div>
</div>


<div class="hidden visible" data-language-content="language" data-language="php">
<div class="unsupported">The <span class="sdk-platform"></span> SDK does not use Optimizely managers.</div>
</div>


<div class="hidden visible" data-language-content="language" data-language="python">
<div class="unsupported">The <span class="sdk-platform"></span> SDK does not use Optimizely managers.</div>
</div>


<div class="hidden visible" data-language-content="language" data-language="ruby">
<div class="unsupported">The <span class="sdk-platform"></span> SDK does not use Optimizely managers.</div>
</div>


<div class="hidden visible" data-language-content="language" data-language="swift">
<div class="unsupported">The <span class="sdk-platform"></span> SDK does not use Optimizely managers.</div>
</div>

<br>