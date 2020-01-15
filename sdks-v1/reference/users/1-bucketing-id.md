---
template: multi-example
title: Bucketing IDs ʙᴇᴛᴀ
anchor: bucketing-id
code_examples:
  python:
    lang: python
    request: |
        experiment_key = 'my_experiment'
        user_id = 'user123'
        attributes = {
            'device': 'iphone',
            'ad_source': 'my_campaign',
            '$opt_bucketing_id': 'bucketingId123'
        };

        # activate with the bucketing ID
        variation_key = optimizely_client.activate(experiment_key, user_id, attributes)

        # track with the bucketing ID
        event_key = 'my_cnversion'
        optimizely_client.track(event_key, user_id, attributes)

        # get variation with the bucketing ID
        variation_key = optimizely_client.get_variation(experiment_key, user_id, attributes)

  java:
    lang: java
    request: |
        String experiementKey = "myExperiment";
        // for simplicity sake, we are just using a generated user id
        String userId = UUID.randomUUID().toString();
        Map<String,String> attributes = new HashMap<String,String>();
        attributes.put("ad_source", "my_campaign");
        attributes.put("browser", "chrome");
        // bucketing id can be passed in alone or with other attributes
        attributes.put(DecisionService.BUCKETING_ATTRIBUTE, "bucketId");

        // Activate with bucketing ID
        Variation backgroundVariation = optimizely.activate(experiementKey, userId, attributes);

        // Track with bucketing ID
        // This tracks a conversion event for the event named `sample_conversion`
        optimizely.track("sample_conversion", userId, attributes);

        // GetVariation with bucketing ID
        optimizely.getVariation(experimentKey, userId, attributes);


  csharp:
    lang: csharp
    request: |
        using OptimizelySDK.Entity;

        var experimentKey = "my_experiment"
        var userId = "user123"
        UserAttributes attributes = new UserAttributes
        {
            { "DEVICE", "iPhone" },
            { "AD_SOURCE", "my_campaign" },
            { "$opt_bucketing_id", "bucketingId123" }
        };

        // activate with the bucketing ID
        var variationKey = OptimizelyClient.Activate(experimentKey, userId, attributes)

        // track with the bucketing ID
        var eventKey = "my_cnversion"
        OptimizelyClient.Track(eventKey, userId, attributes)

        // get variation with the bucketing ID
        var variationKey = OptimizelyClient.GetVariation(experimentKey, userId, attributes)

  android:
    lang: java
    request: |
        SharedPreferences sharedPreferences = getSharedPreferences("user", Context.MODE_PRIVATE);
        String experiementKey = "experimentKey";
        String id = sharedPreferences.getString("userId", null);
        if (id == null) {
            id = UUID.randomUUID().toString();
            sharedPreferences.edit().putString("userId", id).apply();
        }
        Map<String,String> attributes = new HashMap<String,String>();
        // bucketing id can be passed in alone or with other attributes
        attributes.put(DecisionService.BUCKETING_ATTRIBUTE, "bucketId");
        attributes.put("ad_source", "my_campaign");
        attributes.put("browser", "chrome");

        // Activate with bucketing ID
        Variation backgroundVariation = optimizelyManager.getOptimizely().activate(experiementKey, id, attributes);

        // Track with bucketing ID
        // This tracks a conversion event for the event named `sample_conversion`
        OptimizelyClient optimizely = optimizelyManager.getOptimizely();
        optimizely.track("sample_conversion", id, attributes);

        // GetVariation with bucketing ID
        OptimizelyClient optimizely = optimizelyManager.getOptimizely();
        optimizely.getVariation(experimentKey, id, attributes);

  ruby:
    lang: ruby
    request: |
        experiment_key = 'my_experiment'
        user_id = 'user123'
        attributes = {
            'device' => 'iphone',
            'ad_source' => 'my_campaign',
            '$opt_bucketing_id' => 'bucketingId123'
        };

        # activate with the bucketing ID
        variation_key = optimizely_client.activate(experiment_key, user_id, attributes)

        # track with the bucketing ID
        event_key = 'my_cnversion'
        optimizely_client.track(event_key, user_id, attributes)

        # get variation with the bucketing ID
        variation_key = optimizely_client.get_variation(experiment_key, user_id, attributes)

  node:
    lang: javascript
    request: |
        var experimentKey = 'my_experiment';
        var userId = 'user123';
        var attributes = {
            'device': 'iphone',
            'ad_source': 'my_campaign',
            '$opt_bucketing_id': 'bucketingId123'
        };

        // activate with the bucketing ID
        var variationKey = optimizelyClient.activate(experimentKey, userId, attributes);

        // track with the bucketing ID
        var eventkey = 'my_conversion';
        optimizelyClient.track(eventKey, userId, attributes);

        // get variation with the bucketing ID
        var variationKey = optimizelyClient.getVariation(experimentKey, userId, attributes);

  javascript:
    lang: javascript
    request: |
        var experimentKey = 'my_experiment';
        var userId = 'user123';
        var attributes = {
            'device': 'iphone',
            'ad_source': 'my_campaign',
            '$opt_bucketing_id': 'bucketingId123'
        };

        // activate with the bucketing ID
        var variationKey = optimizelyClient.activate(experimentKey, userId, attributes);

        // track with the bucketing ID
        var eventkey = 'my_conversion';
        optimizelyClient.track(eventKey, userId, attributes);

        // get variation with the bucketing ID
        var variationKey = optimizelyClient.getVariation(experimentKey, userId, attributes);

  php:
    lang: php
    request: |
        $experimentKey = 'my_experiment';
        $userId = 'user123';
        $attributes = [
            'device' => 'iphone',
            'ad_source' => 'my_campaign',
            '$opt_bucketing_id' => 'bucketingId123'
        ];

        // activate with the bucketing ID
        $variationKey = $optimizelyClient->activate($experimentKey, $userId, $attributes);

        // track with the bucketing ID
        $eventKey = 'my_conversion';
        $optimizelyClient->track($eventKey, $userId, $attributes);

        // get variation with the bucketing ID
        $variationKey = $optimizelyClient->getVariation($experimentKey, $userId, $attributes);

  objectivec:
    lang: objectivec
    request: |
        NSString *experimentKey = @"myExperiment";
        NSString *userId = @"user123";
        NSDictionary *attributes = @{@"device"              : @"iPhone",
                                     @"ad_source"           : @"my_campaign",
                                     @"$opt_bucketing_id"   : @"bucketingId123"};

        // activate with the bucketing ID
        OPTLYVariation *variation = [optimizelyClient activate:experimentKey
                                                        userId:user123
                                                    attributes:attributes];

        // track with the bucketing ID
        NSString *eventKey = @"myEvent";
        [optimizelyClient track:eventKey
                                userId:user123
                            attributes:attributes];

        // get variation with the bucketing ID
        OPTLYVariation *variation = [optimizelyClient activate:experimentKey
                                                        userId:user123
                                                    attributes:attributes];

  swift:
    lang: swift
    request: |
        let experimentKey = "myExperiment"
        let userId = "user123"
        let forcedVariationKey = "treatment"
        let attributes = ["device"          : "iPhone",
                          "ad_source"       : "my_campaign",
                          "bucketingId"     : "bucketingId123"]

        // activate with the bucketing ID
        optimizelyClient?.activate(experimentKey, userId, attributes)

        // track with the bucketing ID
        let eventKey = 'myConversion'
        optimizelyClient?.track(eventKey, userId, attributes)

        // get variation with the bucketing ID
        let variation = optimizelyClient?.getVariation(experimentKey, userId, attributes)

---

<div class="attention attention--warning push--bottom">
Bucketing ID is a beta feature intended to support customers who want to assign variations with different identifier than they use to count visitors. For example, a company might want to assign variations by account ID while counting visitors by user ID. We're investigating the implications of Bucketing IDs on results analysis, and we'd love your feedback! If you want to participate in this beta release, [open a ticket with our support team](http://www.optimizely.com/support).
</div>


By default, Optimizely assigns users to variations, i.e., [Optimizely "buckets" users](https://www.optimizely.com/optimization-glossary/bucket-testing/), based on submitted user IDs. You can change this behavior by including a bucketing ID.

With a bucketing ID, you decouple user bucketing from user identification. Users who have the same bucketing ID are put into the same bucket and are exposed to the same variation.


<div style="display: none" class="sdk-python">
<div></div>

To include a bucketing ID, use the reserved key `$opt_bucketing_id` in the `attributes` parameter of SDK API method calls. (This technique avoids additional parameter requirements in the SDKs' methods.) The bucketing ID serves as [the seed of the hash value used to assign the user to a variation](https://help.optimizely.com/Build_Campaigns_and_Experiments/How_bucketing_works_in_Optimizely's_Full_Stack%2F%2FMobile_SDKs). Users with the same bucketing ID will have the same hash value, which is why they are exposed to the same variation.
</div>

<div style="display: none" class="sdk-java">
<div></div>

To include a bucketing ID, use the reserved key `bucketId` in the `attributes` parameter of SDK API method calls. (This technique avoids additional parameter requirements in the SDKs' methods.) The bucketing ID serves as [the seed of the hash value used to assign the user to a variation](https://help.optimizely.com/Build_Campaigns_and_Experiments/How_bucketing_works_in_Optimizely's_Full_Stack%2F%2FMobile_SDKs). Users with the same bucketing ID will have the same hash value, which is why they are exposed to the same variation.
</div>

<div style="display: none" class="sdk-ruby">
<div></div>

To include a bucketing ID, use the reserved key `$opt_bucketing_id` in the `attributes` parameter of SDK API method calls. (This technique avoids additional parameter requirements in the SDKs' methods.) The bucketing ID serves as [the seed of the hash value used to assign the user to a variation](https://help.optimizely.com/Build_Campaigns_and_Experiments/How_bucketing_works_in_Optimizely's_Full_Stack%2F%2FMobile_SDKs). Users with the same bucketing ID will have the same hash value, which is why they are exposed to the same variation.
</div>

<div style="display: none" class="sdk-php">
<div></div>

To include a bucketing ID, use the reserved key `$opt_bucketing_id` in the `attributes` parameter of SDK API method calls. (This technique avoids additional parameter requirements in the SDKs' methods.) The bucketing ID serves as [the seed of the hash value used to assign the user to a variation](https://help.optimizely.com/Build_Campaigns_and_Experiments/How_bucketing_works_in_Optimizely's_Full_Stack%2F%2FMobile_SDKs). Users with the same bucketing ID will have the same hash value, which is why they are exposed to the same variation.
</div>

<div style="display: none" class="sdk-csharp">
<div></div>

To include a bucketing ID, use the reserved key `$opt_bucketing_id` in the `attributes` parameter of SDK API method calls. (This technique avoids additional parameter requirements in the SDKs' methods.) The bucketing ID serves as [the seed of the hash value used to assign the user to a variation](https://help.optimizely.com/Build_Campaigns_and_Experiments/How_bucketing_works_in_Optimizely's_Full_Stack%2F%2FMobile_SDKs). Users with the same bucketing ID will have the same hash value, which is why they are exposed to the same variation.
</div>

<div style="display: none" class="sdk-node">
<div></div>

To include a bucketing ID, use the reserved key `$opt_bucketing_id` in the `attributes` parameter of SDK API method calls. (This technique avoids additional parameter requirements in the SDKs' methods.) The bucketing ID serves as [the seed of the hash value used to assign the user to a variation](https://help.optimizely.com/Build_Campaigns_and_Experiments/How_bucketing_works_in_Optimizely's_Full_Stack%2F%2FMobile_SDKs). Users with the same bucketing ID will have the same hash value, which is why they are exposed to the same variation.
</div>

<div style="display: none" class="sdk-javascript">
<div></div>

To include a bucketing ID, use the reserved key `$opt_bucketing_id` in the `attributes` parameter of SDK API method calls. (This technique avoids additional parameter requirements in the SDKs' methods.) The bucketing ID serves as [the seed of the hash value used to assign the user to a variation](https://help.optimizely.com/Build_Campaigns_and_Experiments/How_bucketing_works_in_Optimizely's_Full_Stack%2F%2FMobile_SDKs). Users with the same bucketing ID will have the same hash value, which is why they are exposed to the same variation.
</div>

<div style="display: none" class="sdk-objectivec">
<div></div>

To include a bucketing ID, use the reserved key `$opt_bucketing_id` in the `attributes` parameter of SDK API method calls. (This technique avoids additional parameter requirements in the SDKs' methods.) The bucketing ID serves as [the seed of the hash value used to assign the user to a variation](https://help.optimizely.com/Build_Campaigns_and_Experiments/How_bucketing_works_in_Optimizely's_Full_Stack%2F%2FMobile_SDKs). Users with the same bucketing ID will have the same hash value, which is why they are exposed to the same variation.
</div>

<div style="display: none" class="sdk-swift">
<div></div>

To include a bucketing ID, use the reserved key `bucketingId` in the `attributes` parameter of SDK API method calls. (This technique avoids additional parameter requirements in the SDKs' methods.) The bucketing ID serves as [the seed of the hash value used to assign the user to a variation](https://help.optimizely.com/Build_Campaigns_and_Experiments/How_bucketing_works_in_Optimizely's_Full_Stack%2F%2FMobile_SDKs). Users with the same bucketing ID will have the same hash value, which is why they are exposed to the same variation.
</div>

<div style="display: none" class="sdk-android">
<div></div>

To include a bucketing ID, use the reserved key `bucketId` in the `attributes` parameter of SDK API method calls. (This technique avoids additional parameter requirements in the SDKs' methods.) The bucketing ID serves as [the seed of the hash value used to assign the user to a variation](https://help.optimizely.com/Build_Campaigns_and_Experiments/How_bucketing_works_in_Optimizely's_Full_Stack%2F%2FMobile_SDKs). Users with the same bucketing ID will have the same hash value, which is why they are exposed to the same variation.
</div>


Using a bucketing ID does not affect the user ID. Event data submissions will continue to include user IDs. With the exception of assigning users to specific variations, features that rely on user IDs behave the same regardless of the presence of a separate bucketing ID. If you do not pass a bucketing ID to the `attributes` parameter, users will be bucketed by user IDs, which is the default method.

#### Notes

* The bucketing ID is not persisted.
* Bucketing IDs are not compatible with Optimizely's Rollouts feature.

<!-- Hiding this until we have a KB article to explain the tradeoffs -->
<div class="attention push--ends hidden">
    *Note:* Using Bucketing IDs could skew your results as you will no longer be running a true A/B test.
</div>
