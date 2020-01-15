---
template: multi-example
title: User attributes
anchor: targeting
code_examples:
  python:
    lang: python
    request: |
      experiment_key = 'my_experiment'
      user_id = 'user123'
      attributes = {'device': 'iPhone', 'ad_source': 'my_campaign'}

      # Conditionally activate an experiment for the provided user
      variation = optimizely.activate(experiment_key, user_id, attributes)

  java:
    lang: java
    request: |
      String experimentKey = "my_experiment";
      String userId = "user123";

      Map<String, String> attributes = new HashMap<String, String>();
      attributes.put("DEVICE", "iPhone");
      attributes.put("AD_SOURCE", "my_campaign");

      // Conditionally activate an experiment for the provided user
      Variation variation = optimizelyClient.activate(experimentKey, userId, attributes);

  csharp:
    lang: csharp
    request: |
      using OptimizelySDK.Entity;

      var experimentKey = "my_experiment";
      var userId = "user123";

      UserAttributes attributes = new UserAttributes
      {
          { "DEVICE", "iPhone" },
          { "AD_SOURCE", "my_campaign" }
      };

      // Conditionally activate an experiment for the provided user
      var variation = OptimizelyClient.Activate(experimentKey, userId, attributes);

  android:
    lang: java
    request: |

      OptimizelyClient optimizely = optimizelyManager.getOptimizely();

      String experimentKey = "my_experiment";
      String userId = "user123";

      Map<String, String> attributes = new HashMap<String, String>();
      attributes.put("DEVICE", "Nexus 6P");
      attributes.put("AD_SOURCE", "my_campaign");

      // Conditionally activate a experiment for the provided user
      Variation variation = optimizely.activate(experimentKey, userId, attributes);

  ruby:
    lang: ruby
    request: |
      experiment_key = 'my_experiment'
      user_id = 'user123'
      attributes = {'DEVICE' => 'iPhone', 'AD_SOURCE' => 'my_campaign'}

      # Conditionally activate an experiment for the provided user
      variation = optimizely_client.activate(experiment_key, user_id, attributes)

  node:
    lang: javascript
    request: |
      var experimentKey = 'my_experiment';
      var userId = 'user123';
      var attributes = { 'device': 'iphone', 'ad_source': 'my_campaign' };

      // Conditionally activate an experiment for the provided user
      var variation = optimizely.activate(experimentKey, userId, attributes);

  javascript:
    lang: javascript
    request: |
      var experimentKey = 'my_experiment';
      var userId = 'user123';
      var attributes = { 'device': 'iphone', 'ad_source': 'my_campaign' };

      // Conditionally activate an experiment for the provided user
      var variation = optimizelyClientInstance.activate(experimentKey, userId, attributes);

  php:
    lang: php
    request: |
      $experimentKey = 'my_experiment';
      $userId = 'user123';
      $attributes = [
          'device' => 'iphone',
          'ad_source' => 'my_campaign'
      ];

      // Conditionally activate an experiment for the provided user
      $variation = $optimizelyClient->activate($experimentKey, $userId, $attributes);

  objectivec:
    lang: objectivec
    request: |
        NSDictionary *attributes = @{@"device" : @"iPhone", @"ad_source" : @"my_campaign"};

        OPTLYVariation *variation = [optimizely activate:@"my_experiment"
                                                  userId:@"user123"
                                              attributes:attributes];
  swift:
    lang: swift
    request: |
        let attributes = ["device" : "iPhone", "ad_source" : "my_campaign"]

        let variation: OPTLYVariation? = optimizely?.activate("my_experiment", userId:"user123", attributes:attributes)
---

If you'd like to be able to segment your experiment data based on attributes of your users, you should include the optional `attributes` argument when activating experiments. Optimizely will include these attributes in the recorded event data so you can segment them on the Optimizely results page.

Passing attributes will also allow you to target your experiments to a particular audience you've defined in Optimizely. If the provided experiment is targeted to an audience, Optimizely will evaluate whether the user falls in an audience that is associated with the experiment before bucketing.

For more information on managing audiences and attributes, see our [Optiverse article](https://help.optimizely.com/Target_Your_Visitors/Create_audiences_in_Optimizely_X_Full_Stack).
