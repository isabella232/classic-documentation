---
template: multi-example
title: Versioning
anchor: datafile-versioning
---

<div class="hidden visible" data-language-content="language" data-language="csharp">
<div class="unsupported"><div class="attention attention--warning push--bottom">
*Note:* Datafile versioning is not applicable for this SDK.
</div></div></div>

<div class="hidden visible" data-language-content="language" data-language="java">
<div class="unsupported"><div class="attention attention--warning push--bottom">
*Note:* Datafile versioning is not applicable for this SDK.
</div></div></div>

<div class="hidden visible" data-language-content="language" data-language="javascript">
<div class="unsupported"><div class="attention attention--warning push--bottom">
*Note:* Datafile versioning is not applicable for this SDK.
</div></div></div>

<div class="hidden visible" data-language-content="language" data-language="node">
<div class="unsupported"><div class="attention attention--warning push--bottom">
*Note:* Datafile versioning is not applicable for this SDK.
</div></div></div>

<div class="hidden visible" data-language-content="language" data-language="php">
<div class="unsupported"><div class="attention attention--warning push--bottom">
*Note:* Datafile versioning is not applicable for this SDK.
</div></div></div>

<div class="hidden visible" data-language-content="language" data-language="python">
<div class="unsupported"><div class="attention attention--warning push--bottom">
*Note:* Datafile versioning is not applicable for this SDK.
</div></div></div>

<div class="hidden visible" data-language-content="language" data-language="ruby">
<div class="unsupported"><div class="attention attention--warning push--bottom">
*Note:* Datafile versioning is not applicable for this SDK.
</div></div></div>

For iOS, tvOS and Android projects, the datafile is versioned so that we can maintain backwards compatibility with SDKs that have been released out into the wild with older versions of the datafile. This will ensure that in the event our datafile schema changes, experiments will still run in apps that have not been updated with the latest version of the SDK.

All versions of the datafile for your Optimizely project are accessible via the CDN. For example, if the ID of your project is 12345 you can access v3 the datafile at the link below:

`https://cdn.optimizely.com/public/12345/datafile_v3.json`

We will upload every supported version of the datafile to our CDN so that SDKs that are pegged to an older version will be able to retrieve a datafile that is compatible with that SDK.

If you are using `OPTLYManager` (for iOS or tvOS) or `OptimizelyManager` (for Android) to manage datafile updates, these will gracefully handle datafile versioning.  However, if you are managing the datafile on your own, then you have to make sure to fetch the correct version of the datafile according to the SDK version you are using.

<br>
