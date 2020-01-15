---
template: multi-example
title: "> Create an event"
anchor: create-event

---

We'll measure the success of our test by creating an [_event_](https://help.optimizely.com/Measure_success%3A_Track_visitor_behaviors/Events%3A_Tracking_clicks%2C_pageviews%2C_and_other_visitor_actions) and a tracking it in a [_metric_](https://help.optimizely.com/Measure_success%3A_Track_visitor_behaviors/Create_a_metric_in_Optimizely_X). Every Optimizely experiment needs at least one metric.

Under Metrics, click _Create New Event_ and give it a unique _event key_ on the following screen.

<img src="/assets/img/create_new_event.png" alt="Click 'Create New Event'" class="screenshot">

We're using the example event key `my_conversion`. Note that Optimizely generates the <span class="sdk-platform"></span> event tracking code that you can use to report each event from within your code.

<img src="/assets/img/set_event_key.png" alt="Give your new event a unique 'event key'" class="screenshot">

<div style="display: none" class="sdk-objectivec">
<img src="/assets/img/event_tracking_code_ios.png" alt="Event-tracking code sample for iOS projects" class="screenshot">
</div>

<div style="display: none" class="sdk-android">
<img src="/assets/img/event_tracking_code_android.png" alt="Event-tracking code sample for Android projects" class="screenshot">
</div>

Click _Create Event_ when you are satisfied. You should then see your newly-created event key under Events.

<img src="/assets/img/create_event_button.png" alt="Click the Create Event button" class="screenshot">