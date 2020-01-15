---
template: multi-example
title: Installation
anchor: installation
code_examples:
  python:
    lang: python
    request:
      pip install optimizely-sdk
  java:
    lang: java
    request: |
      repositories {
        jcenter()
      }

      dependencies {
        compile 'com.optimizely.ab:core-api:1.9.0'
        compile 'com.optimizely.ab:core-httpclient-impl:1.9.0'

        // The SDK integrates with multiple JSON parsers, here we use
        // Jackson.
        compile 'com.fasterxml.jackson.core:jackson-core:2.7.1'
        compile 'com.fasterxml.jackson.core:jackson-annotations:2.7.1'
        compile 'com.fasterxml.jackson.core:jackson-databind:2.7.1'
      }
  android:
    lang: java
    request: |
      repositories {
        jcenter()
      }

      dependencies {
        compile ('com.optimizely.ab:android-sdk:1.6.1') {
            // exclude default implementation of slf4j if you want to provide 
            // your own.  Multidex can fail if you have more than one 
            // implementation present. If you are having a multidex error
            // this is most likely the issue.
            exclude group: 'com.noveogroup.android', module:'android-logger'
        }

      }
  ruby:
    lang: ruby
    request: |
      gem install optimizely-sdk
  csharp:
    lang: csharp
    request: |
      Install-Package Optimizely.SDK
  node:
    lang: javascript
    request: |
      npm install optimizely-server-sdk --save
  php:
    lang: php
    request: |
      php composer.phar require optimizely/optimizely-sdk
  javascript:
    lang: javascript
    request: |
      npm install optimizely-client-sdk --save
  objectivec:
    lang: bash
    request: |
  swift:
    lang: bash
    request: |
---

<div></div>

<div class="hidden" data-language-content="language" data-language="python">

<div></div>

The Python SDK is distributed through [PyPi](https://pypi.python.org/pypi?name=optimizely-sdk&:action=display). To install, simply use `pip` or add `optimizely-sdk` to your `requirements.txt`.

</div>


<div class="hidden" data-language-content="language" data-language="java">

<div></div>

The Java SDK is distributed through Bintray. The `core-api` and `httpclient` Bintray packages are [optimizely-sdk-core-api](https://bintray.com/optimizely/optimizely/optimizely-sdk-core-api) and [optimizely-sdk-httpclient](https://bintray.com/optimizely/optimizely/optimizely-sdk-httpclient) respectively. You can find repository information as well as instructions on how to install the dependencies on Bintray. Gradle repository and dependency configurations are shown on the right. The SDK is compatible with *Java 1.6* and above.

`core-api` requires `org.slf4j:slf4j-api:1.7.16` and a *supported* JSON parser. We currently integrate with [Jackson](https://github.com/FasterXML/jackson), [GSON](https://github.com/google/gson), [json.org](http://www.json.org/), and [json-simple](https://code.google.com/archive/p/json-simple/). If multiple of these parsers are available at runtime, one will be used by `core-api` according to the aforementioned selection priority. If none of these packages are already provided in your project's classpath, one will need to be added.

`core-httpclient-impl` requires `org.apache.httpcomponents:httpclient:4.5.2` and provides an asynchronous event dispatcher which is described in the [Event Dispatcher](#event-dispatcher) section. This library isn't required and you may provide a custom `EventHandler` implementation which uses a different networking stack.

#### Code Shrinking

Building with Proguard enabled to shrink your application requires adding rules to preserve code that might otherwise be discarded. Add <a href="/assets/files/proguard-rules.pro" target="_blank">these rules</a> to your Proguard file, typically named `proguard-rules.pro`.
</div>

<div class="hidden" data-language-content="language" data-language="csharp">

<div></div>

The C# SDK is distributed through [NuGet](https://www.nuget.org/packages/Optimizely.SDK). To install, run the command shown in the <a href="https://docs.microsoft.com/en-us/nuget/tools/package-manager-console" target="_blank">Package Manager Console</a>.

</div>

<div class="hidden" data-language-content="language" data-language="ruby">

<div></div>

The gem for the Ruby SDK is distributed through [RubyGems](https://rubygems.org/gems/optimizely-sdk). To install, simply use `gem` or bundler to install the gem `optimizely-sdk`.

</div>


<div class="hidden" data-language-content="language" data-language="node">

<div></div>

The Node SDK is distributed through [npm](https://www.npmjs.com/package/optimizely-server-sdk). To install, simply run `npm install optimizely-server-sdk --save`.

</div>


<div class="hidden" data-language-content="language" data-language="javascript">

<div></div>

The JavaScript SDK is distributed through [npm](https://www.npmjs.com/package/optimizely-client-sdk). To install, simply run `npm install optimizely-client-sdk --save`.

If you aren't able to install via `npm` or to use the SDK in a non-CommonJS fashion, follow the [instructions in the SDK's README](https://github.com/optimizely/javascript-sdk) to build a minified snippet.

</div>


<div class="hidden" data-language-content="language" data-language="php">

<div></div>

Our PHP SDK is available through [Composer](https://getcomposer.org/). To install simply `composer require optimizely/optimizely-sdk` or add `optimizely/optimizely-sdk` in the `require` section of your `composer.json`.

#### Requirements
* PHP 5.5+

</div>


<div class="hidden" data-language-content="language" data-language="objectivec">

<div></div>

Our iOS and tvOS SDKs are available for distribution through CocoaPods, Carthage, or manual installation.

#### Requirements
* iOS 8.0+ or tvOS 9.0+

Please note below that ```<platform>``` is used to represent the platform on which you are building your app. Currently, we support iOS and tvOS platforms. You should be pinning your dependency to a major or minor of the SDK to avoid breaking changes (from major version bumps) from affecting your build.

#### Cocoapods

1. Add the following line to the _Podfile_:

    ```
    pod 'OptimizelySDKiOS','1.5.1'
    ```

    Alternatively, if you are developing on tvOS, use:

    ```
    pod 'OptimizelySDKTVOS', '1.5.1'
    ```

    Make sure `use_frameworks!` is also included in the Podfile:

    ```bash
    target 'Your App' do
        use_frameworks!
        pod 'OptimizelySDKiOS','1.5.1'
    end
   ```

2. Run the following command:
    ```bash
    pod install
    ```

Further installation instructions through Cocoapods can be found [here](https://guides.cocoapods.org/using/getting-started.html).

#### Carthage

1. Add the following lines to the _Cartfile_:
```bash
github "optimizely/objective-c-sdk" "1.5.1"
```

2. Run the following command:
```bash
carthage update
```

3. Link the frameworks to your project. Go to your project target's **Link Binary With Libraries** and drag over the following from the _Carthage/Build/&lt;platform&gt;_ folder:
<pre>
OptimizelySDKCore.framework
OptimizelySDKDatafileManager.framework
OptimizelySDKEventDispatcher.framework
OptimizelySDKShared.framework
OptimizelySDKUserProfileService.framework
OptimizelySDK&lt;platform&gt;.framework
</pre>

4. To ensure that proper bitcode-related files and dSYMs are copied when archiving your app, you will need to install a Carthage build script:
      - Add a new **Run Script** phase in your target's **Build Phase**.</br></br>
      - In the script area include:</br>
```
/usr/local/bin/carthage copy-frameworks
```
      - Add the frameworks to the **Input Files** list:</br>
<pre>
$(SRCROOT)/Carthage/Build/&lt;platform&gt;/OptimizelySDKCore.framework
$(SRCROOT)/Carthage/Build/&lt;platform&gt;/OptimizelySDKDatafileManager.framework
$(SRCROOT)/Carthage/Build/&lt;platform&gt;/OptimizelySDKEventDispatcher.framework
$(SRCROOT)/Carthage/Build/&lt;platform&gt;/OptimizelySDKShared.framework
$(SRCROOT)/Carthage/Build/&lt;platform&gt;/OptimizelySDKUserProfileService.framework
$(SRCROOT)/Carthage/Build/&lt;platform&gt;/OptimizelySDK<platform>.framework
</pre>

Futher installation instructions through Carthage can be found [here](https://github.com/Carthage/Carthage).

#### Manual Installation

The universal framework can be used in an application without the need for a third-party dependency manager. The universal framework packages up all Optimizely X Mobile modules, which include:
<pre>
OptimizelySDKCore
OptimizelySDKShared
OptimizelySDKDatafileManager
OptimizelySDKEventDispatcher
OptimizelySDKUserProfileService
</pre>

The universal framework for iOS includes builds for the following architectures:
<pre>
i386
x86_64
ARMv7
ARMv7s
ARM64
</pre>

The universal framework for tvOS includes build for the following architectures:
<pre>
x86_64
ARM64
</pre>

Bitcode is enabled for both the iOS and tvOS universal frameworks.

In order to install the universal framework, follow the steps below:

1. Download the [iOS](https://github.com/optimizely/objective-c-sdk/blob/master/OptimizelySDKUniversal/generated-frameworks/Release-iOS-universal-SDK/OptimizelySDKiOS.framework.zip) or [tvOS](https://github.com/optimizely/objective-c-sdk/blob/master/OptimizelySDKUniversal/generated-frameworks/Release-tvOS-universal-SDK/OptimizelySDKTVOS.framework.zip) framework.

2. Unzip the framework, then drag the framework to your project in Xcode. Xcode should prompt you to select a target. Go to **Build Phases** and make sure that the framework is under the **Link Binary with Libraries** section.

3. Go to the **General** tab and add the framework to the **Embedded Binaries** section. If the **Embedded Binaries** section is not visible, add the framework in the **Copy Files** section (you can add this section in **Build Settings**).

4. The Apple store will reject your app if you have the universal framework installed as it includes simulator binaries. Therefore, a script to strip the extra binaries needs to be run before you upload the app. To do this, go to **Build Phases** and add a **Run Script** section by clicking the ```+``` symbol. Copy and paste the following script (make sure you replace the ```FRAMEWORK_NAME``` with the proper framework name):
```
FRAMEWORK="FRAMEWORK_NAME"
FRAMEWORK_EXECUTABLE_PATH="${BUILT_PRODUCTS_DIR}/${FRAMEWORKS_FOLDER_PATH}/$FRAMEWORK.framework/$FRAMEWORK"
EXTRACTED_ARCHS=()
for ARCH in $ARCHS
do
    lipo -extract "$ARCH" "$FRAMEWORK_EXECUTABLE_PATH" -o "$FRAMEWORK_EXECUTABLE_PATH-$ARCH"
    EXTRACTED_ARCHS+=("$FRAMEWORK_EXECUTABLE_PATH-$ARCH")
done
lipo -o "$FRAMEWORK_EXECUTABLE_PATH-merged" -create "${EXTRACTED_ARCHS[@]}"
rm "${EXTRACTED_ARCHS[@]}"
rm "$FRAMEWORK_EXECUTABLE_PATH"
mv "$FRAMEWORK_EXECUTABLE_PATH-merged" "$FRAMEWORK_EXECUTABLE_PATH"
```

If you choose to build the universal framework yourself, you can do so by building the _OptimizelySDKiOS-Universal_ or _OptimizelySDKTVOS-Universal_ schemes. Our third-party dependencies, which are pulled in as Git submodules, would need to be updated. To do so run the following commands:
```
git submodule init
```
followed by:
```
git submodule update
```
After building these schemes, the frameworks are output in the **OptimizelySDKUniversal/generated-frameworks** folder.
</div>


<div class="hidden" data-language-content="language" data-language="swift">

<div></div>

Our iOS and tvOS SDKs are available for distribution through CocoaPods, Carthage, or manual installation.

#### Requirements
* iOS 8.0+ or tvOS 9.0+

Please note below that ```<platform>``` is used to represent the platform on which you are building your app. Currently, we support iOS and tvOS platforms.

#### Cocoapods

1. Add the following line to the _Podfile_:

    ```
    pod 'OptimizelySDKiOS','1.5.1'
    ```

    Alternatively, if you are developing on tvOS, use:

    ```
    pod 'OptimizelySDKTVOS'
    ```

    Make sure `use_frameworks!` is also included in the Podfile:

    ```bash
    target 'Your App' do
        use_frameworks!
        pod 'OptimizelySDKiOS','1.5.1'
    end
   ```

2. Run the following command:
    ```bash
    pod install
    ```

Further installation instructions through Cocoapods can be found [here](https://guides.cocoapods.org/using/getting-started.html).

#### Carthage

1. Add the following lines to the _Cartfile_:
```bash
github "optimizely/objective-c-sdk" "1.5.1"
```

2. Run the following command:
```bash
carthage update
```

3. Link the frameworks to your project. Go to your project target's **Link Binary With Libraries** and drag over the following from the _Carthage/Build/&lt;platform&gt;_ folder:
<pre>
OptimizelySDKCore.framework
OptimizelySDKDatafileManager.framework
OptimizelySDKEventDispatcher.framework
OptimizelySDKShared.framework
OptimizelySDKUserProfileService.framework
OptimizelySDK&lt;platform&gt;.framework
</pre>

4. To ensure that proper bitcode-related files and dSYMs are copied when archiving your app, you will need to install a Carthage build script:
      - Add a new **Run Script** phase in your target's **Build Phase**.</br></br>
      - In the script area include:</br>
```
/usr/local/bin/carthage copy-frameworks
```
      - Add the frameworks to the **Input Files** list:</br>
<pre>
$(SRCROOT)/Carthage/Build/&lt;platform&gt;/OptimizelySDKCore.framework
$(SRCROOT)/Carthage/Build/&lt;platform&gt;/OptimizelySDKDatafileManager.framework
$(SRCROOT)/Carthage/Build/&lt;platform&gt;/OptimizelySDKEventDispatcher.framework
$(SRCROOT)/Carthage/Build/&lt;platform&gt;/OptimizelySDKShared.framework
$(SRCROOT)/Carthage/Build/&lt;platform&gt;/OptimizelySDKUserProfileService.framework
$(SRCROOT)/Carthage/Build/&lt;platform&gt;/OptimizelySDK<platform>.framework
</pre>

Futher installation instructions through Carthage can be found [here](https://github.com/Carthage/Carthage).

#### Manual Installation

The universal framework can be used in an application without the need for a third-party dependency manager. The universal framework packages up all Optimizely X Mobile modules, which include:
<pre>
OptimizelySDKCore
OptimizelySDKShared
OptimizelySDKDatafileManager
OptimizelySDKEventDispatcher
OptimizelySDKUserProfileService
</pre>

The universal framework for iOS includes builds for the following architectures:
<pre>
i386
x86_64
ARMv7
ARMv7s
ARM64
</pre>

The universal framework for tvOS includes build for the following architectures:
<pre>
x86_64
ARM64
</pre>

Bitcode is enabled for both the iOS and tvOS universal frameworks.

In order to install the universal framework, follow the steps below:

1. Download the [iOS](https://github.com/optimizely/objective-c-sdk/blob/master/OptimizelySDKUniversal/generated-frameworks/Release-iOS-universal-SDK/OptimizelySDKiOS.framework.zip) or [tvOS](https://github.com/optimizely/objective-c-sdk/blob/master/OptimizelySDKUniversal/generated-frameworks/Release-tvOS-universal-SDK/OptimizelySDKTVOS.framework.zip) framework.

2. Unzip the framework, then drag the framework to your project in Xcode. Xcode should prompt you to select a target. Go to **Build Phases** and make sure that the framework is under the **Link Binary with Libraries** section.

3. Go to the **General** tab and add the framework to the **Embedded Binaries** section. If the **Embedded Binaries** section is not visible, add the framework in the **Copy Files** section (you can add this section in **Build Settings**).

4. The Apple store will reject your app if you have the universal framework installed as it includes simulator binaries. Therefore, a script to strip the extra binaries needs to be run before you upload the app. To do this, go to **Build Phases** and add a **Run Script** section by clicking the ```+``` symbol. Copy and paste the following script (make sure you replace the ```FRAMEWORK_NAME``` with the proper framework name):
```
FRAMEWORK="FRAMEWORK_NAME"
FRAMEWORK_EXECUTABLE_PATH="${BUILT_PRODUCTS_DIR}/${FRAMEWORKS_FOLDER_PATH}/$FRAMEWORK.framework/$FRAMEWORK"
EXTRACTED_ARCHS=()
for ARCH in $ARCHS
do
    lipo -extract "$ARCH" "$FRAMEWORK_EXECUTABLE_PATH" -o "$FRAMEWORK_EXECUTABLE_PATH-$ARCH"
    EXTRACTED_ARCHS+=("$FRAMEWORK_EXECUTABLE_PATH-$ARCH")
done
lipo -o "$FRAMEWORK_EXECUTABLE_PATH-merged" -create "${EXTRACTED_ARCHS[@]}"
rm "${EXTRACTED_ARCHS[@]}"
rm "$FRAMEWORK_EXECUTABLE_PATH"
mv "$FRAMEWORK_EXECUTABLE_PATH-merged" "$FRAMEWORK_EXECUTABLE_PATH"
```

If you choose to build the universal framework yourself, you can do so by building the _OptimizelySDKiOS-Universal_ or _OptimizelySDKTVOS-Universal_ schemes. Our third-party dependencies, which are pulled in as Git submodules, would need to be updated. To do so run the following commands:
```
git submodule init
```
followed by:
```
git submodule update
```
After building these schemes, the frameworks are output in the **OptimizelySDKUniversal/generated-frameworks** folder.
</div>

<div class="hidden" data-language-content="language" data-language="android">

<div></div>

The Android SDK packages are available on Jcenter:

* **[android-sdk](https://bintray.com/optimizely/optimizely/optimizely-sdk-android)**: Includes all modules
* [datafile-handler](https://bintray.com/optimizely/optimizely/optimizely-sdk-android-datafile-handler): Datafile download, caching and background services.
* [event-handler](https://bintray.com/optimizely/optimizely/optimizely-sdk-android-event-handler): Dispatches decision and track events to Optimizely
* [user-profile](https://bintray.com/optimizely/optimizely/optimizely-sdk-android-user-profile): Makes bucketing persistent
* [shared](https://bintray.com/optimizely/optimizely/optimizely-sdk-android-shared): Shared code between all modules

The `android-sdk` module transitively depends on the `datafile-handler`, `event-handler`, `user-profile`, and `shared` modules. It also includes the latest version of gson and slf4j logger. Gradle can be used to exclude any dependency if you want to replace one with another version or implementation.

To add the `android-sdk` and all modules to your project simply include the following in your app's `build.gradle` in the `dependencies` block:

```
compile 'com.optimizely.ab:android-sdk:1.6.1'
```
To exclude the default implementation of parser and slf4j like this:

```
compile ('com.optimizely.ab:android-sdk:1.6.1') {
        exclude group: 'com.google.code.gson', module:'gson'
        exclude group: 'com.noveogroup.android', module:'android-logger'
}
```

Check [android-sdk](https://bintray.com/optimizely/optimizely/optimizely-sdk-android) repo on Bintray to determine the latest version. Please note, you should be pinning your dependency to a major or minor of the SDK to avoid breaking changes (from major version bumps) from affecting your build.

Also checkout the [test-app](https://github.com/optimizely/android-sdk/tree/master/test-app) in the sdk repo.

#### Code Shrinking

Building with Proguard enabled to shrink your application requires adding rules to preserve code that might otherwise be discarded. Add <a href="/assets/files/proguard-rules.pro" target="_blank">these rules</a> to your Proguard file, typically named `proguard-rules.pro`.
* Note: As of Android SDK 1.4.0 consumer proguard rules are supplied by the sdk so you don't have to implement these.
</div>

<br>
