---
template: multi-example
title: Initialization
anchor: initialization
code_examples:
  android:
    lang: java
    request: |
      // cold start
      OptimizelyManager optimizelyManager = OptimizelyManager.builder("project_id")
          .build(getApplication());
      optimizelyManager.initialize(this, new OptimizelyStartListener() {
          @Override
          public void onStart(OptimizelyClient optimizely) {
              //user optimizely client here
          }
      });

      // after initializing the Optimizely Client, you can retrieve it from anywhere
      OptimizelyClient optimizelyClient = optimizelyManager.getOptimizely();

  csharp:
    lang: csharp
    request: |
      using OptimizelySDK;

      Optimizely OptimizelyClient;
      try
      {
          OptimizelyClient = new Optimizely(datafile);
      }
      catch (Exception e)
      {
          // Handle exception gracefully
          return;
      }

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
        // Initialize an Optimizely client
        optimizelyClient = Optimizely.builder(datafile, eventHandler).build();
      } catch (ConfigParseException e) {
        // Handle exception gracefully
        return;
      }

  javascript:
    lang: javascript
    request: |
      var optimizely = require('optimizely-client-sdk');

      // Or ES6
      import optimizely from 'optimizely-client-sdk';

      // Initialize an Optimizely client
      var optimizelyClientInstance = optimizely.createInstance({ datafile: datafile });

      // Skip JSON schema validation for the datafile
      var optimizelyClientInstance = optimizely.createInstance({
        datafile: datafile,
        skipJSONValidation: true
      });

  node:
    lang: javascript
    request: |
      var optimizely = require('optimizely-server-sdk');

      // Or ES6
      import optimizely from 'optimizely-server-sdk'

      // Initialize an Optimizely client
      var optimizelyClient = optimizely.createInstance({ datafile: datafile });

      // Skip JSON schema validation for the datafile
      var optimizelyClient = optimizely.createInstance({
        datafile: datafile,
        skipJSONValidation: true
      });

  objectivec:
    lang: objectivec
    request: |
        OPTLYClient *optimizelyClient = [optimizelyManager initializeWithDatafile:datafile];

  php:
    lang: php
    request: |
      use Optimizely\Optimizely;

      // Initialize an Optimizely client
      $optimizelyClient = new Optimizely($datafile);

      // Skip JSON schema validation
      $optimizelyClient = new Optimizely($datafile, null, null, null, true);

  python:
    lang: python
    request: |
      import optimizely

      # Initialize an Optimizely client
      optimizely_client = optimizely.Optimizely(datafile)

      # Skip JSON schema validation (SDK versions 0.1.1 and above)
      optimizely_client = optimizely.Optimizely(datafile,
                                                skip_json_validation=True)

  ruby:
    lang: ruby
    request: |
      require "optimizely"

      # Initialize an Optimizely client
      optimizely_client = Optimizely::Project.new(datafile)

      # Skip JSON schema validation (SDK versions 0.1.1 and above)
      optimizely_client = Optimizely::Project.new(datafile, nil, nil, nil, true)

  swift:
    lang: swift
    request: |
        let optimizelyClient: OPTLYClient? = optimizelyManager?.initialize(withDatafile:jsonDatafile!)
    
---

<style type="text/css">
  img.screenshot {
    max-width: 90%;
    border-radius: 2px;
    margin-left: 1.5em;
    margin-right: 1.5em;
    margin-top: 0.75em;
    margin-bottom: 2em;
    box-shadow: 0px 2px 4px 2px rgba(0, 129, 186, 0.1), 0 3px 10px 0 rgba(76, 76, 76, 0.25);
  }
    img.diagram {
    max-width: 90%;
    border-radius: 2px;
    margin-left: 1.5em;
    margin-right: 1.5em;
    margin-top: 0.75em;
    margin-bottom: 2em;
  }
  p code {
    white-space: nowrap;
  }
</style>

The <span class="sdk-platform"></span> SDK defines an object — the Optimizely client — to simplify your interface with Optimizely. You can use the client to both [activate experiments](#activation) and [track events](#tracking).

Within your code, the client represents the state of your Optimizely project, so changes in your project will reflect in the client. The client accomplishes this by requiring you to provide your project's [datafile](https://help.optimizely.com/Get_Started/Access_the_datafile_for_an_SDK_project) during initialization.

<div class="hidden visible" data-language-content="language" data-language="android">
<div></div>

You can initialize the Optimizely client in the <span class="sdk-platform"></span> SDK with three steps.
1. Decide on your [datafile management strategy (synchronous vs asynchronous)](#sync-methods).
2. [Initialize the Optimizely manager](#create-manager) with your project ID.
3. Use the Optimizely manager to [initialize the Optimizely client](#create-client) based on your datafile management strategy.
</div>


<div class="hidden" data-language-content="language" data-language="java">
<div></div>

After creating the client, you will have several options on how to manage the datafile within your application, which are detailed in the [datafile article](#datafile).

In addition to the datafile, you'll need to provide an `EventHandler` object as an argument to the `Optimizely.builder` function. You can use our default event handler implementation, as shown in the code at right, or provide your own implementation as described in the [Event dispatcher](#event-dispatcher) section.

`Optimizely.builder` throws a checked exception, [ConfigParseException](https://github.com/optimizely/java-sdk/blob/master/core-api/src/main/java/com/optimizely/ab/config/parser/ConfigParseException.java), if the datafile provided is malformed or has an incorrect schema.
</div>


<div class="hidden" data-language-content="language" data-language="javascript">
<div></div>

After creating the client, you will have several options on how to manage the datafile within your application, which are detailed in the [datafile article](#datafile).

You can optionally pass in a `skipJSONValidation` property as `true` to skip JSON schema validation of the datafile upon `optimizely` instantiation. Skipping JSON schema validation enhances instantiation performance. The `skipJSONValidation` property should only be used if the datafile is being pulled from the REST API or CDN.

In SDK versions 1.4.3 and above, the `skipJSONValidation` property is defaulted to `true`. If you'd like to enable JSON schema validation, you must pass in the `skipJSONValidation` property as `false`, and provide a `JSONSchemaValidator`, such as the one provided by the [optimizely-server-sdk](https://github.com/optimizely/node-sdk/blob/master/lib/utils/json_schema_validator/index.js).
</div>


<div class="hidden" data-language-content="language" data-language="node">
<div></div>

After creating the client, you will have several options on how to manage the datafile within your application, which are detailed in the [datafile article](#datafile).

You can optionally pass in a `skipJSONValidation` property as `true` to skip JSON schema validation of the datafile upon `optimizely` instantiation. Skipping JSON schema validation enhances instantiation performance. The `skipJSONValidation` property should only be used if the datafile is being pulled from the REST API or CDN.
</div>


<div class="hidden" data-language-content="language" data-language="objectivec">
<div></div>

The `Optimizely` class has complete feature parity with server side full stack SDKs (activate, getVariation, and track). In order to help to provide additional optimizations for mobile and OTT--automatic polling for the datafile,  dispatching events in the background, and storing bucketing information--we built the DatafileManager, EventDispatcher, and UserProfile modules which are properties of the `OPTLYManager`.

The `OPTLYClient` class wraps the `Optimizely` core while also overriding the basic event dispatcher in the core and persisting bucketing information about users onto the device so they have a consistent experience between sessions even if traffic allocation is changed. An instance of this class will be returned from the `init` calls of an `OPTLYManager` instance.

The `OPTLYManager` class is the factory for `OPTLYClient` instances. It also owns the `OPTLYDatafileManager` which regularly polls the CDN checking for updated datafiles. The `OPTLYManager` also retains a reference to the last initialize `OPTLYClient` instance which you can get with the `getOptimizely` method. 

In the manager's builder block, you can also specify your own datafile manager, event dispatcher, error handler, logger, and user profile as long as the implementation conforms to the `OPTLYDatafileManager`, `OPTLYEventDispatcher`, `OPTLYErrorHandler`, `OPTLYEventDispatcher`, `OPTLYLogger`, and `OPTLYUserProfile` protocols, respectively.

Read the [SDK configuration documentation](#configuration) to explore the different options available when initializing your `OPTLYClient`.
</div>


<div class="hidden visible" data-language-content="language" data-language="python">
<div></div>

After creating the client, you will have several options on how to manage the datafile within your application, which are detailed in the [datafile article](#datafile).

In SDK versions 0.1.1 and above, you can optionally pass in a `skip_json_validation` property as `True` to skip JSON schema validation of the datafile upon `optimizely` instantiation. Skipping JSON schema validation enhances instantiation performance. The `skip_json_validation` property should only be used if the datafile is being pulled from the REST API or CDN.
</div>


<div class="hidden" data-language-content="language" data-language="ruby">
<div></div>

After creating the client, you will have several options on how to manage the datafile within your application, which are detailed in the [datafile article](#datafile).

In SDK versions 0.1.1 and above, you can optionally pass in a `skip_json_validation` property as `true` to skip JSON schema validation of the datafile upon `Project` instantiation. Skipping JSON schema validation enhances instantiation performance. The `skip_json_validation` property should only be used if the datafile is being pulled from the REST API or CDN.
</div>


<div class="hidden" data-language-content="language" data-language="swift">
<div></div>

The `Optimizely` class has complete feature parity with server side full stack SDKs (activate, getVariation, and track). In order to help to provide additional optimizations for mobile and OTT--automatic polling for the datafile, dispatching events in the background, and storing bucketing information--we built the DatafileManager, EventDispatcher, and UserProfile modules which are properties of the `OPTLYManager`.

The `OPTLYClient` class wraps the `Optimizely` core while also overriding the basic event dispatcher in the core and persisting bucketing information about users onto the device so they have a consistent experience between sessions even if traffic allocation is changed. An instance of this class will be returned from the `init` calls of an `OPTLYManager` instance.

The `OPTLYManager` class is the factory for `OPTLYClient` instances. It also owns the `OPTLYDatafileManager` which regularly polls the CDN checking for updated datafiles. The `OPTLYManager` also retains a reference to the last initialize `OPTLYClient` instance which you can get with the `getOptimizely` method. 

In the manager's builder block, you can also specify your own datafile manager, event dispatcher, error handler, logger, and user profile as long as the implementation conforms to the `OPTLYDatafileManager`, `OPTLYEventDispatcher`, `OPTLYErrorHandler`, `OPTLYEventDispatcher`, `OPTLYLogger`, and `OPTLYUserProfile` protocols, respectively.

Read the [SDK configuration documentation](#configuration) to explore the different options available when initializing your `OPTLYClient`.
</div>

<br>