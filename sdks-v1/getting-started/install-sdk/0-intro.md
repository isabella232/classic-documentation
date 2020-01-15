---
template: multi-example
title: "5. Install the SDK"
anchor: install-sdk

---

<div style="display: none" class="sdk-python">

<div></div>

Our Python SDK is available through PyPI and can be installed via [pip](https://pypi.python.org/pypi/pip).

```bash
pip install optimizely-sdk
```

If the installation fails, it might help to isolate this project using [virtualenv](http://docs.python-guide.org/en/latest/dev/virtualenvs/).

</div>

<div style="display: none" class="sdk-java">

<div></div>

The Java SDK packages are available through Bintray:

* [core-api](https://bintray.com/optimizely/optimizely/optimizely-sdk-core-api)
* [httpclient](https://bintray.com/optimizely/optimizely/optimizely-sdk-httpclient)

[More details](/server/reference/index.html?language=java#installation) on installing the SDK.

</div>

<div style="display: none" class="sdk-csharp">

<div></div>

The C# SDK is available through [NuGet](https://www.nuget.org/packages/Optimizely.SDK) and can be installed from the [Package Manager Console](https://docs.microsoft.com/en-us/nuget/tools/package-manager-console).

```bash
Install-Package Optimizely.SDK
```

</div>

<div style="display: none" class="sdk-ruby">

<div></div>

Our Ruby SDK is available through [RubyGems](https://rubygems.org/gems/optimizely-sdk) and can be installed using `gem` or `bundler`.

```bash
gem install optimizely-sdk
```

</div>

<div style="display: none" class="sdk-node">

<div></div>

Our Node SDK is available through [npm](https://www.npmjs.com/package/optimizely-server-sdk) and can be installed as shown below:

```bash
npm install optimizely-server-sdk --save
```

</div>
<div style="display: none" class="sdk-javascript">

<div></div>

Our JavaScript SDK is available through [npm](https://www.npmjs.com/package/optimizely-client-sdk) and can be installed as shown below:

```
npm install optimizely-client-sdk --save
```

If you aren't able to install via `npm` or to use the SDK in a non-CommonJS fashion, follow the [instructions in the SDK's README](https://github.com/optimizely/javascript-sdk) to build a minified snippet.

</div>

<div style="display: none" class="sdk-php">

<div></div>

Our PHP SDK is available through [Composer](https://getcomposer.org/). To install simply `composer require optimizely/optimizely-sdk` or add `optimizely/optimizely-sdk` in the `require` section of your `composer.json`.

</div>


<div style="display: none" class="sdk-android">

<div></div>

To add the Optimizely Android SDK to your app, include `compile 'com.optimizely.ab:android-sdk:+'` in your app's `build.gradle` in the `dependencies` block.

_build.gradle (Module: app)_
```java
repositories {
  jcenter()
}

dependencies {
  compile 'com.optimizely.ab:android-sdk:1.6.1'
}
```
[More details](/server/reference/index.html?language=android#installation) on installing the SDK.

</div>

<div style="display: none" class="sdk-objectivec">
    <div></div>

Our iOS SDK is available through CocoaPods, Carthage, and manual installation.

*[CocoaPods](https://guides.cocoapods.org/using/getting-started.html) instructions*

1.  [Install CocoaPods](https://guides.cocoapods.org/using/getting-started.html#installation).

2.  Initialize a [Podfile](https://guides.cocoapods.org/using/the-podfile.html): with your command-line interface, go to your Xcode project's base directory and [type `pod init`](https://guides.cocoapods.org/terminal/commands.html#pod_init).
    
3.  Open your Podfile and add the `OptimizelySDKiOS` pod.
    ```
    target 'Your App' do
      use_frameworks!
      pod 'OptimizelySDKiOS','1.5.1'
    end
    ```
    *   `Your App` = the name of your Xcode project
    *   To use `OptimizelySDKiOS` as a dynamic framework, make sure `use_frameworks!` is *not* commented out.
4.  Run [`pod install`](https://guides.cocoapods.org/terminal/commands.html#pod_install) from your Xcode project's base directory.


*Carthage and manual installation instructions can be found [here](/x/solutions/sdks/reference/index.html?language=objectivec&platform=mobile#installation).*

</div>

<div style="display: none" class="sdk-swift">

<div></div>

Our tvOS SDK is available through CocoaPods and Carthage. For Cocoapods installation, add `OptimizelySDKTVOS` to your Podfile.

```
target 'Your App' do
  use_frameworks!
  pod 'OptimizelySDKTVOS'
end
```

Make sure you have `use_frameworks!` uncommented to use OptimizelySDKTVOS as a dynamic framework.

Then run `pod install`.

<p>
Carthage installation instructions can be found [here](/x/solutions/sdks/reference/index.html?language=objectivec&platform=mobile#installation).
</p>

</div>
