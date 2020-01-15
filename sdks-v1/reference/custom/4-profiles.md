---
template: multi-example
title: User Profile Service
anchor: profiles
code_examples:
  android:
    lang: java
    request: |
      import com.optimizely.ab.bucketing.UserProfileService;
      import java.util.Map;
      import java.util.concurrent.ConcurrentHashMap;
      
      // You can optionally provide an override to the default user profile service
      // below is an example override that is very thread safe but not persistent.
      UserProfileService userProfileService = new  UserProfileService() {
          ConcurrentHashMap<String, ConcurrentHashMap<String, Object>> userMap = new ConcurrentHashMap<>();

          @Override
          public Map<String, Object> lookup(String userId) throws Exception {
              return userMap.get(userId);
          }

          @Override
          public void save(Map<String, Object> userProfile) throws Exception {
              String userId = (String) userProfile.get("user_id");
              if (userId != null) {
                  ConcurrentHashMap<String, Object> concurrentInnerMap = new ConcurrentHashMap<>(userProfile);
                  userMap.put(userId, concurrentInnerMap);
              }
          }
      };


      Optimizely optimizelyClient = Optimizely.builder("project_id_string")
          .withUserProfile(userProfileService)
          .build(getApplicationContext());

  java:
    lang: java
    request: |
      import com.optimizely.ab.bucketing.UserProfileService;
      import java.util.Map;
      
      // You can optionally provide an override to the default user profile service
      UserProfileService userProfileService = new  UserProfileService() {

          @Override
          public Map<String, Object> lookup(String userId) throws Exception {
              // noop
              return null;
          }

          @Override
          public void save(Map<String, Object> userProfile) throws Exception {
              // noop
          }
      };


      Optimizely optimizelyClient = Optimizely.builder("project_id_string", MyEventHandler)
          .withUserProfileService(userProfileService)
          .build();

  javascript:
    lang: javascript
    request: |
      var optimizely = require('optimizely-client-sdk');

      // Sample user profile service implementation
      var userProfileService = {
        lookup: function(userId) {
          // perform user profile lookup
        },
        save: function(userProfileMap) {
          // persist user profile
        }
      };

      var datafile; // your project's datafile
      var optimizelyClient = optimizely.createInstance({
        datafile: datafile,
        userProfileService: userProfileService,
      });

  node:
    lang: javascript
    request: |
      var optimizely = require('optimizely-server-sdk');

      // Sample user profile service implementation
      var userProfileService = {
        lookup: function(userId) {
          // perform user profile lookup
        },
        save: function(userProfileMap) {
          // persist user profile
        }
      };

      var datafile; // your project's datafile
      var optimizelyClient = optimizely.createInstance({
        datafile: datafile,
        userProfileService: userProfileService,
      });

  objectivec:
    lang: objectivec
    request: |
      CustomUserProfile *customUserProfile = [[CustomUserProfile alloc] init];

      // initialize your Manager (settings will propagate to OPTLYClient and Optimizely)
      OPTLYManager *manager = [OPTLYManager init:^(OPTLYManagerBuilder * _Nullable builder) {
        builder.projectId = kProjectId;
        builder.userProfile = userProfile;
      }];

  php:
    lang: php
    request: |
      use Optimizely\Logger\DefaultLogger;
      use Optimizely\UserProfile\UserProfileServiceInterface;
      use Optimizely\Optimizely;

      class UserProfileService implements UserProfileServiceInterface
      {
        public function lookup($userId)
        {
          // perform user profile lookup
        }

        public function save($userProfileMap) {
          // persist user profile
        }
      }

      $datafile = {}; // your project's datafile
      $optimizelyClient = new Optimizely(
        $datafile,
        null,
        new DefaultLogger(),
        null,
        false,
        new UserProfileService()
      );

  python:
    lang: python
    request: |
      from optimizely import user_profile

      class MyUserProfileService(user_profile.UserProfileService):
        def lookup(self, user_id):
          # Retrieve and return user profile
        def save(self, user_profile):
          # Save user profile

      optimizely_client = optimizely.Optimizely(datafile, user_profile_service=MyUserProfileService())

  ruby:
    lang: ruby
    request: |
      # Sample user profile service implementation
      class UserProfileService
        def lookup(user_id)
          # retrieve user profile
        end

        def save(user_profile)
          # save user profile
        end
      end

      optimizely_client = Optimizely::Project.new(datafile,
                                                  Optimizely::EventDispatcher.new,
                                                  Optimizely::NoOpLogger.new,
                                                  nil,
                                                  false,
                                                  UserProfileService.new)

  csharp:
    lang: csharp
    request: |
      using OptimizelySDK.Bucketing;

      class InMemoryUserProfileService : UserProfileService
      {
        private Dictionary<String, Dictionary<string, object>> userProfiles = new Dictionary<String, Dictionary<string, object>>();
        Dictionary<string, object> UserProfileService.Lookup(string userId)
        {
          // Retrieve and return user profile
        }

        void UserProfileService.Save(Dictionary<string, object> userProfile)
        {
          // Save user profile
        }
      }

      var userProfileService = new InMemoryUserProfileService();
      Optimizely OptimizelyClient = new Optimizely(
          datafile: datafileJSON,
          userProfileService: userProfileService);

  swift:
    lang: swift
    request: |
      let customUserProfile: CustomUserProfile? = CustomUserProfile.init()

      // initialize your Manager (settings will propagate to OPTLYClient and Optimizely)
      let manager: OPTLYManager? =  OPTLYManager.init({ (builder) in
        builder!.projectId = projectId
        builder!.userProfile = customUserProfile
      })
---

Use a *user profile service* to persist information about your users and ensure variation assignments are sticky. For example, if you are working on a backend website, you can create an implementation that reads and saves user profiles from a Redis or memcached store.

Implementing a user profile service is optional and is only necessary if you want to keep variation assignments sticky even when experiment conditions are changed while it is running (e.g. audiences, attributes, variation pausing, traffic distribution). For more information on user profiles and how they used by the SDK, see this [Optiverse article](https://help.optimizely.com/Set_Up_Optimizely/How_Optimizely's_SDKs_work/The_Optimizely_SDKs%3A_How_they_work).

<div class="hidden" data-language-content="language" data-language="python">

<div></div>

To use, you must provide an implementation of the `UserProfileService` that exposes two functions with the following signatures below.

* *lookup*: Takes a `user_id` string and returns a user profile dict.
* *save*: Takes a `user_profile` dict and persists it.

<!-- The next section is language agnostic and we can use throughout once we release all SDKs.-->
The following is the JSON schema for the user profile map:
```
{
  "title": "UserProfile",
  "type": "object",
  "properties": {
    "user_id": {"type": "string"},
    "experiment_bucket_map": {"type": "object",
                              "patternProperties": {
                                "^[a-zA-Z0-9]+$": {"type": "object",
                                                   "properties": {"variation_id": {"type":"string"}},
                                                   "required": ["variation_id"]}
                              },
                             }
  },
  "required": ["user_id", "experiment_bucket_map"]
}
```

The SDK uses the user profile service you provide to override Optimizely's default bucketing behavior in cases when an experiment assignment has been saved.

When implementing your own `UserProfileService` we recommend loading the user profiles into the user profile service on initialization and avoiding performing expensive, blocking lookups on the `lookup` function to minimize the performance impact of incorporating the `UserProfileService`.
</div>

<div class="hidden" data-language-content="language" data-language="java">
Unlike our client-side SDKs, our Java SDK does not currently manage user state. If you would like to persist data about your users between requests (e.g. unique identifiers, user attributes, bucketing decisions) you can store this state in the client or in your own custom datastore. The UserProfileService is available in Optimizely Java SDK 1.7.0.

<div></div>

To use, you must provide an implementation of the `UserProfileService` that exposes two functions with the following signatures below.

* *lookup*: Takes a `user_id` string and returns a user profile dict.
* *save*: Takes a `user_profile` dict and persists it.

<!-- The next section is language agnostic and we can use throughout once we release all SDKs.-->
The following is the JSON schema for the user profile map:
```
{
  "title": "UserProfile",
  "type": "object",
  "properties": {
    "user_id": {"type": "string"},
    "experiment_bucket_map": {"type": "object",
                              "patternProperties": {
                                "^[a-zA-Z0-9]+$": {"type": "object",
                                                   "properties": {"variation_id": {"type":"string"}},
                                                   "required": ["variation_id"]}
                              },
                             }
  },
  "required": ["user_id", "experiment_bucket_map"]
}
```

The SDK uses the user profile service you provide to override Optimizely's default bucketing behavior in cases when an experiment assignment has been saved.

When implementing your own `UserProfileService` we recommend loading the user profiles into the user profile service on initialization and avoiding performing expensive, blocking lookups on the `lookup` function to minimize the performance impact of incorporating the `UserProfileService`.

For full details, check out our user profile service interface [here](https://github.com/optimizely/java-sdk/blob/master/core-api/src/main/java/com/optimizely/ab/bucketing/UserProfileService.java)
</div>

<div class="hidden" data-language-content="language" data-language="csharp">

<div></div>

To use, you must provide an implementation of the `UserProfileService` that exposes two functions with the following signatures below.

* *Lookup*: Takes a `userId` string and returns a user profile dictionary.
* *Save*: Takes a `userProfile` dictionary and persists it.

<!-- The next section is language agnostic and we can use throughout once we release all SDKs.-->
The following is the JSON schema for the user profile dictionary:
```
{
  "title": "UserProfile",
  "type": "object",
  "properties": {
    "user_id": {"type": "string"},
    "experiment_bucket_map": {"type": "object",
                              "patternProperties": {
                                "^[a-zA-Z0-9]+$": {"type": "object",
                                                   "properties": {"variation_id": {"type":"string"}},
                                                   "required": ["variation_id"]}
                              },
                             }
  },
  "required": ["user_id", "experiment_bucket_map"]
}
```

The SDK uses the user profile service you provide to override Optimizely's default bucketing behavior in cases when an experiment assignment has been saved.

When implementing your own `UserProfileService` we recommend loading the user profiles into the user profile service on initialization and avoiding performing expensive, blocking lookups on the `Lookup` function to minimize the performance impact of incorporating the `UserProfileService`.

</div>

<div class="hidden" data-language-content="language" data-language="ruby">

<div></div>

To use, you must provide an implementation of the `UserProfileService` that exposes two functions, `lookup` and `save`, with the following signatures.

* *lookup*: Takes a string `userId` and returns the corresponding user profile Hash.
* *save*: Takes a Hash user profile and persists it.

<!-- The next section is language agnostic and we can use throughout once we release all SDKs.-->
The following is the JSON schema for the user profile map:
```
{
  "title": "UserProfile",
  "type": "object",
  "properties": {
    "user_id": {"type": "string"},
    "experiment_bucket_map": {"type": "object",
                               "patternProperties": {
                                 "^[a-zA-Z0-9]+$": {"type": "object",
                                                    "properties": {"variation_id": {"type":"string"}},
                                                    "required": ["variation_id"]}
                               },
                             }
  },
  "required": ["user_id", "experiment_bucket_map"]
}
```
</div>

<div class="hidden" data-language-content="language" data-language="node">

<div></div>

To use, you must provide an implementation of the `UserProfileService` that exposes two functions with the following signatures below.

* *lookup*: Takes a `userId` string and returns a user profile map.
* *save*: Takes a user profile map and persists it.

<!-- The next section is language agnostic and we can use throughout once we release all SDKs.-->
The following is the JSON schema for the user profile map:
```
{
  "title": "UserProfile",
  "type": "object",
  "properties": {
    "user_id": {"type": "string"},
    "experiment_bucket_map": {"type": "object",
                               "patternProperties": {
                                 "^[a-zA-Z0-9]+$": {"type": "object",
                                                    "properties": {"variation_id": {"type":"string"}},
                                                    "required": ["variation_id"]}
                               },
                             }
  },
  "required": ["user_id", "experiment_bucket_map"]
}
```

The SDK uses the user profile service you provide to override Optimizely's default bucketing behavior in cases when an experiment assignment has been saved.

When implementing your own `UserProfileService` we recommend loading the user profiles into the user profile service on initialization and avoiding performing expensive, blocking lookups on the `lookup` function to minimize the performance impact of incorporating the `UserProfileService`.
</div>

<div class="hidden" data-language-content="language" data-language="javascript">

<div></div>

To use, you must provide an implementation of the `UserProfileService` that exposes two functions with the following signatures below.

* *lookup*: Takes a `userId` string and returns a user profile object.
* *save*: Takes a user profile object and persists it.

<!-- The next section is language agnostic and we can use throughout once we release all SDKs.-->
The following is the JSON schema for the user profile object:
```
{
  "title": "UserProfile",
  "type": "object",
  "properties": {
    "user_id": {"type": "string"},
    "experiment_bucket_map": {"type": "object",
                               "patternProperties": {
                                 "^[a-zA-Z0-9]+$": {"type": "object",
                                                    "properties": {"variation_id": {"type":"string"}},
                                                    "required": ["variation_id"]}
                               },
                             }
  },
  "required": ["user_id", "experiment_bucket_map"]
}
```

The SDK uses the user profile service you provide to override Optimizely's default bucketing behavior in cases when an experiment assignment has been saved.

When implementing your own `UserProfileService` we recommend loading the user profiles into the user profile service on initialization and avoiding performing expensive, blocking lookups on the `lookup` function to minimize the performance impact of incorporating the `UserProfileService`.
</div>

<div class="hidden" data-language-content="language" data-language="php">

<div></div>

To use, you must provide an implementation of the `UserProfileService` that exposes two functions with the following signatures below.

* *lookup*: Takes a `$userId` string and returns a user profile map.
* *save*: Takes a `$userProfileMap` and persists it.

<!-- The next section is language agnostic and we can use throughout once we release all SDKs.-->
The following is the JSON schema for the user profile map:
```
{
  "title": "UserProfile",
  "type": "object",
  "properties": {
    "user_id": {"type": "string"},
    "experiment_bucket_map": {"type": "object",
                              "patternProperties": {
                                "^[a-zA-Z0-9]+$": {"type": "object",
                                                   "properties": {"variation_id": {"type":"string"}},
                                                   "required": ["variation_id"]}
                              },
                             }
  },
  "required": ["user_id", "experiment_bucket_map"]
}
```

The SDK uses the user profile service you provide to override Optimizely's default bucketing behavior in cases when an experiment assignment has been saved.

When implementing your own `UserProfileService` we recommend loading the user profiles into the user profile service on initialization and avoiding performing expensive, blocking lookups on the `lookup` function to minimize the performance impact of incorporating the `UserProfileService`.
</div>


<div class="hidden" data-language-content="language" data-language="android">

<div></div>

The `UserProfileService` interface implementation can be used for persisting information about your users in a local profile. You can provide your own `UserProfileService` implementation if you’d like to change what user information is persisted or how data is stored on the device. The code at right shows how to include your own user profile implementation when constructing an Optimizely client.

Our default `UserProfileService` implementation, `DefaultUserProfileService`, stores data on which experiments and variations have historically been activated for a user.  The Optimizely client uses the supplied user profile to ensure that experiment bucketing is *sticky*, i.e. the user will always be exposed to the same variation on subsequent sessions in the app, even in the case where the experiment is paused or traffic allocation is changed. We plan to expand our implementation in future to include more information about users, including user IDs and attributes.

The `UserProfileService` interface contains the following methods:

* *save:* Takes a `userId`, `experimentId`, and `variationId` and saves this information on the device.
* *lookup:* Takes a `userId` and `experimentId`, and returns the `variationId` that was recorded previously if it exists.
* *remove:* Takes a `userId` and `experimentId`, and deletes the mapping to the variation if it exists.

For full details, check out our user profile interface [here](https://github.com/optimizely/java-sdk/blob/master/core-api/src/main/java/com/optimizely/ab/bucketing/UserProfileService.java) and our default implementation [here](https://github.com/optimizely/android-sdk/blob/master/user-profile/src/main/java/com/optimizely/ab/android/user_profile/DefaultUserProfileService.java).

</div>


<div class="hidden" data-language-content="language" data-language="objectivec">

<div></div>

The `OPTLYUserProfileService` class is used for persisting information about users. You can provide your own `OPTLYUserProfileService` implementation if you want to change what user information is saved or how data is stored on the device. The code at right shows how to include your own user profile implementation when constructing an Optimizely manager.

The default `OPTLYUserProfileService` implementation, `OptimizelySDKUserProfileService`, stores data on which experiments and variations a user has been exposed to.  The Optimizely client uses the supplied user profile service to ensure that experiment bucketing is sticky. We plan to expand our implementation in the future to include more information about users, including attributes.

The `OPTLYUserProfileService` interface contains the following methods:

```
- (NSDictionary *)lookup:(NSString *)userId;
- (void)save:(NSDictionary *)userProfile
```

* *lookup* Fetches a user profile entity corresponding to the specified user ID
* *save* Saves a user profile entity

The user profile entity is a dictionary that contains the user ID and a map of all experiment-to-variation combinations a user has seen. For example, 

```
{
    "userID" : "userID123",
    "experimentBucketMap" : {
        "experimentID1" : {
            "variationKey1" : "variationID1"
        },
        "experimentID2" : {
            "variationKey2" : "variationID2"
        }
    }
}
```

For full details, check out our user profile [interface](https://github.com/optimizely/objective-c-sdk/blob/master/OptimizelySDKCore/OptimizelySDKCore/OPTLYUserProfileServiceBasic.h) and our default [implementation](https://github.com/optimizely/objective-c-sdk/blob/master/OptimizelySDKUserProfileService/OptimizelySDKUserProfileService/OPTLYUserProfileService.m).

</div>


<div class="hidden" data-language-content="language" data-language="swift">

<div></div>

The `OPTLYUserProfileService` class is used for persisting information about users. You can provide your own `OPTLYUserProfileService` implementation if you want to change what user information is saved or how data is stored on the device. The code at right shows how to include your own user profile implementation when constructing an Optimizely manager.

The default `OPTLYUserProfileService` implementation, `OptimizelySDKUserProfileService`, stores data on which experiments and variations a user has been exposed to.  The Optimizely client uses the supplied user profile service to ensure that experiment bucketing is sticky. We plan to expand our implementation in the future to include more information about users, including user IDs and attributes.

The `OPTLYUserProfileService` interface contains the following methods:

```
- (NSDictionary *)lookup:(NSString *)userId;
- (void)save:(NSDictionary *)userProfile
```

* *lookup* Fetches a user profile entity corresponding to the specified user ID
* *save* Saves a user profile entity

The user profile entity is a dictionary that contains the user ID and a map of all experiment-to-variation combinations a user has seen. For example, 

```
{
    "userID" : "userID123",
    "experimentBucketMap" : {
        "experimentID1" : {
            "variationKey1" : "variationID1"
        },
        "experimentID2" : {
            "variationKey2" : "variationID2"
        }
    }
}

For full details, check out our user profile [interface](https://github.com/optimizely/objective-c-sdk/blob/master/OptimizelySDKCore/OptimizelySDKCore/OPTLYUserProfileServiceBasic.h) and our default [implementation](https://github.com/optimizely/objective-c-sdk/blob/master/OptimizelySDKUserProfileService/OptimizelySDKUserProfileService/OPTLYUserProfileService.m).

</div>

<br>
