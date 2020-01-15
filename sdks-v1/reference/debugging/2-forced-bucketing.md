---
template: multi-example
title: Forced Bucketing
anchor: forced-bucketing
code_examples:
  python:
    lang: python
    request: |
        experiment_key = "my_experiment"
        user_id = "user123"
        forced_variation_key = "treatment"

        # set a forced variation
        optimizely_client.set_forced_variation(experiment_key, user_id, forced_variation_key)

        # get a forced variation
        variation = optimizely_client.get_forced_variation(experiment_key, user_id)

        # clear a forced variation
        optimizely_client.set_forced_variation(experiment_key, user_id, null)

  java:
    lang: java
    request: |
        String experimentKey = "myExperiment"
        String userId = "user123"
        String forcedVariationKey = "treatment"

        // set a forced variation
        optimizely.setForcedVariation(experimentKey, userId, forcedVariationKey)

        // get a forced variation
        Variation variation = optimizely.getForcedVariation(experimentKey, userId)

        // clear a forced variation
        optimizely.setForcedVariation(experimentKey, userId, null)

  csharp:
    lang: csharp
    request: |
        var experimentKey = "myExperiment";
        var userId = "user123";
        var forcedVariationKey = "treatment";

        // set a forced variation
        optimizelyClient.setForcedVariation(experimentKey, userId, forcedVariationKey);

        // get a forced variation
        var variation = optimizelyClient.getForcedVariation(experimentKey, userId);

        // clear a forced variation
        optimizelyClient.setForcedVariation(experimentKey, userId, null);


  android:
    lang: java
    request: |
        String experimentKey = "myExperiment";
        String userId = "user123";
        String forcedVariationKey = "treatment";

        // set a forced variation
        optimizelyClient.setForcedVariation(experimentKey, userId, forcedVariationKey);

        // get a forced variation
        Variation variation = optimizelyClient.getForcedVariation(experimentKey, userId);

        // clear a forced variation
        optimizelyClient.setForcedVariation(experimentKey, userId, null);

  ruby:
    lang: ruby
    request: |
        experiment_key = "my_experiment"
        user_id = "user123"
        forced_variation_key = "treatment"

        # set a forced variation
        optimizely_client.set_forced_variation(experiment_key, user_id, forced_variation_key)

        # get a forced variation
        variation_key = optimizely_client.get_forced_variation(experiment_key, user_id)

        # clear a forced variation
        optimizely_client.set_forced_variation(experiment_key, user_id, null)

  node:
    lang: javascript
    request: |
        var experimentKey = "myExperiment"
        var userId = "user123"
        var forcedVariationKey = "treatment"

        // set a forced variation
        optimizelyClient.setForcedVariation(experimentKey, userId, forcedVariationKey);

        // get a forced variation
        variationKey = optimizelyClient.getForcedVariation(experimentKey, userId);

        // clear a forced variation
        optimizelyClient.setForcedVariation(experimentKey, userId, null);

  javascript:
    lang: javascript
    request: |
        var experimentKey = "myExperiment"
        var userId = "user123"
        var forcedVariationKey = "treatment"

        // set a forced variation
        optimizelyClient.setForcedVariation(experimentKey, userId, forcedVariationKey);

        // get a forced variation
        variationKey = optimizelyClient.getForcedVariation(experimentKey, userId);

        // clear a forced variation
        optimizelyClient.setForcedVariation(experimentKey, userId, null);

  php:
    lang: php
    request: |
        $experimentKey = 'my_experiment'
        $userId = 'user123'
        $forcedVariationKey = 'treatment'

        // set a forced variation
        $optimizelyClient->setForcedVariation($experimentKey, $userId, $forcedVariationKey)

        // get a forced variation
        $variationKey = $optimizelyClient->getForcedVariation($experimentKey, $userId)

        // clear a forced variation
        $optimizelyClient->setForcedVariation($experimentKey, $userId, null)


  objectivec:
    lang: objectivec
    request: |
        NSString *experimentKey = @"myExperiment";
        NSString *userId = @"user123";
        NSString *forcedVariationKey = @"treatment";

        // set a forced variation
        [self setForcedVariation:experimentKey userId:userId variationKey:forcedVariationKey];

        // get a forced variation
        OPTLYVariation *forcedVariation = [self getForcedVariation:experimentKey userId:userId];

        // clear a forced variation
        [self setForcedVariation:experimentKey userId:userId variationKey:nil];


  swift:
    lang: swift
    request: |
        let experimentKey = "myExperiment"
        let userId = "user123"
        let forcedVariationKey = "treatment"

        // set a forced variation
        optimizelyClient?.setForcedVariation(experimentKey, userId: userId, variationKey: forcedVariationKey)

        // get a forced variation
        let variation = optimizelyClient?.getForcedVariation(experimentKey, userId: userId)

        // clear a forced variation
        optimizelyClient?.setForcedVariation(experimentKey, userId: userId, variationKey: nil)


---
<p>
The forced bucketing feature allows you to force a user into a variation by calling a method in the SDK. This feature is particularly useful for the purpose of testing as it allows you to set the variation on the client in real time, eliminating the uncertainty and latency of a datafile download.
</p>
<p>
Forced bucketing is similar to [whitelisting](#whitelisting) in that it allows you to force a user into a specific variation. However, what differentiates forced bucketing from whitelisting is that you set the variation in the SDK and not on the Optimizely web dashboard (therefore, eliminating the dependency on a datafile download) and you are not limited to how many users can be forced into a variation as you are when whitelisting. It is important to note that the `forcedVariations` field in the datafile is only related to whitelisted variations and not to variations set by this API.
</p>
<p>
The example code demonstrates how to use the forced bucketing API. An *experiment key*, *user ID*, and *variation key* are passed into the set method. The variation set will be cached and used by all SDK API methods, including `activate` and `track`, for that session (i.e., the lifetime of the Optimizely SDK client instance). Variations are overwritten with each set method call. In order to clear the forced variations so that the normal bucketing flow can occur, simply pass `null` as the *variation key* parameter. A corresponding getter method, which passes in the *experiment key* and *user ID*, will allow you to get the variations that you forced a user into for a particular experiment.
</p>
<p>
Forced bucketing variations will take precedence over whitelisted variations, variations saved in the **User Profile Service** (if one exists), and the normal bucketed variation. Events sent to our results backend will proceed as normal when forced bucketing is enabled.
</p>

<br>
