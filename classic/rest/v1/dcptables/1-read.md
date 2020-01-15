---
template: sidebyside
endpoint: dcp_datasources/678
endpoint_prefix: dcp_datasources/
endpoint_option: 678
type: GET
title: Read a Table
anchor: read-dcptable
fields:
  id: Table ID (also known as `dcp_datasource_id`)
  archived: Boolean indicating whether this DCP Service is archived
  attributes: An array of all attributes inside this Table
  aws_secret_key: Secret key for provisioned aws account
  aws_access_key: Access key for provisioned aws account
  created: Creation date of DCP Service
  dcp_service_id: The DCPService this Table is associated with
  description: A short description
  is_optimizely: Boolean indicating if this is the Optimizely Datasource
  keyfield_locator_type: Type of customer ID locator. Must be one of `"cookie"`, `"query parameter"`, `"js_variable"`, or `"uid"`.
  keyfield_locator_name: Name of customer ID locator. Required for all `keyfield_locator_types` except `"uid"`, and must
                         match the regular expression `/^[a-zA-Z_][a-zA-Z_0-9\$]*$/`
  last_modified: Last modified date of this Table
  name: The name of the Table
  s3_path: S3 path for this Table
response: |
  {
    "id": 678,
    "archived": false,
    "attributes": [],
    "aws_access_key": "AKfakekeyV8SH8XTJBUPO",
    "aws_secret_key": "ailb234vK/fakekeyc8SH8SeGCh2leiuX",
    "created": "2015-08-20T23:26:08.414110Z",
    "dcp_service_id": 567,
    "description": "First party data from my Data Warehouse",
    "is_optimizely": false,
    "keyfield_locator_name": "_my_hashedEmailcookie",
    "keyfield_locator_type": "cookie",
    "last_modified": "2015-08-20T23:26:08.414140Z",
    "name": "My Data Warehouse",
    "s3_path": "dcp/567/678"
  }
---

<a name="read-dcpdatasource"></a>
Get metadata for the specified Table (datasource).  The `dcp_datasource_id` is required in the URL.

