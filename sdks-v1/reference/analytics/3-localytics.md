---
template: multi-example
title: Localytics
anchor: analytics-localytics
code_examples:
  android:
    lang: java
    request: |
      import com.localytics.android.Localytics;
      import com.optimizely.ab.bucketing.UserProfile;
      import com.optimizely.ab.notification.NotificationListener;
      import com.optimizely.ab.notification.TrackNotificationListener;
      import java.util.Map;

      optimizelyManager.getOptimizely().getNotificationCenter().addNotificationListener(NotificationCenter.NotificationType.Track, new TrackNotificationListener() {
       @Override
       public void onTrack(@Nonnull String eventKey, @Nonnull String userId, @Nonnull Map<String, String> attributes, @Nonnull Map<String, ?> eventTags, @Nonnull LogEvent event) { 
          // Make a copy of attributes because it could be immutable
          Map<String, String> attr = new HashMap<>(attributes);

          // Retrieve mapping of experiments to variations
          UserProfile userProfile = optimizelyManager.getUserProfile();
          Map<String, Map<String, String>> allRecords =
              userProfile.getAllRecords();

          // Set event attributes
          if (allRecords.containsKey(userId)) {
              Map<String, String> userRecords = allRecords.get(userId);
              for (Map.Entry<String, String> entry : userRecords.entrySet()) {
                  // Mapping of experiment key to variation key
                  attr.put(entry.getKey(), entry.getValue());
              }
          }

          // Tag custom event with attributes
          Localytics.tagEvent("[Optimizely] " + eventKey, attr);
        }
      });

      // Track a conversion event for the provided user
      optimizelyClient.track(eventKey, userId);

  objectivec:
    lang: objectivec
    request: |
      @import Localytics;

      // Add a Track notification listener
      NSInteger trackNotificationId = [optimizely.notificationCenter addTrackNotificationListener:^(NSString * _Nonnull eventKey, NSString * _Nonnull userId, NSDictionary<NSString *,NSString *> * _Nonnull attributes, NSDictionary * _Nonnull eventTags, NSDictionary<NSString *,NSObject *> * _Nonnull event) {
                    // Tag custom event with attributes
                    NSString *eventIdentifier
                        = [NSString stringWithFormat:@"[Optimizely] %@",
                            eventKey]];
                    [Localytics tagEvent:eventIdentifier attributes:attributes];
                }];

      // Track a conversion event for the provided user
      [optimizely track:eventKey userId:userId];

  swift:
    lang: swift
    request: |
      import Localytics

      // Add a track notification listener
      optimizely?.notificationCenter?.addTrackNotificationListener({ (eventKey, userId, attributes, eventTags, event) in
        // Tag custom event with attributes
        let localyticsEventIdentifier : String = "[Optimizely] " + eventKey
        Localytics.tagEvent(localyticsEventIdentifier, attributes)
      })

      optimizely?.track(eventKey, userId)

---

<div class="hidden" data-language-content="language" data-language="android">
<div></div>

Read the [Localytics Getting Started Guide](http://docs.localytics.com/dev/android.html#android) if you're getting started.

Localytics has a couple of ways that can be used to capture Optimizely experiment information. This example demonstrates the use of [*Custom Events with Attributes*](https://docs.localytics.com/dashboard/analytics.html#events) in this suggested integration. For more details on alternative solutions, see below.

This example involves two parts:
- Add a `TrackNotificationListener` listener for `onEvent` to wrap `Localytics.tagEvent()`
- Add `OptimizelyClient.track()` to track conversions

Instead of calling `Localytics.tagEvent()` directly, wrap the calls with `OptimizelyClient.track()` to include bucketing information as event attributes.

The example code demonstrates how to add a track event listener. Each `OptimizelyClient.track()` event tracking retrieves a mapping of experiment key to variation key from `UserProfile`, which records bucketing decisions. Next, the code calls `Localytics.tagEvent()` and includes the bucketing map among the attributes.

The last step is to add `OptimizelyClient.track()` to [track](#tracking) event conversions.

#### Compare Results

When comparing numbers between Optimizely and Localytics results, remember to apply a date filter in Localytics that corresponds with the dates your Optimizely experiment was running. 

#### Consistent User Identity

Maintaining a consistent user identity across multiple sessions and devices can help ensure proper reporting. Localytics provides some [guidelines](https://docs.localytics.com/dev/android.html#identifying-users-android) for their platform.

Optimizely recommends using the same user ID with the following methods:
- `optimizelyClient.activate()`
- `Localytics.setCustomerId()`

#### Alternative Solution

Another solution is to set Localytics' [Custom Dimensions](https://docs.localytics.com/dashboard/analytics.html#dimensions-custom-dimensions) using an `ActivateNotificationListener`. Custom dimensions can be used to segment users without needing to wrap `Localytics.tagEvent()`, but they require configuration in the Localytics dashboard for each Optimizely experiment.
</div>


<div class="hidden visible" data-language-content="language" data-language="csharp">
<div class="unsupported">Optimizely does not have a suggested solution for integrating Localytics with the <span class="sdk-platform"></span> SDK.</div>
</div>


<div class="hidden visible" data-language-content="language" data-language="java">
<div class="unsupported">Optimizely does not have a suggested solution for integrating Localytics with the <span class="sdk-platform"></span> SDK.</div>
</div>


<div class="hidden visible" data-language-content="language" data-language="javascript">
<div class="unsupported">Optimizely does not have a suggested solution for integrating Localytics with the <span class="sdk-platform"></span> SDK.</div>
</div>


<div class="hidden visible" data-language-content="language" data-language="node">
<div class="unsupported">Optimizely does not have a suggested solution for integrating Localytics with the <span class="sdk-platform"></span> SDK.</div>
</div>


<div class="hidden" data-language-content="language" data-language="objectivec">
<div></div>

Read the [Localytics Getting Started Guide](http://docs.localytics.com/dev/ios.html#ios) if you're just getting started.

Localytics has a couple of ways that can be used to capture Optimizely experiment information. This example demonstrates the use of [*Custom Events with Attributes*](https://docs.localytics.com/dashboard/analytics.html#events) in this suggested integration. For more details on alternative solutions, see below.

This example involves two parts:
- Add a track event listener to wrap `[Localytics tagEvent]`
- Add `[optimizely track]` to track conversions

Instead of calling `[Localytics tagEvent]` directly, wrap the calls with `[optimizely track]` to include bucketing information as event attributes.

The example code demonstrates how to add the track notification listener. Each `[optimizely track]` event tracking adds a mapping of experiment key to variation key to the event attributes and passes the mapping to `[Localytics tagEvent]`.

The last step is to add `[optimizely track]` to [track](#tracking) event conversions.

#### Compare Results

When comparing numbers between Optimizely and Localytics results, remember to apply a date filter in Localytics that corresponds with the dates your Optimizely experiment was running. 

#### Consistent User Identity

Maintaining a consistent user identity across multiple sessions and devices can help ensure proper reporting. Localytics provides some [guidelines](https://docs.localytics.com/dev/ios.html#identifying-users-ios) for their platform.

Optimizely recommends using the same user ID with the following methods:
- `[optimizely activate]`
- `[Localytics setCustomerId]`

#### Alternative Solution

Another solution is to set Localytics' [Custom Dimensions](https://docs.localytics.com/dashboard/analytics.html#dimensions-custom-dimensions) using an activate notification listener. Custom dimensions can be used to segment users without needing to wrap `[Localytics tagEvent]`, but they require configuration in the Localytics dashboard for each Optimizely experiment.
</div>


<div class="hidden visible" data-language-content="language" data-language="php">
<div class="unsupported">Optimizely does not have a suggested solution for integrating Localytics with the <span class="sdk-platform"></span> SDK.</div>
</div>


<div class="hidden visible" data-language-content="language" data-language="python">
<div class="unsupported">Optimizely does not have a suggested solution for integrating Localytics with the <span class="sdk-platform"></span> SDK.</div>
</div>


<div class="hidden visible" data-language-content="language" data-language="ruby">
<div class="unsupported">Optimizely does not have a suggested solution for integrating Localytics with the <span class="sdk-platform"></span> SDK.</div>
</div>


<div class="hidden" data-language-content="language" data-language="swift">
<div></div>

Read the [Localytics Getting Started Guide](http://docs.localytics.com/dev/ios.html#ios) if you're just getting started.

Localytics has a couple of ways that can be used to capture Optimizely experiment information. This example demonstrates the use of [*Custom Events with Attributes*](https://docs.localytics.com/dashboard/analytics.html#events) in this suggested integration. For more details on alternative solutions, see below.

This example involves two parts:
- Add a track notification listener to wrap `Localytics.tagEvent()`
- Add `optimizely.track()` to track conversions

Instead of calling `Localytics.tagEvent()` directly, wrap the calls with `optimizely.track()` to include bucketing information as event attributes.

The example code demonstrates how to add a track notification listener. Each time `optimizely.track()` event tracking adds a mapping of experiment key to variation key to the event attributes and pass the mapping to `Localytics.tagEvent()`.

The last step is to add `optimizely.track()` to [track](#tracking) event conversions.

#### Compare Results

When comparing numbers between Optimizely and Localytics results, remember to apply a date filter in Localytics that corresponds with the dates your Optimizely experiment was running. 

#### Consistent User Identity

Maintaining a consistent user identity across multiple sessions and devices can help ensure proper reporting. Localytics provides some [guidelines](https://docs.localytics.com/dev/ios.html#identifying-users-ios) for their platform.

Optimizely recommends using the same user ID with the following methods:
- `optimizely.activate()`
- `Localytics.setCustomerId()`

#### Alternative Solution

Another solution is to set Localytics' [Custom Dimensions](https://docs.localytics.com/dashboard/analytics.html#dimensions-custom-dimensions) using an activate notification listener. Custom dimensions can be used to segment users without needing to wrap `Localytics.tagEvent()` but requires configuration in the Localytics dashboard for each Optimizely experiment.
</div>

<br>
