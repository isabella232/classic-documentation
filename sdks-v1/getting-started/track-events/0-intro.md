---
template: multi-example
title: "8. Track events"
anchor: track-events

---

You'll want to track your experiment's performance against metrics you've defined. Earlier, we set up one metric called `my_conversion`. The SDK’s `.track()` function will inform Optimizely of this event using the user ID and the corresponding event key. The code below will track a conversion event:

<div style="display: none" class="sdk-python">

<div></div>

```python
optimizely_client.track('my_conversion', 'joe')
```

</div>

<div style="display: none" class="sdk-java">

<div></div>

```java
optimizely.track("my_conversion", "joe")
```

</div>

<div style="display: none" class="sdk-csharp">

<div></div>

```csharp
OptimizelyClient.Track("my_conversion", "joe")
```

</div>

<div style="display: none" class="sdk-ruby">

<div></div>

```ruby
optimizely_client.track('my_conversion', 'joe')
```

</div>

<div style="display: none" class="sdk-node">

<div></div>

```javascript
optimizely.track('my_conversion', 'joe');
```

</div>

<div style="display: none" class="sdk-php">

<div></div>

```php
$optimizelyClient->track('my_conversion', 'joe');
```

</div>

<div style="display: none" class="sdk-javascript">

<div></div>

```javascript
optimizelyClientInstance.track('my_conversion', 'joe');
```

</div>

<div style="display: none" class="sdk-android">

<div></div>

This goes in the `onStart` function under "Track code".

```java
optimizely.track("my_conversion", "currentUser");
```

Full code [snippet](https://gist.github.com/mauerbac/64d2c638b72e38de603f511601dd2b91)
</div>

<div style="display: none" class="sdk-objectivec">

<div></div>

_Objective-C:_
```objectivec
[client track:@"my_conversion" userId:@"currentUser"];
```
Full code [snippet](https://gist.github.com/mauerbac/8243dce3884b460271a0ca9673f84fae)

_Swift:_
```swift
client?.track("my_conversion", userId: "currentUser")
```
Full code [snippet](https://gist.github.com/mauerbac/4dd686a390b6cb305a358844568c0eb4)

</div>


