# iOS Mobile SDK
The iOS Mobile SDK allows you to integrating you custom mobile application into The Blueye Hub's data collection and reporting infrastructure. Users can then be segmented and targeted via various channels in the Hub's media platform.

### Installing the SDK

Download the SDK <a href="https://hub.blueye.com/resources/BlueyeHub.framework.zip" target="_blank">here</a> and extract the files anywhere on your local machine.

### Add the Hub SDK to your iOS Project

Open Xcode, right click Frameworks in the project navigator, select 'Add Files to...' and select the folder extracted when downloading the SDK (make sure to just select the folder level and not an individual file).

<img src="http://hub.blueye.com/img/docs/add_framework.png" />

If successfully added, you should see the framework BlueyeHub in your now listed under your Frameworks directory.

<img src="http://hub.blueye.com/img/docs/frameworks.png" />

Next add a reference to the Hub SDK's header file to your application Prefix.pch file. This will allow the Hub's public methods to be accessible throught your application.

<img src="http://hub.blueye.com/img/docs/prefix_pch.png" />

### Authentication

To connect to the Hub, the mobile SDK requriess an API key that is unique to your application. To obtain your key, please create a new app after logging in to the Hub Developer Console. In your app settings, be sure to select 'Mobile App' and enter a Google Analytics ID, which is required for event tracking.

<img src="http://hub.blueye.com/img/docs/dev_console.png" />

After setting up your app you will now be able to connect to the Hub using the following line of code.

<img src="http://hub.blueye.com/img/docs/connect_hub.png" />

Connecting to the Hubrequires passing in your API key obtained from the Developer Console, and a user's ID. The User ID allows us to tie any future actions performed in the app back to a unique user of the app. If you have Facebook connect enabled in your app, the SDK will also automatically tie actions to the current user's Facebook ID as well. Therefore is Facebook connect is your only user authentication method, simply pass in 0 for the user ID when connecting to the Hub.
