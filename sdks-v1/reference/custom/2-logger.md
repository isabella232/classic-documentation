---
template: multi-example
title: Logger
anchor: logger
code_examples:
  python:
    lang: python
    request: |
      from .logger import NoOpLogger as logger

      optimizely_client = optimizely.Optimizely(datafile,
                                                event_dispatcher=event_dispatcher,
                                                logger=logger)
  ruby:
    lang: ruby
    request: |
      optimizely_client = Optimizely::Project.new(datafile,
                                                  Optimizely::EventDispatcher.new,
                                                  Optimizely::NoOpLogger.new)
  csharp:
    lang: csharp
    request: |
      using OptimizelySDK.Logger;

      ILogger Logger = new Log4NetLogger();
      Optimizely OptimizelyClient = new Optimizely(
          datafile: config.ProjectConfigJson,
          logger: Logger);
  node:
    lang: javascript
    request: |
      var defaultLogger = require('optimizely-server-sdk/lib/plugins/logger');
      var LOG_LEVEL = require('optimizely-server-sdk/lib/enums').LOG_LEVEL;
      var optimizelyClient = optimizely.createInstance({
        datafile: datafile,
        eventDispatcher: defaultEventDispatcher,
        logger: defaultLogger.createLogger({
          logLevel: LOG_LEVEL.INFO
        }),
      });
  javascript:
    lang: javascript
    request: |
      var defaultLogger = {
        log: function(message) {
          console.log(message);
        },
      };

      // custom logger
      var optimizelyClientInstance = optimizely.createInstance({
        datafile: datafile,
        eventDispatcher: defaultEventDispatcher,
        logger: defaultLogger,
      });

      // custom logLevel (2, DEBUG) with default logger
      var optimizelyClientInstance = optimizely.createInstance({
        datafile: datafile,
        logLevel: 2,
      });
  php:
    lang: php
    request: |
      use Optimizely\Logger\DefaultLogger;

      $optimizelyClient = new Optimizely($datafile, null, new DefaultLogger());
  objectivec:
    lang: objectivec
    request: |
      CustomLogger *customLogger = [[CustomLogger alloc] init];

      OPTLYManager *manager = [OPTLYManager init:^(OPTLYManagerBuilder * _Nullable builder) {
        builder.projectId = kProjectId;
        builder.logger = customLogger;
      }];

      OPTLYLoggerDefault *optlyLogger = [[OPTLYLoggerDefault alloc] initWithLogLevel:OptimizelyLogLevelAll];
      OPTLYManager *manager = [OPTLYManager init:^(OPTLYManagerBuilder * _Nullable builder) {
        builder.projectId = kProjectId;
        builder.logger = optlyLogger;
      }];

  swift:
    lang: swift
    request: |
      let customLogger: CustomLogger? = CustomLogger()

      let manager: OPTLYManager? =  OPTLYManager.init({ (builder) in
        builder!.projectId = projectId
        builder!.logger = customLogger
      })

      let optlyLogger: OPTLYLoggerDefault? = OPTLYLoggerDefault.init(logLevel: OptimizelyLogLevel.All)
      let manager: OPTLYManager? =  OPTLYManager.init({ (builder) in
        builder!.projectId = projectId
        builder!.logger = optlyLogger
      })

  android:
    lang: json
    request: |

      # android-logger.properties example

      # Core
      logger.com.optimizely.ab.Optimizely=DEBUG:Optly.core
      logger.com.optimizely.ab.annotations=DEBUG:Optly.annotations
      logger.com.optimizely.ab.bucketing=DEBUG:Optly.bucketing
      logger.com.optimizely.ab.config=DEBUG:Optly.config
      logger.com.optimizely.ab.error=DEBUG:Optly.error
      logger.com.optimizely.ab.event=DEBUG:Optly.event
      logger.com.optimizely.ab.internal=DEBUG:Optly.internal

      # Android
      logger.com.optimizely.ab.android.sdk=DEBUG:Optly.androidSdk
      logger.com.optimizely.ab.android.event_handler=DEBUG:Optly.eventHandler
      logger.com.optimizely.ab.android.shared=DEBUG:Optly.shared
      logger.com.optimizely.ab.android.user_profile=DEBUG:Optly.userProfile

      # Disable most SDK logs by commenting all other lines and uncommenting below
      #logger.com.optimizely.ab=ASSERT:Optly
  ---

The *logger* logs information about your experiments to help you with debugging.

<div class="hidden visible" data-language-content="language" data-language="python">
<p>In the Python SDK, logging functionality is not enabled by default. To improve your experience setting up the SDK and configuring your production environment, we recommend that you pass in a logger for your Optimizely client.</p>
<p>You can use our `SimpleLogger` implementation out of the box, available [here](https://github.com/optimizely/python-sdk/blob/master/optimizely/logger.py#L19).</p>
</div>


<div class="hidden visible" data-language-content="language" data-language="ruby">
<p>In the Ruby SDK, logging functionality is not enabled by default. To improve your experience setting up the SDK and configuring your production environment, we recommend that you pass in a logger for your Optimizely client.</p>
<p>You can use our `SimpleLogger` implementation out of the box, available [here](https://github.com/optimizely/ruby-sdk/blob/master/lib/optimizely/logger.rb#L18).</p>
</div>


<div class="hidden visible" data-language-content="language" data-language="node">
<p>In the Node SDK, logging functionality is not enabled by default. To improve your experience setting up the SDK and configuring your production environment, we recommend that you pass in a logger for your Optimizely client.</p>
<p>You can use our `Logger` implementation out of the box, available [here](https://github.com/optimizely/node-sdk/blob/master/lib/plugins/logger/index.js#L18).</p>
</div>


<div class="hidden visible" data-language-content="language" data-language="javascript">
<p>By default, the JavaScript SDK uses our Logger implementation, available [here](https://github.com/optimizely/node-sdk/blob/master/lib/plugins/logger/index.js#L18). You can also implement your own logger and pass it into the builder when creating an `Optimizely` instance.</p>

<p>It's also possible to configure the log level threshold of the default logger without implementing your own logger. You can do so by passing the constructor an integer `logLevel`. Possible levels are enumerated [here](https://github.com/optimizely/node-sdk/blob/master/lib/utils/enums/index.js#L20-L26).</p>
</div>


<div class="hidden visible" data-language-content="language" data-language="php">
We are working on a default logger for our PHP SDK. Stay posted for updates.
</div>


<div class="hidden visible" data-language-content="language" data-language="java">
<p>In the Java SDK, logging functionality is not enabled by default. To improve your experience setting up the SDK and configuring your production environment, we recommend that you include a [SLF4J](https://www.slf4j.org/) implementation in your dependencies.</p>


<p>For the Java SDK, we require the use of an [SLF4J](http://www.slf4j.org) implementation.</p>
</div>


<div class="hidden" data-language-content="language" data-language="android">

<div></div>

For the Android SDK, you can use our Android SLF4J [logger](https://github.com/noveogroup/android-logger). Logging verbosity can be controlled via the `android-logger.properties` file.  This file can be placed in `src/main/resources`. You can also include a copy in `src/release/resources` with different settings for the build you release to the Play Store.

Read about advanced configuration options [here](https://github.com/noveogroup/android-logger).

</div>


<div class="hidden visible" data-language-content="language" data-language="objectivec">
For the Objective-C SDK, you can use our default logger and configure `OptimizelyLogLevelInfo`. You can initialize it with any log level and pass it in when creating an `Optimizely` instance. You can also implement your own logger and pass it in the builder when creating an `Optimizely` instance.
</div>


<div class="hidden" data-language-content="language" data-language="swift">
For the Swift SDK, you can use our default logger and configure `OptimizelyLogLevel.Info`. You can initialize it with any log level and pass it in when creating an `Optimizely` instance. You can also implement your own logger and pass it in when creating an `Optimizely` instance.
</div>


The log levels vary slightly between SDKs but generally fall in the following buckets:

<h4>Log Levels</h4>
<table class="table">
  <tr>
    <td>`CRITICAL`</td>
    <td>Events that cause the app to crash are logged.</td>
  </tr>
  <tr>
    <td>`ERROR`</td>
    <td>Events that prevent experiments from functioning correctly (e.g., invalid datafile in initialization, invalid experiment keys or event keys) are logged. The user can take action to correct.</td>
  </tr>
  <tr>
    <td>`WARNING`</td>
    <td>Events that don't prevent experiments from functioning correctly, but can have unexpected outcomes (e.g. future API deprecation, logger or error handler are not set properly, nil values from getters) are logged.</td>
  </tr>
  <tr>
    <td>`DEBUG`</td>
    <td>Any information related to errors that can help us debug the issue (e.g., experiment is not running, user is not in experiment, the bucket value generated by our helper method) are logged.</td>
  </tr>
  <tr>
    <td>`INFO`</td>
    <td>Events of significance (e.g, activate started, activate succeeded, tracking started, tracking succeeded) are logged. This is helpful in showing the lifecycle of an API call</td>
  </tr>
</table>

<br>
