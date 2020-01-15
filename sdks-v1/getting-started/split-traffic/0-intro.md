---
template: multi-example
title: "7. Split traffic"
anchor: split-traffic

---

To get statistically-significant results from your experiments, your users need to be _randomly_ assigned to groups (or _buckets_) that determine which of your experiment's variations they are going to see. This act of assigning users to groups is often called *bucketing*.

The Optimizely <span class="sdk-platform"></span> SDK handles user bucketing for you with the `.activate()` function.

When provided with a [user ID](/x/solutions/sdks/faqs/index.html?#user-id), the function returns a [variation key](#create-variation-keys) and reports an [_impression event_ (sometimes called a _decision point_)](https://help.optimizely.com/Analyze_Results/How_Optimizely_counts_conversions) to Optimizely. The user ID can be any string that represents a user.  It can be a UUID from your system, or, if you want to anonymize your users, you can generate a random UUID. Note: the <span class="sdk-platform"></span> SDK does not generate UUIDs.


<div style="display: none" class="sdk-python">

<div></div>

In this example, we are using `.activate()` to bucket two users, "Agatha-71875c482b1b" and "Mahesha-aee098f6454a", into our experiment (`my_experiment`).

```python
variation = optimizely_client.activate('my_experiment', 'Agatha-71875c482b1b')
variation = optimizely_client.activate('my_experiment', 'Mahesha-aee098f6454a')
```

You can print the variation assignment in code to verify bucketing is working as expected:

```python
print variation
```

</div>

<div style="display: none" class="sdk-java">

<div></div>

In this example, we are using `.activate()` to bucket two users, "Agatha-71875c482b1b" and "Mahesha-aee098f6454a", into our experiment (`my_experiment`).

```java
Variation variation = optimizely.activate("my_experiment", "Agatha-71875c482b1b");
Variation variation = optimizely.activate("my_experiment", "Mahesha-aee098f6454a");
```

</div>

<div style="display: none" class="sdk-csharp">

In this example, we are using `.activate()` to bucket two users, "Agatha-71875c482b1b" and "Mahesha-aee098f6454a", into our experiment (`my_experiment`).

<div></div>

```csharp
var variation = Optimizely.Activate("my_experiment", "Agatha-71875c482b1b");
var variation = Optimizely.Activate("my_experiment", "Mahesha-aee098f6454a");
```

</div>



<div style="display: none" class="sdk-ruby">

<div></div>

In this example, we are using `.activate()` to bucket two users, "Agatha-71875c482b1b" and "Mahesha-aee098f6454a", into our experiment (`my_experiment`).

```ruby
variation = optimizely_client.activate('my_experiment', 'Agatha-71875c482b1b')
variation = optimizely_client.activate('my_experiment', 'Mahesha-aee098f6454a')
```

You can print the variation assignment in code to ensure bucketing is working as expected:

```ruby
print variation
```

</div>

<div style="display: none" class="sdk-node">

In this example, we are using `.activate()` to bucket two users, "Agatha-71875c482b1b" and "Mahesha-aee098f6454a", into our experiment (`my_experiment`).

<div></div>

```javascript
var variation1 = optimizely.activate('my_experiment', 'Agatha-71875c482b1b');
var variation2 = optimizely.activate('my_experiment', 'Mahesha-aee098f6454a');
```

You can print the variation assignment in code to ensure bucketing is working:

```javascript
console.log(variation1);
```

</div>

<div style="display: none" class="sdk-javascript">

<div></div>

In this example, we are using `.activate()` to bucket two users, "Agatha-71875c482b1b" and "Mahesha-aee098f6454a", into our experiment (`my_experiment`).

```javascript
var variation1 = optimizelyClientInstance.activate('my_experiment', 'Agatha-71875c482b1b');
var variation2 = optimizelyClientInstance.activate('my_experiment', 'Mahesha-aee098f6454a');
```

You can print the variation assignment in code to ensure bucketing is working:

```javascript
console.log(variation1);
```

</div>

<div style="display: none" class="sdk-php">

<div></div>

In this example, we are using `.activate()` to bucket two users, "Agatha-71875c482b1b" and "Mahesha-aee098f6454a", into our experiment (`my_experiment`).

```php
$variationKey1 = $optimizelyClient->activate('my_experiment', 'Agatha-71875c482b1b');
$variationKey2 = $optimizelyClient->activate('my_experiment', 'Mahesha-aee098f6454a');
```

You can print the variation assignment in code to ensure bucketing is working as expected:

```php
print $variationKey1;
```

</div>

<div style="display: none" class="sdk-android">

<div></div>

This goes in the `onStart` function under "Activate code".

```java
// Logged in user
Variation variation = optimizely.activate("my_experiment", "currentUser");

// Anonymous device id
Variation variation = optimizely.activate("my_experiment", UUID.randomUUID().toString());
```

The Android SDK has "sticky" bucketing enabled by default: Once a user is bucketed into an experiment they will always bucket into that experiment unless your app's storage is cleared.

Full code [snippet](https://gist.github.com/mauerbac/64d2c638b72e38de603f511601dd2b91)
</div>

<div style="display: none" class="sdk-objectivec">

<div></div>

#### A logged-in user

*   Objective-C
    ```objectivec
    OPTLYVariation *variation = [client activate:@"my_experiment" userId:@"currentUser"];
    ``` 
*   Swift
    ```swift
    let variation = client?.activate("my_experiment", userId: "currentUser")
    ```

#### An anonymous device ID

*   Objective-C
    ```objectivec
    OPTLYVariation *variation = [client activate:@"my_experiment" userId:@[[NSUUID UUID] UUIDString]];
    ``` 
*   Swift
    ```swift
    let variation = client?.activate("my_experiment", userId: UUID().uuidString)
    ```


#### Example files

Here are some example files that you can use as a comparison to your own work.

*   [Objective-C example: `AppDelegate.m`](https://gist.github.com/mauerbac/8243dce3884b460271a0ca9673f84fae)
*   [Swift example: `AppDelegate.swift`](https://gist.github.com/mauerbac/4dd686a390b6cb305a358844568c0eb4)

</div>

#### Further reading

*   [Bucket Testing](https://www.optimizely.com/optimization-glossary/bucket-testing/) (Optimization Glossary entry)
*   [Traffic allocation and distribution](https://help.optimizely.com/Target_Your_Visitors/Traffic_allocation_and_distribution) (Knowledge Base article)
*   [How bucketing works in Optimizely's Full Stack/Mobile SDKs](https://help.optimizely.com/Build_Campaigns_and_Experiments/How_bucketing_works_in_Optimizely's_Full_Stack%2F%2FMobile_SDKs) (Knowledge Base article)
*   [Experiment activation](/x/solutions/sdks/reference/index.html#activation) (Developer `.activate()` reference article)