---
template: multi-example
title: Datafile bundling
anchor: bundled-datafile
code_examples:
  objectivec:
    lang: objectivec
    request: |
    
        OPTLYManager *manager = [OPTLYManager init:^(OPTLYManagerBuilder * _Nullable builder)
        {
            builder.projectId = @"projectId";
            
            // Load the datafile from the bundle
            NSString *filePath =[[NSBundle bundleForClass:[self class]]
                                          pathForResource:@"datafileName"
                                                   ofType:@"json"];
            NSString *fileContents =[NSString stringWithContentsOfFile:filePath
                                                              encoding:NSUTF8StringEncoding
                                                                 error:nil];
            NSData *jsonData = [fileContents dataUsingEncoding:NSUTF8StringEncoding];
            
            // Set the datafile in the builder
            builder.datafile = jsonData;
        }];
       
  swift:
    lang: swift
    request: |
    
        let optimizelyManager = OPTLYManager.init {(builder) in
            builder!.projectId = "projectId"
            
            // Load the datafile from the bundle
            let bundle = Bundle.init(for: self.classForCoder)
            let filePath = bundle.path(forResource: "datafileName",
                                       ofType: "json")
            var jsonDatafile: Data? = nil
            do {
                 let fileContents = try String.init(contentsOfFile: filePath!,
                                                    encoding: String.Encoding.utf8)
                 jsonDatafile = fileContents.data(using: String.Encoding.utf8)!
            }
            catch {
                print("Invalid JSON data")
            }
            
            // Set the datafile in the builder
            builder!.datafile = jsonDatafile
        }

---

<div class="hidden" data-language-content="language" data-language="android">
<div></div>

This section applies only if your app uses the datafile handler module included in the Optimizely Android SDK.

When your customer opens your app for the first time after installing or updating it, the Optimizely SDK initializes the Optimizely manager, and during its initialization, the Optimizely manager attempts to pull the newest datafile from the CDN servers.

If your app is unable to contact Optimizely's CDN servers to download a datafile, the Optimizely manager can substitute a datafile that you included ("bundled") when you created your app. By bundling a datafile within your app, you ensure that the Optimizely manager can initialize without waiting for a response from our CDN servers.

<div class="attention attention--good-news push--bottom">
By bundling a datafile, you can prevent poor network connectivity from causing your app to hang or crash while it loads.
</div>

Note: Because optionally revering to a bundled datafile happens during the Optimizely manager's initialization, the process will complete before the manager initializes the Optimizely client. Thus, datafile bundling is compatible with both [synchronous and asynchronous initialization](https://help.optimizely.com/Set_Up_Optimizely/Best_practices%3A_Datafile_management_in_Full_Stack) of the Optimizely client.
</div>


<div class="hidden visible" data-language-content="language" data-language="csharp">
<div class="unsupported">The <span class="sdk-platform"></span> does not use datafile bundling.</div>
</div>


<div class="hidden visible" data-language-content="language" data-language="java">
<div class="unsupported">The <span class="sdk-platform"></span> does not use datafile bundling.</div>
</div>


<div class="hidden visible" data-language-content="language" data-language="javascript">
<div class="unsupported">The <span class="sdk-platform"></span> does not use datafile bundling.</div>
</div>


<div class="hidden visible" data-language-content="language" data-language="node">
<div class="unsupported">The <span class="sdk-platform"></span> does not use datafile bundling.</div>
</div>


<div class="hidden" data-language-content="language" data-language="objectivec">
In both the initialization cases described above, the SDK will fall back to the bundled datafile. We refer to the “bundled” datafile as the datafile stored on the device and provided in the builder during the manager initialization.
</div>


<div class="hidden visible" data-language-content="language" data-language="php">
<div class="unsupported">The <span class="sdk-platform"></span> does not use datafile bundling.</div>
</div>


<div class="hidden visible" data-language-content="language" data-language="python">
<div class="unsupported">The <span class="sdk-platform"></span> does not use datafile bundling.</div>
</div>


<div class="hidden visible" data-language-content="language" data-language="ruby">
<div class="unsupported">The <span class="sdk-platform"></span> does not use datafile bundling.</div>
</div>


<div class="hidden" data-language-content="language" data-language="swift">
In both the initialization cases described above, the SDK will fall back to the bundled datafile. We refer to the “bundled” datafile as the datafile stored on the device and provided in the builder during the manager initialization.
</div>

<br>