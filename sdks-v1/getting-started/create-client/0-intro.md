---
template: multi-example
title: "6. Create an Optimizely client"
anchor: create-client

---

After installing the <span class="sdk-platform"></span> SDK, you're ready to create an *Optimizely client*.

An Optimizely Client is an object that represents the state of your Optimizely project within your application. It gets this information from your project's [datafile](/x/solutions/sdks/reference/index.html?#datafile), a JSON representation of your project's configuration details. The datafile contains all of the instructions needed to activate experiments and track events in your code without requiring any blocking network requests.

You can get your Optimizely project's datafile by using its CDN link. Go to _Settings_ > _Datafile_ in the [Optimizely web app](https://app.optimizely.com/v2/).

<img src="/assets/img/datafile-cdn-link.png" alt="Your datafile's CDN link found in Settings > Datafile" class="screenshot">


<div style="display: none" class="mobile">
Your datafile will change as your project changes, so the SDK has a function named `OptimizelyManager`, which monitors your datafile via the CDN link. When your datafile changes, the OptimizelyManager will automatically rebuild your `OptimizelyClient`. See our [reference material](/x/solutions/sdks/reference/index.html?language=android&platform=mobile#initialization) for more information about the client.
</div>


<div style="display: none" class="sdk-python">

<div></div>

Now you can create an Optimizely client as follows, using the Python [requests](http://docs.python-requests.org/en/master/) library.

```python
url = 'https://cdn.optimizely.com/json/12345.json'
import requests
datafile = requests.get(url).text
from optimizely import optimizely
optimizely_client = optimizely.Optimizely(datafile)
```

</div>

<div style="display: none" class="sdk-java">

<div></div>

Now you can create an Optimizely client by providing the datafile to the constructor. [Read more](/server/reference/index.html?language=java#initialization) about initializing the client.

</div>

<div style="display: none" class="sdk-csharp">

<div></div>

Now you can create an Optimizely client by providing the datafile to the constructor. [Read more](/server/reference/index.html?language=csharp#initialization) about initializing the client.

</div>

<div style="display: none" class="sdk-ruby">

<div></div>

Now you can create an Optimizely client as follows, using the Ruby [HTTParty](https://github.com/jnunemaker/httparty) library.

```ruby
require 'httparty'
require 'optimizely'
url = 'https://cdn.optimizely.com/json/12345.json'
datafile = HTTParty.get(url).body
optimizely_client = Optimizely::Project.new(datafile)
```

</div>

<div style="display: none" class="sdk-node">

<div></div>

Now you can create an Optimizely client by providing the datafile to the constructor. Use your HTTP library of choice to fetch the datafile. [Read more](/server/reference/index.html?language=javascript#initialization) about initializing the client.

```javascript
var url = 'https://cdn.optimizely.com/json/12345.json';
var rp = require('request-promise');
var options = {uri: url, json: true};
var optimizelySDK = require('optimizely-server-sdk');
var optimizely;
rp(options).then(function(datafile) { optimizely = optimizelySDK.createInstance({datafile: datafile}) });
```

</div>

<div style="display: none" class="sdk-javascript">

<div></div>

Now you can create an Optimizely client by providing the datafile to the constructor. Use your HTTP library of choice to fetch the datafile. [Read more](/server/reference/index.html?language=javascript#initialization) about initializing the client.

```javascript
var optimizelyClientInstance;
var url = 'https://cdn.optimizely.com/json/12345.json';
window.fetch(url, { mode: 'cors' })
  .then((response) => response.json())
  .then((datafile) => {
    optimizelyClientInstance = optimizely.createInstance({ datafile: datafile })
  });
```

</div>

<div style="display: none" class="sdk-php">

<div></div>


Now you can create an Optimizely client by providing the datafile to the constructor. [Read more](/server/reference/index.html?language=php#initialization) about initializing the client.

</div>

<div style="display: none" class="sdk-android">

<div></div>

<h5>Create an OptimizelyManager Instance</h5>

The first step in using the SDK is to create an instance of `OptimizelyManager`.  This synchronizes your app with Optimizely and periodically downloads your project's datafile via an Android Service. <br />

For this tutorial, we will setup the `OptimizelyManager` in the MainActivity class. All below snippets will be placed in _MainActivity.java_. Please provide your `project_id`.

```java
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);

    OptimizelyManager optimizelyManager = OptimizelyManager.builder("project_id")
        .build(getApplicationContext());

  }

```

<h5>Create an instance of OptimizelyClient via OptimizelyManager</h5>

This snippet should go below the OptimizelyManager Instance in _MainActivity.java_.

```java
  optimizelyManager.initialize(this, new OptimizelyStartListener() {
      @Override
      public void onStart(OptimizelyClient optimizely) {
          // Activate code (see "Split traffic" in the Getting Started guide)

          // Track code (see "Track events" in the Getting Started guide)
      }

  });
```

Full code [snippet](https://gist.github.com/mauerbac/64d2c638b72e38de603f511601dd2b91)

</div>

<div style="display: none" class="sdk-objectivec">

<div></div>

Because you can do iOS development in both Objective-C and Swift, we are including two files in this tutorial:

* `AppDelegate.m` for Objective-C
* `AppDelegate.swift` for Swift

<div style="border-top: 1px solid rgba(0, 0, 0, 0.05)"></div>

### > Import the Optimizely SDK

Import the <span class="sdk-platform"></span> SDK into your project.

* In AppDelegate.m (Objective-C):
  ```objectivec
  #import <OptimizelySDKiOS/OptimizelySDKiOS.h>
  ```
* In AppDelegate.swift (Swift):
  ```swift
  import OptimizelySDKiOS
  ```

<div style="border-top: 1px solid rgba(0, 0, 0, 0.05)"></div>

### > Initialize the client

Put the following snippet in the `didFinishLaunchingWithOptions` function. Make sure to replace `project_id` with your Project ID (keep the quotation marks). You can find your Project ID on the same page as your datafile (_Settings_ > _Datafile_).

* In AppDelegate.m (Objective-C):
  ```objectivec
  OPTLYManager *manager = [OPTLYManager init:^(OPTLYManagerBuilder * _Nullable builder) {
      builder.projectId = @"project_id";
  }];

  [manager initializeWithCallback:^(NSError * _Nullable error, OPTLYClient * _Nullable client) {
      // Activate code (see "Split traffic" in the Getting Started guide)

      // Track code (see "Track events" in the Getting Started guide)

  }];

  ```

* In AppDelegate.swift (Swift):
  ```swift
  let optimizelyManager = OPTLYManager.init {(builder) in
      builder!.projectId = "project_id"
  }

  optimizelyManager?.initialize() { (error, client) in
      // Activate code (see "Split traffic" in the Getting Started guide)

      // Track code (see "Track events" in the Getting Started guide)

  }
  ```

#### Example files

Here are some example files that you can use as a comparison to your own work.

* [Objective-C example: `AppDelegate.m`](https://gist.github.com/mauerbac/8243dce3884b460271a0ca9673f84fae)
* [Swift example: `AppDelegate.swift`](https://gist.github.com/mauerbac/4dd686a390b6cb305a358844568c0eb4)

</div>

<div style="display: none" class="sdk-swift">

<div></div>

Now you can create an Optimizely client by providing the datafile to the constructor. Use your HTTP library of choice to fetch the datafile. [Read more](/server/reference/index.html?language=swift#initialization) about initializing the client.

_Objective-C:_
```objectivec
#import <OptimizelySDKTVOS/OptimizelySDKTVOS.h>

Optimizely *optimizely = [Optimizely init:^(OPTLYBuilder *builder) {
    builder.datafile = datafile;
}];
```
_Swift:_
```swift
import OptimizelySDKTVOS

let optimizely: Optimizely? = Optimizely.init({ (builder) in
    builder!.datafile = datafile
})
```

</div>


