---
template: multi-example
title: Mixpanel
anchor: analytics-mixpanel
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
  node:
    lang: javascript
  php:
    lang: php
  objectivec:
    lang: objectivec
    request: |
      #import "Mixpanel/Mixpanel.h"

      [optimizely.notificationCenter addActivateNotificationListener:^(OPTLYExperiment *experiment, NSString *userId, NSDictionary<NSString *,NSString *> *attributes, OPTLYVariation *variation, NSDictionary<NSString *,NSString *> *event) {
                    // Mixpanel instance
                    Mixpanel *mixpanel = [Mixpanel sharedInstance];

                    NSString *propertyKey
                        = [NSString stringWithFormat:@"[Optimizely] %@",
                            experiment.experimentKey];
                    [mixpanel
                      registerSuperProperties:@{propertyKey: variation.variationKey}];

                    // Set "People property" for the user
                    [mixpanel.people set:@{propertyKey: variation.variationKey}];

                    // Track impression event (optional)
                    NSString *eventIdentifier
                        = [NSString stringWithFormat:@"[Optimizely] %@ - %@",
                            experiment.experimentKey,
                            variation.variationKey];
                    [mixpanel track:eventIdentifier];
                }];
  swift:
    lang: swift
    request: |
      import Mixpanel

      optimizely?.notificationCenter?.addActivateNotificationListener({ (experiment, userId, attributes, variation, logEvent) in
            // Mixpanel instance
            let mixpanel : MixpanelInstance = Mixpanel.mainInstance()

            // "Super property" will be sent with all future track calls
            let propertyKey : String! = "[Optimizely] " + experiment.experimentKey
            mixpanel.registerSuperProperties([propertyKey: variation.variationKey])

            // Set "People property" for the user
            mixpanel.people.set(property: propertyKey, to: variation.variationKey)

            // Track impression event (optional)
            let eventIdentifier : String = "[Optimizely] "
                + experiment.experimentKey + " - " + variation.variationKey
            mixpanel.track(event:eventIdentifier)
      })
  android:
    lang: java
    request: |
      import android.util.Log;
      import com.mixpanel.android.mpmetrics.MixpanelAPI;
      import com.optimizely.ab.config.Experiment;
      import com.optimizely.ab.config.Variation;
      import com.optimizely.ab.notification.NotificationListener;
      import org.json.JSONException;
      import org.json.JSONObject;

      optimizelyManager.getOptimizely().getNotificationCenter().addNotificationListener(NotificationCenter.NotificationType.Activate, new ActivateNotificationListener() {
          @Override
          public void onActivate(@Nonnull Experiment experiment, @Nonnull String userId, @Nonnull Map<String, String> attributes, @Nonnull Variation variation, @Nonnull LogEvent event) {
          String experimentKey = experiment.getKey();
          String variationKey = variation.getKey();

          // Mixpanel instance
          String projectToken = YOUR_PROJECT_TOKEN;
          MixpanelAPI mixpanel = MixpanelAPI.getInstance(this, projectToken);

          try {
            // "Super property" will be sent with all future track calls
            JSONObject props = new JSONObject();
            props.put("[Optimizely] " + experimentKey, variationKey);
            mixpanel.registerSuperProperties(props);
          } catch (JSONException e) {
            Log.e("MYAPP", "Unable to add properties to JSONObject", e);
          }

          // Set "People property" for the user
          mixpanel.getPeople().set(
              "[Optimizely] " + experimentKey, variationKey);

          // Track impression event (optional)
          mixpanel.track(
              "[Optimizely] " + experimentKey + " - " + variationKey);
        }
      });

---

<div class="hidden" data-language-content="language" data-language="python">
<div></div>
We currently do not have a suggested solution for Python.
</div>

<div class="hidden" data-language-content="language" data-language="java">
<div></div>
We currently do not have a suggested solution for Java.
</div>

<div class="hidden" data-language-content="language" data-language="csharp">
<div></div>
We currently do not have a suggested solution for C#.
</div>

<div class="hidden" data-language-content="language" data-language="ruby">
<div></div>
We currently do not have a suggested solution for Ruby.
</div>

<div class="hidden" data-language-content="language" data-language="javascript">
<div></div>
We currently do not have a suggested solution for JavaScript.
</div>

<div class="hidden" data-language-content="language" data-language="node">
<div></div>
We currently do not have a suggested solution for Node.
</div>

<div class="hidden" data-language-content="language" data-language="php">
<div></div>
We currently do not have a suggested solution for PHP.
</div>

<div class="hidden" data-language-content="language" data-language="objectivec">
<div></div>

Read the <a href="https://mixpanel.com/help/reference/ios" target="_blank">Mixpanel Quick Start Guide</a> if you're just getting started.

Mixpanel supports two types of properties that can be used to segment data in their reports: <a href="https://mixpanel.com/help/questions/articles/what-is-the-difference-between-event-properties-super-properties-and-people-properties-and-which-should-i-use" target="_blank">*Super Properties and People Properties*</a>. Each kind of property captures a slightly different aspect of the events and users they describe and differ in the ways they can be used for reporting. For maximum flexibility in reporting, we will use both super properties and people properties like Mixpanel suggests.

In the example code, we add an activate listener block callback. In the callback, we first set the super property and then the people property with Mixpanel.

Next in the callback we can optionally log an impression event that signifies that the Optimizely experiment was activated for the current user. You can later use this event or another event you may already be tracking to calculate a conversion rate.

#### Compare Results

When comparing numbers between Optimizely and Mixpanel results, remember to apply a date filter in Mixpanel to correspond with the dates your Optimizely experiment was running. People properties and super properties will remain set in Mixpanel even after your Optimizely experiment has stopped running.

#### Consistent User Identity

Maintaining a consistent user identity across multiple sessions and devices can help ensure proper reporting. Mixpanel provides some <a href="https://mixpanel.com/help/questions/articles/how-should-i-handle-my-user-identity-with-the-mixpanel-javascript-library" target="_blank">guidelines</a> for their platform.

We recommend using the same user ID with the following methods:
- `[optimizely activate]`
- `[mixpanel createAlias]`
- `[mixpanel identify]`
</div>

<div class="hidden" data-language-content="language" data-language="swift">
<div></div>

Read the <a href="https://mixpanel.com/help/reference/swift" target="_blank">Mixpanel Quick Start Guide</a> if you're just getting started.

Mixpanel supports two types of properties that can be used to segment data in their reports: <a href="https://mixpanel.com/help/questions/articles/what-is-the-difference-between-event-properties-super-properties-and-people-properties-and-which-should-i-use" target="_blank">*Super Properties and People Properties*</a>. Each kind of property captures a slightly different aspect of the events and users they describe and differ in the ways they can be used for reporting. For maximum flexibility in reporting, we will use both super properties and people properties like Mixpanel suggests.

In the example code, we add an activate listener closure callback. In the callback, we first set the super property and then the people property with Mixpanel.

Next in the callback we can optionally log an impression event that signifies that the Optimizely experiment was activated for the current user. You can later use this event or another event you may already be tracking to calculate a conversion rate.

#### Compare Results

When comparing numbers between Optimizely and Mixpanel results, remember to apply a date filter in Mixpanel to correspond with the dates your Optimizely experiment was running. People properties and super properties will remain set in Mixpanel even after your Optimizely experiment has stopped running.

#### Consistent User Identity

Maintaining a consistent user identity across multiple sessions and devices can help ensure proper reporting. Mixpanel provides some <a href="https://mixpanel.com/help/questions/articles/how-should-i-handle-my-user-identity-with-the-mixpanel-javascript-library" target="_blank">guidelines</a> for their platform.

We recommend using the same user ID with the following methods:
- `optimizely.activate()`
- `mixpanel.createAlias()`
- `mixpanel.identify()`
</div>

<div class="hidden" data-language-content="language" data-language="android">
<div></div>

Read the <a href="https://mixpanel.com/help/reference/android" target="_blank">Mixpanel Quick Start Guide</a> if you're just getting started.

Mixpanel supports two types of properties that can be used to segment data in their reports: <a href="https://mixpanel.com/help/questions/articles/what-is-the-difference-between-event-properties-super-properties-and-people-properties-and-which-should-i-use" target="_blank">*Super Properties and People Properties*</a>. Each kind of property captures a slightly different aspect of the events and users they describe and differ in the ways they can be used for reporting. For maximum flexibility in reporting, we will use both super properties and people properties like Mixpanel suggests.

In the example code, we add a notification listener using `ActivateNotificationListener` abstract class callback (we could also use the `ActivateNotificationListenerInterface` or a lambda). In the callback, we first set the super property and then the people property with Mixpanel.

Next in the callback we can optionally log an impression event that signifies that the Optimizely experiment was activated for the current user. You can later use this event or another event you may already be tracking to calculate a conversion rate.

At the end of the example code, we add our listener to the Optimizely SDK.

#### Compare Results

When comparing numbers between Optimizely and Mixpanel results, remember to apply a date filter in Mixpanel to correspond with the dates your Optimizely experiment was running. People properties and super properties will remain set in Mixpanel even after your Optimizely experiment has stopped running.

#### Consistent User Identity

Maintaining a consistent user identity across multiple sessions and devices can help ensure proper reporting. Mixpanel provides some <a href="https://mixpanel.com/help/questions/articles/how-should-i-handle-my-user-identity-with-the-mixpanel-javascript-library" target="_blank">guidelines</a> for their platform.

We recommend using the same user ID with the following methods:
- `optimizelyClient.activate()`
- `mixpanel.alias()`
- `mixpanel.identify()`
</div>

<br>
