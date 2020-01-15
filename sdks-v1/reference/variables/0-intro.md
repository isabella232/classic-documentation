---
template: multi-example
title: Variables
anchor: variables
code_examples:
  objectivec:
    lang: objectivec
    request: |
      // Get the value of a boolean variable
      bool myVariable = [optimizely variableBoolean: @"myVariable"
                                            userId: userId]
                                 activateExperiment: true];

       // Get the value of a double variable
       double myVariable = [optimizely variableDouble: @"myVariable"
                                               userId: userId
                                   activateExperiment: true];

       // Get the value of an integer variable
       int myVariable = [optimizely variableInteger: @"myVariable"
                                             userId: userId
                                 activateExperiment: true];

       // Get the value of a string variable
       NSString *myVariable = [optimizely variableString: @"myVariable"
                                                  userId: userId
                                      activateExperiment: true];
  swift:
    lang: swift
    request: |
      // Get the value of a boolean variable
      let myVariable = optimizely?.variableBoolean("myVariable",
                                                    userId: "user123",
                                                    attributes: nil,
                                                    activateExperiment: true)

      // Get the value of a double variable
      let myVariable = optimizely?.variableDouble("myVariable",
                                                   userId: "user123",
                                                   attributes: nil,
                                                   activateExperiment: true)

      // Get the value of an integer variable
       let myVariable = optimizely?.variableInteger("myVariable",
                                                   userId: "user123",
                                                   attributes: nil,
                                                   activateExperiment: true)

      // Get the value of a string variable
      let myVariable = optimizely?.variableString("myVariable",
                                                   userId: "user123",
                                                   attributes: nil,
                                                   activateExperiment: true)
  android:
    lang: java
    request: |
      String userId = "user123";

      // Get the value of a Boolean variable
      Boolean myVariable = optimizelyClient.getVariableBoolean("myVariable",
                                                               userId,
                                                               true);

      // Get the value of a floating point variable
      Float myVariable = optimizelyClient.getVariableFloat("myVariable",
                                                            userId,
                                                            true);

      // Get the value of an integer variable
      Integer myVariable = optimizelyClient.getVariableInteger("myVariable",
                                                                userId,
                                                                true);

      // Get the value of a string variable
      String myVariable = optimizelyClient.getVariableString("myVariable",
                                                             userId,
                                                             true);
---

Live Variables are supported in the mobile SDKs.


<div class="hidden" data-language-content="language" data-language="android">
Use *Live Variables* to parameterize your app with features you'd like to experiment with in real-time.

Variables can be declared and initialized once in your app. After deploying those variables to production, you can subsequently run unlimited experiments on different values of those variables without doing another code deploy. Variables can be controlled from the Optimizely UI so you can roll out features and tweak the behavior of your app in real-time. See our [Optiverse article](https://help.optimizely.com/Build_Campaigns_and_Experiments/Create_live_variables_for_your_app) for more details on how to control variables from the Optimizely user interface.

The examples at right show how to retrieve the value of a variable for the current user using the Android SDK. We currently support Boolean, floating point, integer, and string variable types. Each of the `getVariable` functions includes the following arguments:

<ul>
<li> *variableKey*: A unique name of the variable, as defined in the Optimizely UI.</li>
<li>*userId*: A unique identifier for the current user.</li>
<li>*attributes* (optional): A map of user attributes and values for the current user.</li>
<li>*activateExperiment*: If set to `true`, record impression events to Optimizely for the experiment(s) that include this variable.</li>
</ul>

If the current user is part of an experiment that includes the specified variable, the function returns the value of the variable, for the variation that user was assigned to. If the user is not in an experiment that includes the variable, but the variable exists in the datafile, the function returns the default value from the datafile. Otherwise, the function returns `null`. Your code must correctly handle cases where a `null` value is returned.

<p><p>

*Note:* If your experiment can be defined completely by a set of variables, it is not necessary to call `activate` to run the experiment in your code. You can just add getters for each of the relevant variables and subsequently create new experiments on the fly. The `activateExperiment` parameter can be used to ensure that impressions are correctly recorded in Optimizely in the event you are not using `activate`. If you are using `activate` for an experiment that includes the live variable then you can set this to `false` to avoid redundant network requests.
</div>

<div class="hidden" data-language-content="language" data-language="objectivec">
Use *Live Variables* to parameterize your app with features you'd like to experiment with in real-time.

Variables can be declared and initialized once in your app. After deploying those variables to production, you can subsequently run unlimited experiments on different values of those variables without doing another code deploy. Variables can be controlled from the Optimizely UI so you can roll out features and tweak the behavior of your app in real-time. See our [Optiverse article](https://help.optimizely.com/Build_Campaigns_and_Experiments/Create_live_variables_for_your_app) for more details on how to control variables from the Optimizely user interface.

The examples at right show how to retrieve the value of a variable for the current user using the Objective-C SDK. We currently support Boolean, floating point, integer, and string variable types. Each of the `getVariable` functions includes the following arguments:

<ul>
<li> *variableKey*: A unique name of the variable, as defined in the Optimizely UI.</li>
<li>*userId*: A unique identifier for the current user.</li>
<li>*attributes* (optional): A map of user attributes and values for the current user.</li>
<li>*activateExperiment*: If set to `true`, record impression events to Optimizely for the experiment(s) that include this variable.</li>
<li>*error* (optional): An error value to return if the variable key is not present in the datafile.</li>
</ul>

If the current user is part of an experiment that includes the specified variable, the function returns the value of the variable, for the variation that user was assigned to. If no matching variable key is found, then default value is returned if it exists. Otherwise, `nil` is returned. If an error is found, a warning message is logged, and an error will be propagated to the user.

<p><p>

*Note:* If your experiment can be defined completely by a set of variables, it is not necessary to call `activate` to run the experiment in your code. You can just add getters for each of the relevant variables and subsequently create new experiments on the fly. The `activateExperiment` parameter can be used to ensure that impressions are correctly recorded in Optimizely in the event you are not using `activate`. If you are using `activate` for an experiment that includes the live variable then you can set this to `false` to avoid redundant network requests.
</div>

<div class="hidden" data-language-content="language" data-language="swift">
Use *Live Variables* to parameterize your app with features you'd like to experiment with in real-time.

Variables can be declared and initialized once in your app. After deploying those variables to production, you can subsequently run unlimited experiments on different values of those variables without doing another code deploy. Variables can be controlled from the Optimizely UI so you can roll out features and tweak the behavior of your app in real-time. See our [Optiverse article](https://help.optimizely.com/Build_Campaigns_and_Experiments/Create_live_variables_for_your_app) for more details on how to control variables from the Optimizely user interface.

The examples at right show how to retrieve the value of a variable for the current user using the Objective-C SDK. We currently support Boolean, floating point, integer, and string variable types. Each of the `getVariable` functions includes the following arguments:

<ul>
<li> *variableKey*: A unique name of the variable, as defined in the Optimizely UI.</li>
<li>*userId*: A unique identifier for the current user.</li>
<li>*attributes* (optional): A map of user attributes and values for the current user.</li>
<li>*activateExperiment*: If set to `true`, record impression events to Optimizely for the experiment(s) that include this variable.</li>
<li>*error* (optional): An error value to return if the variable key is not present in the datafile.</li>
</ul>

If the current user is part of an experiment that includes the specified variable, the function returns the value of the variable, for the variation that user was assigned to. If no matching variable key is found, then default value is returned if it exists. Otherwise, `nil` is returned. If an error is found, a warning message is logged, and an error will be propagated to the user.

<p><p>

*Note:* If your experiment can be defined completely by a set of variables, it is not necessary to call `activate` to run the experiment in your code. You can just add getters for each of the relevant variables and subsequently create new experiments on the fly. The `activateExperiment` parameter can be used to ensure that impressions are correctly recorded in Optimizely in the event you are not using `activate`. If you are using `activate` for an experiment that includes the live variable then you can set this to `false` to avoid redundant network requests.
</div>

<br>