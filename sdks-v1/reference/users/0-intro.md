---
template: multi-example
title: User IDs
anchor: user-ids
---

*User IDs* are used to uniquely identify the participants in your experiments. You can supply any string you wish for user IDs depending on your experiment design.

For example, if you're running experiments on anonymous users, you can use a 1st party cookie or device ID to identify each participant. If you're running experiments on known users, you can use a universal user identifier (UUID) to identify each participant. If you're using UUIDs then you can run experiments that span multiple devices or applications and ensure that users have a consistent treatment.

User IDs don't necessarily need to correspond to individual users. If you're running experiments in a B2B SaaS application, you may want to pass account IDs to the SDK to ensure that every user in a given account has the same treatment.

Below are some additional tips for using user IDs.

* *Ensure user IDs are unique:* It is essential that user IDs are unique among the population you are using for experiments. Optimizely will bucket users and provide experiment metrics based on this user ID that you provide.

* *Anonymize user IDs:* The user IDs you provide will be sent to Optimizely servers exactly as you provide them. You are responsible for anonymizing any personally identifiable data such as email addresses in accordance with your company's policies.

* *Use IDs from 3rd party platforms:* If you are measuring the impact of your experiments in a 3rd party analytics platform, we recommend leveraging the same user ID from that platform. This will help ensure data consistency and make it easier to reconcile events between systems.

* *Use one namespace per project:* Optimizely generally assumes a single namespace of user IDs for each project. If you are using multiple different conventions for user IDs in a single project (e.g. anonymous visitor IDs for some experiments and UUIDs for others) then Optimizely will be unable to enforce rules such as mutual exclusivity between experiments.

* *Use either logged-out vs. logged-in IDs:* We do not currently provide a mechanism to alias logged-out IDs with logged-in IDs. If you are running experiments that span both logged-out and logged-in states (e.g. experiment on a signup funnel and track conversions after the user has logged in), you must persist logged-out IDs for the lifetime of the experiment.

<br>
