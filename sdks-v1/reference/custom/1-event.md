---
template: multi-example
title: Event dispatcher
anchor: event-dispatcher
code_examples:
  python:
    lang: python
    request: |
      from .event_dispatcher import EventDispatcher as event_dispatcher

      // Create an Optimizely client with the default event dispatcher
      optimizely_client = optimizely.Optimizely(datafile,
                                                event_dispatcher=event_dispatcher)

  java:
    lang: java
    request: |
      import com.optimizely.ab.Optimizely;
      import com.optimizely.ab.config.parser.ConfigParseException;
      import com.optimizely.ab.event.AsyncEventHandler;
      import com.optimizely.ab.event.EventHandler;

      // Creates an async event handler with a max buffer of
      // 20,000 events and a single dispatcher thread
      EventHandler eventHandler = new AsyncEventHandler(20000, 1);

      Optimizely optimizelyClient;
      try {
          // Create an Optimizely client with the default event dispatcher
          optimizelyClient = Optimizely.builder(datafile,
                                                eventHandler).build();
      } catch (ConfigParseException e) {
          // Handle exception gracefully
          return;
      }

  csharp:
    lang: csharp
    request: |
      using OptimizelySDK.Event.Dispatcher;

      // Create an Optimizely client with the default event dispatcher
      Optimizely OptimizelyClient = new Optimizely(
          datafile: config.ProjectConfigJson,
          eventDispatcher: new Event.Dispatcher.DefaultEventDispatcher());

  android:
    lang: java
    request: |
      EventHandler eventHandler = YourEventHandler.getInstance();

      // Create an Optimizely client with your own event handler
      Optimizely optimizelyClient = Optimizely.builder(datafile).
         withEventHandler(eventHandler).
         build(getApplicationContext());

      // With the new Android O differences, you need to register the service for the intent filter you desire in code instead of in the manifest.
      EventRescheduler eventRescheduler = new EventRescheduler();

      getApplicationContext().registerReceiver(eventRescheduler, new IntentFilter(WifiManager.SUPPLICANT_CONNECTION_CHANGE_ACTION));

  ruby:
    lang: ruby
    request: |
      # Create an Optimizely client with the default event dispatcher
      optimizely_client = Optimizely::Project.new(datafile,
                                                  Optimizely::EventDispatcher.new)

  node:
    lang: javascript
    request: |
      var defaultEventDispatcher = require('optimizely-server-sdk/lib/plugins/event_dispatcher');

      // Create an Optimizely client with the default event dispatcher
      var optimizelyClient = optimizely.createInstance({
        datafile: datafile,
        eventDispatcher: defaultEventDispatcher
      });

  javascript:
    lang: javascript
    request: |
      var defaultEventDispatcher = require('optimizely-client-sdk/lib/plugins/event_dispatcher');

      // Create an Optimizely client with the default event dispatcher
      var optimizelyClientInstance = optimizely.createInstance({
        datafile: datafile,
        eventDispatcher: defaultEventDispatcher
      });

  php:
    lang: php
    request: |
      use Optimizely\Event\Dispatcher\DefaultEventDispatcher;

      // Create an Optimizely client with the default event dispatcher
      $optimizelyClient = new Optimizely($datafile, new DefaultEventDispatcher());

  objectivec:
    lang: objectivec
    request: |
      CustomEventDispatcher *customEventDispatcher = [[CustomEventDispatcher alloc] init];

      // initialize your Manager (settings will propagate to OPTLYClient and Optimizely)
      OPTLYManager *manager = [OPTLYManager init:^(OPTLYManagerBuilder * _Nullable builder) {
        builder.projectId = kProjectId;
        builder.eventDispatcher = eventDispatcher;
      }];

  swift:
    lang: swift
    request: |
      let customEventDispatcher: CustomEventDispatcher = CustomEventDispatcher.init()

      // initialize your Manager (settings will propagate to OPTLYClient and Optimizely)
      let manager: OPTLYManager? =  OPTLYManager.init({ (builder) in
        builder!.datafile = datafile
        builder!.eventDispatcher = customEventDispatcher
      })
---

You can optionally change how the SDK sends events to Optimizely by providing an *event dispatcher* method. You should provide your own event dispatcher if you have networking requirements that aren't met by our default dispatcher.

The event dispatching function takes an event object with three properties: `httpVerb`, `url`, and `params`, all of which are built out for you in `EventBuilder`. A `POST` request should be sent to `url` with `params` in the body (be sure to stringify it to JSON) and `{content-type: 'application/json'}` in the headers.

<div class="hidden visible" data-language-content="language" data-language="python">
Our Python SDK includes a basic *synchronous* event dispatcher that can be seen [here](https://github.com/optimizely/python-sdk/blob/master/optimizely/event_dispatcher.py). If you are using the SDK in a production environment you should provide your own event dispatcher using the networking library of your choice. Examples are available in the [code samples](/x/solutions/sdks/code-samples/index.html?language=python#sdk-wrappers) section.
</div>

<div class="hidden visible" data-language-content="language" data-language="ruby">
Our Ruby SDK includes a basic *synchronous* event dispatcher that can be seen [here](https://github.com/optimizely/ruby-sdk/blob/master/lib/optimizely/event_dispatcher.rb). If you are using the SDK in a production environment you should provide your own event dispatcher using the networking library of your choice. Examples are available in the [code samples](/x/solutions/sdks/code-samples/index.html?language=ruby#sdk-wrappers) section.
</div>

<div class="hidden visible" data-language-content="language" data-language="node">
By default, our Node SDK uses a basic asynchronous event dispatcher that can be seen [here](https://github.com/optimizely/node-sdk/blob/master/lib/plugins/event_dispatcher/index.js). If you provide a custom event dispatcher we will expect it to return an ES6 type Promise.
</div>

<div class="hidden visible" data-language-content="language" data-language="php">
Our PHP SDK includes a basic *synchronous* event dispatcher. If you are using the SDK in a production environment you should provide your own event dispatcher using the networking library of your choice.
<br><br>
We also provide another event dispatcher which calls `curl` externally to `POST` data to Optimizely. This event dispatcher has better performance as the process forks and executes in the background, thereby not blocking your application. You need to make sure that you have `curl` installed on your server to be able to use it. The code for this `curl` based event dispatcher can be seen [here](https://github.com/optimizely/php-sdk/blob/master/src/Optimizely/Event/Dispatcher/CurlEventDispatcher.php).
</div>

<div class="hidden visible" data-language-content="language" data-language="javascript">
By default, our JavaScript SDK uses a basic asynchronous event dispatcher that can be seen [here](https://github.com/optimizely/javascript-sdk/blob/master/lib/plugins/event_dispatcher/index.js).
</div>

<div class="hidden visible" data-language-content="language" data-language="csharp">

<div></div>

By default, our C# SDK uses an asynchronous event dispatcher as shown on the right.

</div>

<div class="hidden visible" data-language-content="language" data-language="java">

<div></div>

We provide an asynchronous event dispatcher, [optimizely-sdk-httpclient](https://bintray.com/optimizely/optimizely/optimizely-sdk-httpclient), that requires `org.apache.httpcomponents:httpclient:4.5.2` and is parameterized by in-memory queue size and number of dispatch worker threads.

To use your own event dispatcher, implement the `dispatchEvent` method in our [EventHandler](https://github.com/optimizely/java-sdk/blob/master/core-api/src/main/java/com/optimizely/ab/event/EventHandler.java) interface. `dispatchEvent` takes in a [LogEvent](https://github.com/optimizely/java-sdk/blob/master/core-api/src/main/java/com/optimizely/ab/event/LogEvent.java) object containing all of the information needed to dispatch an event to Optimizely's backend. Events should be sent to `LogEvent.getEndpointUrl` as a `POST` request with `LogEvent.getBody` as the payload and `content-type: "application/json"` as the header.

</div>


<div class="hidden" data-language-content="language" data-language="android">

<div></div>

The included event handler implementation includes queueing and flushing so will work even if an app is offline.  It uses an `IntentService` to queue up events to dispatch.  If they fail to send they are stored in a `sqlite` database and scheduled to be dispatched later.  If you would like to have events flushed when wifi is available or after reboot or reinstall using the default event handler, you need to augment your AndroidManifest.xml to include the intent filter declarations.  

```java
        <!--
          Add these lines to your manifest if you want the event handler background services to schedule themselves again after a boot
          or package replace.
        -->
        <receiver
            android:name="com.optimizely.ab.android.event_handler.EventRescheduler"
            android:enabled="true"
            android:exported="false">
            <intent-filter>
                <action android:name="android.intent.action.MY_PACKAGE_REPLACED" />
                <action android:name="android.intent.action.BOOT_COMPLETED" />
                <action android:name="android.net.wifi.supplicant.CONNECTION_CHANGE" />
            </intent-filter>
        </receiver>
```
You will need to implement [EventHandler](https://github.com/optimizely/java-sdk/blob/master/core-api/src/main/java/com/optimizely/ab/event/EventHandler.java) to use your own.

**Note: In order to handle backgrounding in Android O and later, you will also need to register your event handler rescheduler in code. (See code sample)  
</div>


<div class="hidden" data-language-content="language" data-language="objectivec">

<div></div>

The included event handler implementation, [OptimizelySDKEventDispatcher](https://github.com/optimizely/objective-c-sdk/blob/master/OptimizelySDKEventDispatcher/OptimizelySDKEventDispatcher/OPTLYEventDispatcher.m), includes queueing and flushing so will work even if an app is offline. You will need to implement [OPTLYEventDispatcher](https://github.com/optimizely/objective-c-sdk/blob/master/OptimizelySDKCore/OptimizelySDKCore/OPTLYEventDispatcherBasic.h) to use your own.

</div>


<div class="hidden" data-language-content="language" data-language="swift">

<div></div>

The included event handler implementation, [OptimizelySDKEventDispatcher](https://github.com/optimizely/objective-c-sdk/blob/master/OptimizelySDKEventDispatcher/OptimizelySDKEventDispatcher/OPTLYEventDispatcher.m), includes queueing and flushing so will work even if an app is offline. You will need to implement [OPTLYEventDispatcher](https://github.com/optimizely/objective-c-sdk/blob/master/OptimizelySDKCore/OptimizelySDKCore/OPTLYEventDispatcherBasic.h) to use your own.

</div>
