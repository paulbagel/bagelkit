# [Radialpoint SupportKit](http://supportkit.radialpoint.com)

# tl;dr
    pod 'SupportKit'
    pod update
    [SupportKit initWithSettings:[SKTSettings settingsWithKnowledgeBaseURL:@"https://supportkit.zendesk.com"]];
    [SupportKit show];

Our [APIs](http://radialpoint.github.io/SupportKit) and [Support Center](https://supportkit.zendesk.com).

# Installation

Installation of the SupportKit SDK is ridiculously simple. Quickly integrate the SupportKit SDK with your project through CocoaPods which also manages library dependencies and SDK updates. Alternatively, you can go the manual route and drop the SDK in your Xcode project.


## Installation via CocoaPods


### Step 1: Install CocoaPods.
Run the following command line in Terminal if [CocoaPods](http://beta.cocoapods.org/?q=#install) isn't already installed:

    $ sudo gem install cocoapods


### Step 2: Run SupportKit's CocoaPod.
In your XCode project directory, run the following:

     $ echo "pod 'SupportKit'" >> Podfile
     $ pod install

Open the .xcworkspace file that Cocoapods generates or modifies in your project directory.


### Step 3: Insert code and launch SupportKit.
Time to insert code and launch SupportKit. See section [Insert Code and Launch SupportKit from Your App.](#Insert Code and Launch SupportKit from Your App)


## Installation via SDK package

### Step 1: Download and unzip.
Download [SupportKit](https://github.com/radialpoint/SupportKit/archive/master.zip) and unzip it.


### Step 2: Add SupportKit libraries to XCode.
Drag & drop both SupportKit.framework and SupportKit.bundle to your project in Xcode.

![Xcode with all the frameworks](https://raw.github.com/radialpoint/SupportKit/master/readme_img/dragdrop_sdk.png)


### Step 3: Add other library dependencies.
Add the following frameworks & libs to your project (go to "Build phases" in your project target and select "Link Binary With Libraries"):
- AVFoundation.framework
- CoreGraphics.framework
- CoreMedia.framework
- CoreTelephony.framework
- CoreText.framework
- CoreVideo.framework
- Foundation.framework
- libxml2.dylib
- OpenGLES.framework
- QuartzCore.framework
- Security.framework
- SystemConfiguration.framework
- UIKit.framework



![Xcode with linked frameworks](https://raw.github.com/radialpoint/SupportKit/master/readme_img/linked_framework.png)


### Step 4: Insert one line of code.
Time to insert one line of code and launch SupportKit. See section [Insert Code and Launch SupportKit from Your App.](#Insert Code and Launch SupportKit from Your App)


## Insert Code and Launch SupportKit from Your App
<a name="Insert Code and Launch SupportKit from Your App"></a>
Add the following import statement:

    #import <SupportKit/SupportKit.h>

And insert the init code. This should be called only once in your application:didFinishLaunchingWithOptions:

    [SupportKit initWithSettings:[SKTSettings settingsWithKnowledgeBaseURL:@"https://supportkit.zendesk.com"]];

**Note:** When specifying your Zendesk URL, make sure to include the protocol (http:// or https://) that matches your Zendesk instance's configuration.

Optionally, you can specify the specific URL to your ticket creation page (the SDK uses \<zendeskURL>/anonymous_requests/new by default). Passing nil will disable creating tickets.

    [SupportKit initWithSettings:[SKTSettings settingsWithKnowledgeBaseURL:@"https://supportkit.zendesk.com"
    andTicketURL:@"https://supportkit.zendesk.com/requests/new"]];

There are also other SKTSettings options you can customize. See our [API docs](http://radialpoint.github.io/SupportKit).

You're done. Build and launch your app. Visit our [Support Center](https://supportkit.zendesk.com) if you run into trouble.


# Optional Setup

## SupportKit Console

Out of the box, the SDK will automatically send the following to the [Support Console](http://supportkit.svbtle.com/Stop-probing-and-start-closing-tickets-with-the-new-supportkit-console) with each ticket submission: app screens that your customer visited, touch interactions with your app, device info, searches made to your knowledge base, and each article viewed for your support team.

To have the SDK to also send your existing app logs, and custom events(events that you want your support team to see) please see our [app log guide](https://supportkit.zendesk.com/hc/en-us/articles/201747860-Reporting-logs-to-your-support-team), and [custom event guide](https://supportkit.zendesk.com/hc/en-us/articles/201626494-Custom-Event-track-API-Why-).  You can test out this feature on a simulator using the uploadContextWhenClosingSupportKit SKTSettings api.  Setting it to YES will mimic a ticket submission when closing SupportKit.  This will upload all app logs and custom events that were fired in the recent app session.  A session URL to the SupportKit Console will be logged in your debug console.

## Recommendations

SupportKit provides two APIs for recommending content to your users. These recommendations are immediately visible when the user launches the SupportKit UI.

The `setDefaultRecommendations` API is used to configure a static list of recommendations that can provide your users with more information about your app (basic usage instructions, cool features, solutions to common problems, etc...).

    [SupportKit setDefaultRecommendations:@[ @"https://yourdomain.zendesk.com/hc/en-us/articles/000000000-recommendation-1", @"https://yourdomain.zendesk.com/hc/en-us/articles/000000000-recommendation-2" ]];

The `setTopRecommendation` API is used to configure a context-specific recommendation (for example, if a user fails to log in, you may choose to recommend an article explaining the various types of login errors that can occur). The top recommendation appears at the beginning of the recommendations list, followed by the list of defaults (if any).

    [SupportKit setTopRecommendation:@"https://yourdomain.zendesk.com/hc/en-us/articles/000000000-context-driven-recommendation"];

See our [release post](http://supportkit.svbtle.com/get-your-users-the-right-answer-at-the-right-time-without-a-search-query) for more details and a demo.

## Search Result Filtering

For Zendesk domains that are shared by multiple apps, it's often useful to filter out some of the knowledge base content from SupportKit's search results. The SupportKit [filtering API](http://radialpoint.github.io/SupportKit/Classes/SKTSettings.html#//api/name/excludeSearchResultsIf:categories:sections:) provides a means to accomplish this, and allows filtering of search results based on categories or sections (Zendesk knowledge bases are organized in three tiers: Category -> Section -> Article).

    - (void)excludeSearchResultsIf:(SKTSearchResultsFilterMode)filterMode categories:(NSArray *)categories sections:(NSArray *)sections

For more details, check out our [knowledge base article](https://supportkit.zendesk.com/hc/en-us/articles/201900224) on the subject.

# Demo App
Download our demo [app](https://github.com/radialpoint/SupportKit/archive/master.zip).
