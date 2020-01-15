---
template: multi-example
title: Exclusion groups
anchor: groups
---

You can use *Exclusion Groups* to keep your experiments mutually exclusive and eliminate interaction effects. For more information on how to set up exclusion groups in the Optimizely UI, see our [Optiverse article](https://help.optimizely.com/Build_Campaigns_and_Experiments/Create_mutually_exclusive_experiments_in_Optimizely_X_Full_Stack).

Experiments that are part of a group have the exact same interface in the SDK: you can call `activate` and `track` like any other experiment. The SDK will ensure that two experiments in the same group will never be activated for the same user.

<br>
