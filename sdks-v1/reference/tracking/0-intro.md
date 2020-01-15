---
template: multi-example
title: Events
anchor: tracking
code_examples:
  python:
    lang: python
    request: |
        event_key = 'my_conversion'
        user_id = 'user123'
        attributes = {'device': 'iPhone', 'ad_source': 'my_campaign'}

        # Track a conversion event for the provided user
        optimizely_client.track(event_key, user_id)

        # Track a conversion event for the provided user with attributes
        optimizely_client.track(event_key, user_id, attributes);
  java:
    lang: java
    request: |
        String eventKey = "my_conversion";
        String userId = "user123";

        Map<String, String> attributes = new HashMap<String, String>();
        attributes.put("DEVICE", "iPhone");
        attributes.put("AD_SOURCE", "my_campaign");

        // Track a conversion event for the provided user
        optimizelyClient.track(eventKey, userId);

        // Track a conversion event for the provided user with attributes
        optimizelyClient.track(eventKey, userId, attributes);
  csharp:
    lang: csharp
    request: |
        using OptimizelySDK.Entity;

        var eventKey = "my_conversion";
        var userId = "user123";

        UserAttributes attributes = new UserAttributes
        {
            { "DEVICE", "iPhone" },
            { "AD_SOURCE", "my_campaign" }
        };

        // Track a conversion event for the provided user
        OptimizelyClient.Track(eventKey, userId);

        // Track a conversion event for the provided user with attributes
        OptimizelyClient.Track(eventKey, userId, attributes);
  android:
    lang: java
    request: |
        String eventKey = "my_conversion";
        String userId = "user123";

        Map<String, String> attributes = new HashMap<String, String>();
        attributes.put("DEVICE", "iPhone");
        attributes.put("AD_SOURCE", "my_campaign");

        Optimizely optimizelyClient = optimizelyManager.getOptimizely();

        // Track a conversion event for the provided user
        optimizelyClient.track(eventKey, userId);

        // Track a conversion event for the provided user with attributes
        optimizelyClient.track(eventKey, userId, attributes);
  ruby:
    lang: ruby
    request: |
        event_key = 'my_conversion'
        user_id = 'user123'

        attributes = {
          'device' => 'iPhone',
          'adSource' => 'my_campaign'
        }

        # Track a conversion event for the provided user
        optimizely_client.track(event_key, user_id)

        # Track a conversion event for the provided user with attributes
        optimizely_client.track(event_key, user_id, attributes)
  node:
    lang: javascript
    request: |
        var eventKey = 'my_conversion';
        var userId = 'user123';

        var attributes = {
          device: 'iPhone',
          ad_source: 'my_campaign'
        };
 
        // Track a conversion event for the provided user
        optimizelyClient.track(eventKey, userId);

        // Track a conversion event for the provided user with attributes
        optimizelyClient.track(eventKey, userId, attributes);
  javascript:
    lang: javascript
    request: |
        var eventKey = 'my_conversion';
        var userId = 'user123';

        var attributes = {
          device: 'iPhone',
          ad_source: 'my_campaign'
        };
 
        // Track a conversion event for the provided user
        optimizelyClientInstance.track(eventKey, userId);

        // Track a conversion event for the provided user with attributes
        optimizelyClient.track(eventKey, userId, attributes);
  php:
    lang: php
    request: |
        $eventKey = 'my_conversion';
        $userId = 'user123';

        $attributes = [
            'device' => 'iphone',
            'ad_source' => 'my_campaign'
        ];

        // Track a conversion event for the provided user
        $optimizelyClient->track($eventKey, $userId);

        // Track a conversion event for the provided user with attributes
        $optimizelyClient->track($eventKey, $userId, $attributes);
  objectivec:
    lang: objectivec
    request: |
        NSDictionary *attributes = @{@"device" : @"iPhone", @"ad_source" : @"my_campaign"};

        // Track a conversion event for the provided user
        [optimizely track:@"my_conversion"
                   userId:@"user123"];

        // Track a conversion event for the provided user with attributes
        [optimizely track:@"my_conversion"
                   userId:@"user123"
               attributes:attributes];
  swift:
    lang: swift
    request: |
        let attributes = ["device" : "iPhone", "ad_source" : "my_campaign"]

        // Track a conversion event for the provided user
        optimizely?.track("my_conversion", userId:"user123")

        // Track a conversion event for the provided user with attributes
        optimizely?.track("my_conversion", userId:"user123", attributes:attributes)
---

You can easily track conversion events from your code using the `track` function.

The track function requires an *event key* and a *user ID*. The event key should match the event key you provided when [setting up events](https://help.optimizely.com/Measure_success%3A_Track_visitor_behaviors/Create_events_in_SDK_projects) in the Optimizely web portal. The user ID should match the user ID provided in the `activate` function.

The `track` function can be used to track events across multiple experiments, and will be counted for each experiment only if activate has previously been called for the current user.

To enable segmentation of metrics on the Optimizely results page, you'll also need to pass the same user attributes you used in the `activate` call.

For offline event tracking and other advanced use cases, you can also use the [Event API](/x/events/api).

<div class="attention attention--warning push--bottom">*Note:* The Optimizely experiment results page will only count events that are tracked *after* `activate` has been called. If you are not seeing results on the Optimizely results page, make sure that you are calling `activate` before tracking conversion events.
</div>

<br>
