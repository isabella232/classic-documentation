---
template: sidebyside
title: DCP Tables (Datasources)
anchor: dcp_tables
---

<a name="dcp_datasources"></a> 

<div class="attention attention--warning push--bottom">
*Note:* DCP Datasources are now referred to as "Tables" in the Optimizely Web UI. However, the REST API spec continues to use the word "Datasource". As a result, both terms will be present in developer docs
</div>

A table stores a set of related customer attributes under a common ID space.

<img src="/assets/img/dcp/Datasource.png">

A single DCP Service can have several tables. The figure above shows three tables: "My Data Warehouse",
"Email Platform", "Optimizely Datasource", each with customer attributes obtained from a different source, and each with
a different way to identify the same customer. For example, the customer identified by `ANON_ID_2` in "My Data
Warehouse" could be the same customer identified by `OEU_1` in "Optimizely Datasource". Organizing customer data by
table allows you to send data to Optimizely without requiring you to reconcile data across tables. This task
of reconciling data of the same customer across tables can be achieved using the
[alias](/classic/customer-profiles/index.html#alias) operation.

When creating a table, you will provide a customer ID locator (type and name), which tells Optimizely where we can
find the customer ID on your web pages.  When a customer visits, Optimizely will read their customer ID (for each
table) and alias it to their Optimizely User ID.
In the figure, the "Email Platform" table has a locator whose type is `cookie` and whose name is
`email_platform_cookie_name`.  In order for aliasing to work, you would have to place an appropriate customer ID
(matching the customer ID for every row that you upload for this table) in a `cookie` named
`email_platform_cookie_name`.

If you prefer to alias customer IDs manually, and if you know the corresponding Optimizely User ID for each of your
customer IDs, you can do so using the [alias](#dcp_alias) API.
