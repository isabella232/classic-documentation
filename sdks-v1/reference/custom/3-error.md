---
template: multi-example
title: Error handler
anchor: error-handler
code_examples:
  python:
    lang: python
    request: |
      from .error_handler import NoOpErrorHandler as error_handler

      optimizely_client = optimizely.Optimizely(datafile,
                                                event_dispatcher=event_dispatcher,
                                                logger=logger,
                                                error_handler=error_handler)
  java:
    lang: java
    request: |
      import com.optimizely.ab.Optimizely;
      import com.optimizely.ab.error.ErrorHandler;
      import com.optimizely.ab.error.RaiseExceptionErrorHandler;
      import com.optimizely.ab.event.AsyncEventHandler;
      import com.optimizely.ab.event.EventHandler;

      EventHandler eventHandler = new AsyncEventHandler(20000, 1);

      // Default handler that raises exceptions
      ErrorHandler errorHandler = new RaiseExceptionErrorHandler();

      Optimizely optimizelyClient;
      try {
          // Create an Optimizely client with the default event dispatcher
          optimizelyClient = Optimizely.builder(datafile, eventHandler)
                                 .withErrorHandler(errorHandler)
                                 .build();
      } catch (ConfigParseException e) {
          // Handle exception gracefully
          return;
      }

  csharp:
    lang: csharp
    request: |
      using OptimizelySDK.ErrorHandler;

      Optimizely OptimizelyClient = new Optimizely(
          datafile: config.ProjectConfigJson,
          errorHandler: new DefaultErrorHandler());

  android:
    lang: java
    request: |
      // Event handler is required to make Optimizely
      EventHandler eventHandler = YourEventHandler.getInstance();

      // You can optionally provide an error handler
      ErrorHandler errorHandler = YourErrorHandler.getInstance();

      Optimizely optimizelyClient = Optimizely.builder(datafile)
          .withEventHandler(eventHandler)
          .withErrorHandler(errorHandler)
          .build(getApplicationContext());
  ruby:
    lang: ruby
    request: |
      optimizely_client = Optimizely::Project.new(datafile,
                                                  Optimizely::EventDispatcher.new,
                                                  Optimizely::NoOpLogger.new,
                                                  Optimizely::NoOpErrorHandler.new)
  node:
    lang: javascript
    request: |
      var defaultErrorHandler = require('optimizely-server-sdk/lib/plugins/error_handler');

      optimizelyClient = optimizely.createInstance({
        datafile: datafile,
        errorHandler: defaultErrorHandler,
        eventDispatcher: defaultEventDispatcher,
        logger: defaultLogger.createLogger(),
      });
  javascript:
    lang: javascript
    request: |
      var defaultErrorHandler = require('optimizely-server-sdk/lib/plugins/error_handler');

      var optimizelyClientInstance = optimizely.createInstance({
        datafile: datafile,
        errorHandler: defaultErrorHandler,
        eventDispatcher: defaultEventDispatcher,
        logger: defaultLogger.createLogger(),
      });

  php:
    lang: php
    request: |
      use Optimizely\ErrorHandler\DefaultErrorHandler;

      $optimizelyClient = new Optimizely($datafile, null, null, new DefaultErrorHandler());

  objectivec:
    lang: objectivec
    request: |
      CustomErrorHandler *customErrorHandler = [[CustomErrorHandler alloc] init];

      OPTLYManager *manager = [OPTLYManager init:^(OPTLYManagerBuilder * _Nullable builder) {
        builder.projectId = kProjectId;
        builder.errorHandler = customErrorHandler;
      }];
  swift:
    lang: swift
    request: |
      let customErrorHandler: CustomErrorHandler? = CustomErrorHandler()

      let manager: OPTLYManager? =  OPTLYManager.init({ (builder) in
        builder!.projectId = projectId
        builder!.errorHandler = customErrorHandler
      })
---

You can provide your own custom *error handler* logic to standardize across your production environment. This error handler will be called in the following situations:

* Unknown experiment key referenced
* Unknown event key referenced

If the error handler isn’t overridden, a no-op error handler is used by default.

<div class="hidden" data-language-content="language" data-language="objectivec">
You can provide your own custom error handler logic by replacing the `errorHandler` property in the `OPTLYManagerBuilder` object during initialization. The error handler you create must conform to the `OPTLYErrorHandler` protocol. Overriding this module will allow you to standardize error and exception handling across your application.
</div>

<div class="hidden" data-language-content="language" data-language="swift">
You can provide your own custom error handler logic by replacing the `errorHandler` property in the `OPTLYManagerBuilder` object during initialization. The error handler you create must conform to the `OPTLYErrorHandler` protocol. Overriding this module, will allow you to standardize error and exception handling across your application.
</div>

<br>
