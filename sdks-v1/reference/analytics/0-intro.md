---
template: multi-example
title: Integrations
anchor: analytics
---

You can add Optimizely experiment information to third-party analytics platforms using [Notification Listeners](#notification-listener). Measure the impact of your experiments by segmenting your analytics reports using Optimizely experiment and variation keys or IDs.

Below you will find suggested implementations for some common analytics platforms including [Amplitude](#analytics-amplitude), [Google Analytics](#analytics-google), [Localytics](#analytics-localytics), [Mixpanel](#analytics-mixpanel), and [Segment](#analytics-segment). You can use them as presented or adapt them to meet your specific needs.

Notification Listeners also allow for the flexibility to implement an integration with a platform that is not listed here.


#### Experiment and Variation Identifiers

Experiment keys are unique within an Optimizely project, and variation keys are unique within an experiment. However, experiment and variation keys are not guaranteed to be universally unique since they are user generated. This may become a problem in your analytics reports if you use the same key in multiple Optimizely projects or rename your keys.

For human friendly strings when absolute uniqueness is not required, use keys. If you need to uniquely identify experiments and variations in a way that will not change when you rename keys, you can use the automatically generated IDs.

<div class="hidden" data-language-content="language" data-language="python">
</div>

<div class="hidden" data-language-content="language" data-language="java">
<p>
Keys can be accessed on `Experiment` and `Variation` objects using `getKey()`, and IDs can be accessed using `getId()`.
</p>
</div>

<div class="hidden" data-language-content="language" data-language="csharp">
</div>

<div class="hidden" data-language-content="language" data-language="ruby">
</div>

<div class="hidden" data-language-content="language" data-language="javascript">
</div>

<div class="hidden" data-language-content="language" data-language="node">
</div>

<div class="hidden" data-language-content="language" data-language="php">
</div>

<div class="hidden" data-language-content="language" data-language="objectivec">
<div></div>

Keys and IDs can be accessed on `OPTLYExperiment` objects using `experimentKey` and `experimentId` respectively, and likewise keys and IDs can be accessed on `OPTLYVariation` objects using `variationKey` and `variationId`.
</div>

<div class="hidden" data-language-content="language" data-language="swift">
<div></div>

Keys and IDs can be accessed on `OPTLYExperiment` objects using `experimentKey` and `experimentId` respectively, and likewise keys and IDs can be accessed on `OPTLYVariation` objects using `variationKey` and `variationId`.
</div>

<div class="hidden" data-language-content="language" data-language="android">
<div></div>

Keys can be accessed on `Experiment` and `Variation` objects using `getKey()`, and IDs can be accessed using `getId()`.
</div>

<br>
