# iOS Mobile SDK
The iOS Mobile SDK allows you to integrating you custom mobile application into The Blueye Hub's data collection and reporting infrastructure. Users can then be segmented and targeted via various channels in the Hub's media platform.

### Installing the SDK

Download the SDK <a href="https://hub.blueye.com/resources/BlueyeHub.framework.zip" target="_blank">here</a> and extract the files anywhere on your local machine.

### Add the Hub SDK to your iOS Project

Open Xcode, right click Frameworks in the project navigator, select 'Add Files to...' and select the folder you extracted after downloading the SDK (make sure to just select the folder level and not an individual file).

<img src="http://hub.blueye.com/img/docs/add_framework.png" />

If successfully added, you should see the framework BlueyeHub in now listed under your Frameworks directory.

<img src="http://hub.blueye.com/img/docs/frameworks.png" />

Next add a reference to the Hub SDK's header file to your application Prefix.pch file. This will allow the Hub's public methods to be accessible throughout your application.

<img src="http://hub.blueye.com/img/docs/prefix_pch.png" />

### Authentication

To connect to the Hub, the mobile SDK requriess an API key that is unique to your application. To obtain your key, please create a new app after logging in to the Hub Developer Console. In your app settings, be sure to select 'Mobile App' and enter a Google Analytics ID, which is required for event tracking.

<img src="http://hub.blueye.com/img/docs/dev_console.png" />

After setting up your app you will now be able to connect to the Hub using the following line of code.

<img src="http://hub.blueye.com/img/docs/connect_to_hub.png" />

Connecting to the Hub requires passing in your API key obtained from the Developer Console, and a user's ID. The User ID allows us to tie any future actions performed in the app back to a unique user of the app. If you have Facebook connect enabled in your app, the SDK will also automatically tie actions to the current user's Facebook ID as well. Therefore, if Facebook connect is your only user authentication method, simply pass in 0 for the user ID when connecting to the Hub.

### Tracking

The Hub provides support for mobile screen tracking in addition to granular event tracking. To track any screen, simply call the Hub's method 'track' passing in 'self' (should be a ViewController) as the only parameter.

<img src="http://hub.blueye.com/img/docs/track_screen.png" />

The Hub SDK also allows you complete flexiblity in tracking any and all actions perform in your app through the 'trackItem' method call. Each action is assumed to be performed on an 'item' and thus the item's unique ID is required. If the action is of global nature ('i.e. user invited a friend to use the app'), simply pass in 0 as the item ID. Next the action name, such as like, want, follow, purchase, play, etc. should next be specified, but is optional. If omitted, an action of type 'view' will be used.

<img src="http://hub.blueye.com/img/docs/track_item.png" />

As shown above, additional metdata such as a brief title or brief description, or an image URL, can also be set, but are also not required. The more information that is specified though, the more engaging the data in your analytics dashboard will be, as show in the next section.

## Analytics Dashboard

All events tracked during the life of your Mobile app while connected to the Hub can then be analyzed in our insights dashboard. Additional users can be segmented and filtered by action, and custom audiences can be created that plug directly into our media advertising platform.
