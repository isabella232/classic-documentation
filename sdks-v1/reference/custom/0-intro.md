---
template: multi-example
title: SDK configuration
anchor: configuration
---

You can optionally provide a number of parameters to your Optimizely client to configure how the SDK behaves:

* [Event dispatcher](#event-dispatcher): Configure how the SDK sends events to Optimizely
* [Logger](#logger): Configure how the SDK logs messages when certain events occur
* [Error handler](#error-handler): Configure how errors should be handled in your production code
* [User profile service](#profiles): Configure what user state is persisted by the SDK
* [Datafile handler](#datafile-handler): Configure how and how often the datafile is updated

The SDK provides default implementations of event dispatching, logging, and error handling out of the box, but we encourage you to override the default behavior if you have different requirements in your production application. If you'd like to edit the default behavior, refer to the reference implementations in the SDK source code for examples.

<br>
