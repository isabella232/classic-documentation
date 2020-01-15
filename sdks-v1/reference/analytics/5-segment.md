---
template: multi-example
title: Segment
anchor: analytics-segment
code_examples:
  python:
    lang: python
  java:
    lang: java
  csharp:
    lang: csharp
  ruby:
    lang: ruby
  javascript:
    lang: javascript
    request: |
      <html>
        <head>
          <script type="text/javascript">
            var userId = 'user~1';

            // Load the Segment Lib

            // Initialize Segment
            analytics.load("YOUR_KEY_HERE");
            analytics.page();

            // Identify user + add user attributes/traits
            // These user traits are passed along to Optimizely as user attributes
            analytics.identify(userId, {
              age: 24,
              language: 'yes',
            });

            // Initialize Optimizely and make sure it is appended to the global variable that the Segment integration can use (window.optimizelyClientInstance)
            var datafile = {}; // YOUR DATAFILE HERE
            var optimizelyClientInstance = window.optimizelyClient.createInstance({ datafile: datafile });


            // Metadata associated with the event
            // These are passed along to Optimizely as eventTags
            var eventProperties = { 'category': 'shoes', 'purchasePrice': 42 };
            analytics.track("page_loaded", eventProperties);

            // If you wish to override the userId and user attributes set during the `.identify` call or you don't want to use the `.identify` call you can pass the userId and userAttributes as options to the track call.

            var options = { 'Optimizely': { 'userId': userId, 'attributes': userAttributes } }
            analytics.track("page_loaded", eventProperties, options);
          </script>
        </head>
      </html>
  node:
    lang: javascript
  php:
    lang: php
  objectivec:
    lang: objectivec
    request: |
        #import <Analytics/SEGAnalytics.h>
        [optimizely.notificationCenter addActivateNotificationListener:^(OPTLYExperiment *experiment, NSString *userId, NSDictionary<NSString *,NSString *> *attributes, OPTLYVariation *variation, NSDictionary<NSString *,NSString *> *event) {
               NSDictionary *properties = @{
                   @"experimentId" : [experiment experimentId],
                   @"experimentName" : [experiment experimentKey],
                   @"variationId" : [variation variationId],
                   @"variationName" : [variation variationKey]
                   };
               [[SEGAnalytics sharedAnalytics] track:@"Experiment Viewed" properties:properties];
        }];
  swift:
    lang: swift
    request: |
      import Analytics

      let activateNotificationId = optimizely?.notificationCenter?.addActivateNotificationListener({ (experiment, userId, attributes, variation, logEvent) in
              let properties = ["experimentId": experiment.experimentId as Any,
                        "experimentName": experiment.experimentKey as Any,
                        "variationId": variation.variationId as Any,
                        "variationName": variation.variationKey as Any]
          
              SEGAnalytics.shared().track("Experiment Viewed", properties: properties)
      })
  android:
    lang: java
    request: |
      import com.segment.analytics.Analytics;
      import com.segment.analytics.Properties;


      OptimizelyClient optimizelyClient = optimizelyManager.getOptimizely();
      // Add a Activate listener
      int notificationId = optimizelyClient.getNotificationCenter().addNotificationListener(NotificationCenter.NotificationType.Activate, new ActivateNotificationListener() {
        @Override
        public void onActivate(Experiment experiment,
                          String userId,
                          Map<String, String> attributes,
                          Variation variation) {

          String experimentId = experiment.getId();
          String experimentKey = experiment.getKey();
          String variationId = variation.getId();
          String variationKey = variation.getKey();

          Properties properties = new Properties();
          properties.put("experimentId", experimentId);
          properties.put("experimentName", experimentKey);
          properties.put("variationId", variationId);
          properties.put("variationName", variationKey);

          Analytics.with(getApplicationContext()).track("Experiment Viewed", properties);

        }
      });
      
---

<div class="hidden" data-language-content="language" data-language="python">
Please refer to the <a href="https://segment.com/docs/integrations/optimizely/#optimizely-x-fullstack" target="_blank">Optimizely X Fullstack guide</a> for instructions on integrating our JavaScript SDK with your Segment analytics.
</div>

<div class="hidden" data-language-content="language" data-language="java">
Please refer to the <a href="https://segment.com/docs/integrations/optimizely/#optimizely-x-fullstack" target="_blank">Optimizely X Fullstack guide</a> for instructions on integrating our JavaScript SDK with your Segment analytics.
</div>

<div class="hidden" data-language-content="language" data-language="csharp">
Please refer to the <a href="https://segment.com/docs/integrations/optimizely/#optimizely-x-fullstack" target="_blank">Optimizely X Fullstack guide</a> for instructions on integrating our JavaScript SDK with your Segment analytics.
</div>

<div class="hidden" data-language-content="language" data-language="ruby">
Please refer to the <a href="https://segment.com/docs/integrations/optimizely/#optimizely-x-fullstack" target="_blank">Optimizely X Fullstack guide</a> for instructions on integrating our JavaScript SDK with your Segment analytics.
</div>

<div class="hidden" data-language-content="language" data-language="javascript">
Please refer to the <a href="https://segment.com/docs/integrations/optimizely/#optimizely-x-fullstack" target="_blank">Optimizely X Fullstack guide</a> for instructions on integrating our JavaScript SDK with your Segment analytics.
</div>

<div class="hidden" data-language-content="language" data-language="node">
Please refer to the <a href="https://segment.com/docs/integrations/optimizely/#optimizely-x-fullstack" target="_blank">Optimizely X Fullstack guide</a> for instructions on integrating our JavaScript SDK with your Segment analytics.
</div>

<div class="hidden" data-language-content="language" data-language="php">
Please refer to the <a href="https://segment.com/docs/integrations/optimizely/#optimizely-x-fullstack" target="_blank">Optimizely X Fullstack guide</a> for instructions on integrating our JavaScript SDK with your Segment analytics.
</div>

<div class="hidden" data-language-content="language" data-language="objectivec">
<div></div>
<p>Read the Segment Getting Started Guide if you're just getting started.
https://segment.com/docs/</p>

<p>Segment has a semantic event which can be used for tracking A/B test variations for users.
https://segment.com/docs/spec/ab-testing/</p>

<p>In the example code, we add an activate listener block callback. In the callback, we send Segment's A/B event.</p>
</div>

<div class="hidden" data-language-content="language" data-language="swift">
<div></div>
<p>Read the Segment Getting Started Guide if you're just getting started.
https://segment.com/docs/</p>

<p>Segment has a semantic event which can be used for tracking A/B test variations for users.
https://segment.com/docs/spec/ab-testing/</p>

<p>In the example code, we add an activate listener closure callback. In the callback, we send Segment's A/B event.</p>
</div>

<div class="hidden" data-language-content="language" data-language="android">
<div></div>
<p>Read the Segment Getting Started Guide if you're just getting started.
https://segment.com/docs/</p>

<p>Segment has a semantic event which can be used for tracking A/B test variations for users.
https://segment.com/docs/spec/ab-testing/</p>

<p>In the example code, we add an activate callback via the `ActivateNotificationListener`. In the callback, we send Segment's A/B event.</p>
</div>

<br>
