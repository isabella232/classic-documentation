---
template: multi-example
title: Retrieve a client
anchor: retrieve-client

---

<div class="hidden" data-language-content="language" data-language="android">
<div></div>

Each `OptimizelyManager` object retains a reference to its most recently initialized `OptimizelyClient`, and running `OptimizelyManager#getOptimizely()` will return that client instance.

<div class="attention attention--warning push--bottom">
Note that `OptimizelyManager#getOptimizely()` is annotated *`@NonNull`* and will *always* return an `OptimizelyClient` instance.
</div>

If `OptimizelyManager#getOptimizely()` is called before any `OptimizelyClient` objects have been initialized, a "dummy" `OptimizelyClient` instance will be created and returned. This dummy instance logs errors when any of its methods are used.
</div>


<div class="hidden visible" data-language-content="language" data-language="csharp">
<div class="unsupported">The <span class="sdk-platform"></span> SDK does not have documentation for Optimizely client retrieval here.
</div>


<div class="hidden visible" data-language-content="language" data-language="java">
<div class="unsupported">The <span class="sdk-platform"></span> SDK does not have documentation for Optimizely client retrieval here.
</div>


<div class="hidden visible" data-language-content="language" data-language="javascript">
<div class="unsupported">The <span class="sdk-platform"></span> SDK does not have documentation for Optimizely client retrieval here.
</div>


<div class="hidden visible" data-language-content="language" data-language="node">
<div class="unsupported">The <span class="sdk-platform"></span> SDK does not have documentation for Optimizely client retrieval here.
</div>


<div class="hidden visible" data-language-content="language" data-language="objectivec">
<div class="unsupported">The <span class="sdk-platform"></span> SDK does not have documentation for Optimizely client retrieval here.
</div>


<div class="hidden visible" data-language-content="language" data-language="php">
<div class="unsupported">The <span class="sdk-platform"></span> SDK does not have documentation for Optimizely client retrieval here.
</div>


<div class="hidden visible" data-language-content="language" data-language="python">
<div class="unsupported">The <span class="sdk-platform"></span> SDK does not have documentation for Optimizely client retrieval here.
</div>


<div class="hidden visible" data-language-content="language" data-language="ruby">
<div class="unsupported">The <span class="sdk-platform"></span> SDK does not have documentation for Optimizely client retrieval here.
</div>


<div class="hidden visible" data-language-content="language" data-language="swift">
<div class="unsupported">The <span class="sdk-platform"></span> SDK does not have documentation for Optimizely client retrieval here.
</div>

<br>