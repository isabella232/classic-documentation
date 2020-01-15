---
template: multi-example
title: Experiments
anchor: activation
code_examples:
  python:
    lang: python
    request: |
      experiment_key = 'my_experiment'
      user_id = 'user123'

      # Conditionally activate an experiment for the provided user
      variation = optimizely_client.activate(experiment_key, user_id)

      if variation == 'control':
        # Execute code for control variation
      elif variation == 'treatment':
        # Execute code for treatment variation
      else:
        # Execute default code
  java:
    lang: java
    request: |
      String experimentKey = "my_experiment";
      String userId = "user123";

      // Conditionally activate an experiment for the provided user
      Variation variation = optimizelyClient.activate(experimentKey, userId);

      if (variation != null) {
          if (variation.is("control")) {
              // Execute code for control variation
          } else if (variation.is("treatment")) {
              // Execute code for treatment variation
          }
      } else {
          // Execute default code
      }
  csharp:
    lang: csharp
    request: |
      var experimentKey = "my_experiment";
      var userId = "user123";

      // Conditionally activate an experiment for the provided user
      var variation = OptimizelyClient.Activate(experimentKey, userId);

      if (variation != null)
      {
          if (variation == "control")
          {
              // Execute code for control variation
          }
          else if (variation == "treatment")
          {
              // Execute code for treatment variation
          }
      }
      else
      {
          // Execute default code
      }

  android:
    lang: java
    request: |

      OptimizelyClient optimizelyClient = optimizelyManager.getOptimizely();

      String experimentKey = "my_experiment";
      String userId = "user123";

      // Conditionally activate an experiment for the provided user
      Variation variation = optimizelyClient.activate(experimentKey, userId);

      if (variation != null) {
          if (variation.is("control")) {
              // Execute code for control variation
          } else if (variation.is("treatment")) {
              // Execute code for treatment variation
          }
      } else {
          // Execute default code
      }

  ruby:
    lang: ruby
    request: |
      experiment_key = 'my_experiment'
      user_id = 'user123'

      # Conditionally activate an experiment for the provided user
      variation = optimizely_client.activate(experiment_key, user_id)

      if variation == 'control'
        # Execute code for control variation
      elsif variation == 'treatment'
        # Execute code for treatment variation
      else
        # Execute default code
      end
  node:
    lang: javascript
    request: |
      var experimentKey = 'my_experiment';
      var userId = 'user123';

      // Conditionally activate an experiment for the provided user
      var variation = optimizelyClient.activate(experimentKey, userId);

      if (variation === 'control') {
        // Execute code for control variation
      } else if (variation === 'treatment') {
        // Execute code for treatment variation
      } else {
        // Execute default code
      }
  javascript:
    lang: javascript
    request: |
      var experimentKey = 'my_experiment';
      var userId = 'user123';

      // Conditionally activate an experiment for the provided user
      var variation = optimizelyClientInstance.activate(experimentKey, userId);

      if (variation === 'control') {
        // Execute code for control variation
      } else if (variation === 'treatment') {
        // Execute code for treatment variation
      } else {
        // Execute default code
      }
  php:
    lang: php
    request: |
      $experimentKey = 'my_experiment';
      $userId = 'user123';

      // Conditionally activate an experiment for the provided user
      $variation = $optimizelyClient->activate($experimentKey, $userId);

      if ($variation == 'control') {
        // Execute code for control variation
      } elseif ($variation == 'treatment') {
        // Execute code for treatment variation
      } else {
        # Execute default code
      }
 
  objectivec:
    lang: objectivec
    request: |
        // Conditionally activate an experiment for the provided user
        OPTLYVariation *variation = [optimizely activate:@"my_experiment" userId:@"user123"];

        if ([variation.variationKey isEqualToString:@"control"]) {
            // Execute code for control variation
        }
        else if ([variation.variationKey isEqualToString:@"treatment"]) {
            // Execute code for treatment variation
        }
        else {
            // Execute default code
        }

  swift:
    lang: swift
    request: |
        // Conditionally activate an experiment for the provided userId
        if let variation = optimizely?.activate("my_experiment", userId: "user123")
        {
            if (variation.variationKey == "control") {
                // Execute code for control variation
            }
            else if (variation.variationKey == "treatment") {
                // Execute code for treatment variation
            }
        } else {
            // Execute default code
        }
---

Use the `activate` function to run an experiment at any point in your code.

The `activate` function requires an *experiment key* and a *user ID*. The experiment key should match the experiment key you provide when [setting up the experiment](https://help.optimizely.com/Build_Campaigns_and_Experiments/Create_experiments_in_an_SDK_project) in the Optimizely web portal. The user ID is a string to uniquely identify the participant in the experiment (read more in [User IDs](#user-ids) below).

The `activate` function returns which variation the current user is assigned to. If the experiment is running and the user satisfies audience conditions for the experiment, the function returns a variation based on a deterministic murmur hash of the provided experiment key and user ID. This function also respects [whitelisting](#whitelisting) and and [user profiles](#profiles).

<div class="hidden" data-language-content="language" data-language="python">
If any of the conditions necessary for the experiment are not met, `activate` returns `None`.
</div>

<div class="hidden" data-language-content="language" data-language="java">
If any of the conditions necessary for the experiment are not met, `activate` returns `null`.
</div>

<div class="hidden" data-language-content="language" data-language="csharp">
If any of the conditions necessary for the experiment are not met, `activate` returns `null`.
</div>

<div class="hidden" data-language-content="language" data-language="ruby">
If any of the conditions necessary for the experiment are not met, `activate` returns `nil`.
</div>

<div class="hidden" data-language-content="language" data-language="javascript">
If any of the conditions necessary for the experiment are not met, `activate` returns `null`.
</div>

<div class="hidden" data-language-content="language" data-language="node">
If any of the conditions necessary for the experiment are not met, `activate` returns `null`.
</div>

<div class="hidden" data-language-content="language" data-language="php">
If any of the conditions necessary for the experiment are not met, `activate` returns `null`.
</div>

<div class="hidden" data-language-content="language" data-language="objectivec">
If any of the conditions necessary for the experiment are not met, `activate` returns `nil`.
</div>

<div class="hidden" data-language-content="language" data-language="swift">
If any of the conditions necessary for the experiment are not met, `activate` returns `nil`.
</div>

<div class="hidden" data-language-content="language" data-language="android">
If any of the conditions necessary for the experiment are not met, `activate` returns `null`.
</div>

<p><p>

Make sure that your code adequately deals with the case when the experiment is not activated i.e. execute the default variation.

The `activate` function also sends an event to Optimizely to record that the current user has been exposed to the experiment. You should call `activate` at the point you want to record an experiment exposure to Optimizely. If you don't want to record an experiment exposure, you can use an alternative function below to [get the variation](#variation).

<br>
