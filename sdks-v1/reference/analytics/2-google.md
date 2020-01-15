---
template: multi-example
title: Google Analytics
anchor: analytics-google
code_examples:
  android:
    lang: java
    request: |
      import com.google.android.gms.analytics.GoogleAnalytics;
      import com.google.android.gms.analytics.HitBuilders;
      import com.google.android.gms.analytics.Tracker;
      import com.optimizely.ab.config.Experiment;
      import com.optimizely.ab.config.Variation;
      import com.optimizely.ab.notification.ActivateNotificationListener;
      import com.optimizely.ab.notification.NotificationCenter;
      import com.optimizely.ab.notification.TrackNotificationListener;

      // Add a Activate listener
      int notificationId = optimizely.notificationCenter.addNotificationListener(NotificationCenter.NotificationType.Activate, new ActivateNotificationListener() {
         @Override
         public void onActivate(@Nonnull Experiment experiment, @Nonnull String userId, @Nonnull Map<String, String> attributes, @Nonnull Variation variation, @Nonnull LogEvent event) {
          String experimentKey = experiment.getKey();
          String variationKey = variation.getKey();

          // Google Analytics tracker
          SampleApp application = (SampleApp) getApplication();
          mTracker = application.getDefaultTracker();

          // Build and send a non-interaction Event
          mTracker.send(new HitBuilders.EventBuilder()
              .setCategory("Optimizely")
              .setAction("Experiment - " + experimentKey)
              .setLabel("Variation - " + variationKey)
              .setNonInteraction(true)
              .build());
        }
      });

  javascript:
    lang: javascript
    request: |
      const optimizely = require('optimizely-server-sdk');
      const optimizelyEnums = require('optimizely-server-sdk/lib/utils/enums');

      // Assume the Google Analytics is loaded
      // Add a ACTIVATE notification listener
      let activateId = optly.notificationCenter.addNotificationListener(
                optimizelyEnums.NOTIFICATION_TYPES.ACTIVATE,
                function onActivate(activateObject) {
                   let action = "Experiment - " + activateObject.experiment['key'];
                   let label = "Variation - " + activateObject.variation['key'];
                   ga('send', 'event', 'Optimizely', action, label, {
                      nonInteraction: true
                   }); 
      });

  objectivec:
    lang: objectivec
    request: |
      #import <Google/Analytics.h>

      NSInteger activateNotificationId = [optimizely.notificationCenter addActivateNotificationListener:^(OPTLYExperiment *experiment, NSString *userId, NSDictionary<NSString *,NSString *> *attributes, OPTLYVariation *variation, NSDictionary<NSString *,NSString *> *event) {
          // Google Analytics tracker
          id<GAITracker> tracker = [GAI sharedInstance].defaultTracker;

          NSString *action
              = [NSString stringWithFormat:@"Experiment - %@",
                  experiment.experimentKey];
          NSString *label
              = [NSString stringWithFormat:@"Variation - %@",
                  variation.variationKey];
          [tracker send:[[GAIDictionaryBuilder
              createEventWithCategory:@"Optimizely"
                               action:action
                                label:label
                                value:nil] build]];
      }];

  swift:
    lang: swift
    request: |
      // Add an activate notification listener
      let activateNotificationId = optimizely?.notificationCenter?.addActivateNotificationListener({ (experiment, userId, attributes, variation, logEvent) in
          // Google Analytics tracker
          let tracker : GAITracker? = GAI.sharedInstance().defaultTracker

          let action : String = "Experiment - " + experiment.experimentKey
          let label : String = "Variation - " + variation.variationKey

          // Build and send an Event
          let builder = GAIDictionaryBuilder.createEvent(
              withCategory: "Optimizely",
              action: action,
              label: label,
              value: nil).build()
          tracker?.send(builder as [NSObject : AnyObject]!)
      })

---

<div class="hidden" data-language-content="language" data-language="android">
<div></div>

Read the [Google Analytics Android Setup instructions](https://developers.google.com/analytics/devguides/collection/android/v4/) if you're just getting started.

With Google Analytics, you can use [*events*](https://support.google.com/analytics/answer/1033068?hl=en) to track Optimizely experiment activations and build [*segments*](https://support.google.com/analytics/answer/3123951?hl=en) for each variation in an experiment. For more details on alternative solutions, see below.

In the example code, the `ActivateNotificationListern.onActivate` callback is tracking experiment activations. When the callback is called, the code creates and sends an event containing the experiment key and variation key. Because this event should not affect the bounce rate, it is a non-interaction event.

The example code finishes by adding the listener to the Optimizely SDK.

<div class="attention attention--good-news push--bottom push--top">
<div></div>
Read more about [non-interaction events](https://support.google.com/analytics/answer/1033068#NonInteractionEvents) and support for them in the [Google Analytics Android SDK](https://developers.google.com/analytics/devguides/collection/android/v4/events).
</div>

The next step is to [build segments](https://support.google.com/analytics/answer/3124493) for each variation of your experiment. In the segment-builder user interface, look under Advanced and add a new Condition. Select to filter Users by Event Action and Event Label, enter a name for the segment, and save.

Finally, build a report of metrics you are interested in.

#### Compare results

When comparing numbers between Optimizely and Google Analytics results, remember to apply a date filter in Google Analytics to correspond with the dates your Optimizely experiment was running.

#### Alternative solution

Google offers [*custom dimensions*](https://support.google.com/analytics/answer/2709828?hl=en) as another way to "include non-standard data in your reports." Custom dimensions are the replacement for custom variables from older versions of Google Analytics.

Optimizely's suggested integration does not use custom dimensions because free Google Analytics accounts are limited to 20 indices (or slots), and 360 accounts are limited to 200 indices. Because a custom dimension cannot store a value that exceeds 150 bytes, you would need to dedicate an index for each Optimizely experiment. Google recommends against reusing indices; thus, the number of available indicies is the upper limit of Optimizely experiments that you can use custom dimensions to track and segment.
</div>


<div class="hidden visible" data-language-content="language" data-language="csharp">
<div class="unsupported">Optimizely does not have a suggested solution for integrating Google Analytics with the <span class="sdk-platform"></span> SDK.</div>
</div>


<div class="hidden visible" data-language-content="language" data-language="java">
<div class="unsupported">Optimizely does not have a suggested solution for integrating Google Analytics with the <span class="sdk-platform"></span> SDK.</div>
</div>


<div class="hidden" data-language-content="language" data-language="javascript">
<div></div>

Read the [Google Analytics Javascript Setup instructions](https://developers.google.com/analytics/devguides/collection/analyticsjs/) if you're getting started.

With Google Analytics, you can use [*events*](https://support.google.com/analytics/answer/1033068?hl=en) to track Optimizely experiment activations and build [*segments*](https://support.google.com/analytics/answer/3123951?hl=en) for each variation in an experiment. For more details on alternative solutions, see below.

In the example code, we add a `onActivate` callback to track experiment activations. When the callback is called, we create and send an event containing the experiment key and variation key. Since this should not affect the bounce rate, we mark it as a non-interaction event.

<div class="attention attention--good-news push--bottom push--top">
<div></div>
Read more about [non-interaction events](https://support.google.com/analytics/answer/1033068#NonInteractionEvents) and support for them in the [Google Analytics Javascript SDK](https://developers.google.com/analytics/devguides/collection/analyticsjs/events)".
</div>

The next step is to [build segments](https://support.google.com/analytics/answer/3124493) for each variation of your experiment. In the segment-builder user interface, look under Advanced and add a new Condition. Select to filter Users by Event Action and Event Label, enter a name for the segment, and save.

Finally, build a report of metrics you are interested in.

#### Compare results

When comparing numbers between Optimizely and Google Analytics results, remember to apply a date filter in Google Analytics to correspond with the dates your Optimizely experiment was running.

#### Alternative solution

Google offers [*custom dimensions*](https://support.google.com/analytics/answer/2709828?hl=en) as another way to "include non-standard data in your reports." Custom dimensions are the replacement for custom variables from older versions of Google Analytics.

Optimizely's suggested integration does not use custom dimensions because free Google Analytics accounts are limited to 20 indices (or slots), and 360 accounts are limited to 200 indices. Because a custom dimension cannot store a value that exceeds 150 bytes, you would need to dedicate an index for each Optimizely experiment. Google recommends against reusing indices; thus, the number of available indicies is the upper limit of Optimizely experiments that you can use custom dimensions to track and segment.
</div>


<div class="hidden visible" data-language-content="language" data-language="node">
<div class="unsupported">Optimizely does not have a suggested solution for integrating Google Analytics with the <span class="sdk-platform"></span> SDK.</div>
</div>


<div class="hidden" data-language-content="language" data-language="objectivec">
<div></div>

Read the [Google Analytics iOS Setup instructions](https://developers.google.com/analytics/devguides/collection/ios/v3/) if you're just getting started.

With Google Analytics, you can use [*events*](https://support.google.com/analytics/answer/1033068?hl=en) to track Optimizely experiment activations and build [*segments*](https://support.google.com/analytics/answer/3123951?hl=en) for each variation in an experiment. For more details on alternative solutions, see below.

The example code shows how to add an activate listener block to the notification center. When the callback is called, the code creates and sends an event containing the experiment key and variation key.

<div class="attention attention--warning push--bottom">
<div></div>
The [Google Analytics iOS SDK](https://developers.google.com/analytics/devguides/collection/ios/v3/events) does not support [non-interaction events](https://support.google.com/analytics/answer/1033068#NonInteractionEvents) at this time. This may affect your bounce rate.
</div>

The next step is to [build segments](https://support.google.com/analytics/answer/3124493) for each variation of your experiment. In the segment-builder user interface, look under Advanced and add a new Condition. Select to filter Users by Event Action and Event Label, enter a name for the segment, and save.

Finally, build a report of metrics you are interested in.

#### Compare results

When comparing numbers between Optimizely and Google Analytics results, remember to apply a date filter in Google Analytics to correspond with the dates your Optimizely experiment was running.

#### Alternative solution

Google offers [*custom dimensions*](https://support.google.com/analytics/answer/2709828?hl=en) as another way to "include non-standard data in your reports." Custom dimensions are the replacement for custom variables from older versions of Google Analytics.

Optimizely's suggested integration does not use custom dimensions because free Google Analytics accounts are limited to 20 indices (or slots), and 360 accounts are limited to 200 indices. Because a custom dimension cannot store a value that exceeds 150 bytes, you would need to dedicate an index for each Optimizely experiment. Google recommends against reusing indices; thus, the number of available indicies is the upper limit of Optimizely experiments that you can use custom dimensions to track and segment.
</div>


<div class="hidden visible" data-language-content="language" data-language="php">
<div class="unsupported">Optimizely does not have a suggested solution for integrating Google Analytics with the <span class="sdk-platform"></span> SDK.</div>
</div>


<div class="hidden visible" data-language-content="language" data-language="python">
<div class="unsupported">Optimizely does not have a suggested solution for integrating Google Analytics with the <span class="sdk-platform"></span> SDK.</div>
</div>


<div class="hidden visible" data-language-content="language" data-language="ruby">
<div class="unsupported">Optimizely does not have a suggested solution for integrating Google Analytics with the <span class="sdk-platform"></span> SDK.</div>
</div>


<div class="hidden" data-language-content="language" data-language="swift">
<div></div>

Read the [Google Analytics iOS Setup instructions](https://developers.google.com/analytics/devguides/collection/ios/v3/?ver=swift) if you're just getting started.

With Google Analytics, you can use [*events*](https://support.google.com/analytics/answer/1033068?hl=en) to track Optimizely experiment activations and build [*segments*](https://support.google.com/analytics/answer/3123951?hl=en) for each variation in an experiment. For more details on alternative solutions, see below.

The example code shows how to add an activate listener closure to the notification center. When the callback is called, the code creates and sends an event containing the experiment key and variation key.

<div class="attention attention--warning push--bottom">
<div></div>
The [Google Analytics iOS SDK](https://developers.google.com/analytics/devguides/collection/ios/v3/events) does not support [non-interaction events](https://support.google.com/analytics/answer/1033068#NonInteractionEvents) at this time. This may affect your bounce rate.
</div>

The next step is to [build segments](https://support.google.com/analytics/answer/3124493) for each variation of your experiment. In the segment-builder user interface, look under Advanced and add a new Condition. Select to filter Users by Event Action and Event Label, enter a name for the segment, and save.

Finally, build a report of metrics you are interested in.

#### Compare results

When comparing numbers between Optimizely and Google Analytics results, remember to apply a date filter in Google Analytics to correspond with the dates your Optimizely experiment was running.

#### Alternative solution

Google offers [*custom dimensions*](https://support.google.com/analytics/answer/2709828?hl=en) as another way to "include non-standard data in your reports." Custom dimensions are the replacement for custom variables from older versions of Google Analytics.

Optimizely's suggested integration does not use custom dimensions because free Google Analytics accounts are limited to 20 indices (or slots), and 360 accounts are limited to 200 indices. Because a custom dimension cannot store a value that exceeds 150 bytes, you would need to dedicate an index for each Optimizely experiment. Google recommends against reusing indices; thus, the number of available indicies is the upper limit of Optimizely experiments that you can use custom dimensions to track and segment.
</div>

<br>
