---
template: multi-example
title: Event tags
anchor: event-tags
code_examples:
  python:
      lang: python
      request: |
        event_key = 'my_conversion'
        user_id = 'user123'

        attributes = {
          'device': 'iPhone',
          'adSource': 'my_campaign'
        }

        event_tags = {
          'category': 'shoes',
          'purchasePrice': 64.32,
          'revenue': 6432,  # reserved "revenue" tag
          'value': 4 # reserved "value" tag
        }

        # Track event with user attributes and event tags
        optimizely_client.track(event_key, user_id, attributes, event_tags)

        # Track event with event tags and without user attributes
        optimizely_client.track(event_key, user_id, event_tags=event_tags)
  java:
      lang: java
      request: |
        String eventKey = "my_conversion";
        String userId = "user123";

        Map<String, String> attributes = new HashMap<String, String>();
        attributes.put("DEVICE", "iPhone");
        attributes.put("AD_SOURCE", "my_campaign");

        Map<String, Object> eventTags = new HashMap<String, Object>();
        eventTags.put("purchasePrice", 64.32f);
        eventTags.put("category", "shoes");

        // reserved "revenue" tag
        eventTags.put("revenue", 6432);

        // reserved "value" tag
        eventTags.put("value", 4);

        // Track event with user attributes and event tags
        optimizely.track(eventKey, userId, attributes, eventTags);
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

        EventTags tags = new EventTags
        {
            { "purchasePrice", 64.32 },
            { "category", "shoes" },
            { "revenue", 6432 },  // reserved "revenue" tag
            { "value", 4 }  // reserved "value" tag
        };

        // Track event with user attributes and event tags
        OptimizelyClient.Track(eventKey, userId, attributes, tags);
  ruby:
      lang: ruby
      request: |
        event_key = 'my_conversion'
        user_id = 'user123'

        attributes = {
          'device' => 'iPhone',
          'adSource' => 'my_campaign'
        }

        event_tags = {
          'category' => 'shoes',
          'purchasePrice' => 64.32,
          'revenue' => 6432,  # reserved "revenue" tag
          'value' => 4 # reserved "value" tag
        }

        # Track event with user attributes and event tags
        optimizely_client.track(event_key, user_id, attributes, event_tags)

        # Track event with event tags and without user attributes
        optimizely_client.track(event_key, user_id, nil, event_tags)
  php:
      lang: php
      request: |
        $eventKey = 'my_conversion';
        $userId = 'user123';

        $attributes = [
            'device' => 'iphone',
            'ad_source' => 'my_campaign'
        ];

        $eventTags = [
            'category' => 'shoes',
            'purchasePrice' => 64.32,
            'revenue' => 6432, # reserved "revenue" tag
            'value' => 4 # reserved "value" tag
        ];

        # Track event with user attributes and event tags
        $optimizelyClient->track($eventKey, $userId, $attributes, $eventTags);

        # Track event with event tags and without user attributes
        $optimizelyClient->track($eventKey, $userId, null, $eventTags);
  node:
      lang: javascript
      request: |
        var eventKey = "my_conversion";
        var userId = "user123";

        var attributes = {
          DEVICE: 'iPhone',
          AD_SOURCE: 'my_campaign'
        };

        var eventTags = {
          category: 'shoes',
          purchasePrice: 64.32,
          revenue: 6432,  // reserved "revenue" tag
          value: 4  // reserved "value" tag
        };

        // Track event with user attributes and event tags
        optimizely.track(eventKey, userId, attributes, eventTags);
  javascript:
      lang: javascript
      request: |
        var eventKey = "my_conversion";
        var userId = "user123";

        var attributes = {
          DEVICE: 'iPhone',
          AD_SOURCE: 'my_campaign'
        };

        var eventTags = {
          category: 'shoes',
          purchasePrice: 64.32,
          revenue: 6432,  // reserved "revenue" tag
          value: 4  // reserved "value" tag
        };

        // Track event with user attributes and event tags
        optimizely.track(eventKey, userId, attributes, eventTags);
  objectivec:
      lang: objectivec
      request: |
        NSDictionary *attributes = @{@"device" : @"iPhone", @"ad_source" : @"my_campaign"};

        NSDictionary *eventTags = @{
          @"purchasePrice" : @64.32,
          @"category" : @"shoes",
          @"revenue": @6432  // reserved "revenue" tag
        };

        // Track event with user attributes and event tags
        [optimizely track:@"my_conversion"
                   userId:@"user123"
               attributes:attributes
               eventTags:eventTags];

  swift:
      lang: swift
      request: |
        let attributes = ["device" : "iPhone", "ad_source" : "my_campaign"]

        var eventTags = Dictionary<String, Any>()
        eventTags["purchasePrice"] = 64.32
        eventTags["category"] = "shoes"
        eventTags["revenue"] = 6432  // reserved "revenue" tag
        eventTags["value"] = 4 // reserved "value" tag

        // Track event with user attributes and event tags
        optimizely?.track("my_conversion",
                          userId:"user123",
                          attributes:attributes,
                          eventTags:eventTags)
  android:
      lang: java
      request: |
        String eventKey = "my_conversion";
        String userId = "user123";

        Map<String, String> attributes = new HashMap<String, String>();
        attributes.put("DEVICE", "iPhone");
        attributes.put("AD_SOURCE", "my_campaign");

        Map<String, Object> eventTags = new HashMap<String, Object>();
        eventTags.put("purchasePrice", 64.32f);
        eventTags.put("category", "shoes");

        // reserved "revenue" tag
        eventTags.put("revenue", 6432);

        // reserved "value" tag
        eventTags.put("value", 4);

        Optimizely optimizelyClient = optimizelyManager.getOptimizely();

        // Track event with user attributes and event tags
        optimizelyClient.track(eventKey, userId, attributes, eventTags);
---

*Event tags* are contextual metadata about conversion events that you track.

You can use event tags to attach any key/value data you wish to events. For example, for a product purchase event you may want to attach a product SKU, product category, order ID, and purchase amount. Event tags can be strings, integers, floating point numbers, or Boolean values.

You can include event tags with an optional argument in `track` as shown on the right.

Event tags are distinct from [user attributes](#targeting) which should be reserved for user-level targeting and segmentation. Event tags do not affect audiences or the Optimizely results page, and do not need to be registered in the Optimizely web interface.

Event tags are accessible via [raw data export](/x/events/export/index.html) in the `event_features` column. You should include any event tags you need to reconcile your conversion event data with your data warehouse.



#### Reserved tags

The following tag keys are reserved and will be included in their corresponding fields in the Optimizely event API payload. They're bundled into event tags for your convenience. Use them if you'd like to benefit from specific reporting features such as revenue metrics or numeric metrics.

* `revenue` - An integer value that is used to track the Revenue metric for your experiments, aggregated across all conversion events. Revenue is recorded in cents: if you'd like to record a revenue value of $64.32 use `6432`. Any event you want to track revenue for will need to be added as a Metric to your experiment. You can use the Overall Revenue Metric to aggregate multiple Metrics tracking separate revenue events. The Overall Revenue Event won't track any revenue unless there are other Metrics in your experiment tracking an increase or decrease in total revenue – it won't work on its own.

* `value` - A floating point value that is used to track a custom value for your experiments.

</br>
