---
template: multi-example
title: Securing webhooks
anchor: datafile-securing-webhooks
---

When you create a webhook, Optimizely generates a secret token that is used to create a hash signature of webhook payloads. Webhook requests include this signature in a header `X-Hub-Signature` that can be used to verify the request originated from Optimizely.

You will only be able to view a webhook's secret token once immediately after creation. If you forget a webhook's secret token, you'll need to regenerate it on your [project settings](https://help.optimizely.com/Set_Up_Optimizely/Set_up_a_webhook_for_the_Optimizely_Full_Stack_datafile) page.

The `X-Hub-Signature` header contains a SHA1 HMAC hexdigest of the webhook payload, using the webhook's secret token as the key and prefixed with `sha1=`. While the way you verify this signature will vary depending on the language of your codebase, we've provided a [Flask reference implementation](https://gist.github.com/delikat/272415e6669ba7b63c235eee9b0a4e91).

<div class="attention attention--warning push--bottom">
*Note:* We strongly recommend that you use a constant time string comparison function such as Python's [`hmac.compare_digest`](https://docs.python.org/2/library/hmac.html#hmac.compare_digest) or Rack's [`secure_compare`](http://www.rubydoc.info/github/rack/rack/master/Rack/Utils.secure_compare) instead of the `==` operator when verifying webhook signatures. This prevents timing analysis attacks.
</div>

<br>
