---
template: page-sidebar
title: "Optimizely X SDK FAQs"
---

# <span class="sdk-solution"></span> FAQs

Below are some frequently asked questions about our SDKs.

<div style="display: none" class="mobile">
We also recommend checking out our [Optimizely X Mobile FAQs](https://help.optimizely.com/Frequently_Asked_Questions%3A_Optimizely_X_Mobile) in Optiverse.
<p><p>
</div>

If you have any questions or feedback, you can [submit a ticket to the developer support team](https://optimizely.com/support). We'll be happy to assist you.

<a href="#target-users">*Q:* How do I target my experiment to a group of users?</a><br>
<a href="#preview">*Q:* How do I QA or preview my experiment?</a><br>
<a href="#mutex">*Q:* How do I make experiments mutually exclusive?</a><br>
<a href="#bot">*Q:* Do your SDKs handle bot detection?</a><br>
<a href="#raw">*Q:* How do I access the raw events I’ve sent to Optimizely?</a><br>
<a href="#performance">*Q:* What is the SDK performance?</a><br>
<a href="#user-id">*Q:* What user IDs should I use in activate() and track()?</a><br>
<a href="#bucketing">*Q:* How does Optimizely consistently bucket users across SDKs?</a><br>
<a href="#datafile-consistency">*Q:* Can I use the same datafile across different SDKs?</a><br>
<a href="#multiple-sdks">*Q:* How does Optimizely work with multiple apps and/or services?</a><br>
<a href="#datafile-management">*Q:* How does datafile management work across SDKs?</a><br>
<a href="#client">*Q:* How do I track user events that occur client-side in a web browser?</a><br>
<a href="#caching">*Q:* How is Optimizely Full Stack compatible with caching?</a></br>
<!-- <a href="#build-custom">*Q:* My language of choice isn’t listed. Can I build my own SDK?</a><br> -->

<a name="target-users"></a>
##### *Q: How do I target my experiment to a group of users?*
*A:* Our SDKs allow you to [conditionally activate](/server/reference/index.html#targeting) experiments based on user attributes you provide. You can define user attributes in the Optimizely UI as well as audiences consisting of one or more user attributes.

<a name="preview"></a>
##### *Q: How do I QA or preview my experiment?*
*A:* You can use our [Whitelisting feature](https://help.optimizely.com/QA_Campaigns_and_Experiments/QA%3A_Whitelist_users_in_Optimizely_X_Full_Stack) to force users into specific variations for QA purposes. The whitelist feature allows you to specify a list of user IDs and their corresponding variations. We're working on adding an option to force users into variations from the SDK as well as a preview mode for our Mobile SDKs.

<a name="mutex"></a>
##### *Q: How do I make experiments mutually exclusive?*
*A:* SDK projects support mutually exclusive experiments out of the box.  Simply create an [experiment group](https://help.optimizely.com/Build_Campaigns_and_Experiments/Create_mutually_exclusive_experiments_in_Optimizely_X_Full_Stack) and assign experiments to that group.

<a name="bot"></a>
##### *Q: Do your SDKs handle bot detection?*
*A:* Our SDKs do not handle bot detection out of the box. If you’re using your own bot detection, we recommend calling `activate()` only for users that have passed your bot detection filter to remove bots from your experiments.

<a name="raw"></a>
##### *Q: How do I access the raw events I’ve sent to Optimizely?*
*A:* Our [raw data export](/x/events/export/index.html) feature allows you to export all of the events you’ve sent to Optimizely on a daily basis.

<a name="performance"></a>
##### *Q: What is the SDK performance?*
*A:* We’ve built our SDKs so you can split traffic to experiments without any network requests.  All decisions are made in-memory based on the [datafile](/server/reference/index.html#datafile) cached in your application so there is negligible impact on latency. Please contact us if you’re interested in seeing performance benchmarks for any of our SDKs.

<a name="user-id"></a>
##### *Q: What user IDs should I use in activate() and track()?*
*A:* We’ve designed our SDKs to be platform-agnostic, so you may use whatever user ID makes the most sense for your experiments. If you’re experimenting on anonymous users, we recommend using a cookie, device ID, or an automatically generated ID from your analytics provider.  If you’re experimenting on a logged in application or device, or experimenting across multiple channels, you can use a hashed email address, universal user identifier (UUID), or any other unique ID.

<a name="bucketing"></a>
##### *Q: How does Optimizely consistently bucket users across SDKs?*
*A:* All of our SDKs use deterministic bucketing via [MurmurHash3](https://en.wikipedia.org/wiki/MurmurHash) to determine what experiments and variations should be active for a user.  This ensures that users will be given the same treatment across multiple visits or on different channels. We’ve also ensured that all of our SDKs give the same output no matter what language you’re using.

<a name="datafile-consistency"></a>
##### *Q: Can I use the same datafile across different SDKs?*
*A:* Yes. The datafile is language agnostic and you can use the same datafile from the same project across different SDKs and you would get consistent bucketing across them. This way, you can activate and track the exact same experiments across different SDKs and get consistent results.

<a name="multiple-sdks"></a>
##### *Q: How does Optimizely work with multiple apps and/or services?*
*A:* It is possible to perform the traffic splitting in one backend using your SDK of choice and then track conversion events in multiple different places using other SDKs, such as other backend services, mobile clients or from the browser with our JavaScript SDK.

<a name="datafile-management"></a>
##### *Q: How does datafile management work across SDKs?*
*A:* The recommended way to manage the datafile file across multiple SDKs is to have a centralized service that subscribes to the datafile webhook on your project and pushes updates to other services that subscribe to datafile file changes. Those services in turn would re-instantiate their Optimizely client using whichever Optimizely SDK they have.

<a name="client"></a>
##### *Q: How do I track user events that occur client-side in a web browser?*
*A:* We’ve created a lightweight [JavaScript SDK](/server/reference/index.html#webtracking) that can be used for tracking conversion events from a web browser. Note that this is different than our standard [JavaScript snippet](https://help.optimizely.com/Set_Up_Optimizely/Implement_the_Optimizely_snippet), so it won’t interfere with any experiments that you’re running client-side in the browser.

<a name="caching"></a>
##### *Q: How is Optimizely Full Stack compatible with caching?*
*A:* Many of our customers are using a CDN to cache content, which means that using one of Optimizely’s SDKs in the backend may require custom configuration. There are a number of ways you can use Optimizely Full Stack in your caching architecture:

1. (Recommended) Use an off-the-shelf load balancer provided by your CDN.<br>
  a. Implement one of our SDKs at this layer to run bucketing logic.<br>
  b. Use the variation key you get from bucketing and the URL as part of the cache key to determine which variation to show.

2. Build your own load balancer on top of your CDN and perform bucketing logic in it to determine which variation to show the user.

3. Use CDN side-scripting such as Edge Side Includes (ESI) for Akamai to run bucketing logic to determine the correct variation to return.

4. Run inline JavaScript code in the <head> of the page.<br>
  a. Add a script with our JavaScript SDK and datafile.<br>
  b. Script will run bucketing logic, set a cookie or URL query param and reload the page.<br>
  c. The caching layer should use the query param or cookie along with the URL as the cache key to determine which variation to show.

<!-- <a name="build-custom"></a>
##### *Q: My language of choice isn’t listed. Can I build my own SDK?*
*A:* Yes! You can use our [datafile](/server/reference/index.html) and our [event API](/events/api/) to build an SDK in any language of your choice.  We’ll publish an SDK developer guide shortly.  In the meantime, please let us know if you’re interested in developing your own SDK and we’ll provide you the documentation and support you need. -->
