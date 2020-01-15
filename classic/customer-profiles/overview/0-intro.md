---
template: page-sidebar
title: Overview
anchor: overview
---

Dynamic Customer Profiles (DCP) are a collection of your customers' attributes, including demographic data, behavioral
characteristics, or any other information particular to your industry and customers. DCP provides a consolidated,
dynamic view of your customers, enabling you to refine this view as you obtain more information, and to take action
based on this view.

A single customer profile contains attributes collected by you, or by services
that you use, and provided to Optimizely to create a single view of the customer. These attributes are organized and
stored in [Tables](/rest/reference#dcp_tables)(also known as datasources) and linked across Tables using identity
[aliases](#alias).

<img src="/assets/img/dcp/overview.png">

Customer profiles can be used to create audiences for targeting, and exported for use in other integrations, or analysis.

Use the [v1 REST API](/classic/rest/v1/) to configure DCP [Services](/classic/rest/v1/#dcp_services),
[Tables](/classic/rest/v1/#dcp_tables), and
[attributes](/classic/rest/v1/#dcp_attributes). You can also [read and write customer profiles](/classic/rest/v1/#dcp_customer_profiles), or
[get and create aliases](/classic/rest/v1/#dcp_alias) using the v1 REST API.

Currently, all DCP REST APIs make use of only [classic tokens](/classic/token/) for authorization. They do not
accept [personal-tokens](/x/authentication/personal-token) to authorize api requests.

To enable DCP for your account, please contact [techpartners@optimizely.com](mailto:techpartners@optimizely.com)

<div class="attention attention--warning push--bottom">
<p>
Remember, your terms of service prohibit you from collecting or sending any *personally identifiable information*
(such as names, social security numbers, email addresses, or any similar data)
to Optimizely's services or systems through Dynamic Customer Profiles or any other feature.
</p>

<p>
Please read the article on [PII](https://help.optimizely.com/Account_Settings/PII%3A_Personally_identifiable_information_in_Optimizely)
to learn more about sending data to Optimizely and handling personally identifiable information.
</p>
</div>
