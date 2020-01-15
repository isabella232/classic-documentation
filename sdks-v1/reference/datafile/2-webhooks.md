---
template: multi-example
title: Webhooks
anchor: webhooks
code_examples:
  python:
    lang: json
    request: |
      {
          "project_id": 1234,
          "timestamp": 1468447113,
          "event": "project.datafile_updated",
          "data": {
              "revision": 1,
              "origin_url": "https://optimizely.s3.amazonaws.com/json/1234.json",
              "cdn_url": "https://cdn.optimizely.com/json/1234.json"
          }
      }

  java:
    lang: json
    request: |
      {
          "project_id": 1234,
          "timestamp": 1468447113,
          "event": "project.datafile_updated",
          "data": {
              "revision": 1,
              "origin_url": "https://optimizely.s3.amazonaws.com/json/1234.json",
              "cdn_url": "https://cdn.optimizely.com/json/1234.json"
          }
      }

  csharp:
    lang: json
    request: |
      {
          "project_id": 1234,
          "timestamp": 1468447113,
          "event": "project.datafile_updated",
          "data": {
              "revision": 1,
              "origin_url": "https://optimizely.s3.amazonaws.com/json/1234.json",
              "cdn_url": "https://cdn.optimizely.com/json/1234.json"
          }
      }
 
  android:
    lang: json
    request: |
      {
          "project_id": 1234,
          "timestamp": 1468447113,
          "event": "project.datafile_updated",
          "data": {
              "revision": 1,
              "origin_url": "https://optimizely.s3.amazonaws.com/json/1234.json",
              "cdn_url": "https://cdn.optimizely.com/json/1234.json"
          }
      }
 
  ruby:
    lang: json
    request: |
      {
          "project_id": 1234,
          "timestamp": 1468447113,
          "event": "project.datafile_updated",
          "data": {
              "revision": 1,
              "origin_url": "https://optimizely.s3.amazonaws.com/json/1234.json",
              "cdn_url": "https://cdn.optimizely.com/json/1234.json"
          }
      }
 
  node:
    lang: json
    request: |
      {
          "project_id": 1234,
          "timestamp": 1468447113,
          "event": "project.datafile_updated",
          "data": {
              "revision": 1,
              "origin_url": "https://optimizely.s3.amazonaws.com/json/1234.json",
              "cdn_url": "https://cdn.optimizely.com/json/1234.json"
          }
      }
 
  javascript:
    lang: json
    request: |
      {
          "project_id": 1234,
          "timestamp": 1468447113,
          "event": "project.datafile_updated",
          "data": {
              "revision": 1,
              "origin_url": "https://optimizely.s3.amazonaws.com/json/1234.json",
              "cdn_url": "https://cdn.optimizely.com/json/1234.json"
          }
      }
 
  php:
    lang: json
    request: |
      {
          "project_id": 1234,
          "timestamp": 1468447113,
          "event": "project.datafile_updated",
          "data": {
              "revision": 1,
              "origin_url": "https://optimizely.s3.amazonaws.com/json/1234.json",
              "cdn_url": "https://cdn.optimizely.com/json/1234.json"
          }
      }
 
  objectivec:
    lang: json
    request: |
      {
          "project_id": 1234,
          "timestamp": 1468447113,
          "event": "project.datafile_updated",
          "data": {
              "revision": 1,
              "origin_url": "https://optimizely.s3.amazonaws.com/json/1234.json",
              "cdn_url": "https://cdn.optimizely.com/json/1234.json"
          }
      }
 
  swift:
    lang: json
    request: |
      {
          "project_id": 1234,
          "timestamp": 1468447113,
          "event": "project.datafile_updated",
          "data": {
              "revision": 1,
              "origin_url": "https://optimizely.s3.amazonaws.com/json/1234.json",
              "cdn_url": "https://cdn.optimizely.com/json/1234.json"
          }
      }
 
---


If you are managing your datafile from a server-side application, we recommend configuring [webhooks](https://help.optimizely.com/Set_Up_Optimizely/Set_up_a_webhook_for_the_Optimizely_Full_Stack_datafile) to maintain the most up-to-date version of the datafile. Your supplied endpoint will be sent a POST request whenever the respective project is modified. Anytime the datafile is updated, you must re-instantiate the Optimizely object in the SDK for the changes to take affect.

You can setup a webhook in your [project settings](https://help.optimizely.com/Set_Up_Optimizely/Set_up_a_webhook_for_the_Optimizely_Full_Stack_datafile) and add the URL the webhook service should ping.

The webhook payload structure is shown at right. As of today, we support one event type, `project.datafile_updated`.

<div class="hidden" data-language-content="language" data-language="android">
If your app and backend have push messaging set up, you can keep your [datafile](#datafile) in sync. You can send a push message from your server to devices running your app telling them to update the datafile. You will need to build a new `OptimizelyClient` object with the `OptimizelyManager#initialize` method to get a new object backed by the new datafile.  Read more in the [Initialization](#initialization) section.
</div>

<div class="hidden" data-language-content="language" data-language="objectivec">
If your app and backend have push messaging set up, you can keep your [datafile](#datafile) in sync. You can send a push message from your server to devices running your app telling them to update the datafile.  You will need to build a new `OPTLYClient` object with one of the `OPTLYManager.init()` methods to get a new object backed by the new datafile.  Read more in the [Initialization](#initialization) section.
</div>

<div class="hidden" data-language-content="language" data-language="swift">
If your app and backend have push messaging set up, you can keep your [datafile](#datafile) in sync. You can send a push message from your server to devices running your app telling them to update the datafile. You will need to build a new `OPTLYClient` object with one of the `[OPTLYManager init]` methods to get a new object backed by the new datafile.  Read more in the [Initialization](#initialization) section.
</div>

<br>
