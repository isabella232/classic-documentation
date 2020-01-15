---
template: multi-example
title: Whitelists
anchor: whitelisting
---

You can use *Whitelisting* to force users into specific variations for QA purposes. For more information on how to set up whitelists in the Optimizely UI, see our [Optiverse article](https://help.optimizely.com/QA_Campaigns_and_Experiments/QA%3A_Whitelist_users_in_Optimizely_X_Full_Stack).

Whitelists are included in your datafile in the `forcedVariations` field. You don't need to do anything differently in the SDK; if you've set up a whitelist, experiment activation will force the variation output based on the whitelist you've provided.  Whitelisting overrides audience targeting and traffic allocation.  Whitelisting does not work if the experiment is not running.

<br>
