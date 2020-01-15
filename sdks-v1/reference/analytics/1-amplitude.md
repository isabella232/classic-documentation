---
template: multi-example
title: Amplitude
anchor: analytics-amplitude
code_examples:
  android:
    lang: java
    request: |
      import com.amplitude.api.Amplitude;
      import com.amplitude.api.AmplitudeClient;
      import com.amplitude.api.Identify;
      import com.optimizely.ab.config.Experiment;
      import com.optimizely.ab.config.Variation;
      import com.optimizely.ab.notification.ActivateNotificationListener;
      import com.optimizely.ab.notification.NotificationCenter;

      OptimizelyClient optimizelyClient = optimizelyManager.getOptimizely();
      // Add a Activate listener
      int notificationId = optimizelyClient.getNotificationCenter().addNotificationListener(NotificationCenter.NotificationType.Activate, new ActivateNotificationListener() {
            @Override
            public void onActivate(@Nonnull Experiment experiment, @Nonnull String userId, @Nonnull Map<String, String> attributes, @Nonnull Variation variation, @Nonnull LogEvent event) {

          String experimentKey = experiment.getKey();
          String variationKey = variation.getKey();

          // Set "user property" for the user
          Identify identify = new Identify().set(
              "[Optimizely] " + experimentKey, variationKey);
          AmplitudeClient amplitudeClient = Amplitude.getInstance();
          amplitudeClient.identify(identify);

          // Track impression event (optional)
          amplitudeClient.logEvent(
              "[Optimizely] " + experimentKey + " - " + variationKey);
        }
      });

  javascript:
    lang: javascript
    request: |
        function onActivate(activateObject) {
          var experimentKey = activateObject.experiment['key'];
          var variationKey = activateObject.variation['key'];
          // Set "user property" for the user
          var identify = new amplitude.Identify().set(
              "[Optimizely] " + experimentKey, variationKey);
          amplitude.identify(identify);

          // Track impression event (optional)
          amplitude.logEvent(
              "[Optimizely] " + experimentKey + " - " + variationKey);
        }

        // Add a ACTIVATE notification listener
        var activateId = optimizelyClientInstance.notificationCenter.addNotificationListener(
                  optimizelyEnums.NOTIFICATION_TYPES.ACTIVATE,
                  onActivate
            );

  objectivec:
    lang: objectivec
    request: |
      #import "Amplitude.h"
      #import "AMPIdentify.h"

      [optimizely.notificationCenter addActivateNotificationListener:^(OPTLYExperiment *experiment, NSString *userId, NSDictionary<NSString *,NSString *> *attributes, OPTLYVariation *variation, NSDictionary<NSString *,NSString *> *event) {
                  NSString *propertyKey
                      = [NSString stringWithFormat:@"[Optimizely] %@",
                          experiment.experimentKey];
                  AMPIdentify *identify
                      = [[AMPIdentify identify] set:propertyKey
                                              value:variation.variationKey];
                  [[Amplitude instance] identify:identify];

                  // Track impression event (optional)
                  NSString *eventIdentifier
                      = [NSString stringWithFormat:@"[Optimizely] %@ - %@",
                          experiment.experimentKey,
                          variation.variationKey];
                  [[Amplitude instance] logEvent:eventIdentifier];
                }];

  swift:
    lang: swift
    request: |
      import Amplitude_iOS
      let activateNotificationId = optimizely?.notificationCenter?.addActivateNotificationListener({ (experiment, userId, attributes, variation, logEvent) in
            // Set "user property" for the user
            let propertyKey : String! = "[Optimizely] " + experiment.experimentKey
            let identify : AMPIdentify = AMPIdentify()
            identify.set(propertyKey, value:variation.variationKey as NSObject!)

            // Track impression event (optional)
            let eventIdentifier : String = "[Optimizely] "
                + experiment.experimentKey + " - " + variation.variationKey
            Amplitude.instance().logEvent(eventIdentifier)
          }
        }
      })

---

<div class="hidden" data-language-content="language" data-language="android">
<div></div>

Read the [Amplitude Quick Start Guide](https://amplitude.zendesk.com/hc/en-us/sections/201146908-Amplitude-Quick-Start-Guide) if you're getting started.

Amplitude features two types of properties that can be used to enrich and segment their reports with Optimizely experiment information: [*event properties*](https://amplitude.zendesk.com/hc/en-us/articles/207108327#event-properties) and [*user properties*](https://amplitude.zendesk.com/hc/en-us/articles/207108327#user-properties).

* User properties describe a user across all logged events. After you set a user property, Amplitude applies it in their backend to subsequent recorded events until someone changes the property.

* Event properties describe a single event, so they must be added to each logged event. The Amplitude SDK and backend do not automatically add event properties to future events. For this reason, user properties are simpler to work with than event properties are.

The example code demonstrates the `ActivateNotificationListerner.onActivate` callback. In the callback, the code shows Amplitude's `Identify` interface setting a new user property, which includes the experiment key and variation key. The user property should immediately propagate to the Amplitude backend and be visible in their dashboard. To compare the performances of variations in an experiment, create a new segment for each variation.

Optionally, you can log an impression event in the callback to signify that the Optimizely experiment was activated for the current user. You can later use this event (or another event you may already be tracking) to calculate a conversion rate.

#### Compare results

When comparing numbers between Optimizely and Amplitude results, remember to apply a date filter in Amplitude that corresponds with the dates your Optimizely experiment was running. Note: user properties remain set in Amplitude, regardless of whether your Optimizely experiment is running.

#### Alternative solution for Optimizely Enterprise accounts 

If you have an Optimizely Enterprise plan, you alternatively can use Amplitude's [Behavioral Cohort Analysis](https://amplitude.com/behavioral-cohorts), which can segment on the impression event tracked in the example code.
</div>


<div class="hidden visible" data-language-content="language" data-language="csharp">
<div class="unsupported">Optimizely does not have a suggested solution for integrating Amplitude with the <span class="sdk-platform"></span> SDK.</div>
</div>


<div class="hidden visible" data-language-content="language" data-language="java">
<div class="unsupported">Optimizely does not have a suggested solution for integrating Amplitude with the <span class="sdk-platform"></span> SDK.</div>
</div>


<div class="hidden" data-language-content="language" data-language="javascript">
<div></div>

Read the [Amplitude Quick Start Guide](https://amplitude.zendesk.com/hc/en-us/sections/201146908-Amplitude-Quick-Start-Guide) if you're getting started.

Amplitude features two types of properties that can be used to enrich and segment their reports with Optimizely experiment information: [*event properties*](https://amplitude.zendesk.com/hc/en-us/articles/207108327#event-properties) and [*user properties*](https://amplitude.zendesk.com/hc/en-us/articles/207108327#user-properties).

* User properties describe a user across all logged events. After you set a user property, Amplitude applies it in their backend to subsequent recorded events until someone changes the property.

* Event properties describe a single event, so they must be added to each logged event. The Amplitude SDK and backend do not automatically add event properties to future events. For this reason, user properties are simpler to work with than event properties are.

The example code demonstrates an `onActivate` callback. In the callback, the code shows Amplitude's `Identify` interface setting a new user property, which includes the experiment key and variation key. The user property should immediately propagate to the Amplitude backend and be visible in its dashboard. To compare the performances of variations in an experiment, create a new segment for each variation.

Optionally, you can log an impression event in the callback to signify that the Optimizely experiment was activated for the current user. You can later use this event (or another event you may already be tracking) to calculate a conversion rate.

#### Compare results

When comparing numbers between Optimizely and Amplitude results, remember to apply a date filter in Amplitude that corresponds with the dates your Optimizely experiment was running. Note: user properties remain set in Amplitude, regardless of whether your Optimizely experiment is running.

#### Alternative solution for Optimizely Enterprise accounts

If you have an Optimizely Enterprise plan, you alternatively can use Amplitude's [Behavioral Cohort Analysis](https://amplitude.com/behavioral-cohorts), which can segment on the impression event tracked in the example code.

</div>


<div class="hidden visible" data-language-content="language" data-language="node">
<div class="unsupported">Optimizely does not have a suggested solution for integrating Amplitude with the <span class="sdk-platform"></span> SDK.</div>
</div>


<div class="hidden" data-language-content="language" data-language="objectivec">
<div></div>

Read the [Amplitude Quick Start Guide](https://amplitude.zendesk.com/hc/en-us/sections/201146908-Amplitude-Quick-Start-Guide) if you're just getting started.

Amplitude features two types of properties that can be used to enrich and segment their reports with Optimizely experiment information: [*event properties*](https://amplitude.zendesk.com/hc/en-us/articles/207108327#event-properties) and [*user properties*](https://amplitude.zendesk.com/hc/en-us/articles/207108327#user-properties).

* User properties describe a user across all logged events. After you set a user property, Amplitude applies it in their backend to subsequent recorded events until someone changes the property.

* Event properties describe a single event, so they must be added to each logged event. The Amplitude SDK and backend do not automatically add event properties to future events. For this reason, user properties are simpler to work with than event properties are.

The example code demonstrates an activate callback. In the callback, the code shows Amplitude's `AMPIdentify` interface setting a new user property, which includes the experiment key and variation key. The user property should immediately propagate to the Amplitude backend and be visible in its dashboard. To compare the performances of variations in an experiment, create a new segment for each variation.

Optionally, you can log an impression event in the callback to signify that the Optimizely experiment was activated for the current user. You can later use this event (or another event you may already be tracking) to calculate a conversion rate.

#### Compare Results

When comparing numbers between Optimizely and Amplitude results, remember to apply a date filter in Amplitude that corresponds with the dates your Optimizely experiment was running. Note: user properties remain set in Amplitude, regardless of whether your Optimizely experiment is running.

#### Alternative Solution

If you have an Optimizely Enterprise plan, you alternatively can use Amplitude's [Behavioral Cohort Analysis](https://amplitude.com/behavioral-cohorts), which can segment on the impression event tracked in the example code.
</div>


<div class="hidden visible" data-language-content="language" data-language="php">
<div class="unsupported">Optimizely does not have a suggested solution for integrating Amplitude with the <span class="sdk-platform"></span> SDK.</div>
</div>


<div class="hidden visible" data-language-content="language" data-language="python">
<div class="unsupported">Optimizely does not have a suggested solution for integrating Amplitude with the <span class="sdk-platform"></span> SDK.</div>
</div>


<div class="hidden visible" data-language-content="language" data-language="ruby">
<div class="unsupported">Optimizely does not have a suggested solution for integrating Amplitude with the <span class="sdk-platform"></span> SDK.</div>
</div>


<div class="hidden" data-language-content="language" data-language="swift">
<div></div>

Read the [Amplitude Quick Start Guide](https://amplitude.zendesk.com/hc/en-us/sections/201146908-Amplitude-Quick-Start-Guide) if you're just getting started.

Amplitude features two types of properties that can be used to enrich and segment their reports with Optimizely experiment information: [*event properties*](https://amplitude.zendesk.com/hc/en-us/articles/207108327#event-properties) and [*user properties*](https://amplitude.zendesk.com/hc/en-us/articles/207108327#user-properties).

* User properties describe a user across all logged events. After you set a user property, Amplitude applies it in their backend to subsequent recorded events until someone changes the property.

* Event properties describe a single event, so they must be added to each logged event. The Amplitude SDK and backend do not automatically add event properties to future events. For this reason, user properties are simpler to work with than event properties are.

The example code demonstrates an activate callback. In the callback, the code shows Amplitude's `AMPIdentify` interface setting a new user property, which includes the experiment key and variation key. The user property should immediately propagate to the Amplitude backend and be visible in their dashboard. To compare the performances of variations in an experiment, create a new segment for each variation.

Optionally, you can log an impression event in the callback to signify that the Optimizely experiment was activated for the current user. You can later use this event (or another event you may already be tracking) to calculate a conversion rate.

#### Compare results

When comparing numbers between Optimizely and Amplitude results, remember to apply a date filter in Amplitude that corresponds with the dates your Optimizely experiment was running. Note: user properties remain set in Amplitude, regardless of whether your Optimizely experiment is running.

#### Alternative solution for Optimizely Enterprise accounts

If you have an Optimizely Enterprise plan, you alternatively can use Amplitude's [Behavioral Cohort Analysis](https://amplitude.com/behavioral-cohorts), which can segment on the impression event tracked in the example code.
</div>


<br>
