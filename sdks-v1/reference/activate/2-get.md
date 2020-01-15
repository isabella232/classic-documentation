---
template: multi-example
title: Variation assignments
anchor: variation
code_examples:
  python:
    lang: python
    request: |
      experiment_key = 'my_experiment'
      user_id = 'user123'

      # Get the active variation for the provided user
      variation = optimizely_client.get_variation(experiment_key, user_id)
  java:
    lang: java
    request: |
      String experimentKey = "my_experiment";
      String userId = "user123";

      // Get the active variation for the provided user
      Variation variation = optimizelyClient.getVariation(experimentKey, userId);
  csharp:
    lang: csharp
    request: |
      var experimentKey = "my_experiment";
      var userId = "user123";

      // Get the active variation for the provided user
      var variation = OptimizelyClient.GetVariation(experimentKey, userId);
  android:
    lang: java
    request: |
      String experimentKey = "my_experiment";
      String userId = "user123";

      Optimizely optimizelyClient = optimizelyManager.getOptimizely();

      // Get the active variation for the provided user
      Variation variation = optimizelyClient.getVariation(experimentKey, userId);
  ruby:
    lang: ruby
    request: |
      experiment_key = 'my_experiment'
      user_id = 'user123'

      # Get the active variation for the provided user
      variation = optimizely_client.get_variation(experiment_key, user_id)

  php:
    lang: php
    request: |
      $experimentKey = 'my_experiment';
      $userId = 'user123';

      # Get the active variation for the provided user
      $variation = $optimizelyClient->getVariation($experimentKey, $userId);

  javascript:
    lang: javascript
    request: |
      var experimentKey = 'my_experiment';
      var userId = 'user123';

      // Get the active variation for the provided user
      var variation = optimizelyClientInstance.getVariation(experimentKey, userId);
  node:
    lang: javascript
    request: |
      var experimentKey = 'my_experiment';
      var userId = 'user123';

      // Get the active variation for the provided user
      var variation = optimizelyClient.getVariation(experimentKey, userId);
  objectivec:
    lang: objectivec
    request: |
      // Get the active variation for an experiment for the provided user
      OPTLYVariation *variation = [optimizely variation:@"my_experiment"
                                                 userId:@"user123"];

  swift:
    lang: swift
    request: |
      // Get the active variation for an experiment for the provided user
      let variation: OPTLYVariation? = optimizely?.variation("my_experiment", userId:"user123")
---

If you would like to retrieve the variation assignment for a given experiment and user without sending a network request to Optimizely, use the code shown on the right. This function has identical behavior to `activate` except that no event is dispatched to Optimizely.

You may want to use this if you're calling `activate` in a different part of your application, or in a different part of your stack, and you want to fork code for your experiment in multiple places. It is still necessary to call `activate` at least once to register that the user was exposed to the experiment.

<br>
