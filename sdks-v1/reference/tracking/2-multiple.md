---
template: multi-example
title: Tracking with other SDKs
anchor: multiple-sdks
---

You can use any of our SDKs to track events, so you can run experiments that span multiple applications, services, or devices. All of our SDKs have the same bucketing and targeting behavior so you'll see the exact same output from experiment activation and tracking, provided you are using the same datafile and user IDs.

For example, if you're running experiments on your server you can activate experiments with our [Python](/x/solutions/sdks/reference/index.html?language=python#tracking), [Java](/x/solutions/sdks/reference/index.html?language=java#tracking), [Ruby](/x/solutions/sdks/reference/index.html?language=ruby#tracking), [C#](/x/solutions/sdks/reference/index.html?language=csharp#tracking), [Node](/x/solutions/sdks/reference/index.html?language=node#tracking), or [PHP](/x/solutions/sdks/reference/index.html?language=php#tracking) SDKs, but track user actions client-side using our [JavaScript](/x/solutions/sdks/reference/index.html?language=javascript#tracking), [Objective-C](/x/solutions/sdks/reference/index.html?language=objectivec#tracking) or [Android](/x/solutions/sdks/reference/index.html?language=android#tracking) SDKs.

If you plan on using multiple SDKs for the same project, make sure that all SDKs are sharing the same datafile and user IDs.

<br>
