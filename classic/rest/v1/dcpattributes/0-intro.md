---
template: sidebyside
title: DCP Attributes
anchor: dcp_attributes
---

A Table Attribute describes one aspect of a customer's profile within a Table. As shown in the figure below, your data
warehouse might store a customer's "Lifetime Value", and "Loyalty Card" information, while your email platform might
store if the customer "Opens Frequently".  In DCP, attributes require a datatype, and some datatypes (e.g. datetime)
require a format.  Providing attribute datatypes and formats makes data validation and export to other databases feasible.

<img src="/assets/img/dcp/attributes.png">

Use the Attributes APIs below to register and manage attribute metadata for a given Table, and the [customer
profile](/customer-profiles/index.html#customer_profiles) APIs to upload and update attribute values.
