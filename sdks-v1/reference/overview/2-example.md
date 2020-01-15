---
template: multi-example
title: Example usage
anchor: basic
code_examples:
  python:
    lang: python
    request: |
      from optimizely import optimizely

      # Initialize an Optimizely client
      optimizely_client = optimizely.Optimizely(datafile)

      # Activate user in an experiment
      variation = optimizely_client.activate('my_experiment', user_id)

      if variation == 'control':
        # Execute code for variation A
      elif variation == 'treatment':
        # Execute code for variation B
      else:
        # Execute default code

      # Track conversion event
      optimizely_client.track('my_conversion', user_id)

  java:
    lang: java
    request: |
      import com.optimizely.ab.Optimizely;
      import com.optimizely.ab.config.Variation;

      // Initialize an Optimizely client
      optimizelyClient = Optimizely.builder(datafile, myEventHandler).build();

      // Activate user in an experiment
      Variation variation = optimizelyClient.activate("my_experiment", userId);

      if (variation != null) {
        if (variation.is("control")) {
          // Execute code for variation A
        } else if (variation.is("treatment")) {
          // Execute code for variation B
        }
      } else {
        // Execute default code
      }

      // Track conversion event
      optimizelyClient.track("my_conversion", userId);

  csharp:
    lang: csharp
    request: |
      using OptimizelySDK;

      // Initialize an Optimizely client
      Optimizely OptimizelyClient = new Optimizely(datafile);

      // Activate user in an experiment
      var variation = OptimizelyClient.Activate("my_experiment", userId);

      if (variation != null)
      {
          if (variation == "control")
          {
              // Execute code for variation A
          }
          else if (variation == "treatment")
          {
              // Execute code for variation B
          }
      }
      else
      {
          // Execute default code
      }

      // Track conversion event
      OptimizelyClient.Track("my_conversion", userId);

  android:
    lang: java
    request: |
      import com.optimizely.ab.Optimizely;

      // Get an Optimizely client
      OptimizelyClient optimizelyClient = optimizelyManager.getOptimizely();

      // Activate user in an experiment
      Variation variation = optimizelyClient.activate("my_experiment", "user_id");

      if (variation != null) {
        if (variation.is("control")) {
          // Execute code for variation A
        } else if (variation.is("treatment")) {
          // Execute code for variation B
        }
      } else {
        // Execute default code
      }

      // Track conversion event
      optimizelyClient.track("my_conversion", user_id);

  ruby:
    lang: ruby
    request: |
      require "optimizely"

      # Initialize an Optimizely client
      optimizely_client = Optimizely::Project.new(datafile)

      # Activate user in an experiment
      variation = optimizely_client.activate("my_experiment", user_id)

      if variation == 'control'
        # Execute code for variation A
      elsif variation == 'treatment'
        # Execute code for variation B
      else
        # Execute default code
      end

      # Track conversion event
      optimizely_client.track("my_conversion", user_id)

  node:
    lang: javascript
    request: |
      var optimizely = require('optimizely-server-sdk');

      // Initialize an Optimizely client
      var optimizelyClient = optimizely.createInstance({ datafile: datafile });

      // Activate user in an experiment
      var variation = optimizelyClient.activate("my_experiment", userId);

      if (variation === 'control') {
        // Execute code for variation A
      } else if (variation === 'treatment') {
        // Execute code for variation B
      } else {
        // Execute default code
      }

      // Track conversion event
      optimizelyClient.track("my_conversion", userId);

  javascript:
    lang: javascript
    request: |
      var optimizely = require('optimizely-client-sdk');

      // Initialize an Optimizely client
      var optimizelyClientInstance = optimizely.createInstance({ datafile: datafile });

      // Alternatively, if you don't use CommonJS or npm, you can install the minified snippet and use the globally exported varible as follows
      var optimizelyClientInstance = window.optimizelyClient.createInstance({ datafile: datafile });

      // Activate user in an experiment
      var variation = optimizelyClientInstance.activate("my_experiment", userId);

      if (variation === 'control') {
        // Execute code for variation A
      } else if (variation === 'treatment') {
        // Execute code for variation B
      } else {
        // Execute default code
      }

      // Track conversion event
      optimizelyClientInstance.track("my_conversion", userId);

  php:
    lang: php
    request: |
      use Optimizely\Optimizely;

      // Initialize an Optimizely client
      $optimizelyClient = new Optimizely($datafile);

      // Activate user in an experiment
      $variation = $optimizelyClient->activate('my_experiment', $userId);

      if ($variation == 'control') {
        // Execute code for variation A
      } elseif ($variation == 'treatment') {
        // Execute code for variation B
      } else {
        // Execute default code
      }

      // Track conversion event
      $optimizelyClient->track('my_conversion', $userId);

  objectivec:
    lang: objectivec
    request: |
        // Initialize an Optimizely manager
        OPTLYManager *optlyManager = [OPTLYManager init:^(OPTLYManagerBuilder * _Nullable builder) {
            builder.projectId = @"projectId";
        }];

        // Initialize an Optimizely client by asynchronously downloading the datafile
        [optlyManager initializeWithCallback:^(NSError * _Nullable error, OPTLYClient * _Nullable client) {
            // Activate user in an experiment
            OPTLYVariation *variation = [client activate:@"my_experiment" userId:@"userId"];

            if ([variation.variationKey isEqualToString:@"control"]) {
                // Execute code for the control
            } else if ([variation.variationKey isEqualToString:@"treatment"]) {
                // Execute code for the treatment
            } else {
                // Execute default code
            }

            // Track conversion event
            [client track:@"my_conversion" userId:@"userId"];
        }];

  swift:
    lang: swift
    request: |
        // Initialize an Optimizely manager
        let optimizelyManager : OPTLYManager? = OPTLYManager.init {(builder) in
            builder!.projectId = "projectId"
        }

        // Initialize an Optimizely client by asynchronously downloading the datafile
        optimizelyManager?.initialize(callback: { [weak self] (error, optimizelyClient) in

            // Activate user in an experiment
            if let variation = optimizelyClient?.activate("my_experiment", userId: "userId")
            {
                if (variation.variationKey == "control") {
                    // Execute code for the control
                }
                else if (variation.variationKey == "treatment") {
                    // Execute code for the treatment
                }
            } else {
                // execute default code
            }

            // Track conversion event
            optimizelyClient?.track("my_conversion", userId: "userId")
        })

---

The code at right illustrates the basic usage of the SDK to run an experiment in your code.

First, you need to initialize an [Optimizely client](#initialization) based on your Optimizely project's [datafile](#datafile).

To run an experiment, you'll want to [activate](#activation) the experiment at the point you want to split traffic in your code. The `activate` function returns which variation the current user is assigned to. The `activate` function also sends an event to Optimizely to record that the current user has been exposed to the experiment. In this example, we've created an experiment *my_experiment* with two variations *control* and *treatment*.

You'll also want to [track](#tracking) events for your key conversion metrics. In this example, there is one conversion metric, *my_conversion*. The `track` function can be used to track events across multiple experiments, and will be counted for each experiment only if `activate` has previously been called for the current user.

**Note:** The purpose of this example is familiarize you with the `track` method. However, the example simply shows you how to call the `track` method right after a bucketing decision without any conditions. Normally, you would create a condition for a conversion event and then call the `track` method when that condition is true.

The SDK requires you to provide your own unique user IDs for all of your `activate` and `track` calls. See [User IDs](#user-ids) for more details and best practices on what user IDs to provide.

<div class="hidden" data-language-content="language" data-language="android">

<div></div>

You are responsible for creating and distributing `OptimizelyManager` around your application's components. The manager handles
setting up caches, [**datafile**](#datafile) syncing, and more off of the main thread.  See [Initialization](#initialization) for more details.

</div>

<br>
