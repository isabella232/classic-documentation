---
template: multi-example
title: Datafile
anchor: datafile
datafile: true
code_examples:
  python:
    lang: python
  java:
    lang: java
  csharp:
    lang: csharp
  ruby:
    lang: ruby
  javascript:
    lang: javascript
  node:
    lang: javascript
  php:
    lang: php
  objectivec:
    lang: objectivec
  swift:
    lang: swift
  android:
    lang: java
---

The SDKs are required to read and parse a *datafile* at initialization.

The datafile is in JSON format and compactly represents all of the instructions needed to activate experiments and track events in your code without requiring any blocking network requests. For example, the datafile displayed on the right represents an example project from the [Getting started](/server/getting-started) guide and the basic usage above.

Unless you are building your own SDK, there shouldn't be any need to interact with the datafile directly. Our SDKs should provide all the interfaces you need to interact with Optimizely after parsing the datafile.

#### Access datafile via CDN

You can fetch the datafile for your Optimizely project from Optimizely's CDN. For example, if the ID of your project is 12345 you can access the file at the link below:

`https://cdn.optimizely.com/json/12345.json`

You can easily access this link from your [Optimizely project settings](https://help.optimizely.com/Troubleshoot_Problems/Troubleshooting%3A_Access_the_datafile_for_a_Full_Stack_project).

#### Access datafile via REST API

Alternatively, you can also access the datafile via Optimizely's authenticated REST API. For example, if the ID of your project is 12345 you can access the file at:

`https://www.optimizelyapis.com/experiment/v1/projects/12345/json`

Please note that as with other requests to the REST API, you will have to [authenticate with an API token](/rest/getting-started) and use the preferred request library of your language.

<br>
