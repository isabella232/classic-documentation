---
template: page-sidebar
endpoint_prefix: customer_profile/
title: Bulk Upload
anchor: bulk
---

You can upload a CSV (or TSV) file to the `optimizely-import` S3 bucket using the provided Table S3
path.  We will parse the given CSV, validate each row of data against the registered
[attributes](/rest/reference/#dcp_attributes), and store the successfully processed rows.  Each row is treated as
an [update](/rest/reference/#update-customer_profile) request.

Using the provided AWS credentials, it's possible to upload CSV files in a variety of ways. The simplest approach is to
use an S3 client application, such as [Cyberduck](http://www.cyberduck.io/?l=en).

#### Using Cyberduck

Once you have downloaded and installed Cyberduck, follow these steps to upload a file:
1. Retrieve the datasource's `AWS Access Key`, `AWS Secret Key` and `S3 Import Path` from the Optimizely interface (Audiences > Attributes > More Actions > Data Upload).
2. Launch Cyberduck and create a new Bookmark (Bookmark menu > New Bookmark).
3. Enter a descriptive name for the datasource and your `AWS Access Key`.
4. Click "More Options" to enter the `S3 Import Path`.

  <img src="/assets/img/dcp/cyberduck.png">

  Note: Cyberduck requires the full S3 import path, including both the `optimizely-import` bucket and the given `s3_path`,
for example, when `s3_path=dcp/567/678`, use `/optimizely-import/dcp/567/678`

5. View your bookmarks and double-click to connect to the S3 bucket. Cyberduck will prompt you to enter the `AWS Secret Key` from Step 1.

  <img src="/assets/img/dcp/cyberduck_login.png">

6. You are now connected to your Datasource's S3 bucket! You can drag and drop files to be uploaded via the Cyberduck interface.

Please note that this process may change in future versions of Cyberduck. See the [official Cyberduck website](http://www.cyberduck.io/?l=en) for current documentation.

#### Programmatically
It's also possible to upload files programmatically, using the [AWS
CLI](http://docs.aws.amazon.com/cli/latest/userguide/using-s3-commands.html), an available
[SDK](https://aws.amazon.com/tools/), or [library](http://boto3.readthedocs.org/en/latest/reference/services/s3.html).

You can retrieve the AWS credentials and S3 path from the [Table endpoint](/rest/reference/#read-dcptable). This information is also displayed in the Optimizely web application in the Data Upload menu within each Table.

After uploading a file to S3, you can check Upload History to confirm that your file has been processed. If you need to upload an updated version of your file, make sure that any files with the same name have already been processed. Uploading multiple files with the same name to the same S3 path can cause the files to be processed out of order and prevent your updates from being detected.

##### CSV Formatting Requirements
- You can download a template CSV file for each of your Tables under the Data Upload menu. This file will include a correctly formatted header row with each of the attributes registered for the Table:

<img src="/assets/img/dcp/data_upload.png">

- Each column in the header row must be a registered [attribute](/rest/reference#dcp_attributes) `name`. A CSV
  may contain a subset of the registered [attributes](/rest/reference#dcp_attributes)
- The header row must include a column named `customerId` (case-insensitive). All rows must also contain a valid value for this column. Note that the values of this column should correspond with expected values for the Table's Customer ID field (defined during [Table configuration](https://help.optimizely.com/Target_Your_Visitors/Personalization%3A_Create_Audiences_with_Dynamic_Customer_Profiles#2._Add_a_datasource)). For example, if your Table's Customer ID Field is a cookie named "logged_in_id", then the value of the `customerId` column for each row should be the user's ID as it would appear in their "logged_in_id" cookie.
- If a column header does not correspond to a registered [attribute](/rest/reference#dcp_attributes) `name`, the
  upload will fail
- If an attribute value does not respect the [attribute's](/rest/reference#dcp_attributes) `datatype`/`format`,
  the upload will fail
- If you add an attribute of type String or Text, make sure that any double quotation marks that are part of the
  attribute are escaped with another quotation mark prefixed before it.
  Except for double quotes, none of the other symbols or characters require to be escaped.

  For example:
    A formatted data row in your input file can look like this:
        "CustomerId1", "John Doe", "Height: 6'1"""

    As shown for the "Height" attribute in above sample row, the double quotes that are part of the data need to be
    escaped with another double quote even though the field value is enclosed in separate double quotes,
    while the single quote, in attribute value, can be used as is.

- Here's an example of what your CSV file would look like for a Table containing two attributes, `most_viewed_category` and `LTV`:

<img src="/assets/img/dcp/csv.png">
