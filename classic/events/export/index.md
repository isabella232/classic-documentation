---
template: page-sidebar
title: "Data Export"
---
# Data Export Guide

<div class="attention attention--warning push--bottom">
*Updates to Data Export file retention policy* Starting 25 May 2018, to comply with [the upcoming GDPR privacy requirements](https://www.optimizely.com/compliance/gdpr/) and to enhance your control over your data, Optimizely will retain the files in your Data Export bucket for 30 days. To keep your file history over 30 days, update your import process to archive your files at least once every 30 days.
</div>

<br> Data Export allows developers to access all of their Optimizely event data. This data is computed daily and contain the last 24 hours of events for all A/B testing experiments in an account. The data will be written securely to an S3 bucket, which you can then programmatically access via Amazon’s APIs and a set of secure credentials provided by Optimizely.

You can use Data Export to access Optimizely experiment data with your own data warehouse.

<div class="attention attention--warning push--bottom">If you have any questions, you can [submit a ticket to the developer support team](https://optimizely.com/support). We'll be happy to assist you.</div>

## Availability

Currently, this feature is available to Enterprise customers; please reach out to your Customer Success Manager if you wish to utilize this feature. If you do not have a CSM, [submit a ticket to the developer support team](https://optimizely.com/support) to verify your plan and eligibility.

## Technical Details

Data is written out for all experiments in all projects running under an Optimizely account, and one file will be written per experiment per day. Each file will contain 24 hours worth of data, thru midnight UTC of the previous night. These files are gzipped tab-delimited files with the format described below. Also, if you currently receive a data export via the Technical Support team, the data will be in the same format as the current exports, with the addition of one column indicating user_agent for web experiment data. There is also a standard header row.

The S3 bucket location will follow the format: `/optimizely-export/{account_id}/{project_id}/yyyy/mm/dd/{file_name}`

The file name follows the format: `experiment_id-yyyy-mm-dd.tsv.gz` . Example: `123-2016-03-20.tsv.gz`

<img alt="Data Export Chart" width="500px" src="/assets/img/data/data-export-chart.png" />

<b>Note:</b> Partitioning of results will occur for very large experiments. 40 different files will be produced for one experiment. E.g. instead of 7473240577-2016-10-15.tsv.gz the file names will be 7473240557-<i>&lt;index&gt;</i>-2016-10-15.tsv.gz where <i>&lt;index&gt;</i> ranges from 0-39.

### Web Dictionary

<h5> <a href="/data/web_sample.tsv"> Sample File </a></h5>

<h4>Definitions</h4>
<table class="table">
   <tbody>
      <tr>
         <td align="left"><b>timestamp</b></td>
         <td class="desc">
            <p>The timestamp of when the event was received, not necessarily when it occurred in the browser. The format is YYYY-MM-DDTHH24:MI:SS.sssZ (ISO format), and the timezone is UTC.</p>
         </td>
      </tr>
      <tr>
         <td align="left"><b>project_id</b></td>
         <td class="desc">
            <p>Your Optimizely project ID on which the experiment lives.</p>
         </td>
      </tr>
      <tr>
         <td align="left"><b>experiment_id</b></td>
         <td class="desc">
            <p>The experiment ID.</p>
         </td>
      </tr>
      <tr>
         <td align="left"><b>variation_id</b></td>
         <td class="desc">
            <p>The id we use to identify the variation the user saw. This should correspond to the variation id in the Diagnostic Report in the Options menu of the Visual Editor.
            </p>
         </td>
      </tr>
      <tr>
         <td align="left"><b>end_user_id</b></td>
         <td class="desc">
            <p>This is the anonymous optimizelyEndUserId cookie value.  It represents a unique visitor.</p>
         </td>
      </tr>
      <tr>
         <td align="left"><b>uuid</b></td>
         <td class="desc">
            <p>Similar in scope to end_user_id, but this is the customer's API-provided unique ID they want to track in lieu of the optimizelyEndUserId cookie value.  This was renamed from the legacy ppid on Thursday, 2016-05-19.</p>
         </td>
      </tr>
      <tr>
         <td align="left"><b>user_ip</b></td>
         <td class="desc">
            <p>IP of the user associated with this tracking call.</p>
         </td>
      </tr>
      <tr>
         <td align="left"><b>user_agent</b></td>
         <td class="desc">
            <p>User-Agent header passed from the browser.</p>
         </td>
      </tr>
      <tr>
         <td align="left"><b>revenue</b></td>
         <td class="desc">
            <p>If applicable, the amount of the transaction in cents (399 corresponds to $3.99). This will only be populated with a non-zero value for revenue goals.</p>
         </td>
      </tr>
      <tr>
         <td align="left"><b>event_name</b></td>
         <td class="desc">
            <p>The event name of the tracking call.  For pageviews this is the URL of the page; for the default Engagement goal this is 'engagement'; and for everything else this is the custom event name.  When an experiment activates, if there are matching pageview goals (project-wide), there will be one row with a value of 'optly_activate' and one row with the URL per pageview goal.  If there are no matching pageview goals, there will be one row with the URL of the page where the experiment was activated.</p>
         </td>
      </tr>
      <tr>
         <td align="left"><b>mobile visitors</b></td>
         <td class="desc">
            <p>For accounts with segmentation a true or false value of whether or not the user was using a mobile device (this is an Optimizely default segment, so tablets are considered mobile here).</p>
         </td>
      </tr>
      <tr>
         <td align="left"><b>browser</b></td>
         <td class="desc">
            <p>For accounts with segmentation this is the browser that was being used by the user when the tracking call was made.  gc is Google Chrome, ff is Firefox, and ie is Internet Explorer.  safari, opera, and <a href="https://en.wikipedia.org/wiki/UC_Browser"> ucbrowser </a> are listed as-is.</p>
         </td>
      </tr>
      <tr>
         <td align="left"><b>source type</b></td>
         <td class="desc">
            <p>For accounts with segmentation this is the value of the <a href="https://help.optimizely.com/hc/en-us/articles/201876450#traffic"> traffic source </a> that the user falls into (campaign, direct, referral, search).</p>
         </td>
      </tr>
      <tr>
         <td align="left"><b>campaign</b></td>
         <td class="desc">
            <p>The value of the campaign segment (i.e. AdWords utm_campaign parameter value) tied to this user.  Default value is "none." Any fields after this are your segmented audiences or dimension names.</p>
         </td>
      </tr>
   </tbody>
</table>

**Please Note**:
   * Any fields after this are your segmented audiences or dimension names.
   * Adding or removing segments or dimensions could alter the layout of the event data files. Please account for this if you build an automated import of this data.
   * Redirect tests might have the redirect page views out of order due to the timing of the log request being sent to our system.


### Android Dictionary

<h5> <a href="/data/android_sample.tsv"> Sample File </a></h5>

<h4>Definitions</h4>
<table class="table">
   <tbody>
      <tr>
         <td align="left"><b>timestamp</b></td>
         <td class="desc">
            <p>The timestamp of when the event was received, not necessarily when it occurred in the browser. The format is YYYY-MM-DDTHH24:MI:SS.sssZ (ISO format), and the timezone is UTC.</p>
         </td>
      </tr>
      <tr>
         <td align="left"><b>project_id</b></td>
         <td class="desc">
            <p>Your Optimizely project ID on which the experiment lives.</p>
         </td>
      </tr>
      <tr>
         <td align="left"><b>experiment_id</b></td>
         <td class="desc">
            <p>The experiment ID.</p>
         </td>
      </tr>
      <tr>
         <td align="left"><b>variation_id</b></td>
         <td class="desc">
            <p>The id we use to identify the variation the user saw. This should correspond to the variation id in the Diagnostic Report in the Options menu of the Visual Editor.
            </p>
         </td>
      </tr>
      <tr>
         <td align="left"><b>end_user_id</b></td>
         <td class="desc">
            <p>  This is the anonymous optimizelyEndUserId value.  It represents a unique visitor.</p>
         </td>
      </tr>
      <tr>
         <td align="left"><b>uuid</b></td>
         <td class="desc">
            <p>  Similar in scope to end_user_id, but this is the customer's API-provided unique ID they want to track in lieu of the anonymous value.  This was renamed from the legacy ppid on Thursday, 2016-05-19.</p>
         </td>
      </tr>
      <tr>
         <td align="left"><b>user_ip</b></td>
         <td class="desc">
            <p> IP of the user associated with this tracking call.</p>
         </td>
      </tr>
      <tr>
         <td align="left"><b>revenue</b></td>
         <td class="desc">
            <p>  If applicable, the amount of the transaction in cents (399 corresponds to $3.99). This will only be populated with a non-zero value for revenue goals.  For event_name values of "mobile_session," this will also show the length of the session in seconds..</p>
         </td>
      </tr>
      <tr>
         <td align="left"><b>event_name</b></td>
         <td class="desc">
            <p>  The event name of the tracking call.  A value of "mobile_session" means a new session was recorded (a session is a period of activity during which the app is foregrounded, without a break longer than 30 seconds).  A value of "visitor-event" shows the first time a visitor sees an experiment.  A tap or view goal will show the view name with #tap or #view appended.  For everything else it is the custom event name.</p>
         </td>
      </tr>
      <tr>
         <td align="left"><b>Android App Version</b></td>
         <td class="desc">
            <p> The numeric version of your Android app running on the user’s device.</p>
         </td>
      </tr>
      <tr>
         <td align="left"><b>Android SDK Version</b></td>
         <td class="desc">
            <p> The numeric version of Optimizely’s Android SDK running in your app on the user’s device.</p>
         </td>
      </tr>
      <tr>
         <td align="left"><b>Android Device Model</b></td>
         <td class="desc">
            <p> The device’s name as returned to Optimizely’s SDK, e.g. Google Galaxy Nexus - 4.2.2 - API 17 - 720x1280.</p>
         </td>
      </tr>
   </tbody>
</table>


### iOS Dictionary

<h5> <a href="/data/ios_sample.tsv"> Sample File </a></h5>

<h4>Definitions</h4>
<table class="table">
   <tbody>
      <tr>
         <td align="left"><b>timestamp</b></td>
         <td class="desc">
            <p>The timestamp of when the event was received, not necessarily when it occurred in the browser. The format is YYYY-MM-DDTHH24:MI:SS.sssZ (ISO format), and the timezone is UTC.</p>
         </td>
      </tr>
      <tr>
         <td align="left"><b>project_id</b></td>
         <td class="desc">
            <p>Your Optimizely project ID on which the experiment lives.</p>
         </td>
      </tr>
      <tr>
         <td align="left"><b>experiment_id</b></td>
         <td class="desc">
            <p>The experiment ID.</p>
         </td>
      </tr>
      <tr>
         <td align="left"><b>variation_id</b></td>
         <td class="desc">
            <p>The id we use to identify the variation the user saw. This should correspond to the variation id in the Diagnostic Report in the Options menu of the Editor.
            </p>
         </td>
      </tr>
      <tr>
         <td align="left"><b>end_user_id</b></td>
         <td class="desc">
            <p>This is the anonymous optimizelyEndUserId value set in NSUserDefaults.  It represents a unique visitor.</p>
         </td>
      </tr>
      <tr>
         <td align="left"><b>uuid</b></td>
         <td class="desc">
            <p> Similar in scope to end_user_id, but this is the customer's API-provided unique ID they want to track in lieu of the anonymous value.  This was renamed from the legacy ppid on Thursday, 2016-05-19.</p>
         </td>
      </tr>
      <tr>
         <td align="left"><b>user_ip</b></td>
         <td class="desc">
            <p> IP of the user associated with this tracking call.</p>
         </td>
      </tr>
      <tr>
         <td align="left"><b>revenue</b></td>
         <td class="desc">
            <p>  If applicable, the amount of the transaction in cents (399 corresponds to $3.99). This will only be populated with a non-zero value for revenue goals.  For event_name values of "mobile_session," this will also show the length of the session in seconds.</p>
         </td>
      </tr>
      <tr>
         <td align="left"><b>event_name</b></td>
         <td class="desc">
            <p> The event name of the tracking call.  A value of "mobile_session" means a new session was recorded (a session is a period of activity during which the app is foregrounded, without a break longer than 30 seconds).  A value of "visitor-event" shows the first time a visitor sees an experiment.  A tap or view goal will show the view name with #tap or #view appended.  For everything else it is the custom event name.</p>
         </td>
      </tr>
      <tr>
         <td align="left"><b>iOS App Version</b></td>
         <td class="desc">
            <p> The numeric version of your iOS app running on the user’s device.</p>
         </td>
      </tr>
      <tr>
         <td align="left"><b>iOS Device Model </b></td>
         <td class="desc">
            <p> The device’s name as returned to Optimizely’s SDK, e.g. iPhone.</p>
         </td>
      </tr>
      <tr>
         <td align="left"><b>iOS SDK Version</b></td>
         <td class="desc">
            <p> The numeric version of Optimizely’s iOS SDK running in your app on the user’s device.</p>
         </td>
      </tr>
   </tbody>
</table>

**Please Note: (web, iOS & Android)**

* Data is de-duplicated on the results screen but not in the Data Export. Revenue goals are never de-duplicated.

### Data formats

As these files are TSVs, nulls will be empty tabs.
<ul>
   <li><b>project_id</b>, <b>experiment_id</b>, and <b>variation_id</b> will always be integers.</li>
   <li><b>end_user_id</b> is the concatenation of a Unix timestamp and a random number (with a couple additional alpha characters).    Example: oeu1460584472759r0.9885484367665214.</li>
   <li><b>uuid</b> would be a customer-provided known unique user ID.</li>
   <li><b>user_ip</b> is the public IP address of the device on which the event occurred. The longest possible value here should be an expanded value in IPv6 format.</li>
   <li><b>user_agent</b> is the raw alphanumeric value returned from the browser.</li>
   <li><b>revenue</b> will never be a decimal - Optimizely preserves the converted value into cents as an integer.</li>
   <li><b>event_name</b>, at its largest, is either a full alphanumeric URL with all query parameters included, or a custom event name your team determines.</li>
   <li><b>mobile visitors</b> is a string with possible values 'true' and 'false.'</li>
   <li><b>browser</b> is a deterministic alpha string defined by Optimizely.</li>
   <li><b>source_type</b> is a deterministic alpha string defined by Optimizely.</li>
   <li><b>campaign</b> is maximum 20 characters. 'none' represents the absence of a campaign value.</li>
</ul>

### Primary Keys

<ul>
   <li>Optimizely Data Export files represent a raw output of all events that occur in the browser. It is recommended that customers import all records. There are no duplicates in these files, because each and every event the visitor initiates on your site or app is captured. For example, this would include five records if the visitor landed on your home page five times. Optimizely doesn't reproduce rows in the same or subsequent files unless that event actually happened anew.</li>
   <li>For Optimizely Classic files, a composite key of timestamp, end_user_id, and event_name may be used as a primary key only if multiple instances of the same event are not meaningful to your analysis. You would have to decide if you want to take the first (earliest timestamp) or last (latest timestamp) instance of that event. Events may carry the same timestamp.</li>
</ul>

### Status File

A status file will be provided to track the success or failure of that day's experiment event files. This file is named status.yaml and is included in the daily folder per project. The format contains: failed_exports, successful_exports, and a timestamp in UTC seconds since epoch. View a *sample YAML file* [with](/data/status.yaml) and [without](/data/sample-status.yaml) failed export files.

**Additional Notes:**
<ul>
   <li>If a single day's folder is not present for some project, but other folders are present for that day for other projects, that means the job succeeded and there isn't activity to export for that day for those specific projects.</li>
   <li>If all folders for all projects for a single day are absent, that could mean:</li>
   <ul><li>There is no experiment activity across the account for that day</li>
   <li>The job is still running</li>
   <li>The job has failed (all files are transferred in one step)</li></ul>
   <li>If data files are present but the status.yaml file is not, the status file may still be in process or that file itself may have failed (it is a separate step after data file transfer).</li>
   <li>Should a given day or project be reprocessed later, those experiment files will be deposited in the folder corresponding to the same date when the data was captured, not when the job was rerun.</li>
   <li>It generally should not be the case that if an experiment's file is listed as failed, the file is present. If such a case does occur, do not process the file and Optimizely will replace it once the job reruns successfully.</li>
</ul>

### Miscellaneous

<ul>
   <li>The Optimizely job kicks off at 0130 UTC and completion time depends on data volume. Depend on the status.yaml file to tell when you should begin importing files.</li>
</ul>
