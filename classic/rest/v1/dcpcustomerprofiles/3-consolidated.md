---
template: sidebyside
endpoint: consolidatedCustomerView/567/678/oeu1234.5678
endpoint_prefix: consolidatedCustomerView/
endpoint_domain: https://vis.optimizely.com/api/
endpoint_option: 567
type: GET
title: Read consolidated customer profile
anchor: consolidated-profile
response: |
  [
    {
      "dcpServiceId": "567",
      "datasourceId": "789",
      "customerId": "oeu1234.5678",
      "data": {
        "Life-time value": 10,
        "most_viewed_category": "jeans"
      }
    },
    {
      "dcpServiceId": "567",
      "datasourceId": "790",
      "customerId": "sfdc1223a3_ji$ddd",
      "data": {
        "mrr": 10000
      }
    }
  ]
---

Get a consolidated view of a single customer profile.  The `dcp_service_id`, `optimizely_datasource_id` and `optimizely_user_id` are required in the URL.

The profile is consolidated by [aliasing](#dcp_alias) across different Tables in the DCP Service.

<div class="attention attention--warning push--bottom">
The `datasourceId` for this call should be the ID of the "Optimizely Datasource". You can find this ID using [List
Tables](#list-dcptables) and finding the Table with `is_optimizely=true`.
In this example, it is *678*.  The `customerId` for this call should be the Optimizely User ID. In this example, it is
*oeu1234.5678*.
</div>
