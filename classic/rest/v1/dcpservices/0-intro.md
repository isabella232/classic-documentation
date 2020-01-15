---
template: sidebyside
title: DCP Services
anchor: dcp_services
---
A DCP Service provides all Customer Profile related services including storage, processing, and delivery. A DCP Service
stores customer data in a set of [tables](#dcp_tables) (also known as datasources). A table stores a set of
related customer attributes under a common ID space. For example, all customer attributes collected by your CRM may be 
stored in a "CRM" table; customer attributes from your data warehouse may be stored in a separate
"Data Warehouse" table. Because the same customer will likely be identified using different IDs in different tables, a DCP
Service also stores [aliases](#dcp_alias) (identity links) to reconcile attributes of the same customer
across tables. In the figure below, because the customer identified by `ANON_ID_1` in "My Data Warehouse" is the
same customer identified by `OEU_2` in "Optimizely Datasource", the Alias Table records this identity as a row.

<div class="attention attention--warning push--bottom">
Currently, each Optimizely Account can have a maximum of one DCP Service. Please submit a support ticket if you think you have a need for multiple DCP Services.
</div>

<img src="/assets/img/dcp/DCP_Service.png">

##### Associating Optimizely Projects to a DCP Service
Upon creation, a DCP Service is not linked to any projects. In order to build audiences which reference DCP data in a given project, you must link 
that project to a DCP Service using [update project](#update-project). Multiple Optimizely projects can be linked to a single DCP Service.

##### Uploading Data
To upload customer attributes from a particular source, [add a table](#create-dcptable)
to your DCP Service. Each DCP Service contains a provisioned [AWS](http://aws.amazon.com/) account used for bulk data
uploads.  Details on uploading data to a table can be found [here](/classic/customer-profiles/index.html#customer_profiles). You
can upload customer attributes to a table in a streaming manner using the [customer profile
APIs](#update-customer_profile) or in bulk using the [table's S3
bucket](/classic/customer-profiles/index.html#bulk).
